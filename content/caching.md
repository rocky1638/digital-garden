---
date: 2022-11-26
updated: 2024-10-08
type: concept
---

![](https://github.com/donnemartin/system-design-primer/raw/master/images/Q6z24La.png)

In-memory caches, such as Memcached or Redis, serve as a buffering layer between your application and data storage, helping balance server loads between reads and writes. Caches are extremely fast—Redis can handle hundreds of thousands of read operations per second.

Caching can occur on the client-side, within a content delivery network (CDN), or on the server-side. Server-side caching has two primary methods:

- **Caching queries**: Stores query results so repeated queries can be quickly retrieved from the cache. However, if any data in the result changes, the entire query result must be removed from the cache.

- **Caching objects**: Stores objects or classes (similar to object-oriented programming) and can evict items when the object is updated. Commonly cached items include user sessions, fully rendered HTML files, and social network friend relationships.

## cache update policies

### write-through

The application writes and reads all data through the cache, which updates the database synchronously.

- [p] The cache and database are always in sync.
- [c] Writes are slower.

### write-around

The application directly writes to the database, and the cache is only populated by read requests that cause cache misses.

- [p] Lower write latency.
- [c] Reads are slower and their are guaranteed cache misses on first read of data.

### write-behind / write-back

Similar to write-through, but the cache updates the database asynchronously via a queue. This can lead to data loss if the cache fails before the database is updated.

![300](https://github.com/donnemartin/system-design-primer/raw/master/images/rgSrvjG.png)

### refresh-ahead

The cache is configured to refresh entries before they expire, which works well if future data needs can be predicted accurately.

---

All of these strategies have the challenge of maintaining consistency between the cache and the database. Additionally, using Redis or Memcached requires extra integration effort within the application.

## cache read strategies

### read-through cache

The cache itself is responsible for grabbing up-to-date data on a cache miss.

### read-aside cache/cache-aside

The application makes a second call to read data from the database on a cache miss, and is responsible for updating the cache afterwards.

## references

- https://www.lecloud.net/post/9246290032/scalability-for-dummies-part-3-cache
- https://www.designgurus.io/course-play/grokking-the-system-design-interview/doc/caching
