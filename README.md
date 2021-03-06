Fork from [mixpanel](https://github.com/mixpanel/mixpanel-js)
# 修改
## 添加 track_timeout 配置项
  用于配置发送 xhr 请求超时时间, 默认 300 (ms)
## 修改 identify 方法
  删除对 alias id 的判断
## 修改 alias 函数参数
  添加 callback 参数

## 添加 mixpanel.set_client_ip 方法
如果设置 config.ip = false 则该方法则失效，详细见[Special properties in events](https://mixpanel.com/help/reference/http#tracking-events)中的 ip 参数
注：使用 mixpanel.register({ ip: ip }) 存储设置的ip地址

ip 将用于设置用户的国家及地区: `mixpanel.set_client_ip(ip)`
清除 ip 设置: `mixpanel.set_client_ip(null)`
你可以使用下面的方法获取上一次设置的ip: `mixpanel.get_property('ip')`

# Mixpanel JavaScript Library
The Mixpanel JavaScript Library is a set of methods attached to a global `mixpanel` object
intended to be used by websites wishing to send data to Mixpanel projects. A full reference
is available [here](https://mixpanel.com/help/reference/javascript).

## Alternative installation via NPM
This library is available as a [package on NPM](https://www.npmjs.com/package/mixpanel-browser) (named `mixpanel-browser` to distinguish it from Mixpanel's server-side Node.js library, available on NPM as `mixpanel`). To install into a project using NPM with a front-end packager such as [Browserify](http://browserify.org/) or [Webpack](https://webpack.github.io/):

```sh
npm install --save mixpanel-browser
```

You can then require the lib like a standard Node.js module:

```javascript
var mixpanel = require('mixpanel-browser');

mixpanel.init("YOUR_TOKEN");
mixpanel.track("An event");
```

## Alternative installation via Bower
`mixpanel-js` is also available via front-end package manager [Bower](http://bower.io/). After installing Bower, fetch into your project's `bower_components` dir with:
```sh
bower install mixpanel
```

### Using Bower to load the snippet
You can then load the lib via the embed code (snippet) with a script reference:
```html
<script src="bower_components/mixpanel/mixpanel-jslib-snippet.min.js"></script>
```
which loads the _latest_ library version from the Mixpanel CDN ([http://cdn.mxpnl.com/libs/mixpanel-2-latest.min.js](http://cdn.mxpnl.com/libs/mixpanel-2-latest.min.js)).

### Using Bower to load the entire library
If you wish to load the specific version downloaded in your Bower package, there are two options.

1) Override the CDN library location with the global `MIXPANEL_CUSTOM_LIB_URL` var:
```html
<script>
  window.MIXPANEL_CUSTOM_LIB_URL = 'bower_components/mixpanel/mixpanel.js';
</script>
<script src="bower_components/mixpanel/mixpanel-jslib-snippet.min.js"></script>
```
or

2) Recompile the snippet with a custom `MIXPANEL_LIB_URL` using [Closure Compiler](https://developers.google.com/closure/compiler/):
```sh
java -jar compiler.jar --js mixpanel-jslib-snippet.js --js_output_file mixpanel-jslib-snippet.min.js --compilation_level ADVANCED_OPTIMIZATIONS --define='MIXPANEL_LIB_URL="bower_components/mixpanel/mixpanel.js"'
```

### Upgrading from mixpanel-bower v2.2.0 or v2.0.0
If you originally installed Mixpanel via Bower at its previous home ([https://github.com/drubin/mixpanel-bower](https://github.com/drubin/mixpanel-bower)), the two old versions have remained functionally unchanged. To upgrade to v2.3.6 or later (the first Bower version in the official repo) from a previous Bower install, note the changed filenames: previous references to `mixpanel.js` should become `mixpanel-jslib-snippet.min.js` (the minified embed code), and previous references to `mixpanel.dev.js` should become `mixpanel.js` (the library source) or `mixpanel.min.js` (the minified library for production use).

## Building bundles for release
- Install development dependencies: `npm install`
- Build: `npm run build`

## Running tests
- Install development dependencies: `npm install`
- Start test server: `npm test`
- Browse to [http://localhost:3000/tests/](http://localhost:3000/tests/) and choose a scenario to run

In the future we plan to automate the last step with a headless browser to streamline development (although
Mixpanel production releases are tested against a large matrix of browsers and operating systems).

## Thanks
For patches and support: @bohanyang, @dehau, @drubin, @D1plo1d, @feychenie, @mogstad, @pfhayes, @sandorfr, @stefansedich
