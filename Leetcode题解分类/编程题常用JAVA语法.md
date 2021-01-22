#### 1-Java common used data structures
#### 2-Java map common used syntax
(1) map get设置key不存在时的默认值
```
Map<Integer, Integer> map = new HashMap<>();
# 当map里不包含对num为key的mapping时返回0而不是返回null
map.getOrDefault(num, 0)
```
(2)Collections对自定义对象排序、TreeMap自定义排序
实现Comparable接口，或者传入实现
(2)Collections快速新建对象
List对象：Arrays.asList(1,2);//这种方法生成的list，是不支持添加或删除元素的
Map对象：
new HashMap<Integer, String>(){{
    put("k1","v1");
    put("k2","v2");
}