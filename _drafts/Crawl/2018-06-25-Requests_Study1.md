---
# layout: "post"
title: "Request 예제1"
slug: request1
# categories: Crawl
tag: Crawl
header:
  teaser: /assets/images/9.png
---
## Request 라이브러리의 예제


  <div class="input_area" markdown="1">

```python
import requests, json
```

  </div>

### request를 확인할 수 있는 사이트
- https://httpbin.org


  <div class="input_area" markdown="1">

```python
s = requests.Session()
r = s.get('https://httpbin.org')
print('1',r.text)
```

  </div>

  {:.output_stream}
  ```
  1 <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>httpbin.org</title>
  <link href="https://fonts.googleapis.com/css?family=Open+Sans:400,700|Source+Code+Pro:300,600|Titillium+Web:400,600,700" rel="stylesheet">
  <link rel="stylesheet" type="text/css" href="/flasgger_static/swagger-ui.css" >
  <link rel="icon" type="image/png" href="/flasgger_static/favicon-32x32.png" sizes="32x32" />
  <link rel="icon" type="image/png" href="/flasgger_static/favicon-16x16.png" sizes="16x16" />
  <style>
    html
    {
        box-sizing: border-box;
        overflow: -moz-scrollbars-vertical;
        overflow-y: scroll;
    }
    *,
    *:before,
    *:after
    {
        box-sizing: inherit;
    }

    body {
      margin:0;
      background: #fafafa;
    }
  </style>
</head>

<body>
    <a href="https://github.com/requests/httpbin" class="github-corner" aria-label="View source on Github">
  <svg width="80" height="80" viewBox="0 0 250 250" style="fill:#151513; color:#fff; position: absolute; top: 0; border: 0; right: 0;" aria-hidden="true">
    <path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path>
    <path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path>
    <path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path>
  </svg>
</a>
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" style="position:absolute;width:0;height:0">
  <defs>
    <symbol viewBox="0 0 20 20" id="unlocked">
          <path d="M15.8 8H14V5.6C14 2.703 12.665 1 10 1 7.334 1 6 2.703 6 5.6V6h2v-.801C8 3.754 8.797 3 10 3c1.203 0 2 .754 2 2.199V8H4c-.553 0-1 .646-1 1.199V17c0 .549.428 1.139.951 1.307l1.197.387C5.672 18.861 6.55 19 7.1 19h5.8c.549 0 1.428-.139 1.951-.307l1.196-.387c.524-.167.953-.757.953-1.306V9.199C17 8.646 16.352 8 15.8 8z"></path>
    </symbol>

    <symbol viewBox="0 0 20 20" id="locked">
      <path d="M15.8 8H14V5.6C14 2.703 12.665 1 10 1 7.334 1 6 2.703 6 5.6V8H4c-.553 0-1 .646-1 1.199V17c0 .549.428 1.139.951 1.307l1.197.387C5.672 18.861 6.55 19 7.1 19h5.8c.549 0 1.428-.139 1.951-.307l1.196-.387c.524-.167.953-.757.953-1.306V9.199C17 8.646 16.352 8 15.8 8zM12 8H8V5.199C8 3.754 8.797 3 10 3c1.203 0 2 .754 2 2.199V8z"/>
    </symbol>

    <symbol viewBox="0 0 20 20" id="close">
      <path d="M14.348 14.849c-.469.469-1.229.469-1.697 0L10 11.819l-2.651 3.029c-.469.469-1.229.469-1.697 0-.469-.469-.469-1.229 0-1.697l2.758-3.15-2.759-3.152c-.469-.469-.469-1.228 0-1.697.469-.469 1.228-.469 1.697 0L10 8.183l2.651-3.031c.469-.469 1.228-.469 1.697 0 .469.469.469 1.229 0 1.697l-2.758 3.152 2.758 3.15c.469.469.469 1.229 0 1.698z"/>
    </symbol>

    <symbol viewBox="0 0 20 20" id="large-arrow">
      <path d="M13.25 10L6.109 2.58c-.268-.27-.268-.707 0-.979.268-.27.701-.27.969 0l7.83 7.908c.268.271.268.709 0 .979l-7.83 7.908c-.268.271-.701.27-.969 0-.268-.269-.268-.707 0-.979L13.25 10z"/>
    </symbol>

    <symbol viewBox="0 0 20 20" id="large-arrow-down">
      <path d="M17.418 6.109c.272-.268.709-.268.979 0s.271.701 0 .969l-7.908 7.83c-.27.268-.707.268-.979 0l-7.908-7.83c-.27-.268-.27-.701 0-.969.271-.268.709-.268.979 0L10 13.25l7.418-7.141z"/>
    </symbol>


    <symbol viewBox="0 0 24 24" id="jump-to">
      <path d="M19 7v4H5.83l3.58-3.59L8 6l-6 6 6 6 1.41-1.41L5.83 13H21V7z"/>
    </symbol>

    <symbol viewBox="0 0 24 24" id="expand">
      <path d="M10 18h4v-2h-4v2zM3 6v2h18V6H3zm3 7h12v-2H6v2z"/>
    </symbol>

  </defs>
</svg>


<div id="swagger-ui">
    <div data-reactroot="" class="swagger-ui">
        <div>
        <div class="information-container wrapper">
            <section class="block col-12">
                <div class="info">
                <hgroup class="main">
                    <h2 class="title">httpbin.org<small><pre class="version">0.9.0</pre></small></h2>
                    <pre class="base-url">[ Base URL: httpbin.org/ ]</pre>
                </hgroup>
                <div class="description">
                    <div class="markdown">
                    <p>A simple HTTP Request &amp; Response Service.
                    <br> <br> <b>Run locally: </b> <code>$ docker run -p 80:80 kennethreitz/httpbin</code></p>
                    </div>
                </div>
                <div>
                  <div><a href="https://kennethreitz.org" target="_blank">the developer - Website</a></div>
                  <a href="mailto:me@kennethreitz.org">Send email to the developer</a>
                </div>
                </div>
                <!-- ADDS THE LOADER SPINNER -->
                <div class="loading-container"><div class="loading"></div></div>

            </section>
        </div>
    </div>
    </div>
</div>


<div class='swagger-ui'>
<div class="wrapper">
    <section class="clear">
        <span style="float: right;">
            [Powered by <a target="_blank" href="https://github.com/rochacbruno/flasgger">Flasgger</a>]
            <br>
        </span>
    </section>
</div>
</div>



<script src="/flasgger_static/swagger-ui-bundle.js"> </script>
<script src="/flasgger_static/swagger-ui-standalone-preset.js"> </script>
<script src='/flasgger_static/lib/jquery.min.js' type='text/javascript'></script>
<script>

window.onload = function() {


    fetch("/spec.json")
    .then(function(response) {
        response.json()
        .then(function(json) {
        var current_protocol = window.location.protocol.slice(0, -1);
        if (json.schemes[0] != current_protocol){
            // Switches scheme to the current in use
            var other_protocol = json.schemes[0];
            json.schemes[0] = current_protocol;
            json.schemes[1] = other_protocol;

        }
        json.host = window.location.host;  // sets the current host

        const ui = SwaggerUIBundle({
            spec: json,
            validatorUrl: null,
            dom_id: '#swagger-ui',
            deepLinking: true,
            jsonEditor: true,
            docExpansion: "none",
            apisSorter: "alpha",
            //operationsSorter: "alpha",
            presets: [
                SwaggerUIBundle.presets.apis,
                // yay ES6 modules ↘
                Array.isArray(SwaggerUIStandalonePreset) ? SwaggerUIStandalonePreset : SwaggerUIStandalonePreset.default
            ],
            plugins: [
                SwaggerUIBundle.plugins.DownloadUrl
            ],

            // layout: "StandaloneLayout"  // uncomment to enable the green top header
        })

        window.ui = ui

        // uncomment to rename the top brand if layout is enabled
        // $(".topbar-wrapper .link span").replaceWith("<span>httpbin</span>");
        })
    })
}
</script>




<script type="text/javascript">
  var _gauges = _gauges || [];
  (function() {
    var t   = document.createElement('script');
    t.type  = 'text/javascript';
    t.async = true;
    t.id    = 'gauges-tracker';
    t.setAttribute('data-site-id', '58cb2e71c88d9043ac01d000');
    t.setAttribute('data-track-path', 'https://track.gaug.es/track.gif');
    t.src = 'https://d36ee2fcip1434.cloudfront.net/track.js';
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(t, s);
  })();
</script>


<div class='swagger-ui'>
<div class="wrapper">
<section class="block col-12 block-desktop col-12-desktop">
<div>

<h2>Other Utilities</h2>

<ul>
    <li><a href="/forms/post">HTML form</a> that posts to /post /forms/post</li>
    <li><a href='//now.httpbin.org'>now.httpbin.org</a> The current time, in a variety of formats."</li>
</ul>

<br /><br />
</div>
</section>
</div>
</div>
</body>
</html>

  ```


  <div class="input_area" markdown="1">

