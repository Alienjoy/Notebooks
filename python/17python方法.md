# 1.enumrate列举

enumerate是列举出来对象的元素，并返回一个索引和元素内容的迭代器

见下例子：

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print(list(enumerate(seasons)))
print(dict(enumerate(seasons)))
for i ,elem in enumerate(seasons):
  print(i,elem)
输出：
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
{0: 'Spring', 1: 'Summer', 2: 'Fall', 3: 'Winter'}
0 Spring
1 Summer
2 Fall
3 Winter
```
