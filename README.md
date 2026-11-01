## Riftanalyzer - Riftbound Deck Analyzer

**Analyze. Optimize. Improve your deck and game.**

Riftbound Deck Analyzer is a web application designed to help players understand, evaluate, and improve their Riftbound decks.

The application provides detailed deck statistics, identifies potential weaknesses, analyzes card synergies, and generates actionable recommendations to help players build more consistent and well-balanced decks.


## Overview

Building a deck is not just about choosing individually powerful cards. A well-constructed deck needs a balanced cost curve, a consistent card distribution, a coherent strategy, and meaningful synergies between its cards.

Riftbound Deck Analyzer aims to make deck analysis easier by transforming a decklist into an understandable analytical report.

Instead of relying entirely on intuition, players can use data-driven insights to identify potential improvements.

## Features

### Deck Analysis

- **Cost Curve Analysis** – Analyze card cost distribution, average cost, and overall deck curve.
- **Card Type Distribution** – Examine the balance between different card types.
- **Synergy Detection** – Identify potential interactions and synergies between cards.
- **Smart Recommendations** – Receive suggestions highlighting potential weaknesses and areas for improvement.

## Analysis Modules

The analysis engine is the core component of the application.
Each analyzer is responsible for a specific aspect of deck construction. Their results are combined into a single analysis report.

| Module | Description |
|---|---|
| Cost Curve Analyzer | Evaluates the distribution of card costs. |
| Card Type Analyzer | Examines the proportions of different card types. |
| Domain Analyzer | Evaluates domain distribution and consistency. |
| Synergy Analyzer | Detects potential interactions between cards. |
| Deck Scoring Engine | Combines individual analysis results into an overall score. |
| Recommendation Engine | Generates actionable suggestions based on analysis results. |

The analysis engine is designed to be modular and extensible, making it possible to introduce new analysis algorithms without changing the existing modules.

## Tech Stack
```text
In building
```

## Architecture

The application follows a modular architecture with a clear separation of responsibilities.
In the near future, the product will be broken down into components, with responsibilities allocated accordingly
The backend is responsible for business logic, deck management, card data synchronization, and analytical calculations.
The frontend provides an interactive interface for managing decks and visualizing analysis results.
PostgreSQL stores application data, including cards, decks, users, and analysis history.

## How It Works

A typical analysis workflow consists of the following steps:

1. The user creates or imports a deck.
2. The backend retrieves the corresponding card information.
3. The analysis engine processes the deck.
4. Individual analyzers calculate statistics and identify potential issues.
5. The scoring and recommendation engines combine the results.
6. The frontend displays the generated report using charts, statistics, and recommendations.

## Getting Started

> Installation and configuration instructions will be added as the project develops.

```bash
In Building
```

Backend and frontend setup instructions will be provided here once the initial application structure is available.

## Roadmap

- [ ] Initial project setup
- [ ] Card database integration
- [ ] PostgreSQL data model
- [ ] Card search and filtering
- [ ] Deck creation and management
- [ ] Decklist import
- [ ] Cost Curve Analyzer
- [ ] Card Type Analyzer
- [ ] Domain Analyzer
- [ ] Analysis dashboard
- [ ] Deck scoring system
- [ ] Recommendation engine
- [ ] Card synergy detection
- [ ] Deck version history
- [ ] Deck comparison
- [ ] Automated tests
- [ ] Docker configuration
- [ ] CI/CD pipeline
- [ ] Public deployment

## Project Goals

This project is developed as a practical full-stack application and a learning opportunity focused on:

- Designing maintainable backend architecture with Java and Spring Boot.
- Building RESTful APIs.
- Implementing modular business logic and analytical algorithms.
- Working with relational databases and data modeling.
- Developing interactive interfaces with React and TypeScript.
- Writing automated tests.
- Containerizing and deploying a full-stack application.

## Data Sources & Attribution

The application may use external Riftbound card data sources, including:

- [OpenRift](https://openrift.app/developers)
- [RiftScribe](https://riftscribe.gg/api-docs)

Card data, names, artwork, and other game-related assets remain subject to their respective owners' rights and applicable API terms.

Riftbound is a trademark of Riot Games, Inc. This project is an independent, community-oriented project and is not affiliated with, endorsed, sponsored, or specifically approved by Riot Games.

## License

License information will be added before the first public release.
