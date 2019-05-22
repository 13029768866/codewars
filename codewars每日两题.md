# 第一题

查询字符串中的元音字符？（a,e,i,o,u）

```javascript
function getCount(str) {
  return (str.match(/[a,e,i,o,u]/ig) || []).length
}
```

知识点：

1. `match`方法返回的是一个满足正则条件的数组，如果没有返回一个空数组
2. `正则`中"[]"的作用

# 第二题

两个字符串拼接，去重后按英文字符顺序排序？

```javascript
function longest(s1, s2) {
  return [...new Set(s1+s2)].sort().join('')
}
```

1. `new Set`的用法和基础API

# 第三题

完成一个函数，第一个参数是数组 ，第二个参数是除数，返回所有可以被整除的数的新数组？

```javascript
let divisibleBy = (numbers, divisor) => numbers.filter(number => !(number % divisor))
```

知识点：

1. `filter`返回满足条件的数组
2. 能整除的项返回的结果是0，布尔值是false，取反就能得到正确结果。

# 第四题

给定一个数组，输出数组中出现偶数次的奇数，或者出现奇数次的偶数？

个人完成版本：通过对象的属性名和属性值来计数

```javascript
function findOdd(A) {
  let obj = {}
   A.map(item => {
    if(!obj.hasOwnProperty(item)){
      obj[item] = 1;
    }else{
      ++obj[item]
    }
  })
  for(let key in obj){
   if(obj[key] % 2){
        return Number(key)
      }
  }
}
```

大神版本：

```
const findOdd = (xs) => xs.reduce((a,b) => a ^ b)
```

知识点：

1.  ^ ：异或根据计算位是否相同决定结果位，结果位相同位0，否则为1
2. let a = 1 , b = 2  
3. a ^ b  0001 ^ 0010  = 0011 
4. a^b^a 0011 ^ 0001 = 0010
5. 所以使用这种方法的前提是该数组中有且只有1个出现奇数次的项

# 第五题

写一个函数，第一个参数str，第二个参数是array,获取数组中跟str组成字母相同的所有项？

个人完成版本：

```javascript
const anagrams = (w1,w2) => {
  let arr = []
  w2.forEach(item => {
    item.split('').sort().join() === w1.split('').sort().join()?arr.push(item):null;
  })
  return arr
}
```

点赞最多的版本：

```javascript
String.prototype.sort = function(){
  return this.split('').sort().join('')
}
const anagrams = (w1,w2) =>{
  return w2.filter( item => {
    return item.sort() === w1.sort()
  })
}
```

知识点：

1. 字符串没有sort()方法，给其原型上绑定一个sort方法执行字符串排序
2. filter返回的是一个满足条件的数组

# 第六题

获取一个整数所有的能被3和5整除的数的和？

个人版本：

```javascript
const solution = (num) => {
 let sum = 0;
 for(let i=0;i < num; i++){
   if( !(i % 3 ) || !(i % 5)){
     sum += i;
   }
 }
 return sum;
}
```

