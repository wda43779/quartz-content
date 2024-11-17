#  头尾增减：shift、unshift、push、pop

|     | 头部            | 尾部         |
| --- | ------------- | ---------- |
| 增加  | `arr.unshift` | `arr.push` |
| 删除  | `arr.shift`   | `arr.pop`  |
当栈使用：push pop
当队列使用：push shift

# 函数式转换： map, filter, reduce, reduceRight

## map
把回调函数逐个应用到数组元素上，返回值组成新的数组
回调函数签名速记：cia（当前值，当前序号i，完整数组）
如果不要返回值，这个对应的是forEach

## filter
过滤数组，把回调应用到数组元素，根据返回的布尔值决定是否保留，返回真则保留。
回调函数签名速记：cia（当前值，当前序号i，完整数组）
## reduce
处理数组合成一个值，把回调应用到数组元素，每次从旧的结果计算新的结果
本体签名：[].reduce(cb, initValue?)
回调函数签名速记：pcia（之前合成的结果，当前值，当前序号i，完整数组）
编码风格：initialValue一定要传

## 带副作用的map：forEach

# 量词 every, some, 
$$\forall(every),  $$
$$\exists(some) $$

# 查找：

## 找值(第二项参数跳过一部分，支持负数)
includes
indexOf
lastIndexOf
## 找符合条件的
find
findIndex
findLast
findLastIndex

# 遍历：`[].keys(), [].values(), [].entries()

# 创建数组

## 字面量
`a= [1,2,3]`
## 用fill预分配
`new Array(3).fill(0)`
## 预分配2D
`new Array(3).fill().map(_=>new Array(3).fill(0))`

## 静态方法
```
Array.from([1,2,3])
Array.from([1,2,3], x=>2x)
Array.of(1,2,3)
```

# Array.isArray() //检查是否数组

# 改变顺序：sort, reverse

# 转字符串：join, toLocaleString, toString

# 切分连接：slice splice concat

# 其他 flat flatMap copyWithin





# 在array like对象上使用数组的方法

[].map.call(document.querySelectorAll("a"), x => console.log(x))