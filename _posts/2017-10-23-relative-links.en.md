---
title: Relative links
date: 2017-10-23 15:34:19 +0300
lang: en
source: 2017-10-23-relative-links.ru.md
---

There is one subject in Jekyll that enrages me. And the subject is links.

I am deeply convinced that _really_ static site must have relative links,
and not in meaning which Jekyll developers imply in filter `relative_url`.

A traditional simple example.

```html
<link rel="stylesheet" href="...">
```

How should a link to CSS looks?

| Source page               | `relative_url`    | Proper link           |
|---------------------------|-------------------|-----------------------|
| /about.html               | /css/main.css     | css/main.css          |
| /contact/main-office.html | /css/main.css     | ../css/main.css       |
| /2017/10/23/example.html  | /css/main.css     | ../../../css/main.css |

Main use case for links like that — «site on USB pen drive», possibility
to open browser without web server, just from local files.

Damn, that's one of the key features of a static build!

Also that gives possibility to host site in any subfolder of any
other site _without rebuilding_ with new `baseurl` value. Someone
might think it's not important, but not me. I want my site
will opens well without issues from some crazy address like
`http://127.0.0.1/dk487.github.io/_site/` (such a _incredible_ address,
isn't it?)

What can be done to get such kind of links? Probably
some plugin might be installed. It's not my case by many reasons,
at least because using plugins is incompatible with Github Pages.

But in general, you can do this using the Liquid only.

{% raw %}
```liquid
{%      assign root_prefix = ''
%}{%    assign root_subfolders = page.url | split: '/' | size | minus: 2
%}{%    for x in (1..root_subfolders)
%}{%        assign root_prefix = root_prefix | append: '../'
%}{%    endfor
%}<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <link rel="stylesheet" href="{{ root_prefix }}css/main.css">
```
{% endraw %}

Looks ugly, but works.

Variable {% raw %}`{{ root_prefix }}`{% endraw %} might be useful
in templates, which need to assemble proper relative links to styles,
scripts and other pages.

Site content should be written with relative links:

```markdown
Go to [front page](../../../index.en.html).
```

I hope that those ugly hacks [one day will not be necessary][1].
But for now they helps a lot.

[1]: https://github.com/jekyll/jekyll/issues/6360
