---
layout: post
title: RESTful Web services
date:   2015-02-01 12:00:00 +0100
description: Learn about RESET and RESTful Web services, and how the resource-oriented architecture can be used.
categories: [web, api]
lang: fr
---

## Introduction

A RESTful web service is a Web service implemented using HTTP and the principles of REST. Representational State Transfer (REST) is a style of software architecture for distributed systems, introduced and defined in 2000 by Roy Fielding in [his doctoral dissertation](http://www.ics.uci.edu/fielding/pubs/dissertation/restarchstyle.htm). Fielding is one of the principal authors of the Hypertext Transfer Protocol (HTTP) specification versions 1.0 and 1.1. The Resource-Oriented Architecture (ROA) is a commonsense set of rules for designing RESTful Web services, introduced by Leonard Richardson et Sam Ruby in the book RESTful Web services.


## Competing Web Service Architectures

We can distinguish between three common Web service architectures: RESTful resource-oriented, RPC-style, and REST-RPC hybrid.

### RESTful, Resource-Oriented Architectures

In RESTful architectures, the method information goes into the HTTP method. In Resource-Oriented Architectures, the scoping information goes into the URI. This is actually the main topic of this article.

### RPC-Style Architectures

An RPC-style Web service accepts an envelope full of data from its client, and sends a similar envelope back. The method and the scoping information are kept inside the envelope. SOAP is a popular envelope format, generally put inside an HTTP envelope. Every RPC-style service defines a brand new vocabulary. By contrast, all RESTful Web services share a standard vocabulary of HTTP methods. Every object in a RESTful service responds to the same basic interface.

The Web is simple, based on the existing HTTP protocol. REST utilizes its methods and other existing features; SOAP RPC over HTTP, on the other hand, encourages each application designer to define new and arbitrary methods that supplant HTTP method.

### REST-RPC Hybrid Architectures

REST-RPC hybrid architecture is a term made up by Richardson & Ruby for describing Web services that fit somewhere in between the RESTful Web services and the purely RPC-style services. These services are clearly designed as RPC-style services (ones that use HTTP as their envelope format), despite the “REST" in the URI. The scoping information is in the URI, just like a RESTful resource-oriented service; but the method information also goes in the URI. In a RESTful service, the method information would go into the HTTP method, and whatever was leftover would become scoping information. Such a service is simply using HTTP as an envelope format, sticking the method and scoping information wherever it pleases.


## REST and Resource-Oriented Architecture (ROA)

### Properties

REST relies on the well-known, well-defined HTTP protocol, and heavily uses its properties:

* URIs (uniform resource identifier)
* Internet media types (MIME types or Content types)
* methods (`GET`, `POST`, `PUT`, `DELETE`, `HEAD`, `OPTIONS`)
* response codes

The resource-oriented architecture has the following properties:

* uniform interface: the method information is kept in the HTTP method
* addressability: expose at least one URI for every resource
* statelessness: every request happens in complete isolation (i.e. the server never relies on information from previous requests; application state resides in requests)
* connectedness: resources should link to each other in their representation

### Resources and URIs

While **RPC architecture** (including SOAP) exposes **internal algorithms**, or verbs, **ROA** exposes **internal data**, or nouns (objects). In that sense, ROA may be considered as an "extreme object-oriented" architecture.

Requests and responses are built around the transfer of representations of *resources*. **A resource can be essentially any coherent and meaningful concept that may be addressed**, or in other words anything important enough to be referenced as a "thing".

A resource must have at least one URI; the URI is the name and address of a resource.

A RESTful Web service exposes both its data and its algorithms through resources. URIs should be descriptive; there’s usually a hierarchy that starts out small and branches out into infinitely many leaf nodes. For algorithmic resource, query variables can be used.
Ex: /parent/child1;child?start=10

### HTTP methods

The HTTP method corresponds to the HTTP *verb*, or *action*, and indicates how the client expects the sever to process this envelope. The following methods are used:

* `GET`: retrieve information
* `POST`: create a new entry (from parent)
* `PUT`: update an existing entry or create a new one (with all information)
* `DELETE`: delete an existing resource
* `HEAD`: retrieve a metadata-only representation
* `OPTIONS`: check which HTTP methods a particular resource supports

The `POST` method can be overloaded for some specific reasons, such as:

* simulating `PUT` and `DELETE` for clients that do not support them
* a workaround for max length URI (ex: Apache = 8KB)

### HTTP header

The HTTP header is very helpful metadata when building resource-oriented Web services. It can give information about request authentication, encoding, (re)location, etc... without even inspecting the request body.

### HTTP response codes

HTTP response codes are very important; they tell the client how to deal with the object(s) in the entity body, or what to do if they can't understand the it. 

### Media types (format)

REST is not tied up to any specific format. Usually though, common representations like `XML`, `ATOM`, `JSON`, `JPEG`, etc… are used, compressed or not.

## Documenting a RESTful Web service

> A REST API should spend almost all of its descriptive effort in defining the media type(s) used for representing resources and driving application state, or in defining extended relation names and/or hypertext-enabled mark-up for existing standard media types. Any effort spent describing what methods to use on what URIs of interest should be entirely defined within the scope of the processing rules for a media type.

Lack of a standard description language is often cited as a limitation of REST. In reality, machine-readable description languages do not communicate the semantics necessary for client developers to write code. Thus, most REST services are documented by no more than a textual description (a human-readable HTML file).

With version 2.0, WSDL supports all HTTP verbs and it is now considered to be an acceptable method of documenting REST services. An alternative is [WADL](http://www.w3.org/Submission/wadl/), the Web Application Description Language, which is lightweight, easier to understand and easier to write than WSDL. However, WSDL and even WADL are usually considered to be an overkill.

A RESTful Web service documentation should fully describe the following in human readable description:

* All resources, and methods supported for each resource.
* Media types and representation formats for resources in requests and responses.
* Each link relation used, its business significance, HTTP method to be used, and resource that the link identifies.
* All fixed URIs that are not supplied via links.
* Query parameters used for all fixed URIs.
* URI templates, and token substitution rules.
* Authentication and security credentials for accessing resources.
* For XML representations, if your clients and servers are capable of supporting XML schemas, use a schema language as a “convention” to describe the structure of XML documents used for representations in requests and responses. For other formats, use conventions to describe representations in prose (such as JSON schemas).

Example of RESTful Web service documentation:

* http://kenai.com/projects/suncloudapis/pages/CloudAPISpecificationResourceModels
* http://wiki.openstreetmap.org/wiki/API_v0.6
* http://weblog.bocoup.com/documenting-your-api/
* http://predic8.com/rest-webservices.htm

