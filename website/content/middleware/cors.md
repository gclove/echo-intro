+++
title = "CORS"
[menu.side]
  name = "CORS"
  parent = "middleware"
  weight = 5
+++

## CORS Middleware

CORS middleware implements [CORS](http://www.w3.org/TR/cors) specification.
CORS gives web servers cross-domain access controls, which enable secure cross-domain
data transfers.

### Configuration

```go
CORSConfig struct {
  // AllowOrigin defines a list of origins that may access the resource.
  // Optional. Default value []string{"*"}.
  AllowOrigins []string

  // AllowMethods defines a list methods allowed when accessing the resource.
  // This is used in response to a preflight request.
  // Optional. Default value DefaultCORSConfig.AllowMethods.
  AllowMethods []string

  // AllowHeaders defines a list of request headers that can be used when
  // making the actual request. This in response to a preflight request.
  // Optional. Default value []string{}.
  AllowHeaders []string

  // AllowCredentials indicates whether or not the response to the request
  // can be exposed when the credentials flag is true. When used as part of
  // a response to a preflight request, this indicates whether or not the
  // actual request can be made using credentials.
  // Optional. Default value false.
  AllowCredentials bool

  // ExposeHeaders defines a whitelist headers that clients are allowed to
  // access.
  // Optional. Default value []string{}.
  ExposeHeaders []string

  // MaxAge indicates how long (in seconds) the results of a preflight request
  // can be cached.
  // Optional. Default value 0.
  MaxAge int
}
```

### Default Configuration

```go
DefaultCORSConfig = CORSConfig{
	AllowOrigins: []string{"*"},
	AllowMethods: []string{echo.GET, echo.HEAD, echo.PUT, echo.PATCH, echo.POST, echo.DELETE},
}
```

*Usage*

`e.Use(middleware.CORS())`

### Custom Configuration

*Usage*

```go
e := echo.New()
e.Use(middleware.CORSWithConfig(middleware.CORSConfig{
  AllowOrigins: []string{"https://labstack.com", "https://labstack.net"},
  AllowHeaders: []string{echo.HeaderOrigin, echo.HeaderContentType, echo.HeaderAccept},
}))
```
