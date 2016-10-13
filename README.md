# Wagtail Simple Gallery
Is an extension for Torchbox's [Wagtail CMS](https://github.com/torchbox/wagtail) for creating a simple image gallery either by creating a page using the template or templatetag.

Current version should work with Wagtail version >= 1.5.3 and Python 2.7, 3.4 and 3.5.


## Getting started
### Install
- Install via pip `pip install wagtail-simple-gallery`.
- Add `wagtail_simple_gallery` to `INSTALLED_APPS` in your project settings.
- Run `python manage.py migrate wagtail_simple_gallery`.

### Use
- Create a new collection in Wagtail CMS: **Settings -> Collections**.
- Add or upload images to the collection.
- Create a new page using the **Simple Gallery Index** template and select the new collection.
- You are done, preview or publish the page and you should see the gallery in action.


## Features / Options
- Toggleable [Lightbox](https://feimosi.github.io/baguetteBox.js/) for viewing images.
- Show images from selected collection.
- The amount of images shown on one page (before the paginator kicks in) is changeable.


## Templatetags
### `{% simple_gallery %}` inclusion tag
Uses the template **wagtail_simple_gallery/simple_gallery.html**. You can use the simple-gallery style with this tag using: `<link rel="stylesheet" href="{% static 'css/simple-gallery.css' %}">`.

- `collection` (default: None): Show images from this collection. **Required**, example: `{% simple_gallery collection="Root" %}`.
- `tags` (default: None): Filter images by their tags. Example: `{% simple_gallery tags="cats dogs" %}`.
- `image_limit` (default: None): Limit the amount of images to show. Example: `{% simple_gallery image_limit=4 %}`.
- `use_lightbox` (default: True): Use lightbox for viewing images. Example: `{% simple_gallery use_lightbox=False %}`.

### `{% img|original_url %}` filter
- Takes wagtails Image object and returns its real original url instead of the one that wagtail creates. Example: `/media/original_images/foo.jpg`.


## Template
Look at **simple_gallery_index.html** template for an example or copy paste it and start modifying to make it look a part of your page. Your custom **simple_gallery_index.html** template should reside in **/templates/wagtail_simple_gallery/simple_gallery_index.html**

Or if **simple_gallery_index.html** is good enough for your use, then you can just create a **simple_gallery_base.html** in your own templates directory with the following content:
```
{% extends "base.html" %}

{% block content %}{% endblock %}
```


## Admin Interface
The admin view for images is customized so it can show more images at once. By default there are 20 images on one page, but you can have 32 by adding `url(r'', include('wagtail_simple_gallery.urls')),` in your urls.py above the `url(r'^admin/', include(wagtailadmin_urls)),` line.