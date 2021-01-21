#### 1-Java common used data structures
#### 2-Java map common used syntax
(1) method-getOrDefault
```
Map<Integer, Integer> map = new HashMap<>();
# 当map里不包含对num为key的mapping时返回0而不是返回null
map.getOrDefault(num, 0)
```
(2)Collections对自定义对象排序、TreeMap自定义排序
实现Comparable接口，或者传入实现
