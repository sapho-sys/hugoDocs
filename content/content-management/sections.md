---
title: Content Sections
linktitle: Sections
description: "Hugo generates a **section tree** that matches your content."
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-02-01
categories: [content management]
keywords: [lists,sections,content types,organization]
menu:
  docs:
    parent: "content-management"
    weight: 50
weight: 50	#rem
draft: false
aliases: [/content/sections/]
toc: true
---


## Nested Sections

The sections can be nested as deeply as you need.

```bash
blog
├── funny-cats
│   └── kittens
│       └── _index.md
└── tech
    └── _index.md
```


**The important part to understand is, that to make the section tree fully navigational, at least the lower-most section needs a content file. (e.g. `_index.md`).** 


{{% note %}}
When we talk about a **section** in correlation with template selection, it is currently always the root section only (`/blog/funny/mypost/ => blog`). 

It is currently not possible to add a specific layout for one of the sub-sections.
{{% /note %}}


## Example: Breadcrumb Navigation

With the available [section variables and methods](#section-page-variables-and-methods) you can build powerful navigation. One common example would be a partial to show Breadcrumb navigation:


```html
<ul>
  {{ template "breadcrumbnav" (dict "p1" . "p2" .) }}
</ul>
{{ define "breadcrumbnav" }}
{{ if .p1.Parent }}
{{ template "breadcrumbnav" (dict "p1" .p1.Parent "p2" .p2 )  }}
{{ else if not .p1.IsHome }}
{{ template "breadcrumbnav" (dict "p1" .p1.Site.Home "p2" .p2 )  }}
{{ end }}
<li>
  {{ if eq .p1 .p2 }}
  {{ .p1.Title }}
  {{ else }}
  <a href="{{ .p1.Permalink }}">{{ .p1.Title }}</a>
  {{ end }}
</li>
{{ end }}
```


## Section Page Variables and Methods

Also see [Page Variables](/variables/page/).

{{< readfile file="/content/readfiles/sectionvars.md" markdown="true" >}}

## Content Section Lists

Hugo will automatically create pages for each section root that list all of the content in that section. See the documentation on [section templates][] for details on customizing the way these pages are rendered.

## Content *Section* vs Content *Type*

By default, everything created within a section will use the [content type][] that matches the root section name. For example, Hugo will assume that `posts/post-1.md` has a `posts` content type. If you are using an [archetype][] for your posts section, Hugo will generate front matter according to what it finds in `archetypes/posts.md`.

[archetype]: /content-management/archetypes/
[content type]: /content-management/types/
[directory structure]: /getting-started/directory-structure/
[section templates]: /templates/section-templates/

