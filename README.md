Custom Callback for HTML Webpack Plugin
=======================================

This is an extension plugin for the [webpack](http://webpack.github.io) plugin [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin) - a plugin that simplifies the creation of HTML files to serve your webpack bundles.

The raw [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin) incorporates all webpack-generated javascipt as synchronous`<script>` elements in the generated html.  This plugin allows you to:
- add custom callback to update HTML

Installation
------------
You must be running webpack (4.x) on node 6+.
Install the plugin with npm:
```shell
$ npm install html-webpack-custom-callback-plugin --save-dev
```
Not that you will need v3.0.6+ of [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin)

Usage
-----------
Add the plugin to your webpack config as follows: 

```javascript
plugins: [
  new HtmlWebpackPlugin(),
  new HtmlWebpackCustomCallbackPlugin({
    callback: updateBundleHtml,
  }),
]  
```
Here is the example of custom callback
```javascript
const updateAbtestBundleHtml = (html) => {
  // Strip <head> tags.
  html = html.replace(/<(\/)?head>/g, '');
  // Swap <style> and <script> positions.
  html = html.replace(/(<style .*(?=<\/style>)<\/style>)(<script .*(?=<\/script>)<\/script>)/, '$2$1');
  return html;
}
```
