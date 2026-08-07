# TMDB API Test Automation

A Postman API testing project for validating **The Movie Database (TMDB) API** through functional tests, response schema checks, authentication workflows, and business-rule validations.

## Project Overview

This project contains an organized Postman collection that tests multiple TMDB API endpoints. JavaScript test scripts are used to validate HTTP status codes, response data, required fields, sorting, filtering, pagination, date ranges, and authentication.

## Technologies Used

* Postman
* JavaScript
* TMDB REST API
* Postman Collection Runner
* Git and GitHub

## Test Scenarios

1. Verify API authentication using movie details.
2. Search for movies by keyword.
3. Search for TV shows by name.
4. Get movie details by movie ID.
5. Get movie credits.
6. Get popular movies.
7. Get TV show details by ID.
8. Get the movie genres list.
9. Discover movies by genre.
10. Get now-playing movies.
11. Get person details by person ID.

## Bonus Scenario

The project also implements the TMDB user authentication flow:

1. Create a request token.
2. Approve the request token through the TMDB website.
3. Create a user session.
4. Retrieve account details.
5. Add a movie to the account watchlist.
6. Validate the repeated request for idempotency.

## Validations Covered

* HTTP status code validation
* Response body validation
* Required field validation
* Array and object structure validation
* Search result relevance
* Genre filtering
* Pagination fields
* Popularity sorting
* Release-date range validation
* Authentication and session handling
* Watchlist request-body validation
* Idempotency validation

## Collection Runner Result

| Metric           | Result |
| ---------------- | -----: |
| Total Tests      |     55 |
| Passed           |     52 |
| Failed Findings  |      3 |
| Execution Errors |      0 |

The failed validations represent observed API response deviations rather than collection configuration errors.

## Observed API Findings

### 1. Popular Movies Sorting

The Popular Movies endpoint returned `200 OK`, but the complete result set was not strictly sorted by `popularity` in descending order.

### 2. Now Playing Date Range

The Now Playing endpoint returned a movie whose `release_date` was earlier than the minimum date provided in the response `dates` object.

### 3. Watchlist Idempotency

Adding a movie to the watchlist returned `201 Created`. Repeating the identical request also returned `201 Created`, while the expected idempotent response was `200 OK`.

## Project Files

```text
TMDB-API-Test-Automation/
├── TMDB API Test Automation.postman_collection.json
├── TMDB API Environment Template.postman_environment.json
└── README.md
```

## Setup and Execution

1. Create an account on [TMDB](https://www.themoviedb.org/).
2. Generate an API key and API Read Access Token.
3. Import the Postman collection JSON file.
4. Import the environment template JSON file.
5. Add your credentials to the environment:

   * `api_key`
   * `bearer_token`
6. Select `TMDB API Environment Template` in Postman.
7. Open the collection and run it using the Postman Collection Runner.

## Bonus Authentication Setup

The watchlist scenario requires additional account variables:

* `request_token`
* `session_id`
* `account_id`

Run the authentication requests in sequence and manually approve the generated request token before creating the session.

## Environment Variables

| Variable        | Purpose                            |
| --------------- | ---------------------------------- |
| `base_url`      | TMDB API base URL                  |
| `api_key`       | TMDB API key                       |
| `bearer_token`  | API Read Access Token              |
| `movie_id`      | Movie used in test requests        |
| `series_id`     | TV show used in test requests      |
| `genre_id`      | Genre used for discovery filtering |
| `person_id`     | Person used in details validation  |
| `request_token` | Temporary authentication token     |
| `session_id`    | Authenticated user session         |
| `account_id`    | TMDB account identifier            |

## Security

The exported environment template does not contain API credentials, session IDs, or account information. Each user must supply their own credentials locally before running the collection.

## Author

**Abdelhamid Ahmed Elsharkawy**

## TMDB Attribution

This product uses the TMDB API but is not endorsed or certified by TMDB.
