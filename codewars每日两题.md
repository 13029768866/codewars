# 第一题、查询元音字符

查询字符串中的元音字符？（a,e,i,o,u）

```javascript
function getCount(str) {
  return (str.match(/[aeiou]/ig) || []).length
}
```

知识点：

1. `match`方法返回的是一个满足正则条件的数组，如果没有返回一个空数组
2. `正则`中"[]"的作用

# 第二题、两个字符串去重

两个字符串拼接，去重后按英文字符顺序排序？

```javascript
function longest(s1, s2) {
  return [...new Set(s1+s2)].sort().join('')
}
```

1. `new Set`的用法和基础API

# 第三题、获取被整除数的新数组 

完成一个函数，第一个参数是数组 ，第二个参数是除数，返回所有可以被整除的数的新数组？

```javascript
let divisibleBy = (numbers, divisor) => numbers.filter(number => !(number % divisor))
```

知识点：

1. `filter`返回满足条件的数组
2. 能整除的项返回的结果是0，布尔值是false，取反就能得到正确结果。

# 第四题、输出数组中出现奇数次数的项

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

# 第五题、获取数组中组成字符相同的项

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

# 第六题、获取一个数中所有能被3和5整除的数的和

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

# 第七题、判断一个数字是否是偶数

判断一个数字是否是偶数？

个人版本：

```javascript
const even_or_odd = num => {
  num = Math.floor(num)
  return  !(num % 2) ? 'Even':'Odd';
}
```

# 第八题、奇数字符串获取中间一项，偶数获取中间两项

给定一个字符串，如果字符串长度是偶数截取中间2位，如果字符串式长度是奇数，截取中间1位的函数？

个人版本：

```javascript
const getMiddle = (words) => {
  let getIdx = Math.floor(words.length / 2)
  return !(words.length % 2) ? 
  words.slice(getIdx - 1 , getIdx + 1):
  words.slice(getIdx , getIdx + 1)
}
```

改进版本：

```javascript
const getMiddle = (s) => {
  return s.substr(Math.ceil(s.length / 2 - 1),!(s.length % 2)?2:1)
}
```

知识点：

1. 截取字符串方法`substr`,`substring`,`slice`
2. 一参索引到最后，二参包左不包右
3. `substr`,一参索引，二参截取个数
4. `substring`两个参数都是索引
5. `slice`可以倒着截取输入`-`负号

# 第九题、获取数字的相反数

```javascript
let opposite = num => -num
```

# 第十题、accum("abcd") -> "A-Bb-Ccc-Dddd"

个人版本：

```javascript
let accum = s =>{
let res = ''
  s.split('').map((item,idx) => {
    res += item.toUpperCase()
     for(let i =0;i<idx;i++){
       res += item.toLowerCase()
     }
     return res += '-'
  })
  return  res.slice(0,res.length -1)
}
```

升级进阶版本：

```javascript
let accum = (s) => s.split('').map((item,idx) => item.toUpperCase() + item.toLowerCase().repeat(idx)).join('-')
```

知识点：

1. 字符大小写转化，toUpperCase、toLowerCase
2. `repeat()`方法不能传入 `负数`，`Infinity`,传入小数向下取整

# 第十一题、删除元音字符

```javascript
const disemvowel = str => str.replace(/[aeiou]/ig, '')
```

# 第十二题、获取字符串最大值或最小值

个人版本：

```javascript
String.prototype.sort = function(){
  return this.split(' ').sort((a,b)=> a-b)
}
const highAndLow = str => str.sort()[str.sort().length - 1] + ' ' + str.sort()[0]
```

升级进阶版本：

```javascript
const highAndLow = str =>{
    arr = str.split(' ')
    // 也可以把数组中的类型转换成Number
    //	arr = str.split(' ').map(Number)
    return Math.max.apply('',arr) + ' ' +Math.min.apply('',arr)
}
```

# 第十三题、检测一个数字是否可以完全开方

```javascript
const isSquare = n => Number.isInteger(Math.sqrt(n))
```

知识点：

1. Math.sqrt()执行开方运算
2. Number.isInteger()判断是否为一个整数

# 第十四题、把字符串中每一个单词的首字母大写

```javascript
String.prototype.toJadenCase = function () {
 return this.toLowerCase().replace(/( |^)[a-z]/g,L => L.toUpperCase())
};
```

# 第十五提、获取一个数字每位数平方拼接的字符串

个人完成版本：

```javascript
let squareDigits = num => {
let res = ''
num.toString().split('').map(item => {
  res += Math.pow(Number(item),2)
})
return Number(res)
}
```

# 第十六题、不考虑数据类型，字符串不为空的情况下获取最短word的长度

个人版本：

```javascript
let findShort = s => Math.min.apply('',s.split(' ').map(item => item.length))
```

# 第十七题、比较一个字符串中两个给定字符的出现次数是否相等？

```javascript
let XO = s => {
  let x = s.match(/x/ig)
  let o = s.match(/o/ig)
  return (x && x.length)  === (o && o.length)
}
```

# 第十八题、数字各个位数相加求和，直到和为一位数时输出结果？

```javascript
let digital_root = n =>  { 
let sum = 0;
String(n).split('').map(item => sum += Number(item))
if(String(sum).length == 1){
  return sum 
}else{
return digital_root(sum)
}
}
```

**你不知道为什么，但是就是 感觉很牛逼的版本**

