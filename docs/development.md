
# Local development

## Install

1. `git clone https://github.com/FarmBot-Docs/farmbot-docs`
0. `cd farmbot-docs`
0. [Install ruby](https://www.ruby-lang.org/en/documentation/installation/)
(check installation with `ruby -v`)
0. `gem install bundler`
0. `bundle install`

## Serve

1. `bundle exec jekyll serve`
0. Open [http://localhost:4000/](http://localhost:4000/) in a browser


## Edit

Saving any changes will automatically trigger a rebuild.
Changes to `_config.yml` require re-running `bundle exec jekyll serve`.


# Adding a new page

## Template

Every page starts with (`description` is optional):

```
---
title: "Page Title"
slug: "page-slug"
description: "Page description."
---

* toc
{:toc}

```

after which begins the page content.

Pages should be saved as `page-slug.md` in the appropriate directory
(for example, `/v1.0/Documentation/page-slug.md`).

## Add page to the navigation panel table of contents

in `_data/toc/v1.0.yml` (where `1.0` is the documentation version), add:

```
- title: Page Title
  url: page-slug
```

to the desired location. The toc page organization should match the
documentation version directory folder structure.

## (Optional) Permalink redirect

If a `doc.farm.bot/docs/page-slug` permalink url is necessary,
in `_redirects` add a new `page-slug.md` file with:

```
---
permalink: /docs/page-slug
page_path: /Documentation/path/to/page-slug
layout: redirect
---
```

where `/Documentation/path/to/` is the path to the `page-slug.md` file
in the `v1.0` (or latest version) directory.


# Adding a new version

1. Copy the latest version documentation directory.

> `/v1.0/` -> `/v1.1/`

2. Copy the latest version data files.

> `/_data/toc/v1.0.yml` -> `/_data/toc/v1.1.yml`
> (if applicable) `/_data/section_images/v1.0.yml` -> `/_data/section_images/v1.1.yml`
> (if applicable) `/_data/cad/v1.0.yml` -> `/_data/cad/v1.1.yml`

3. Change the `version_number` in the new data files.

> `version_number: 1.0` -> `version_number: 1.1`

5. (if necessary)
Change any version-specific titles and urls in the new toc file.

> `home: FarmBot-Model-v1.0/intro` -> `home: FarmBot-Model-v1.1/intro`
> `title: FarmBot Model V1.0` -> `title: FarmBot Model V1.1`
> `url: FarmBot-Model-v1.0` -> `url: FarmBot-Model-v1.1`
> `` -> ``

6. (if necessary)
Change any version-specific folder names within `/v1.1`. Pay attention to case.

> `FarmBot-Model-v1.0` -> `FarmBot-Model-v1.1`

7. (if necessary)
Change any version-specific titles and urls in documentation content files.

> Within the `/v1.1` folder, find and replace `/FarmBot-Model-v1.0/` -> `/FarmBot-Model-v1.1/`

> search for `v1.0` within the `/v1.1` folder and edit content appropriately

8. Change the `redirect_from` value for the home page in the
new documentation version folder. (The home page path can be found at
the top of the table of contents data file in the `home` field.)

> `redirect_from: /docs/v1.0/` to `redirect_from: /docs/v1.1/`

9. When ready to publish the new version,
update `latest_version_number` in `/_config.yml`.

> `latest_version_number: 1.0` -> `latest_version_number: 1.1`

`latest_version_number` specifies the documentation version for:

 * the default documentation home page
 * permalink redirects
 * the latest documentation available in the version navigation menu

Until `latest_version_number` is updated with the latest documentation version,
pages in newer versions (if a newer version exists) are accessible only via url.

# Adding an image

1. Upload the image to the `_images` folder in the same directory as the
`page-slug.md` file it will be used in.
(Create the `_images` folder if it does not exist.)
0. Link to the image with:

```
![image alt text description](_images/image_filename.png)
```

Verify that the image appears in the GitHub markdown preview
(or when served by `localhost`).

# Adding a gallery

Existing images can be combined into galleries:

```
{% include gallery.html images='
![image alt text description](_images/image_filename.png)
![image alt text description](_images/image_filename.png)
' %}
```

Embeds can be added to galleries:

```
{% include gallery.html images='
![image alt text description](_images/image_filename.png)
<iframe src="https://..."></iframe>
' %}
```

Notice that `images='...'` uses single quotes so double quotes can be used
for iframe attributes. Opposite quote types can also be used.

# Adding a callout

```
{%
include callout.html
type="info"
title="Title"
content="Content."
%}
```
will render as:

![info_callout](https://user-images.githubusercontent.com/12681652/95519979-23babc80-097b-11eb-846f-d1acc850b253.png)

`type`: One of:
 * `info` (blue :information_source:)
 * `success` (green :heavy_check_mark:)
 * `warning` (orange :warning:)
 * `danger` (red :exclamation:)

`title`: Callout header. May be empty.

`content`: Callout content. May be empty.

`"` characters within `title` or `content` must be escaped
(for example, `content="This is \"content\"."`).

# Adding HTML

In addition to markdown, HTML is also supported.
However, markdown nested within HTML will be rendered as plain text.

# Modifying the theme

The common documentation theme (assets/css, layouts, includes) can be modified
in the [farmbot-theme](https://github.com/FarmBot-Docs/farmbot-theme) repository.
Sample components are provided for quick local development.
See [local development instructions](#local-development) for additional information.
