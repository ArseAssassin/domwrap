DOMWrap is a thin wrapper over xml.dom.minidom aimed to make parsing XML documents easier. It's designed to be lightweight and easy to distribute for projects where using more fully featured libraries like ElementTree or lxml doesn't make sense.

# Installation
```$ easy_install domwrap```
OR
```$ python setup.py install```

# Usage	
```python
>>> import domwrap, urllib2
>>> d = domwrap.parse(urllib2.urlopen("https://github.com/blog.atom"))
>>> d["feed"]
<ElementList [<DOM Element: feed at 0x143fa08>]>
```

Prefix your selector with a backslash to query all descendants.

```python
>>> d['feed']['/entry']
<ElementList [<DOM Element: entry at 0x1508530>, <DOM Element: entry at 0x1508e40>, <DOM Element: entry at 0x150e788>, <DOM Element: entry at 0x15140d0>, <DOM Element: entry at 0x15149e0>, <DOM Element: entry at 0x151a328>, <DOM Element: entry at 0x151ac38>, <DOM Element: entry at 0x151f580>, <DOM Element: entry at 0x151fe90>, <DOM Element: entry at 0x15237b0>, <DOM Element: entry at 0x15290f8>, <DOM Element: entry at 0x1529a08>, <DOM Element: entry at 0x152d350>, <DOM Element: entry at 0x152dc60>, <DOM Element: entry at 0x15325a8>]>
```

## List access

```python
>>> doc['/entry']['title'][0].text
u'Eric Gerhardt is a GitHubber'

>>> d['feed']['/entry'][:5]
<ElementList [<DOM Element: entry at 0x1508530>, <DOM Element: entry at 0x1508e40>, <DOM Element: entry at 0x150e788>, <DOM Element: entry at 0x15140d0>, <DOM Element: entry at 0x15149e0>]>
```

## Attribute access

```python
>>> doc['/entry']['media:thumbnail'][0]['@url']
u'https://secure.gravatar.com/avatar/881bd08b6b94e600475ce431e8e6ea35?s=30&d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-140.png'

>>> d['feed']['/entry'][:5]['media:thumbnail']
<ElementList [<DOM Element: media:thumbnail at 0x1508bc0>, <DOM Element: media:thumbnail at 0x150e508>, <DOM Element: media:thumbnail at 0x150ee18>, <DOM Element: media:thumbnail at 0x1514760>, <DOM Element: media:thumbnail at 0x151a0a8>]>

>>> doc['/entry'][:3]['media:thumbnail']['@url']
[u'https://secure.gravatar.com/avatar/881bd08b6b94e600475ce431e8e6ea35?s=30&d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-140.png', u'https://secure.gravatar.com/avatar/b8dbb1987e8e5318584865f880036796?s=30&d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-140.png', u'https://secure.gravatar.com/avatar/bbe5dc8dcf248706525ab76f46185520?s=30&d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-140.png']
```
	
## Wrapping DOM

You can wrap also wrap parsed DOM elements to simplify reading their content.

```python	
	>>> wrapper = domwrap.DocumentWrapper(document)
	>>> wrapper['/p']
	<ElementList [<DOM Element: p at 0x1508bc0>, <DOM Element: p at 0x150e508>, <DOM Element: p at 0x150ee18>, <DOM Element: p at 0x1514760>, <DOM Element: p at 0x151a0a8>]>

	>>> wrapper = domwrap.NodeWrapper(element)
	>>> wrapper['title'][0].text
	u"@mention autocompletion"
```