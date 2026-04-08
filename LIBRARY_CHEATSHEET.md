# Animepahe API Cheatsheet

## Installation
To install the animepahe-api library in your Node.js project, run the following command:
```bash
npm install animepahe-api
```

## Quick Start
To get started, require the library in your application and create an instance:
```javascript
const AnimepaheAPI = require('animepahe-api');
const api = new AnimepaheAPI();
```

## Complete API Reference
### Search Anime
**Endpoint:** `/search`
- **Method:** `GET`
- **Parameters:** 
  - `title` (string): The title of the anime to search for.

**Example:**
```javascript
api.search({ title: 'Naruto' }).then(result => console.log(result));
```

### Get Anime Details
**Endpoint:** `/details`
- **Method:** `GET`
- **Parameters:** 
  - `id` (string): The ID of the anime.

**Example:**
```javascript
api.details({ id: '123' }).then(details => console.log(details));
```

### List Genres
**Endpoint:** `/genres`
- **Method:** `GET`

**Example:**
```javascript
api.genres().then(genres => console.log(genres));
```

### Advanced API Options
You can also use advanced options for searching:
```javascript
api.search({ title: 'Bleach', genre: 'action', page: 1 }).then(result => console.log(result));
```

## Response Structures
Responses from the API are typically in JSON format. Here’s what you can expect:

### Search Response:
```json
{
  "results": [
    {
      "id": "123",
      "title": "Naruto",
      "genres": ["action", "adventure"],
      "synopsis": "A story about ninjas..."
    }
  ],
  "pagination": {
    "current_page": 1,
    "total_pages": 10
  }
}
```

## Error Handling
You should handle errors gracefully in your application. Use try-catch or promise.catch:
```javascript
api.search({ title: 'Some Nonexistent Anime' })
  .then(result => console.log(result))
  .catch(err => console.error('Error:', err.message));
```

## Practical Use Cases
1. **Fetching popular anime:** Use the search API to get trending or popular anime.
2. **Displaying anime information:** Use the details API to show information on your website or app.
3. **Creating an anime list:** Build a feature where users can save their favorite anime by fetching and displaying various titles.

This cheatsheet provides a structured approach to getting started with the animepahe-api. Happy coding!