# Environment Variables

The server can be configured via the following environment variables.

!!! tip "Remember"
    - Environment variables are equivalent to their command-line arguments.
    - [Command line arguments](./command-line-arguments.md) take precedence over their equivalent environment variables.

### SERVER_HOST
The address of the host (E.g 127.0.0.1). Default `[::]`.

### SERVER_PORT
The port of the host. Default `80`.

### SERVER_LISTEN_FD
Optional file descriptor number (e.g. `0`) to inherit an already-opened TCP listener on (instead of using `SERVER_HOST` and/or `SERVER_PORT`). Default empty (disabled).

### SERVER_ROOT
Relative or absolute root directory path of static files. Default `./public`.

### SERVER_LOG_LEVEL
Specify a logging level in lower case. Possible values are `error`, `warn`, `info`, `debug` or `trace`. Default `error`.

### SERVER_ERROR_PAGE_404
HTML file path for 404 errors. If path is not specified or simply don't exists then server will use a generic HTML error message. Default `./public/404.html`.

### SERVER_ERROR_PAGE_50X
HTML file path for 50x errors. If path is not specified or simply don't exists then server will use a generic HTML error message. Default `./public/50x.html`

### SERVER_THREADS_MULTIPLIER
Number of worker threads multiplier that'll be multiplied by the number of system CPUs using the formula: `worker threads = number of CPUs * n` where `n` is the value that changes here. When multiplier value is 0 or 1 then the `number of CPUs` is used. Number of worker threads result should be a number between 1 and 32,768 though it is advised to keep this value on the smaller side. Default one thread per core.

### SERVER_HTTP2_TLS
Enable HTTP/2 with TLS support. Make sure also to adjust current server port. Default `false` (disabled).

### SERVER_HTTP2_TLS_CERT
Specify the file path to read the certificate. Default empty (disabled).

### SERVER_HTTP2_TLS_KEY
Specify the file path to read the private key. Default empty (disabled).

### SERVER_CORS_ALLOW_ORIGINS
Specify a optional CORS list of allowed origin hosts separated by comas. Host ports or protocols aren't being checked. Use an asterisk (*) to allow any host. Default empty (disabled).

### SERVER_COMPRESSION
`Gzip`, `Deflate` or `Brotli` compression on demand determined by the `Accept-Encoding` header and applied to text-based web file types only. See [ad-hoc mime-type list](https://github.com/joseluisq/static-web-server/blob/master/src/compression.rs#L20). Default `true` (enabled).

### SERVER_DIRECTORY_LISTING
Enable directory listing for all requests ending with the slash character (‘/’). Default `false` (disabled).

### SERVER_SECURITY_HEADERS
Enable security headers by default when HTTP/2 feature is activated. Headers included: `Strict-Transport-Security: max-age=63072000; includeSubDomains; preload` (2 years max-age), `X-Frame-Options: DENY`, `X-XSS-Protection: 1; mode=block` and `Content-Security-Policy: frame-ancestors 'self'`. Default `false` (disabled).

### SERVER_CACHE_CONTROL_HEADERS
Enable cache control headers for incoming requests based on a set of file types. The file type list can be found on [`src/control_headers.rs`](https://github.com/joseluisq/static-web-server/blob/master//src/control_headers.rs) file. Default `true` (enabled).

### SERVER_BASIC_AUTH
It provides [The "Basic" HTTP Authentication Scheme](https://datatracker.ietf.org/doc/html/rfc7617) using credentials as `user-id:password` pairs, encoded using `Base64`. Password must be encoded using the [BCrypt](https://en.wikipedia.org/wiki/Bcrypt) password-hashing function. Default empty (disabled).