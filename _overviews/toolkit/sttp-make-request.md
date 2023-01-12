---
title: How to make an HTTP request?
type: section
description: How to make any HTTP request with Scala Toolkit.
num: 13
previous-page: sttp-intro
next-page: sttp-variable-urls
---

{% include markdown.html path="_markdown/install-sttp.md" %}

## Make a request
The simplest way to make a request with Scala Toolkit's http client library, sttp, is to use the `SimpleHttpClient` instance. 
You need to import a few members from the library, and then write the code that makes the request:

```scala
import sttp.client3.{SimpleHttpClient, UriContext, basicRequest}

val client = SimpleHttpClient() // Create the instance of SimpleHttpClient
val request = basicRequest.get(uri"https://httpbin.org/get") // Construct a get request to an example service - https://httpbin.org/get
val response = client.send(request) // send the request and get the response
println(response.body) // print the body of the response
```

## Other request types
You can swap `basicRequest.get` with any HTTP method you want. For example:
```scala
val request = basicRequest.post(uri"https://httpbin.org/get").body("Hello, world!")
```
Will make a `POST` request with `Hello, world!` as the body.

## The `basicRequest`
Sttp library takes an approach of starting with a simple request description, the `basicRequest`, then modifying it to suit your needs. 
The `basicRequest` is already set up with some [basic headers](https://sttp.softwaremill.com/en/latest/requests/basics.html#initial-requests) - all you need to do is provide the address and the method you want to preform with `get` method. 
Other methods are available for different HTTP methods. 

The `uri` operator in the `uri"https://httpbin.org/get"` keeps you safe from making some of the mistakes in the provided addresses.
It can also interpolate values from variables as described in [How to construct URLs from variables](/overviews/toolkit/sttp-variable-urls.html).
