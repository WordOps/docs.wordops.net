# Microcaching with Nginx

## Context

This guide applies to WordPress sites with Nginx fastcgi_cache (created with `--wpfc`). WordOps cache pages for 24 hours, as set in `/etc/nginx/conf.d/fastcgi.conf`:

```
...
fastcgi_cache_valid 200 24h;
...
```

This works very well on pages where you have content that rarely changes. But what if you have a page (or pages) with dynamic content? What if you have a page that queries an external API and stores the result somewhere? Looking for an alternative to WordPress Transients API?

One solution is to use microcaching in Nginx where the page only is cached for a couple of minutes. This way your server can handle bursts of traffic while still serving dynamic content.

## Getting started

Nginx lets you set dynamic cache expiration times with the `X-Accel-Expires` header. So if you have a specific page you want to microcache, consider this snippet placed in a plugin or in your theme's `functions.php`:

```
function add_expires_header( $headers, $wp ) {
    if ( 0 === strpos( $wp->request, 'sample-page' ) ) {
        $headers['X-Accel-Expires'] = '120';
    }
    return $headers;
}
add_filter( 'wp_headers', 'add_expires_header', 10, 2 );
```

This sets the TTL (time to live) on the URL `https://domain.tld/sample-page` for 2 minutes (120 seconds). Remember to purge any existing cache so that the new `X-Accel-Expires` header is registered by Nginx:

```
wp nginx-helper purge-all --path=/var/www/domain.tld/htdocs
```

## Testing

On the first request, Nginx returns `x-fastcgi-cache: MISS`, caches the page, and registers the TTL. Note that `X-Accel-Expires` is an internal header, and does not get outputted in the header:

```
curl -Ik https://domain.tld/sample-page/
HTTP/2 200
server: nginx
...
x-fastcgi-cache: MISS
```

On the next request, Nginx returns `x-fastcgi-cache: HIT`:

```
curl -Ik https://domain.tld/sample-page/
HTTP/2 200
server: nginx
...
x-fastcgi-cache: HIT
```

After 2 minutes, Nginx returns `x-fastcgi-cache: STALE`, which means it begins to fetch a new version **in the background**:

```
curl -Ik https://domain.tld/sample-page/
HTTP/2 200
server: nginx
...
x-fastcgi-cache: STALE
```

Any requests before Nginx is finished, gets served with the old cached version, returning `x-fastcgi-cache: UPDATING`:

```
curl -Ik https://domain.tld/sample-page/
HTTP/2 200
server: nginx
...
x-fastcgi-cache: UPDATING
```

When Nginx is done fetching in the background, the cache is updated with the new version of the page, and returns `x-fastcgi-cache: HIT` once again.

This technique is **superuseful**, especially on slow pages with dynamic content.

## WordPress REST API

Microcaching is also very effective if you have a custom REST API endpoint serving dynamic data. But you have to use a different filter since `wp_headers` is not used for API requests. For example:

```
function add_expires_header( $served, $result, $request ) {
    if ( strpos( $request->get_route(), '/custom_endpoint' ) === 0 ) {
        header('X-Accel-Expires: 120');
    }
}
add_filter( 'rest_pre_serve_request', 'add_expires_header', 10, 3 );
```