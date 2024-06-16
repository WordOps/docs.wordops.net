# How to enable/disable brotli compression with Nginx

Since WordOps release v3.21.0, you can enable or disable brotli compression with Nginx with the following commands :

```shell
# enable brotli compression
wo stack install --brotli

## disable brotli compression
wo stack remove --brotli
```

<asciinema-player src="/images/brotli.cast" autoplay loop cols="125" rows="30"></asciinema-player>

Brotli compression is not enabled by default in WordOps, our default configuration use GZIP compression. If you enable then disable Brotli compression, WordOps will use GZIP back.
