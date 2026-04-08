# AnimePahe API Cheatsheet

## Introduction
The AnimePahe API allows users to access anime-related data programmatically. This cheatsheet provides an overview of all API objects, methods, utilities, and configurations you can use with the API.

## API Objects
### 1. Anime
- **Description**: Represents an anime object that contains various details about the anime.
- **Properties**:
  - `id`: Unique identifier for the anime.
  - `title`: Title of the anime.
  - `episodes`: Total number of episodes.
  - `genres`: Array of genres associated with the anime.

### 2. User
- **Description**: Represents user information in the API.
- **Properties**:
  - `userId`: Unique identifier for the user.
  - `username`: Username of the user.

## API Methods
### 1. Get Anime
- **Endpoint**: `/api/anime`
- **Method**: GET
- **Parameters**:
  - `id`: (required) The ID of the anime to fetch.
- **Example**:
  ```bash
  curl -X GET 'https://api.animepahe.com/api/anime?id=123'
  ```

### 2. Search Anime
- **Endpoint**: `/api/search`
- **Method**: GET
- **Parameters**:
  - `query`: (required) Search term.
- **Example**:
  ```bash
  curl -X GET 'https://api.animepahe.com/api/search?query=Naruto'
  ```

## Utilities
### 1. Pagination
- **Description**: Use pagination to navigate large sets of data. Include `page` and `limit` parameters in your requests.
- **Example**:
  ```bash
  curl -X GET 'https://api.animepahe.com/api/anime?page=1&limit=10'
  ```

### 2. Error Handling
- **Description**: Handle errors gracefully by checking response status codes.
- **Example**:
  ```javascript
  if (response.status !== 200) {
      console.error('Error fetching data:', response.statusText);
  }
  ```

## Configurations
- **Base URL**: The base URL for the API is `https://api.animepahe.com`
- **Timeout Settings**: Configure timeout settings for your requests to avoid hanging connections.
- **Authentication**: Ensure to utilize API keys as necessary for secured endpoints.

## Complete Examples
### Example 1: Fetching Anime Details
```javascript
async function fetchAnimeDetails(animeId) {
    const response = await fetch(`https://api.animepahe.com/api/anime?id=${animeId}`);
    const data = await response.json();
    console.log(data);
}
```

### Example 2: Searching for Anime
```javascript
async function searchAnime(query) {
    const response = await fetch(`https://api.animepahe.com/api/search?query=${encodeURIComponent(query)}`);
    const data = await response.json();
    console.log(data);
}
```

## Conclusion
This cheatsheet serves as a quick reference for using the AnimePahe API. For more detailed information, refer to the official documentation.