---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
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

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the DataViz API! This extensive API powers applications, services and scripts developed by DataViz in order to provide technical support for the Regional Planning Program at MTC. 

Data science projects are developed using Python, with APIs managed using FastAPI. Web applications are built using a javascript framework, with APIs managed using Node.js. Descriptions and examples are provided with all API definitions in this documentation. If you have any questions or require any further information, please contact us: dataviz@bayareametro.gov.


# Authentication/User Management

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Authentication for DataViz apps is handled in two ways:

  - [Firebase](https://firebase.google.com/) by Google for non-MTC users
  - Single Sign On via [OneLogin](https://www.onelogin.com/) for MTC Users

Once a user is authenticated via one of these two methods, a json web token is generated to create and maintain a session with the application

<aside class="notice">
The user table for all applications is managed as a protected table in Socrata. The user table does not store or manage any user passwords.
</aside>

## Me

This endpoint retrieves information for the current logged in user. 

Data is returned as json.

Headers: `Authorization: Bearer samplemtcjsonwebtoken`

```javascript

http.get('https://jsapi.mtcanalytics.org/users/me', userData)
.then(token => {
  if token console.log(token)
})
.catch(err => {
  if err console.log(err);
});
```

> The above command returns JSON structured like this:

```json
[
  {
    token: sampletokenresponse
  }
]
```
### HTTP Request

`GET https://api.mtcanalytics.org/users/me`


<aside class="success">
Once a user is authenticated, all requests to protected API endpoints should include an Authorization header
</aside>

# Socrata

## Get Parcel Geography

This endpoint retrieves the geography for a single parcel.
Data is returned as geojson.



```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "parcel_id": "-122p23426X37p76707X",
    "geo_id": "-122.23426:+37.76707:",
    "county": "Alameda",
    "jurisdiction": "Alameda",
    "geometry": {
      "type": "MultiPolygon",
      "coordinates": [
        [
          [
            [
              -122.2338080648335,
              37.76740264551864
            ],
            [
              -122.2338366420393,
              37.76736779416968
            ],
            [
              -122.2339260630376,
              37.76725873500524
            ],
            [
              -122.2340079489674,
              37.76715886681279
            ],
            [
              -122.234013757474,
              37.76715203826209
            ],
            [
              -122.2340857628339,
              37.76706396864847
            ],
            [
              -122.2340905068369,
              37.76705817971169
            ],
            [
              -122.2340914258134,
              37.76705705913479
            ],
            [
              -122.2341665213779,
              37.76696547215583
            ],
            [
              -122.23417214034,
              37.76695861518223
            ],
            [
              -122.2343720819661,
              37.76671476755052
            ],
            [
              -122.2347407281008,
              37.76690523998366
            ],
            [
              -122.2346256898455,
              37.76704370239677
            ],
            [
              -122.2346201364604,
              37.76705039532361
            ],
            [
              -122.2343926461996,
              37.76732420475108
            ],
            [
              -122.233882909768,
              37.76742936241326
            ],
            [
              -122.2338646308486,
              37.76743313244657
            ],
            [
              -122.2338080648335,
              37.76740264551864
            ],
            [
              -122.2338080648335,
              37.76740264551864
            ]
          ]
        ]
      ]
    },
    "x_26910": "567439.146317296",
    "y_26910": "4180250.1057599145"
  }
]
```
### HTTP Request

`GET https://api.mtcanalytics.org/api/socrata/parcel/geo/<parcel_id>`

### URL Parameters

Parameter | Description
--------- | -----------
geo | The geography for the dashboard [regional, county, jurisdiction]
name | For county or jurisdiction, the name of the county or jurisdiction


<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
[
  {
    "parcel_id": "-122p23426X37p76707X",
    "geo_id": "-122.23426:+37.76707:",
    "county": "Alameda",
    "jurisdiction": "Alameda",
    "geometry": {
      "type": "MultiPolygon",
      "coordinates": [
        [
          [
            [
              -122.2338080648335,
              37.76740264551864
            ],
            [
              -122.2338366420393,
              37.76736779416968
            ],
            [
              -122.2339260630376,
              37.76725873500524
            ],
            [
              -122.2340079489674,
              37.76715886681279
            ],
            [
              -122.234013757474,
              37.76715203826209
            ],
            [
              -122.2340857628339,
              37.76706396864847
            ],
            [
              -122.2340905068369,
              37.76705817971169
            ],
            [
              -122.2340914258134,
              37.76705705913479
            ],
            [
              -122.2341665213779,
              37.76696547215583
            ],
            [
              -122.23417214034,
              37.76695861518223
            ],
            [
              -122.2343720819661,
              37.76671476755052
            ],
            [
              -122.2347407281008,
              37.76690523998366
            ],
            [
              -122.2346256898455,
              37.76704370239677
            ],
            [
              -122.2346201364604,
              37.76705039532361
            ],
            [
              -122.2343926461996,
              37.76732420475108
            ],
            [
              -122.233882909768,
              37.76742936241326
            ],
            [
              -122.2338646308486,
              37.76743313244657
            ],
            [
              -122.2338080648335,
              37.76740264551864
            ],
            [
              -122.2338080648335,
              37.76740264551864
            ]
          ]
        ]
      ]
    },
    "x_26910": "567439.146317296",
    "y_26910": "4180250.1057599145"
  }
]
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete


# Mode

## Get a Specific Dashboard URL

This endpoint retrieves a specific dashboard URL for a white label embed.

### HTTP Request

`GET https://api.mtcanalytics.org/api/mode/dashboard/<geo>/<name>`

### URL Parameters

Parameter | Description
--------- | -----------
geo | The geography for the dashboard [regional, county, jurisdiction]
name | For county or jurisdiction, the name of the county or jurisdiction

# HLUV