```python
r = s.get('http://httpbin.org/cookies',cookies={'from':'myName'})
print(r.text)
```

  </div>

  {:.output_stream}
  ```
  {"cookies":{"from":"myName"}}


  ```


  <div class="input_area" markdown="1">

```python
url = 'http://httpbin.org/get'
headers = {'user-agent':'myPythonApp'}
r = s.get(url,headers=headers)
print(r.text)
```

  </div>

  {:.output_stream}
  ```
  {"args":{},"headers":{"Accept":"*/*","Accept-Encoding":"gzip, deflate","Connection":"close","Host":"httpbin.org","User-Agent":"myPythonApp"},"origin":"211.173.143.94","url":"http://httpbin.org/get"}


  ```


  <div class="input_area" markdown="1">

```python
s.close()
```

  </div>

### 아래와 같은 문법으로 사용할 수도 있다.


  <div class="input_area" markdown="1">

```python
with requests.Session() as s:
    r = s.get("http://httpbin.org/")
    print(r.text)
```

  </div>

  {:.output_stream}
  ```
  <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>httpbin.org</title>
  <link href="https://fonts.googleapis.com/css?family=Open+Sans:400,700|Source+Code+Pro:300,600|Titillium+Web:400,600,700" rel="stylesheet">
  <link rel="stylesheet" type="text/css" href="/flasgger_static/swagger-ui.css" >
  <link rel="icon" type="image/png" href="/flasgger_static/favicon-32x32.png" sizes="32x32" />
  <link rel="icon" type="image/png" href="/flasgger_static/favicon-16x16.png" sizes="16x16" />
  <style>
    html
    {
        box-sizing: border-box;
        overflow: -moz-scrollbars-vertical;
        overflow-y: scroll;
    }
    *,
    *:before,
    *:after
    {
        box-sizing: inherit;
    }

    body {
      margin:0;
      background: #fafafa;
    }
  </style>
</head>

<body>
    <a href="https://github.com/requests/httpbin" class="github-corner" aria-label="View source on Github">
  <svg width="80" height="80" viewBox="0 0 250 250" style="fill:#151513; color:#fff; position: absolute; top: 0; border: 0; right: 0;" aria-hidden="true">
    <path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path>
    <path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path>
    <path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path>
  </svg>
</a>
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" style="position:absolute;width:0;height:0">
  <defs>
    <symbol viewBox="0 0 20 20" id="unlocked">
          <path d="M15.8 8H14V5.6C14 2.703 12.665 1 10 1 7.334 1 6 2.703 6 5.6V6h2v-.801C8 3.754 8.797 3 10 3c1.203 0 2 .754 2 2.199V8H4c-.553 0-1 .646-1 1.199V17c0 .549.428 1.139.951 1.307l1.197.387C5.672 18.861 6.55 19 7.1 19h5.8c.549 0 1.428-.139 1.951-.307l1.196-.387c.524-.167.953-.757.953-1.306V9.199C17 8.646 16.352 8 15.8 8z"></path>
    </symbol>

    <symbol viewBox="0 0 20 20" id="locked">
      <path d="M15.8 8H14V5.6C14 2.703 12.665 1 10 1 7.334 1 6 2.703 6 5.6V8H4c-.553 0-1 .646-1 1.199V17c0 .549.428 1.139.951 1.307l1.197.387C5.672 18.861 6.55 19 7.1 19h5.8c.549 0 1.428-.139 1.951-.307l1.196-.387c.524-.167.953-.757.953-1.306V9.199C17 8.646 16.352 8 15.8 8zM12 8H8V5.199C8 3.754 8.797 3 10 3c1.203 0 2 .754 2 2.199V8z"/>
    </symbol>

    <symbol viewBox="0 0 20 20" id="close">
      <path d="M14.348 14.849c-.469.469-1.229.469-1.697 0L10 11.819l-2.651 3.029c-.469.469-1.229.469-1.697 0-.469-.469-.469-1.229 0-1.697l2.758-3.15-2.759-3.152c-.469-.469-.469-1.228 0-1.697.469-.469 1.228-.469 1.697 0L10 8.183l2.651-3.031c.469-.469 1.228-.469 1.697 0 .469.469.469 1.229 0 1.697l-2.758 3.152 2.758 3.15c.469.469.469 1.229 0 1.698z"/>
    </symbol>

    <symbol viewBox="0 0 20 20" id="large-arrow">
      <path d="M13.25 10L6.109 2.58c-.268-.27-.268-.707 0-.979.268-.27.701-.27.969 0l7.83 7.908c.268.271.268.709 0 .979l-7.83 7.908c-.268.271-.701.27-.969 0-.268-.269-.268-.707 0-.979L13.25 10z"/>
    </symbol>

    <symbol viewBox="0 0 20 20" id="large-arrow-down">
      <path d="M17.418 6.109c.272-.268.709-.268.979 0s.271.701 0 .969l-7.908 7.83c-.27.268-.707.268-.979 0l-7.908-7.83c-.27-.268-.27-.701 0-.969.271-.268.709-.268.979 0L10 13.25l7.418-7.141z"/>
    </symbol>


    <symbol viewBox="0 0 24 24" id="jump-to">
      <path d="M19 7v4H5.83l3.58-3.59L8 6l-6 6 6 6 1.41-1.41L5.83 13H21V7z"/>
    </symbol>

    <symbol viewBox="0 0 24 24" id="expand">
      <path d="M10 18h4v-2h-4v2zM3 6v2h18V6H3zm3 7h12v-2H6v2z"/>
    </symbol>

  </defs>
</svg>


<div id="swagger-ui">
    <div data-reactroot="" class="swagger-ui">
        <div>
        <div class="information-container wrapper">
            <section class="block col-12">
                <div class="info">
                <hgroup class="main">
                    <h2 class="title">httpbin.org<small><pre class="version">0.9.0</pre></small></h2>
                    <pre class="base-url">[ Base URL: httpbin.org/ ]</pre>
                </hgroup>
                <div class="description">
                    <div class="markdown">
                    <p>A simple HTTP Request &amp; Response Service.
                    <br> <br> <b>Run locally: </b> <code>$ docker run -p 80:80 kennethreitz/httpbin</code></p>
                    </div>
                </div>
                <div>
                  <div><a href="https://kennethreitz.org" target="_blank">the developer - Website</a></div>
                  <a href="mailto:me@kennethreitz.org">Send email to the developer</a>
                </div>
                </div>
                <!-- ADDS THE LOADER SPINNER -->
                <div class="loading-container"><div class="loading"></div></div>

            </section>
        </div>
    </div>
    </div>
</div>


<div class='swagger-ui'>
<div class="wrapper">
    <section class="clear">
        <span style="float: right;">
            [Powered by <a target="_blank" href="https://github.com/rochacbruno/flasgger">Flasgger</a>]
            <br>
        </span>
    </section>
</div>
</div>



<script src="/flasgger_static/swagger-ui-bundle.js"> </script>
<script src="/flasgger_static/swagger-ui-standalone-preset.js"> </script>
<script src='/flasgger_static/lib/jquery.min.js' type='text/javascript'></script>
<script>

window.onload = function() {


    fetch("/spec.json")
    .then(function(response) {
        response.json()
        .then(function(json) {
        var current_protocol = window.location.protocol.slice(0, -1);
        if (json.schemes[0] != current_protocol){
            // Switches scheme to the current in use
            var other_protocol = json.schemes[0];
            json.schemes[0] = current_protocol;
            json.schemes[1] = other_protocol;

        }
        json.host = window.location.host;  // sets the current host

        const ui = SwaggerUIBundle({
            spec: json,
            validatorUrl: null,
            dom_id: '#swagger-ui',
            deepLinking: true,
            jsonEditor: true,
            docExpansion: "none",
            apisSorter: "alpha",
            //operationsSorter: "alpha",
            presets: [
                SwaggerUIBundle.presets.apis,
                // yay ES6 modules ↘
                Array.isArray(SwaggerUIStandalonePreset) ? SwaggerUIStandalonePreset : SwaggerUIStandalonePreset.default
            ],
            plugins: [
                SwaggerUIBundle.plugins.DownloadUrl
            ],

            // layout: "StandaloneLayout"  // uncomment to enable the green top header
        })

        window.ui = ui

        // uncomment to rename the top brand if layout is enabled
        // $(".topbar-wrapper .link span").replaceWith("<span>httpbin</span>");
        })
    })
}
</script>




<script type="text/javascript">
  var _gauges = _gauges || [];
  (function() {
    var t   = document.createElement('script');
    t.type  = 'text/javascript';
    t.async = true;
    t.id    = 'gauges-tracker';
    t.setAttribute('data-site-id', '58cb2e71c88d9043ac01d000');
    t.setAttribute('data-track-path', 'https://track.gaug.es/track.gif');
    t.src = 'https://d36ee2fcip1434.cloudfront.net/track.js';
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(t, s);
  })();
</script>


<div class='swagger-ui'>
<div class="wrapper">
<section class="block col-12 block-desktop col-12-desktop">
<div>

<h2>Other Utilities</h2>

<ul>
    <li><a href="/forms/post">HTML form</a> that posts to /post /forms/post</li>
    <li><a href='//now.httpbin.org'>now.httpbin.org</a> The current time, in a variety of formats."</li>
</ul>

<br /><br />
</div>
</section>
</div>
</div>
</body>
</html>

  ```

