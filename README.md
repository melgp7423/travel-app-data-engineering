# Solo Traveler Data Engineering Project

A simple AWS data pipeline that pulls travel cost data from four sources: exchange rates, flights, hotels and meal prices. It stores the raw data, transforms it, and makes it queryable for dashboards.

## Data Sources

| Data                    | Source                                                                                                             |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Currency exchange rates | [Exchange Rates API](https://exchangeratesapi.io/)                                                                 |
| Flight costs            | [SerpApi – Google Flights API](https://serpapi.com/google-flights-api)                                             |
| Hotel room costs        | [SerpApi – Google Hotels API](https://serpapi.com/google-hotels-api)                                               |
| Meal price per city     | [Numbeo – Cost of Living by City](https://www.numbeo.com/cost-of-living/region_prices_by_city?itemId=2&region=150) |

## Architecture

```
API Gateway
    │
Step Functions ──┬── Lambda: exchange rates ──┐
                 ├── Lambda: flights ─────────┤
                 ├── Lambda: hotels ──────────┼──► S3 (raw)
                 └── Lambda: meal prices ─────┘
                                                    │
                                          Lambda: transform
                                                    │
                                                DynamoDB
                                                    │
                                                 Athena
                                                    │
                                            Amazon Quick Suite
```

1. **API Gateway** exposes REST endpoints to trigger ingestion.
2. **Step Functions** runs the four ingestion Lambda functions in parallel.
3. **Lambda (ingest)** calls each API and writes the raw responses to **S3**.
4. **Lambda (transform)** cleans and standardizes the raw data.
5. **DynamoDB** stores the transformed data.
6. **Athena** queries the data (via the Athena DynamoDB connector).
7. **Amazon Quick Suite** visualizes the results.

## Tech Stack

- AWS Lambda
- AWS Step Functions
- Amazon API Gateway
- Amazon S3
- Amazon DynamoDB
- Amazon Athena
- Amazon Quick Suite

## Project Structure

```
.
├── .github/     # CI/CD workflows
├── src/         # Lambda function code
├── tests/       # Tests
└── README.md
```

## Setup

_TODO: prerequisites, API keys, and deployment steps._

## Usage

_TODO: how to trigger the pipeline and view results._
