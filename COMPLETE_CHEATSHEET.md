
# 🎬 AnimePahe API - Library Cheatsheet

Quick reference for all **9 functions** that the animepahe-api library provides.

---

## 📦 Installation

```bash
npm install github:anime-kun32/animepahe-api
```

---

## 🚀 Basic Setup

```javascript
const animepahe = require('animepahe-api');

async function main() {
  // Initialize once (refreshes cookies)
  await animepahe.initialize();
  
  // Now use any function
  const results = await animepahe.search('Naruto');
  console.log(results);
}

main();
```

---

## 📚 The 9 Library Functions

### 1️⃣ search(query, page = 1)

Search for anime by title.

```javascript
const results = await animepahe.search('Naruto');
const sessionId = results.data[0].session;  // Use this for other functions!
```

---

### 2️⃣ getAiring(page = 1)

Get currently airing anime.

```javascript
const airing = await animepahe.getAiring();
```

---

### 3️⃣ getInfo(animeId)

Get detailed anime information.

```javascript
const info = await animepahe.getInfo('naruto');
// Returns: title, genre, status, episodes, studio, synopsis, ids, external_links, relations, recommendations
```

---

### 4️⃣ getReleases(animeId, sort = 'episode_desc', page = 1)

Get episode releases for an anime.

```javascript
const episodes = await animepahe.getReleases('naruto');
const episodeSession = episodes.data[0].session;  // Use for getStreamingLinks!
```

---

### 5️⃣ getStreamingLinks(animeId, episodeId, includeDownloads = true)

Get streaming (m3u8) and download links for an episode.

```javascript
const streaming = await animepahe.getStreamingLinks('naruto', 'episode-session-id');
// Returns: sources (m3u8 URLs), downloads, episode info
```

---

### 6️⃣ getDownloadLink(url)

Get direct download link from a pahewin URL.

```javascript
const directLink = await animepahe.getDownloadLink('https://pahe.win/...');
// Returns: downloadUrl
```

---

### 7️⃣ getAnimeList(tab, tag1, tag2)

Get anime list (A-Z index) with optional filters.

```javascript
// All anime
const all = await animepahe.getAnimeList();

// By letter
const animeA = await animepahe.getAnimeList('A');

// By genre
const action = await animepahe.getAnimeList(null, 'genre', 'action');
```

---

### 8️⃣ getQueue()

Get encoding queue status (upcoming releases).

```javascript
const queue = await animepahe.getQueue();
```

---

### 9️⃣ initialize()

Initialize library and refresh cookies (call once at startup).

```javascript
await animepahe.initialize();
```

---

## 🔧 Advanced Access

### Raw Scraper
```javascript
const { Animepahe } = require('animepahe-api');
await Animepahe.initialize();
```

### Configuration
```javascript
const { Config } = require('animepahe-api');
Config.baseUrl = 'https://animepahe.si';
Config.userAgent = 'Your Custom Agent';
```

### Models
```javascript
const { models } = require('animepahe-api');
const info = await models.AnimeInfoModel.getAnimeInfo('naruto');
```

---

## 💡 Quick Examples

### Example 1: Search and Stream
```javascript
async function streamAnime(query) {
  await animepahe.initialize();
  
  const search = await animepahe.search(query);
  const anime = search.data[0];
  
  const episodes = await animepahe.getReleases(anime.session);
  const episode = episodes.data[0];
  
  const streaming = await animepahe.getStreamingLinks(anime.session, episode.session);
  
  console.log(`${anime.title} - EP ${episode.episode}`);
  console.log(`Stream: ${streaming.sources[0].source}`);
}

streamAnime('Naruto');
```

### Example 2: Browse Airing
```javascript
async function browseAiring() {
  await animepahe.initialize();
  
  const airing = await animepahe.getAiring();
  airing.data.forEach(anime => {
    console.log(`${anime.title} (${anime.episodes} eps)`);
  });
}

browseAiring();
```

### Example 3: Get Anime Details
```javascript
async function getDetails(query) {
  await animepahe.initialize();
  
  const search = await animepahe.search(query);
  const anime = search.data[0];
  
  const info = await animepahe.getInfo(anime.session);
  
  console.log(`Title: ${info.title}`);
  console.log(`Genres: ${info.genre.join(', ')}`);
  console.log(`Status: ${info.status}`);
  console.log(`Synopsis: ${info.synopsis.substring(0, 100)}...`);
}

getDetails('Naruto');
```

---

## ⚡ Error Handling

```javascript
try {
  const results = await animepahe.search('Naruto');
} catch (error) {
  console.error('Error:', error.message);
}
```

---

## ⚙️ Environment Variables

```env
BASE_URL=https://animepahe.si
USER_AGENT=Mozilla/5.0...
IFRAME_BASE_URL=kwik.cx
USE_PROXY=true
PROXIES=http://proxy.com:8080
```

---

## 📋 Summary

| Function | Purpose |
|----------|---------|
| `search()` | Find anime |
| `getAiring()` | Currently airing |
| `getInfo()` | Anime details |
| `getReleases()` | Episode list |
| `getStreamingLinks()` | Streams & downloads |
| `getDownloadLink()` | Direct download |
| `getAnimeList()` | Browse by letter/genre |
| `getQueue()` | Encoding queue |
| `initialize()` | Init & refresh |

---

## 🎯 Key Points

✅ Use **session IDs** from search results for other functions  
✅ Call **initialize()** once at startup  
✅ Use **try-catch** for errors  
✅ Respect **rate limits** - add delays between requests  

---

That's all 9 functions! Happy coding! 🎬✨