## Response code


  <div class="input_area" markdown="1">

```python
s =requests.Session()
r = s.get("http://httpbin.org/get")
print(r.status_code)
print(r.ok)
```

  </div>

  {:.output_stream}
  ```
  200
True

  ```

## Json 가공
- https://jsonplaceholder.typicode.com
- json을 연습삼아 받을 수 있는 사이트


  <div class="input_area" markdown="1">

```python
r = s.get('https://jsonplaceholder.typicode.com/albums')
print(r.text)
```

  </div>

  {:.output_stream}
  ```
  [
  {
    "userId": 1,
    "id": 1,
    "title": "quidem molestiae enim"
  },
  {
    "userId": 1,
    "id": 2,
    "title": "sunt qui excepturi placeat culpa"
  },
  {
    "userId": 1,
    "id": 3,
    "title": "omnis laborum odio"
  },
  {
    "userId": 1,
    "id": 4,
    "title": "non esse culpa molestiae omnis sed optio"
  },
  {
    "userId": 1,
    "id": 5,
    "title": "eaque aut omnis a"
  },
  {
    "userId": 1,
    "id": 6,
    "title": "natus impedit quibusdam illo est"
  },
  {
    "userId": 1,
    "id": 7,
    "title": "quibusdam autem aliquid et et quia"
  },
  {
    "userId": 1,
    "id": 8,
    "title": "qui fuga est a eum"
  },
  {
    "userId": 1,
    "id": 9,
    "title": "saepe unde necessitatibus rem"
  },
  {
    "userId": 1,
    "id": 10,
    "title": "distinctio laborum qui"
  },
  {
    "userId": 2,
    "id": 11,
    "title": "quam nostrum impedit mollitia quod et dolor"
  },
  {
    "userId": 2,
    "id": 12,
    "title": "consequatur autem doloribus natus consectetur"
  },
  {
    "userId": 2,
    "id": 13,
    "title": "ab rerum non rerum consequatur ut ea unde"
  },
  {
    "userId": 2,
    "id": 14,
    "title": "ducimus molestias eos animi atque nihil"
  },
  {
    "userId": 2,
    "id": 15,
    "title": "ut pariatur rerum ipsum natus repellendus praesentium"
  },
  {
    "userId": 2,
    "id": 16,
    "title": "voluptatem aut maxime inventore autem magnam atque repellat"
  },
  {
    "userId": 2,
    "id": 17,
    "title": "aut minima voluptatem ut velit"
  },
  {
    "userId": 2,
    "id": 18,
    "title": "nesciunt quia et doloremque"
  },
  {
    "userId": 2,
    "id": 19,
    "title": "velit pariatur quaerat similique libero omnis quia"
  },
  {
    "userId": 2,
    "id": 20,
    "title": "voluptas rerum iure ut enim"
  },
  {
    "userId": 3,
    "id": 21,
    "title": "repudiandae voluptatem optio est consequatur rem in temporibus et"
  },
  {
    "userId": 3,
    "id": 22,
    "title": "et rem non provident vel ut"
  },
  {
    "userId": 3,
    "id": 23,
    "title": "incidunt quisquam hic adipisci sequi"
  },
  {
    "userId": 3,
    "id": 24,
    "title": "dolores ut et facere placeat"
  },
  {
    "userId": 3,
    "id": 25,
    "title": "vero maxime id possimus sunt neque et consequatur"
  },
  {
    "userId": 3,
    "id": 26,
    "title": "quibusdam saepe ipsa vel harum"
  },
  {
    "userId": 3,
    "id": 27,
    "title": "id non nostrum expedita"
  },
  {
    "userId": 3,
    "id": 28,
    "title": "omnis neque exercitationem sed dolor atque maxime aut cum"
  },
  {
    "userId": 3,
    "id": 29,
    "title": "inventore ut quasi magnam itaque est fugit"
  },
  {
    "userId": 3,
    "id": 30,
    "title": "tempora assumenda et similique odit distinctio error"
  },
  {
    "userId": 4,
    "id": 31,
    "title": "adipisci laborum fuga laboriosam"
  },
  {
    "userId": 4,
    "id": 32,
    "title": "reiciendis dolores a ut qui debitis non quo labore"
  },
  {
    "userId": 4,
    "id": 33,
    "title": "iste eos nostrum"
  },
  {
    "userId": 4,
    "id": 34,
    "title": "cumque voluptatibus rerum architecto blanditiis"
  },
  {
    "userId": 4,
    "id": 35,
    "title": "et impedit nisi quae magni necessitatibus sed aut pariatur"
  },
  {
    "userId": 4,
    "id": 36,
    "title": "nihil cupiditate voluptate neque"
  },
  {
    "userId": 4,
    "id": 37,
    "title": "est placeat dicta ut nisi rerum iste"
  },
  {
    "userId": 4,
    "id": 38,
    "title": "unde a sequi id"
  },
  {
    "userId": 4,
    "id": 39,
    "title": "ratione porro illum labore eum aperiam sed"
  },
  {
    "userId": 4,
    "id": 40,
    "title": "voluptas neque et sint aut quo odit"
  },
  {
    "userId": 5,
    "id": 41,
    "title": "ea voluptates maiores eos accusantium officiis tempore mollitia consequatur"
  },
  {
    "userId": 5,
    "id": 42,
    "title": "tenetur explicabo ea"
  },
  {
    "userId": 5,
    "id": 43,
    "title": "aperiam doloremque nihil"
  },
  {
    "userId": 5,
    "id": 44,
    "title": "sapiente cum numquam officia consequatur vel natus quos suscipit"
  },
  {
    "userId": 5,
    "id": 45,
    "title": "tenetur quos ea unde est enim corrupti qui"
  },
  {
    "userId": 5,
    "id": 46,
    "title": "molestiae voluptate non"
  },
  {
    "userId": 5,
    "id": 47,
    "title": "temporibus molestiae aut"
  },
  {
    "userId": 5,
    "id": 48,
    "title": "modi consequatur culpa aut quam soluta alias perspiciatis laudantium"
  },
  {
    "userId": 5,
    "id": 49,
    "title": "ut aut vero repudiandae voluptas ullam voluptas at consequatur"
  },
  {
    "userId": 5,
    "id": 50,
    "title": "sed qui sed quas sit ducimus dolor"
  },
  {
    "userId": 6,
    "id": 51,
    "title": "odit laboriosam sint quia cupiditate animi quis"
  },
  {
    "userId": 6,
    "id": 52,
    "title": "necessitatibus quas et sunt at voluptatem"
  },
  {
    "userId": 6,
    "id": 53,
    "title": "est vel sequi voluptatem nemo quam molestiae modi enim"
  },
  {
    "userId": 6,
    "id": 54,
    "title": "aut non illo amet perferendis"
  },
  {
    "userId": 6,
    "id": 55,
    "title": "qui culpa itaque omnis in nesciunt architecto error"
  },
  {
    "userId": 6,
    "id": 56,
    "title": "omnis qui maiores tempora officiis omnis rerum sed repellat"
  },
  {
    "userId": 6,
    "id": 57,
    "title": "libero excepturi voluptatem est architecto quae voluptatum officia tempora"
  },
  {
    "userId": 6,
    "id": 58,
    "title": "nulla illo consequatur aspernatur veritatis aut error delectus et"
  },
  {
    "userId": 6,
    "id": 59,
    "title": "eligendi similique provident nihil"
  },
  {
    "userId": 6,
    "id": 60,
    "title": "omnis mollitia sunt aliquid eum consequatur fugit minus laudantium"
  },
  {
    "userId": 7,
    "id": 61,
    "title": "delectus iusto et"
  },
  {
    "userId": 7,
    "id": 62,
    "title": "eos ea non recusandae iste ut quasi"
  },
  {
    "userId": 7,
    "id": 63,
    "title": "velit est quam"
  },
  {
    "userId": 7,
    "id": 64,
    "title": "autem voluptatem amet iure quae"
  },
  {
    "userId": 7,
    "id": 65,
    "title": "voluptates delectus iure iste qui"
  },
  {
    "userId": 7,
    "id": 66,
    "title": "velit sed quia dolor dolores delectus"
  },
  {
    "userId": 7,
    "id": 67,
    "title": "ad voluptas nostrum et nihil"
  },
  {
    "userId": 7,
    "id": 68,
    "title": "qui quasi nihil aut voluptatum sit dolore minima"
  },
  {
    "userId": 7,
    "id": 69,
    "title": "qui aut est"
  },
  {
    "userId": 7,
    "id": 70,
    "title": "et deleniti unde"
  },
  {
    "userId": 8,
    "id": 71,
    "title": "et vel corporis"
  },
  {
    "userId": 8,
    "id": 72,
    "title": "unde exercitationem ut"
  },
  {
    "userId": 8,
    "id": 73,
    "title": "quos omnis officia"
  },
  {
    "userId": 8,
    "id": 74,
    "title": "quia est eius vitae dolor"
  },
  {
    "userId": 8,
    "id": 75,
    "title": "aut quia expedita non"
  },
  {
    "userId": 8,
    "id": 76,
    "title": "dolorem magnam facere itaque ut reprehenderit tenetur corrupti"
  },
  {
    "userId": 8,
    "id": 77,
    "title": "cupiditate sapiente maiores iusto ducimus cum excepturi veritatis quia"
  },
  {
    "userId": 8,
    "id": 78,
    "title": "est minima eius possimus ea ratione velit et"
  },
  {
    "userId": 8,
    "id": 79,
    "title": "ipsa quae voluptas natus ut suscipit soluta quia quidem"
  },
  {
    "userId": 8,
    "id": 80,
    "title": "id nihil reprehenderit"
  },
  {
    "userId": 9,
    "id": 81,
    "title": "quibusdam sapiente et"
  },
  {
    "userId": 9,
    "id": 82,
    "title": "recusandae consequatur vel amet unde"
  },
  {
    "userId": 9,
    "id": 83,
    "title": "aperiam odio fugiat"
  },
  {
    "userId": 9,
    "id": 84,
    "title": "est et at eos expedita"
  },
  {
    "userId": 9,
    "id": 85,
    "title": "qui voluptatem consequatur aut ab quis temporibus praesentium"
  },
  {
    "userId": 9,
    "id": 86,
    "title": "eligendi mollitia alias aspernatur vel ut iusto"
  },
  {
    "userId": 9,
    "id": 87,
    "title": "aut aut architecto"
  },
  {
    "userId": 9,
    "id": 88,
    "title": "quas perspiciatis optio"
  },
  {
    "userId": 9,
    "id": 89,
    "title": "sit optio id voluptatem est eum et"
  },
  {
    "userId": 9,
    "id": 90,
    "title": "est vel dignissimos"
  },
  {
    "userId": 10,
    "id": 91,
    "title": "repellendus praesentium debitis officiis"
  },
  {
    "userId": 10,
    "id": 92,
    "title": "incidunt et et eligendi assumenda soluta quia recusandae"
  },
  {
    "userId": 10,
    "id": 93,
    "title": "nisi qui dolores perspiciatis"
  },
  {
    "userId": 10,
    "id": 94,
    "title": "quisquam a dolores et earum vitae"
  },
  {
    "userId": 10,
    "id": 95,
    "title": "consectetur vel rerum qui aperiam modi eos aspernatur ipsa"
  },
  {
    "userId": 10,
    "id": 96,
    "title": "unde et ut molestiae est molestias voluptatem sint"
  },
  {
    "userId": 10,
    "id": 97,
    "title": "est quod aut"
  },
  {
    "userId": 10,
    "id": 98,
    "title": "omnis quia possimus nesciunt deleniti assumenda sed autem"
  },
  {
    "userId": 10,
    "id": 99,
    "title": "consectetur ut id impedit dolores sit ad ex aut"
  },
  {
    "userId": 10,
    "id": 100,
    "title": "enim repellat iste"
  }
]

  ```


  <div class="input_area" markdown="1">

