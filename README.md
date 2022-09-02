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
1. `Per-view cache`: Output of a specific view.
2. `Template fragment cache`: A part of template. (which is difficult to produce)
3. `Per-site cache`: The entire site.
4. `Low-level cache API`: Instead of full page, we cache only those results which is not likely to change in a page.

### Where can the cache be saved?
1. Database
2. File system
3. Directly in memory

## Django Caching Types

1. <b>Memcached:</b> It is a <b>memory-based</b>, key-value store for small chunks of data. It supports distributed caching across multiple servers.

2. <b>Database:</b> The cache fragments are <b>stored in database</b>. It can be useful for <b>storing complex database queries</b>. However, it is <b>not much efficient</b>, in general.

3. <b>File system:</b> The cache is saved on the file system, in <b>separate files</b> for each cache value. It is the <b>easiest</b> for setting up but is the <b>slowest</b> of all.

4. <b>Local memory:</b> Local memory cache, which is <b>best-suited for your local development or testing environments</b>. While it's almost as fast as Memcached, it cannot scale beyond a single server, so it's not appropriate to use as a data cache for any app that uses more than one web server.

5. <b>Dummy:</b> A "dummy" cache that <b>doesn't actually cache anything</b> but still implements the cache interface. It's meant to be used in development or testing when you don't want caching, but do not wish to change your code.


### Lets do it practically...

## PER-SITE CACHE
1. We have to add two middleware `UpdateCacheMiddleware` and `FetchFromCacheMiddleware` in the `settings.py` file. (Sequence is important)
  ```
  MIDDLEWARE = [
    'django.middleware.cache.UpdateCacheMiddleware',   
    'django.middleware.common.CommonMiddleware',
    'django.middleware.cache.FetchFromCacheMiddleware', 
  ]
  ```
2. Also add the following constants in `settings.py` file.
  ```
  CACHE_MIDDLEWARE_ALIAS = 'default'  #Alias for cache
  CACHE_MIDDLEWARE_SECONDS = '600'    #Number of seconds to cache a page
  CACHE_MIDDLEWARE_KEY_PREFIX = ''    #Should be used if the cache is shared across multiple sites that use the same Django instance
  ```
3. It is useful when, site has little or no dynamic content. But it may not be appropriate to use for large sites.

## PER-VIEW CACHE
1. We can cache a specific view instead of wasting our precious memory for caching whole page.
2. You can implement this type of cache with the cache_page decorator either on the view function directly or in the path.
  ```
  from django.views.decorators.cache import cache_page
  
  @cache_page(60 * 15)
  def your_view(request):
      pass

  # or

  from django.views.decorators.cache import cache_page
  
  urlpatterns = [
      path('students-list/', cache_page(60 * 15)(StudentView.as_view())),
  ]
  ```

