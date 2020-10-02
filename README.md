# Jekyll Image Set Plugin (Pure Liquid)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Get all image URL of posts. Pure Liquid, and easy to use.**

Jekyll doesn't provide `page.images` variable, so when you want to show image in your post list, you may need to define a variable in Front Matter.

I wrote this pure liquid solution to get all image URL of post automaticly.

## Usage

1. Download `image_set.html` to `_includes` folder.
2. Use `include` tag like this:

```
{%- include image_set.html content=post.content -%}
# return first image URL of the page. 
http://via.placeholder.com/200x150
```

If you add parameter `range="all"`, this will return all image URL joined by `,`.
```
{%- include image_set.html content=post.content range=all -%}

# Return all image URL joined by comma.
http://via.placeholder.com/200x150,/i/eg_tulip.jpg
```

You can use `split` filter to turn it into array.

> ⚠️ NOTE: the result might contain whitespace on both left and right sides, use `strip` filter to remove it.

```
{%- capture img_set -%}
    {%- include image_set.html content=post.content range="all" -%}
{%- endcapture -%}

{% assign img_set = img_set | strip | split: "," %}

{% for url in img_set %}
<p>{{ url }}</p>
{% endfor %}
```

Open `index.html` as a refrence.

## Parameters

* `content`: The page content.
* `range`:
    * "first": Get first image URL of the page content.
    * "all": Get all image URL of the page content.

<sup>*</sup> You must provide content parameter, or it will return empty string. `"first"` is default value of range.  

## Demo

You can clone full repository to local, then run `jekyll serve` to view demo.

## Enviroment

- Ruby 2.7
- Jekyll 3.9.0

## License
This project is licensed under the terms of the [MIT](https://github.com/rijieli/jekyll-image-set/blob/main/LICENSE) license.