```python
r = s.get('https://jsonplaceholder.typicode.com/posts/1')
print(r.text) # 결과물은 단순 string임.
```

  </div>

  {:.output_stream}
  ```
  {
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}

  ```


  <div class="input_area" markdown="1">

```python
print(r.json()) # 결과물은 사전형태임. python에서 가공이 편함
```

  </div>

  {:.output_stream}
  ```
  {'userId': 1, 'id': 1, 'title': 'sunt aut facere repellat provident occaecati excepturi optio reprehenderit', 'body': 'quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto'}

  ```


  <div class="input_area" markdown="1">

```python
print(r.json().keys())
```

  </div>

  {:.output_stream}
  ```
  dict_keys(['userId', 'id', 'title', 'body'])

  ```


  <div class="input_area" markdown="1">

```python
print(r.json().values())
```

  </div>

  {:.output_stream}
  ```
  dict_values([1, 1, 'sunt aut facere repellat provident occaecati excepturi optio reprehenderit', 'quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto'])

  ```


  <div class="input_area" markdown="1">

```python
type(r.json()) # dict처럼 사용가능
```

  </div>




  {:.output_data_text}
  ```
  dict
  ```




  <div class="input_area" markdown="1">

```python
type(r.text)
```

  </div>




  {:.output_data_text}
  ```
  str
  ```




  <div class="input_area" markdown="1">

