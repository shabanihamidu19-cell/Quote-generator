# Quote Generator

A lightweight REST API that serves inspirational Swahili quotes, built with Express.js. Includes category filtering, random quote retrieval, and a full Jest/Supertest test suite.

## Features

- Get all quotes, or filter by category
- Fetch a single random quote (optionally scoped to a category)
- Fetch a quote by ID
- Health check endpoint for uptime monitoring / container orchestration
- Zero-database, in-memory dataset — fast to run and deploy anywhere

## Requirements

- Node.js >= 18

## Getting Started

```bash
# install dependencies
npm install

# run the server
npm start

# run in watch mode (auto-restart on file changes)
npm run dev
```

The server starts on `http://localhost:3000` by default. Set the `PORT` environment variable to change it.

## API Reference

### `GET /health`
Returns service status and quote count.

```json
{ "status": "ok", "quotes": 25 }
```

### `GET /api/categories`
Returns the list of available categories.

```json
{ "categories": ["elimu", "bidii", "mafanikio", "maisha"] }
```

### `GET /api/quotes`
Returns all quotes. Supports an optional `category` query parameter.

```
GET /api/quotes
GET /api/quotes?category=elimu
```

### `GET /api/quotes/random`
Returns a single random quote. Supports an optional `category` query parameter.

```
GET /api/quotes/random
GET /api/quotes/random?category=bidii
```

### `GET /api/quotes/:id`
Returns a single quote by its numeric ID.

```
GET /api/quotes/1
```

### Error responses
Invalid categories or missing IDs return a `404` with a JSON error body, e.g.:

```json
{ "error": "category_not_found", "message": "Category 'xyz' not found.", "categories": ["elimu", "bidii", "mafanikio", "maisha"] }
```

## Testing

```bash
npm test
```

Runs the full Jest test suite with coverage reporting, using Supertest against the Express app instance (no server binding required).

## Docker

```bash
# build the image
docker build -t quote-generator .

# run the container
docker run -p 3000:3000 quote-generator
```

## Project Structure

```
quote-generator/
 ├── src/
 │    └── server.js        # Express app and API routes
 ├── test/
 │    └── server.test.js   # Jest + Supertest test suite
 ├── package.json
 ├── .gitignore
 ├── README.md
 ├── LICENSE
 └── Dockerfile
```

## License

MIT — see [LICENSE](./LICENSE) for details.
