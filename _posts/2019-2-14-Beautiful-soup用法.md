---
title: Beautiful soup用法
tags: bs4
---



Beautiful soup 对象可分为4种：Tag, NavigableString, BeautifulSoup, Comment.

Tag:bs4.element.Tag

NavigableString:bs4.element.Tag

### 遍历文档树

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
head_tag = soup.head
head_tag
# <head><title>the Dormouse's story</title></head>

head_tag.contents
[<title>The Dormouse's story</title>]
 
```

字符串没有contents属性，因为字符串没有子节点

.children返回生成器

#### .descendants

.descendants方法返回子孙节点的生成器

```python
html = '''<div class = "asd">
  <h1>Soup</h1>
  <p>Beautiful</p>
  <div>
    <a href = "www.baidu.com">baidu</a>
  </div>
</div>'''
soup = bs4.BeautifulSoup(html,"html.parser")
for i in soup.descendants:
    print(i)
    print("---------------------"

```

#### .string

如果tag只有一个NavigableString，可以用.string得到子节点

```python
import bs4

html = '''<div class = "asd">
  <h1>Soup</h1>
  <p>Beautiful</p>
  <div>
    <a href = "www.baidu.com">baidu</a>
  </div>
</div>'''
soup = bs4.BeautifulSoup(html,"html.parser")
print(isinstance(soup.p.string,bs4.element.NavigableString))

```

#### .strings 和 .stripped_strings

如果tag中包含多个字符串, 可以用.strings来循环获取

.strings 和 .stripped_strings 返回生成器

```python
import bs4

html = '''<div class = "asd">
  <h1>Soup</h1>
  <p>Beautiful</p>
  <div>
    <a href = "www.baidu.com">baidu</a>
  </div>
</div>'''
soup = bs4.BeautifulSoup(html,"html.parser")
for st in soup.strings:
    print(st)
    print('---')
#

---
Soup
---


---
Beautiful
---


---


---
baidu
---


---


---
```

输出的字符串可能包含了很多空格或空行，使用.stripped_strings可以去除

```python
import bs4

html = '''<div class = "asd">
  <h1>Soup</h1>
  <p>Beautiful</p>
  <div>
    <a href = "www.baidu.com">baidu</a>
  </div>
</div>'''
soup = bs4.BeautifulSoup(html,"html.parser")
for st in soup.stripped_strings:
    print(st)
    print('---')
#Soup
---
Beautiful
---
baidu
---
```

### 搜索文档树

.find()和find_all()

find_all(name,attrs,recursive,text,**kwargs)

name