# TOML Configuration File

**`SWS`** can be configured using a [TOML](https://toml.io/en/) file to adjust the general server features as well as other advanced ones.

It's disabled by default and can be enabled by passing a _string file path_ via the `-w, --config-file` option or its equivalent [SERVER_CONFIG_FILE](./../configuration/environment-variables.md#server_config_file) env.

## TOML File (Manifest)

Below is just an example showing all features with their default values.

```toml
[general]

#### Address & Root dir
host = "::"
port = 80
root = "./public"

#### Logging
log-level = "error"

#### Cache Control headers
cache-control-headers = true

#### Auto Compression
compression = true

#### Error pages
page404 = "./public/404.html"
page50x = "./public/50x.html"

#### HTTP/2 + TLS
http2 = false
http2-tls-cert = ""
http2-tls-key = ""
https-redirect = false
https-redirect-host = "localhost"
https-redirect-from-port = 80
https-redirect-from-hosts = "localhost"

#### CORS & Security headers
# security-headers = true
# cors-allow-origins = ""

#### Directory listing
directory-listing = false

#### Directory listing sorting code
directory-listing-order = 1

#### Directory listing content format
directory-listing-format = "html"

#### Basic Authentication
# basic-auth = ""

#### File descriptor binding
# fd = ""

#### Worker threads
threads-multiplier = 1

#### Grace period after a graceful shutdown
grace-period = 0

#### Page fallback for 404s
# page-fallback = ""

#### Log request Remote Address if available
log-remote-address = false

#### Redirect to trailing slash in the requested directory uri
redirect-trailing-slash = true

#### Check for existing pre-compressed files
compression-static = true

#### Health-check endpoint (GET or HEAD `/health`)
health = false

### Windows Only

#### Run the web server as a Windows Service
# windows-service = false


[advanced]

#### HTTP Headers customization (examples only)

#### a. Oneline version
# [[advanced.headers]]
# source = "**/*.{js,css}"
# headers = { Access-Control-Allow-Origin = "*" }

#### b. Multiline version
# [[advanced.headers]]
# source = "/index.html"
# [advanced.headers.headers]
# Cache-Control = "public, max-age=36000"
# Content-Security-Policy = "frame-ancestors 'self'"
# Strict-Transport-Security = "max-age=63072000; includeSubDomains; preload"

#### c. Multiline version with explicit key (dotted)
# [[advanced.headers]]
# source = "**/*.{jpg,jpeg,png,ico,gif}"
# headers.Strict-Transport-Security = "max-age=63072000; includeSubDomains; preload"


### URL Redirects (examples only)

# [[advanced.redirects]]
# source = "**/*.{jpg,jpeg}"
# destination = "/images/generic1.png"
# kind = 301

# [[advanced.redirects]]
# source = "/index.html"
# destination = "https://static-web-server.net"
# kind = 302

### URL Rewrites (examples only)

# [[advanced.rewrites]]
# source = "**/*.{png,ico,gif}"
# destination = "/assets/favicon.ico"

# [[advanced.rewrites]]
# source = "**/*.{jpg,jpeg}"
# destination = "/images/sws.png"
```

### General options

The TOML `[general]` section allows adjusting the current options available via the CLI/ENV ones.

So they are equivalent to each other **except** for the `-w, --config-file` option which is omitted and can not be used for obvious reasons.

!!! info "Config file-based features are optional"
    All server feature options via the configuration file are optional and can be omitted as needed.

### Advanced options

The TOML `[advanced]` section is intended for more complex features.

For example [Custom HTTP Headers](../features/custom-http-headers.md), [Custom URL Redirects](../features/url-redirects.md), [URL Rewrites](../features/url-rewrites.md), or [Virtual Hosting](../features/virtual-hosting.md)

### Precedence

Whatever config file-based feature option will take precedence over its CLI or ENV equivalent.

## Usage

The following command runs the server using a specific `config.toml` file.

```sh
static-web-server -w config.toml
```