```python
print(r.encoding) #인코딩 확인
```

  </div>

  {:.output_stream}
  ```
  utf-8

  ```


  <div class="input_area" markdown="1">

```python
print(r.content) # binary 형태로 가져옴
```

  </div>

  {:.output_stream}
  ```
  b'{\n  "userId": 1,\n  "id": 1,\n  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",\n  "body": "quia et suscipit\\nsuscipit recusandae consequuntur expedita et cum\\nreprehenderit molestiae ut ut quas totam\\nnostrum rerum est autem sunt rem eveniet architecto"\n}'

  ```


  <div class="input_area" markdown="1">

```python
print(r.raw)
```

  </div>

  {:.output_stream}
  ```
  <urllib3.response.HTTPResponse object at 0x104b9bef0>

  ```


  <div class="input_area" markdown="1">

```python
s.close()
```

  </div>


  <div class="input_area" markdown="1">

```python
s = requests.Session()
```

  </div>


  <div class="input_area" markdown="1">

```python
r = s.get('http://httpbin.org/stream/20', stream = True)
print(r.text)
```

  </div>

  {:.output_stream}
  ```
  {"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 0}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 1}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 2}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 3}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 4}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 5}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 6}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 7}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 8}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 9}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 10}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 11}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 12}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 13}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 14}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 15}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 16}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 17}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 18}
{"url": "http://httpbin.org/stream/20", "args": {}, "headers": {"Host": "httpbin.org", "Connection": "close", "User-Agent": "python-requests/2.18.4", "Accept-Encoding": "gzip, deflate", "Accept": "*/*"}, "origin": "211.173.143.94", "id": 19}


  ```


  <div class="input_area" markdown="1">

```python
type(r)
```

  </div>




  {:.output_data_text}
  ```
  requests.models.Response
  ```




  <div class="input_area" markdown="1">

```python
print(r.encoding)
```

  </div>

  {:.output_stream}
  ```
  None

  ```


  <div class="input_area" markdown="1">

```python
if r.encoding is None :
    r.encoding ='utf-8'

for line in r.iter_lines(decode_unicode=True):
#     print(line)
    b = json.loads(line)
#     print(b['origin'])
#     print('b',b)
    for e in b.keys():
        print("key:",e,"value:",b[e])

```

  </div>

  {:.output_stream}
  ```
  key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 0
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 1
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 2
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 3
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 4
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 5
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 6
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 7
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 8
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 9
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 10
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 11
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 12
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 13
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 14
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 15
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 16
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 17
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 18
key: url value: http://httpbin.org/stream/20
key: args value: {}
key: headers value: {'Host': 'httpbin.org', 'Connection': 'close', 'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*'}
key: origin value: 211.173.143.94
key: id value: 19

  ```


  <div class="input_area" markdown="1">

```python
s.close()
```

  </div>
