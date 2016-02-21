i18n in node.js
=======

Howto get started with the [i18n](https://www.npmjs.com/package/i18n) module in an node.js cli, application or website.

### Install
```sh
npm install i18n --save
```

### Load
```js
var express = require('express'),
    i18n = require("i18n");
```

### Configure

```js
i18n.configure({
    locales:['en', 'de'],
    directory: __dirname + '/locales'
});
```

### Use

```js
app.use(i18n.init());

app.get('/de', function(req, res){
  var greeting = res.__('Hello');
});
```

### Translate

```json
{
    "Hello": "Hallo"
}
```

go ahead to learn about the details. 
