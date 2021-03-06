---
aliases:
- /features/other/
lastmod: 2016-04-14
date: 2016-04-14
toc: true
linktitle: Content Types
title: Content Types
weight: 50
menu:
  main:
    parent: features
---

# Backend content types

KrakenD supports several content types or encodings:

- JSON
- String
- XML
- RSS

Each backend declaration is able to define which encoder should be used before processing its responses, as shown in this example:

	...
	"endpoints": [
    {
      "endpoint": "/abc",
      "backend": [
        {
          "url_pattern": "/a",
          "encoding": "json",
          "host": [
            "http://service-a.company.com"
          ]
        },
        {
          "url_pattern": "/b",
          "encoding": "xml",
          "host": [
            "http://service-b.company.com"
          ]
        },
        {
          "url_pattern": "/c",
          "encoding": "rss",
          "host": [
            "http://service-c.company.com"
          ]
        }
      ]
    }
    ...

As you can see, having the `encoding`declaration in every backend allows you to consume services with different content types (in the example JSON, XML and RSS) that will be later aggregated into a unified content type (e.g: JSON).

# Response content type

KrakenD supports sending responses back to the client using content types other than JSON (v0.5 or greater). The list of supported content types depends on the selected router package.

Each endpoint declaration is able to define which encoder should be used, as shown in this example. By default, the KrakenD router will fall back to JSON:

	...
	"endpoints": [
    {
      "endpoint": "/a",
      "output_encoding": "negotiate",
      "backend": [
        {
          "url_pattern": "/a"
        }
      ]
    },
    {
      "endpoint": "/b",
      "output_encoding": "string",
      "backend": [
        {
          "url_pattern": "/b"
        }
      ]
    },
    {
      "endpoint": "/c",
      "backend": [
        {
          "url_pattern": "/c"
        }
      ]
    }
    ...

## Mux

The three mux based routers supported by the KrakenD framework include these output encodings:

- JSON
- String

## Gin

The gin-based KrakenD router includes these output encodings:

- JSON
- String
- Negotiate: internally supports JSON, XML and YAML and selects one or another depending on the received `Accept` header.
