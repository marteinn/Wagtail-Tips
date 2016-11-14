# Using Wagtail with Factory Boy

Wagtail uses treebeard at its base and therefore uses its path struture, by generating the path with a sequence we can in a easy way create test models.

This is how a factory might look like

```python
import factory
from wagtail.wagtailcore.models import Site, Page


class PageFactory(factory.DjangoModelFactory):
    class Meta:
        model = Page

    path = factory.Sequence(lambda x: '00010001{:04d}'.format(x+1))
    depth = 3
    numchild = 0
    live = True

    title = factory.Sequence(lambda x: 'page-title-{0}'.format(x))
```

And this is how you might use it in a unittest.

```python
import myapp.factories import PageFactory
page = PageFactory.create(title='mypage')

self.assertEquals(page.title, 'mypage')
```

Keep in mind that this approach put a bit more responsibility on you, when for instance creating sub-children.

```python
import myapp.factories import PageFactory
page = PageFactory.create(title='mypage')


sub_page = PageFactory.create(title='mypage', path='{}0001'.format(page.path))
```
