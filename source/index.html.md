---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript


toc_footers:
  - <a href='https://www.srvup.com/register'>Sign Up</a>
  - <a href='https://www.srvup.com/login'>Login</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the srvup reference docs. This will show you how to build clients to consume the srvup api. 

<aside class="warning">
These docs are still under construction.
</aside>


# Register Client

Go to [https://www.srvup.com/apps](https://www.srvup.com/apps) to register a client. 

For local testing, use the `localhost` as your value for your domain. 

Take note of the `public token` and `secret token` those will be used below.

For web clients, the `secret token` will be ignored while the domain origin will be stricly enforced along with your `public token`


# Installation

**[srvup.js](https://github.com/srvup/srvup.js)** 
Our JavaScript for web applications that require the srvup api. This client makes it convenient to do API calls.

To install, `npm install srvup --save`



**srvup.py** _coming soon_

> To install srvup.js, run below next to your `package.json`

```shell
$ npm install srvup --save
```


# App Authorization

## Web Client Authorization

Generally speaking, our `web-clients` are restricted to a origin (like a domain), `public token` and a `user auth token`.  We also want to keep our `secret token`, well, a secret. So we don't want that exposed to the public at large. Therefore we can ignore this token in `web-clients`.

`secret token` is for Native Apps and Server-side apps as discussed below.


> To authorize, use this code:


```javascript
import srvup from 'srvup'
const yourPublicToken = 'value from above'
srvup.api(yourPublicToken)
```


> Set the value of `yourPublicToken` with your client's **public key**.

Srvup uses public keys to general to your client and srvup account. This allows us to enforce the domain (origin) as well as the public key is associated to your account. We use this in conjunction with `Authorization` tokens, which we'll add later.

srvup expects for the API key to be included in all API requests to the server in a header that contains:

`X-Srvup-Signature: yourPublicToken`

<aside class="notice">
You must set the value of <code>yourPublicToken</code> with your client's <b>public token</b>.
</aside>


## Native Apps and Server-side Authorization

Native apps are anything you have to install on your system. Mobile apps are certainly the most popular native apps. Desktop Apps are not far behind. TV apps on the rise. Video Game Console Apps. Car Apps (like CarPlay, Android Auto, etc). 

We treat server-side apps just as native apps as far as authenticating with srvup.

To authenticate, you'll use the `public token` and `secret token` from creating your client above.


The specifics of this type of authentication are forthcoming. 


# Users

## User Authorization

To authenticate a user, you must: 

- [Create a Client](https://www.srvup.com/apps) for your App

- Authorize your App through a (1) [Web Client](#web-client-authorization) or (2) [Native App/Server-side app](#native-apps-and-server-side-authorization)

- [Register a User](#register-user) and get the user's JWT `token`

- [Login a User](#login-user) and get the user's JWT `token`

- Set the following header on all requests made by the user:


`Authorization: JWT <token>`


## Register User 

_coming soon_

## Login User

_coming soon_


# Posts


## All Posts

> Basic

```javascript
function myResponseCallback (responseData, statusCode){
  console.log(responseData, statusCode)
}
srvup.get('/posts/', myResponseCallback)
```

> Inline callback

```javascript
srvup.get('/posts/', (responseData, statusCode)=>{
    console.log(responseData, statusCode)
})
```

> React

```javascript
class MyComponent extends React.Compoment {
  constructor(props){
    super(props)
    this.state ={
      posts: [],
      loading: true,
    }
  }

  handleResponse = (responseData, statusCode) => {
    console.log(responseData, statusCode)
    if (statusCode === 200){
      this.setState({
        loading: false,
        posts: responseData.results
      })
    }
  }
  componentDidMount() {
    srvup.get('/posts/', this.handleResponse)
  }

  render () {
    return <h1>Results Count {this.state.posts.length}</h1>
  }
  
}
```




> Response Data

```json
{
  "results": [
    {
      "id": 1,
      "name": "Hello World",
      "slug": "hello-word",
      "content": "",
      "publish": ""
    },
    {
      "id": 2,
      "name": "Hello World",
      "slug": "hello-word",
      "content": "",
      "publish": ""
    }
  ]
}
```

This endpoint retrieves all published posts. To manage these posts, login to your account on [https://www.srvup.com](http://www.srvup.com).

### HTTP Request

`GET https://api.srvup.com/v1/posts/`


### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | Changes maximum number of returned results.


<aside class="success">
Remember — this endpoint is for consumption not for management!
</aside>

## Single Post Item

> Basic

```javascript
function myResponseCallback (responseData, statusCode){
  console.log(responseData, statusCode)
}
srvup.get(`/posts/${postSlug}/`, myResponseCallback)
```

> Inline callback

```javascript
srvup.get(`/posts/${postSlug}/`, (responseData, statusCode)=>{
    console.log(responseData, statusCode)
})
```


> The above command returns JSON structured like this:

```json
{
      "id": 2,
      "name": "Hello World",
      "slug": "hello-word",
      "content": "",
      "publish": ""
    }
```

This endpoint retrieves a post that has already been published otherwise returns a 404.


### HTTP Request

`GET https://api.srvup.com/v1/posts/<slug>/`


### URL Parameters

Parameter | Description
--------- | -----------
Slug | The related slug of the post to retrieve


# Pages


## All Pages

> Basic

```javascript
function myResponseCallback (responseData, statusCode){
  console.log(responseData, statusCode)
}
srvup.get('/pages/', myResponseCallback)
```

> Inline callback

```javascript
srvup.get('/pages/', (responseData, statusCode)=>{
    console.log(responseData, statusCode)
})
```

> React

```javascript
class MyComponent extends React.Compoment {
  constructor(props){
    super(props)
    this.state ={
      pages: [],
      loading: true,
    }
  }

  handleResponse = (responseData, statusCode) => {
    console.log(responseData, statusCode)
    if (statusCode === 200){
      this.setState({
        loading: false,
        pages: responseData.results
      })
    }
  }
  componentDidMount() {
    srvup.get('/pages/', this.handleResponse)
  }

  render () {
    return <h1>Results Count {this.state.pages.length}</h1>
  }
  
}
```




> Response Data

```json
{
  "results": [
    {
      "id": 1,
      "name": "Hello World",
      "slug": "hello-word",
      "content": "",
      "publish": ""
    },
    {
      "id": 2,
      "name": "Hello World",
      "slug": "hello-word",
      "content": "",
      "publish": ""
    }
  ]
}
```

This endpoint retrieves all published pages. To manage these pages, login to your account on [https://www.srvup.com](http://www.srvup.com).

### HTTP Request

`GET https://api.srvup.com/v1/pages/`


### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | Changes maximum number of returned results.


<aside class="success">
Remember — this endpoint is for consumption not for management!
</aside>

## Single Page Item

> Basic

```javascript
function myResponseCallback (responseData, statusCode){
  console.log(responseData, statusCode)
}
srvup.get(`/pages/${pageSlug}/`, myResponseCallback)
```

> Inline callback

```javascript
srvup.get(`/pages/${pageSlug}/`, (responseData, statusCode)=>{
    console.log(responseData, statusCode)
})
```


> The above command returns JSON structured like this:

```json
{
      "id": 2,
      "name": "Hello World",
      "slug": "hello-word",
      "content": "",
      "publish": ""
    }
```

This endpoint retrieves a page that has already been published otherwise returns a 404.


### HTTP Request

`GET https://api.srvup.com/v1/pages/<slug>/`


### URL Parameters

Parameter | Description
--------- | -----------
Slug | The related slug of the page to retrieve

