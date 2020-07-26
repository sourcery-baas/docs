---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Sourcery API!

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```ruby
require 'sourcery'

api = Sourcery::APIClient.authorize!('API_KEY')
```

```python
import sourcery

api = sourcery.authorize('API_KEY')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: API_KEY"
```

```javascript
const sourcery = require('sourcery');

let api = sourcery.authorize('API_KEY');
```

> Make sure to replace `API_KEY` with your API key.

Sourcery uses API keys to allow access to the API. You can register a new API key at our [developer portal](https://event-sourcery.co/developers).

Sourcery expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: API_KEY`

<aside class="notice">
You must replace <code>API_KEY</code> with your personal API key.
</aside>

# Streams

## Create a Stream

```ruby
require 'sourcery'

api = Sourcery::APIClient.authorize!('API_KEY')
api.streams.create('orders', { id: 'uuid', item: 'string', qty: 'number' })
```

```python
import sourcery

api = sourcery.authorize('API_KEY')
api.streams.create('orders', { id: 'uuid', item: 'string', qty: 'number' })
```
```shell
curl -X POST "https://event-sourcery.co/api/streams"
  -H "Authorization: API_KEY"
```

```javascript
const sourcery = require('sourcery');

let api = sourcery.authorize('API_KEY');
api.streams.create('orders', { id: 'uuid', item: 'string', qty: 'number' });
```

> The above command returns JSON structured like this:

```json
{
  "id": "9b8cc8f7-0019-4275-b065-e0fac9871ac0",
  "name": "orders",
  "schema": {
    "id": "uuid",
    "item": "string",
    "qty": "number"
  }
}
```

This endpoint creates a new Stream. Streams allow you to start feeding data to your backend.

### HTTP Request

`GET https://event-sourcery.co/api/streams`

## Get a Specific Stream

```ruby
require 'sourcery'

api = Sourcery::APIClient.authorize!('API_KEY')
api.streams.get('84cb9811-2281-4ee2-97ce-6ebdcb45ecf5')
```

```python
import sourcery

api = sourcery.authorize('API_KEY')
api.streams.get('84cb9811-2281-4ee2-97ce-6ebdcb45ecf5')
```

```shell
curl "https://event-sourcery.co/api/streams/84cb9811-2281-4ee2-97ce-6ebdcb45ecf5"
  -H "Authorization: API_KEY"
```

```javascript
const sourcery = require('sourcery');

let api = sourcery.authorize('API_KEY');
let max = api.streams.get('84cb9811-2281-4ee2-97ce-6ebdcb45ecf5');
```

> The above command returns JSON structured like this:

```json
{
  "id": "84cb9811-2281-4ee2-97ce-6ebdcb45ecf5",
  "name": "orders",
  "schema": {
    "id": "uuid",
    "item": "string",
    "qty": "number"
  }
}
```

This endpoint retrieves data for a specific stream.

### HTTP Request

`GET https://event-sourcery.co/streams/<id>`

### URL Parameters

Parameter | Description
--------- | -----------
id | The id of the stream to retrieve

## Delete a Specific Stream

```ruby
require 'sourcery'

api = Sourcery::APIClient.authorize!('API_KEY')
api.streams.delete('84cb9811-2281-4ee2-97ce-6ebdcb45ecf5')
```

```python
import sourcery

api = sourcery.authorize('API_KEY')
api.streams.delete('84cb9811-2281-4ee2-97ce-6ebdcb45ecf5')
```

```shell
curl "https://event-sourcery.co/api/streams/2"
  -X DELETE
  -H "Authorization: API_KEY"
```

```javascript
const sourcery = require('sourcery');

let api = sourcery.authorize('API_KEY');
let max = api.streams.delete('84cb9811-2281-4ee2-97ce-6ebdcb45ecf5');
```

> The above command returns JSON structured like this:

```json
{
  "id": "84cb9811-2281-4ee2-97ce-6ebdcb45ecf5",
  "name": "orders",
  "deleted" : ":("
}
```

This endpoint deletes a specific stream.

### HTTP Request

`DELETE https://event-sourcery.co/streams/<id>`

### URL Parameters

Parameter | Description
--------- | -----------
id | The id of the stream to delete

# Stream Processors

## Create a Stream Processor

```ruby
require 'sourcery'

api = Sourcery::APIClient.authorize!('API_KEY')
api.processors.create('order-validation', { name: 'order-validation', from: 'orders' })
```

```python
import sourcery

api = sourcery.authorize('API_KEY')
api.processors.create('orders', { name: 'order-validation', from: 'orders' })
```

```shell
curl "https://event-sourcery.co/api/processors"
  -X POST
  -d '{ "name": "order-validation", "from": "orders" }'
  -H "Content-Type: application/json"
  -H "Authorization: API_KEY"
```

```javascript
const sourcery = require('sourcery');

let api = sourcery.authorize('API_KEY');
api.processors.create('orders', { name: 'order-validation', from: 'orders' });
```

> The above command returns JSON structured like this:

```json
{
  "id": "9b8cc8f7-0019-4275-b065-e0fac9871ac0",
  "name": "orders-validation",
  "from": "orders"
}
```

This endpoint creates a new Stream Processor. A Processor is how you implement stateless business logic that let you transform and combine data from existing streams into new streams of data.

### HTTP Request

`POST https://event-sourcery.co/api/processors`

# Views

## Create a View

```ruby
require 'sourcery'

api = Sourcery::APIClient.authorize!('API_KEY')
api.views.create('pending-orders', { from: 'orders' })
```

```python
import sourcery

api = sourcery.authorize('API_KEY')
api.views.create('pending-orders', { from: 'orders' })
```
```shell
curl "https://event-sourcery.co/api/views"
  -X POST
  -d '{"from": "orders"}'
  -H "Content-Type: application/json"
  -H "Authorization: API_KEY"
```

```javascript
const sourcery = require('sourcery');

let api = sourcery.authorize('API_KEY');
api.views.create('pending-orders', { from: 'orders' });
```

> The above command returns JSON structured like this:

```json
{
  "id": "9b8cc8f7-0019-4275-b065-e0fac9871ac0",
  "name": "pending-orders",
  "from": "orders",
  "groupBy": "id",
  "filter": { "status": "pending" }
}
```

This endpoint creates a new View. Views allow you to get read representations of your data, so you can query to populate your UI.

### HTTP Request

`POST https://event-sourcery.co/api/views`

# Suscriptions

## Create a Suscription

# Sinks

## Create a Sink
