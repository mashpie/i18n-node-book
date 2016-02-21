# From scratch to cli

Ok, the only assumption is an installed working version of node.js and npm. If you never ever worked with node on your machine: [Learn how to install Node.js and npm here](https://docs.npmjs.com/getting-started/installing-node).

Let's start with an empty directory and init a new application. 

```shell
$ npm init
```

Just commit the defaults for now. You'll end up with a directory containing just one single file `package.json`:

```shell
$ tree -L 2
.
└── package.json
```

Now add another file `index.js` and paste some code:

```js
// any hello world should do
console.log('Hello');
```

Not to surprisingly see what you get when you run `index.js` with node:

```shell
$ node index
Hello
```

## Install and configure i18n
It's time to add some i18n to take care of localized strings:

```js
$ npm install i18n --save
```

That adds the module itself to your directory and `package.json`.

```shell
$ tree -L 2
.
├── index.js
├── node_modules
│   └── i18n
└── package.json
```

Ready to use i18n in your `index.js`:

```js
// require module
var i18n = require('i18n');

// configure module
i18n.configure({
  locales:['en', 'de'],
  directory: __dirname + '/locales'
});

// output in default locale
console.log(i18n.__('Hello'));
```
Again, see what you get when you run `index.js` with node:

```shell
$ node index
Hello
```
i18n has added the skeleton directory of locale-files as configured in `i18n.configure()` above:

```shell
tree -L 2
.
├── index.js
├── locales
│   ├── de.json
│   └── en.json
├── node_modules
│   └── i18n
└── package.json
```

## Add and test your first translation
Now go ahead and edit the `locales/de.json` file according to:

```json
{
    "Hello": "Hallo"
}
```

And switch the locale setting in your tiny little cli skript, ie. like so:

```js
// output in default locale 
console.log('default: ', i18n.__('Hello'));

// switch current locale
i18n.setLocale('de');

// output should be in german now
console.log('german: ', i18n.__('Hello'));
```

Again, see what you get when you run `index.js` with node:

```shell
$ node index.js
default:  Hello
german:  Hallo
```

> Heads up! This is the simplest possible implementation of i18n. It sticks to all defaults and will work fine for single user cli scripting as i18n can be used globally in that case. In order to use it in context of web applications you'll need to ensure separated scopes for each request as been shown in "From CLI to HTTP".