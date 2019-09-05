# Blog Tools for 11ty

This plugin is a series of shortcodes and filters that aim to help you write and organize your blog

## Install instructions

Available on [npm](https://www.npmjs.com/package/eleventy-plugin-blog-tools).

```
npm install eleventy-plugin-blog-tools --save
```

Open up your Eleventy config file (probably `.eleventy.js`) and add the plugin:

```
const blogTools = require("eleventy-plugin-blog-tools");
module.exports = function(eleventyConfig) {
  eleventyConfig.addPlugin(blogTools);
};
```

## Usage

There are multiple shortcodes and filters in this plugin. Each has its own usage.

### YouTube

The YouTube shortcode takes a YouTube video ID and creates the markup for a fluidly-responsive YouTube embed.

```
{% youtube "idstring" %}
```

### CodePen

The CodePen shortcode takes multiple values to customize your embed.
```
{% codepen "URL", {options} %}

{% codepen "https://codepen.io/url/path" %}
{% codepen "http://codepen.io/brob/pen/vGRBeQ/", "css,result", "900", "26704"  %}

```

The various options have a required order (hopefully that will change in the future): 
* `url`: The full URL to your pen 
* `tabs`: String of the tabs of your codepen to display (default: `"html,result"`)
* `height`: A unitless value of the height in pixels (default: `"300"`)
* `theme`: If you have a saved theme in your Pens, you can use them with the id of the theme (default: `""`);

The first argument is the only required argument and it's the Pen's full URL. In Nunjucks, they need to be comma separated, in Liquid commas are optional.

## Related Filter

The related filter will pull items from a list based on parameters passed to the function.

### Usage

The basic usage is to filter a collection based on an array of items and a threshold.

Syntax: `{{ collections.posts | related(<sort-field-key>, <sort-field-data>, <threshold-integer Defaults to 1>, <URL-to-Exclude-optional>)}}`

The threshold integer is meant to force a number of array items in common. Defaults to 1.

```
{% for post in collections.posts | related("sortField", sortField, 1) %}
  {{ post.data.title }}
{% endfor %}
```