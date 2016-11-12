# Customize available WYSIWYG text formats

Wagtail uses a javascript object called halloPlugins to setup the wysiwyg editor, by changing its properties we can customize the editor.

In the example below we are only allowing p and h3 format tags.

```python
# wagtail_hooks.py (tested on wagtail 1.7)

@hooks.register('insert_editor_js')
def override_editor_heading_formats():
    return """
        <script>
        halloPlugins.halloheadings.formatBlocks = ['p', 'h3'];
        </script>
        """
```
