# Riftingester

Mikroserwis odpowiedzialny za pobieranie katalogu kart Riftbound z OpenRift i jego trwałe przechowywanie w PostgreSQL. To jest **template architektoniczny**: adapter OpenRift nie wykonuje jeszcze requestu ani nie mapuje struktury kart.

## Architektura

Projekt używa heksagonalnej architektury (ports and adapters):

```text
HTTP / scheduler --> application port --> application service
                                      |                |
                               CatalogSourcePort  CatalogSnapshotRepositoryPort
                                      |                |
                               OpenRift adapter   PostgreSQL/JPA adapter
```

* `domain` — niezmiennicze modele oraz wyniki synchronizacji.
* `application` — przypadek użycia i porty; nie zna Springa, JPA ani HTTP.
* `adapter/in` — endpoint operacyjny i scheduler; później można dodać konsumenta wiadomości bez naruszania use case.
* `adapter/out/openrift` — jedyne miejsce dla HTTP DTO i zasad protokołu dostawcy.
* `adapter/out/persistence` — jedyne miejsce dla JPA/PostgreSQL i transakcji.

## Następne kroki implementacji

1. W `OpenRiftCatalogAdapter` użyj `RestClient` do `GET /api/v1/catalog`; ustaw `User-Agent` z konfiguracji oraz `If-None-Match` z portu.
2. Zamapuj `200` na `FetchResult.Modified`, a `304` na `FetchResult.NotModified`. Obsłuż timeouty i błędy jako wyjątki infrastrukturalne.
3. Zdefiniuj rekordy `Card`, `Printing`, `Set` w `domain` po zatwierdzeniu modelu dla pozostałych mikroserwisów, następnie zastąp surowy `payload` tabelami z idempotentnym upsertem.
4. Dodaj retry/backoff, metryki i blokadę rozproszoną albo przenieś harmonogram do Kubernetes `CronJob`, aby wiele replik nie synchronizowało równocześnie.
5. Ogranicz `/internal/catalog-sync` poprzez Spring Security i politykę sieciową Kubernetes.

## Konfiguracja

Zmienne środowiskowe: `DATABASE_URL`, `DATABASE_USERNAME`, `DATABASE_PASSWORD`. Przed wdrożeniem ustaw prawdziwy kontakt w `ingester.openrift.user-agent`.

## Uruchomienie

Wymagane są Java 25, Gradle i PostgreSQL:

```bash
gradle bootRun
```

Lub zbuduj obraz:

```bash
docker build -t riftingester .
```

## Kubernetes

Minimalne manifesty są w `k8s/`. Uzupełnij nazwę obrazu i utwórz sekret `riftingester-database` z kluczami `url`, `username`, `password`. Deployment celowo ma jedną replikę, gdy działa scheduler w aplikacji. Dla skalowania wyłącz `ingester.sync.scheduler-enabled` i użyj CronJoba lub blokady rozproszonej.

## OpenRift

Źródłem jest `GET https://openrift.app/api/v1/catalog`. OpenRift publikuje katalog jako odpowiedź cacheowalną z ETag; pełny katalog należy pobierać oszczędnie i bez masowego pobierania obrazów. Szczegóły: https://openrift.app/developers
