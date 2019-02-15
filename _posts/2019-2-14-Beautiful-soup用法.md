---

title:Beautiful soup用法
tags:bs4

---



Beautiful soup 对象可分为4种：Tag, NavigableString, BeautifulSoup, Comment.

Tag:bs4.element.Tag

NavigableString:bs4.element.Tag

### Tag

Tag 对象有自己的名字，通过.name来获取

```python
soup = BeautifulSoup('<b class="bold“>Extremely bold</b>')
tag = soup.b
type(tag)
#<class 'bs4.element.Tag'>
```



多次调用这个方法

```py
soup.body.b #获取body标签中的第一个b标签
```

#### .contents和.children

tag的contents属性可以将tag的子节点以列表方式输出

```python

```

