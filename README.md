# Django Caching

### What is Cache?
1. In general, cache means hidden.
2. In computing, a cache is a hardware or software component that stores data so that future requests for that data can be served faster.

### Why caching is required?
1. A cache's primary purpose is to increase data retrieval performance by reducing the need to access the underlying slower storage layer.
2. It is the most effective way to boost an application's overall performance.

### Does your application require caching?
From database queries to template rendering to business logic everything needs time to be executed. For small scale sites, it is not much relevant but for medium- to high-traffic sites, it’s essential to implement caching.

### How caching works?
1. URL is given.
2. Try finding that page in cache.
3. If found, return the cached page.
4. Else, generate the page. Save that page in cache, for next time & return the generated page.

### What all things can we cache?
1. Output of a specific view.
2. A part of template that is difficult to produce.
3. The entire site.

### Where can the cache be saved?
1. Database
2. File system
3. Directly in memory

## Django Caching Types

1. <b>Memcached:</b> Memcached is a memory-based, key-value store for small chunks of data. It supports distributed caching across multiple servers.

2. <b>Database:</b> Here, the cache fragments are stored in a database. A table for that purpose can be created with one of the Django's admin commands. This isn't the most performant caching type, but it can be useful for storing complex database queries.

3. <b>File system:</b> The cache is saved on the file system, in separate files for each cache value. This is the slowest of all the caching types, but it's the easiest to set up in a production environment.

4. <b>Local memory:</b> Local memory cache, which is best-suited for your local development or testing environments. While it's almost as fast as Memcached, it cannot scale beyond a single server, so it's not appropriate to use as a data cache for any app that uses more than one web server.

5. <b>Dummy:</b> A "dummy" cache that doesn't actually cache anything but still implements the cache interface. It's meant to be used in development or testing when you don't want caching, but do not wish to change your code.
