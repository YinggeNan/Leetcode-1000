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
#### 3-char[]和String互转
"ss".toCharArray();
new String(new char{'a','i'});

#### 4-字符串排序，长度相等的字符串，字典顺序在前面的排在前面
s1.compareTo(s0); // 返回true则s1字典序更小

#### 5-map检查是否存在某个key
map.containsKey(1);
#### 6.注意Integer、Character这种包装类对象不能用==来做值比对，必须用equals()

#### 7.数组splice
#### 8-得到某个范围内的随机值
Random rand = new Random(); //使用系统时间作为随机种子
rand.nextInt(10); //得到[0,10)的随机整数
#### 9-List的子序列
List<$Integer$> list = new ArrayList<>();
list.subList(0, 2); // [0,2)
#### 10-List一次性加入一个序列
list.addALl(list.subList(0,2));
#### 11-构造数组元素为List类型的数组
List<$Integer$>[] list = new ArrayList[2]; // 不能写成 new ArrayList<>[2]