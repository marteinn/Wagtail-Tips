# Creating image rendition without using templatetags

The [wagtail docs](http://docs.wagtail.io/en/v1.7/topics/images.html) are very clear when it comes to showing how to generating different image sizes in templates.

```html
{% load wagtailimages_tags %}
{% image page.photo fill-80x80 %}
```

...but how would one go about doing this with pure python? Turns out there is a really nice shortcut function called `get_rendition_or_not_found`. Just pass in image and behaviour to generate your image.


```python
from wagtail.wagtailimages.shortcuts import get_rendition_or_not_found

rendition = get_rendition_or_not_found(page_model.image, 'fill-500x500')
```