```javascript
let digital_root = n => (n - 1)%9 - 1
```

# 第十九题、数字反转?

```javascript
let descendingOrder = n => Number(n.toString().split('').sort((a,b)=>b-a).join(''))
```

# 第二十题、给定一个只有字符和空格组成的字符串，把之中字符长度在5以上的字符串反转？

个人版本：

```javascript
String.prototype.strReverse= function(){
  return this.split('').reverse().join('')
}
let spinWords = s =>{ 
  s.split(' ').map(item => {
   if(item.length >= 5){
     let re = new RegExp(item,'g')
     return s = s.replace(re, item.strReverse())
   }    
  })
  return s
}
```

进阶优化版本：

```javascript
let spinWords = s => s.replace(/\w{5,}/g, S => S.split('').reverse().join(''))
```

# 第二十一题、给定一个数组（至少3项），如果是偶数数组只有一个奇数，如果是奇数数组只有一个偶数，获取其值？

个人完成版本：

```javascript
let findOutlier = intergers =>{
  let  filterArr = intergers.filter(item => item % 2)
  return  filterArr.length > 1?
          intergers.filter(item => !(item %2))[0]:
          filterArr[0];
}
```

# 第二十二题、给定两个整数，求所有之间所有整数的和？

感觉自己是个弱智版本：

```javascript
let GetSum = (a,b) =>{
 if(a === b){ return a}
 if( Math.abs(a) === b ||  a === Math.abs(b)){
   return 0;
 }
 if(a < b){
   let sum = 0
   for(let i=a;i<=b;i++){
     sum += i;
     if(i == b){
       return sum;
     }
   }   
 }else if (a  > b){
   let sum = 0;
   for(let i = b;i <= a;i++){
     sum += i;
     if(i == a){
       return sum
     }
   }
```

**智商在线版本**

```javascript
 let GetSum =(a,b) => (Math.abs(a - b) + 1) * (a+b) / 2;
```

# 第二十三题、写一个函数实现下列功能？

```javascript
likes [] // must be "no one likes this"
likes ["Peter"] // must be "Peter likes this"
likes ["Jacob", "Alex"] // must be "Jacob and Alex like this"
likes ["Max", "John", "Mark"] // must be "Max, John and Mark like this"
likes ["Alex", "Jacob", "Mark", "Max"] // must be "Alex, Jacob and 2 others like this"
```

个人完成if--else版本：

```javascript
let likes = name => {
  if(name.length == 0){
    return "no one likes this"
  }else if(name.length == 1){
    return name[0] + ' likes this'
  }else if(name.length == 2){
    return name[0] + ' and ' + name[1] + ' like this'
  }else if(name.length == 3){
   return name[0] + ', '+name[1] + ' and ' +name[2] + ' like this'
  }else{
     return name[0] + ', ' + name[1] + ' and ' + Number(name.length - 2) +' others like this'
  }
}
```

进阶版本：

```javascript
let likes = names => [
  'no one likes this',
  `${names[0]} likes this`,
  `${names[0]} and ${names[1]} like this`,
  `${names[0]}, ${names[1]} and ${names[2]} like this`,
  `${names[0]}, ${names[1]} and ${names.length - 2} others like this`
][Math.min(4,names.length)]
```

知识点：

1. 运用ES6运算符，和template语法实现，通过Math.min实现对索引的操纵。

# 第二十四题、获取一个数字二进制中1的个数？

```javascript
let countBits = n => (n.toString(2).match(/[1]/g)|| []).length
```

知识点：

1. toString(2)把数字转化成二进制

# 第二十五题、获取整数数组中所有正整数的和？

```javascript
const positiveSum = arr => arr.reduce((prev,cur) => prev + (cur > 0? cur: 0),0)
```

# 第二十六题、给一个数字，如果各个位数相乘不是个位数，继续相乘，知道是个位数位置，请写一个函数输出计算次数？

```javascript
 persistence(39) === 3 // because 3*9 = 27, 2*7 = 14, 1*4=4
// and 4 has only one digit
persistence(999) === 4 // because 9*9*9 = 729, 7*2*9 = 126,
// 1*2*6 = 12, and finally 1*2 = 2
persistence(4) === 0 // because 4 is already a one-digit number
```

```javascript
let persistence = (num,crr) => {  
  if(num.toString().split('').length <= 1){
    return 0
  }
  let mul = 1 ,
      count = crr || 0;
  num.toString().split('').map(item => mul *= item)
  if(mul.toString().split('').length > 1){
    count++
    return persistence(mul,count)
  }else{
    return count + 1;
  }  
}
```

reduece优化版本：

```javascript
const persistence = num => {
  return `${num}`.length > 1?
      1 + persistence(`${num}`.split('').reduce((a,b) => a * b))
      : 0;    
}
```

# 第二十七题、获取数组中类型是Number的项组成新数组？

```javascript
const filter_list = l => l.filter(item => Number.isInteger(item))
```

# 第二十八题、createPhoneNumber([1, 2, 3, 4, 5, 6, 7, 8, 9, 0]) // => returns "(123) 456-7890"

个人版本：es6+模板字符串

```javascript
const createPhoneNumber = num =>`${num.slice(0,3).join('')}` ${num.slice(3,6)-${num.slice(6).join('')}}
```

正则方式：

```javascript
const createPhoneNumber = nums => nums.join('').replace(/(\d{3})(\d{3})(\d{4})/,'($1) $2-$3')
```

