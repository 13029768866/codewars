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

# 第二十九题、给定两个数组，获取A数组中独有的项？

题目实例：

array_diff([1,2,2,2,3],[2]) == [1,3]



个人初始版本：

1. 判断两种极端状况，然后统一处理

```javascript
const array_diff = (a,b) => {
  if(!(a.length)){
    return []
  }else if(!(b.length)){
    return a
  }
  for(let i = 0;i < b.length;i++){
    a = a.filter(item => item != b[i]) 
  }
  return a;
}
```

优化版本：

1、数组查询字符串Array.prototype.includes()

```javascript
const array_diff = (a,b) => a.filter(item => !(b.includes(item)))
```

2、数组查询字符串Array.prototype.indexOf()

```javascript
const array_diff = (a,b) => a.filter(item => b.indexOf(item) === -1)
```

# 第三十题、写一个函数，两个参数，让字符串重复多次？

```javascript
const repeatStr = (n,s) => s.repeat(n)
```

# 第三十一题、给定三个正整数，判断能否组成正方形？

```javascript
let isTriangle = (a,b,c)  => a+b>c && b+c>a && a+c>b
```

# 第三十二题、人数增长问题？

题目：

**在一个小镇上，人口在年初是p0 = 1000。人口每年定期增长2%，而且每年有50名新居民来此居住。这个城镇的人口需要多少年才能超过或等于p = 1200居民?**

个人版本：

```javascript
let nbYear = (p0,percent,aug,p,y)  =>{
  let year =  y  || 1;
  p0 = p0 + (p0 * percent / 100)  + aug
  if(p0 < p){
   year++
   return nbYear(p0,percent,aug,p,year)
  }
  return year
}
```

借鉴优化版本：

```javascript
let nbYear = (p0,percent,aug,p) => {
  for(var y = 0; p0 < p; y++){
    p0 = p0 + (p0 * percent / 100) + aug
  }
  return y
}
```

# 第三十三题、散步问题？

问题：

```
你住在一个叫Cartesia的城市里，所有的道路都被布置成一个完美的网格。你比约定的时间早到了十分钟，所以你决定抓住这个机会出去散一会儿步。这座城市为市民提供了一款手机上的步行生成应用程序——每次你按下这个按钮，它都会向你发送一个由一个字母组成的字符串组成的数组，这些字符串代表步行的方向(例如，“步行”)。['n'， 's'， 'w'， 'e'])。你总是只有一个块的方向走,你知道你需要一分钟的时间穿过一个街区,所以创建一个函数,该函数会返回true,如果走程序给你将你到底十分钟(你不想早或晚!)和意志,当然,你回到你的起点。否则返回假。
```

个人初始版本：

```javascript
const isValidWalk = walk => {
let nArr =  walk.filter(item => item == 'n'),
    sArr =  walk.filter(item => item == 's'),
    wArr =  walk.filter(item => item == 'w'),
    eArr =  walk.filter(item => item == 'e')
return (nArr.length === sArr.length)  && (wArr.length === eArr.length) && walk.length == 10
}
```

优化进阶版本：

```javascript
let isValidWalk = walk => {
  let dirChoose = direction => walk.filter(item => item == direction).length
  return walk.length == 10 && (dirChoose('n') === dirChoose('s')) && (dirChoose('w') === dirChoose('e'))
}
```

# 第三十四题、字符串replace，正则使用？

题目示例：

```javascript
songDecoder("WUBWEWUBAREWUBWUBTHEWUBCHAMPIONSWUBMYWUBFRIENDWUB")
// =>  WE ARE THE CHAMPIONS MY FRIEND
```

个人版本：

```javascript
let songDecoder = song => {
 return  song.replace(/(WUB)+/g,' ').trim()
}
```

# 第三十五题、至少4项的非空数组最小两个数求和？

个人版本：

```javascript
let sumTwoSmallestNumbers = nums => {
  nums.sort((a,b) => a - b)
  return nums[0] + nums[1]
}
```

更骚一点的版本：

```javascript
let sumTwoSmallestNumbers = nums => {
  let [a,b] = nums.sort((a,b) => a - b)
  return a + b;
}
```

# 第三十六题、返回一个数的负数？

个人版本：

```javascript
let makeNegative = num => -Math.abs(num)
```

# 第三十七题、检测一个字符粗是否有重复的字母？

个人版本：

```javascript
let isIsogram = str => str.toLowerCase() == [...new Set(str.toLowerCase().split(''))].join('')
```

吸收大佬经验的进阶版本：

```javascript
let isIsogram = str => [...new Set(str.toLowerCase())].length == str.length
```

大佬告诉你，正则到底可以多么优雅：

```javascript
let isIsogram = str => !/(\w).*\1/i.test(str)
```

知识点：

1. 英文字母只出现一次匹配正则 `!/(\w).*\1/i`

# 第三十八题、给定两个参数，第一个是至少3位的数组，第二个是数组长度，数组从第4项开始，每一项是前3项的和，写一个函数？

例题：

```javascript
Test.assertSimilar(tribonacci([1,1,1],1),[1])
Test.assertSimilar(tribonacci([300,200,100],0),[])
Test.assertSimilar(tribonacci([1,1,1],10),[1,1,1,3,5,9,17,31,57,105])
```

个人初始完成笨比版本：

```javascript
let tribonacci  = (arr , count) => {
  if(count == 0 ){
    return []
  }else if(arr.length >= count){
    return arr.slice(0,count )
  }else if(arr.length < count){
    for(let i = arr.length; i < count;i++){
     let sum = 0
     arr.slice(arr.length - 3).map(item => {
        return sum += item
      })
      arr.push(sum)
    }
    return arr
  }
}
```

优化版本：

1. 第二个参数是数组长度，通过遍历补全数组
2. 从这个数组截取长度

```javascript
let tribonacci = (arr , n) => {
  for(let i = 0; i < n - 3;i++){
    arr.push(arr[i] + arr[i+1] + arr[i+2])
  }
  return arr.slice(0,n)
}
```

# 第三十八题、获取下一个可开方数？

示例：

```javascript
findNextSquare(121) --> returns 144
findNextSquare(625) --> returns 676
findNextSquare(114) --> returns -1 since 114 is not a perfect
```

一发入魂的最优版本：

```javascript
let findNextSquare = sq => Number.isInteger(Math.sqrt(sq))?
 Math.pow(Math.sqrt(sq)+1,2):
 -1;
```

# 第三十九题、字符串去重变换？

示例：

```javascript
"din"      =>  "((("
"recede"   =>  "()()()"
"Success"  =>  ")())())"
"(( @"     =>  "))((" 
```

个人完成版本：

```javascript
var duplicateEncode = word => {
  let obj = {}
  word.toLowerCase().split('').map(item => {
  return  obj.hasOwnProperty(item)?
    obj[item]++:
    obj[item] = 1;
  })
  
 let newArr =  word.toLowerCase().split('').map(item =>{
    if(obj[item] > 1){
      return  item = ")"
     }else{
      return item = '('
     }
  })
  return newArr.join('')
}
```

优化思路 ：

1. 如果是该字符串中唯一的字符，所以是唯一的及indeOf() == lastIndexOf()

```javascript
let duplicateEncode = word => {
word = word.toLowerCase()
return word.replace(/./g,L=>word.indexOf(L) === word.lastIndexOf(L)? '(':')')
}
```

# 四十题、获取字符串中出现多次字符的个数？

示例：

```javascript
Test.assertEquals(duplicateCount(""), 0);
Test.assertEquals(duplicateCount("abcde"), 0);
Test.assertEquals(duplicateCount("aabbcde"), 2);
Test.assertEquals(duplicateCount("aabBcde"), 2,"should ignore case");
Test.assertEquals(duplicateCount("Indivisibility"), 1)
Test.assertEquals(duplicateCount("Indivisibilities"), 2, "characters may not be adjacent")
```

个人完成版本：

```javascript
let duplicateCount = text => {
 let arr = []
 text = text.toLowerCase().split('')
 text.map(item => {
   !(text.indexOf(item) == text.lastIndexOf(item))?
     arr.push(item):
     '';   
 })
 return [...new Set(arr)].length
}
```

吸收经验，进阶 优化版本：

```js
let duplicateCount = text => (text.toLowerCase().split('').sort().join('').match(/([^])\1+/g) || []).length
```

`/([^])\1+/ `  任意地方匹配连续出现多次

# 第四十一题、数组、字符串连续出现去重？

示例：

```js
uniqueInOrder('AAAABBBCCDAABBB') == ['A', 'B', 'C', 'D', 'A', 'B']
uniqueInOrder('ABBCcAD')         == ['A', 'B', 'C', 'c', 'A', 'D']
uniqueInOrder([1,2,2,3,3])       == [1,2,3]
```

个人版本：

```javascript
let uniqueInOrder = (it) =>{
return  
  typeof(it) == 'string'?
  it.split('').filter((item,idx) => item != it.split('')[idx + 1]):
  it.filter((item,idx) => item != it[idx - 1]);
}
```

优化版本：

```js
let uniqueInOrder = it => [...it].filter((item,idx) => item != it[idx - 1])
```

# 第四十二题、带数字字符串，按数字顺序排序

示例

```js
"is2 Thi1s T4est 3a"  -->  "Thi1s is2 3a T4est"
"4of Fo1r pe6ople g3ood th5e the2"  -->  "Fo1r the2 g3ood 4of th5e pe6ople"
""  -->  ""
```

个人版本：

```js
let order = words => {
  let arr = [];
   for(let i = 1; i <=  words.length;i++){
     words.split(' ').map((item,idx) => {
       item.includes(i)?arr.push(item): '';
     })
   }
  return arr.join(' ')
}
```

进化版本：

```js
let order = words => words.split(' ').sort((a,b) => a.match(/\d/)  - b.match(/\d/)).join(' ')
```

# 四十三题、bool类型转化成字符串？

```js
let boolToString = bool => bool.toString()
```

# 第四十四题、其他类型转成字符串？

```js
let numToString = num => num.toString()
```

# 第四十五题、字符串去除第一项和最后一项？

```js
let removeChar = str => str.slice(1,-1)
```

# 第四十六题、号码部分加密？

示例：

```js
Test.assertEquals(maskify('4556364607935616'), '############5616');
    Test.assertEquals(maskify('1'), '1');
    Test.assertEquals(maskify('11111'), '#1111');
```

个人版本：

```js
let maskify = cc => {
  return cc.length > 4?
  cc.slice( 0, -4).replace(/(\w)/g,'#') + cc.slice(-4):
  cc;
  }
```

优化版本：

```js
let maskify = str => str.slice(0,-4).replace(/./g,'#') + str.slice(-4)
```

# 第四十七题、获取字符串中英文字母‘m’字后的英文字母‘a-z’所占的比例？

示例:

```js
s="aaabbbbhaijjjm"
error_printer(s) => "0/14"

s="aaaxbbbbyyhwawiwjjjwwm"
error_printer(s) => "8/22"
```

个人版本：

```js
let printerError = s =>{ 
  let sortS = s.split('').sort((a,b)=> a.localeCompare(b)),
      idx  = sortS.lastIndexOf('m')
  return sortS.slice(idx).length - 1 + '/' + s.length
}
```

正则怎么这么牛逼版本：

```js
let printerError = s => (s.match(/[^a-m]/g)|| []).length + '/' + s.length
let printerError = s => (s.match(/[n-z]/g)|| []).length + '/' + s.length
```

知识点：

1. match()方法如果没有匹配项，返回的不是`[]`而是`null`

# 第四十八题、数字校验？

示例：

```js
validatePIN("1234") === true
validatePIN("12345") === false
validatePIN("a234") === false

只能4或6位纯数字
```

个人版本：

```js
let validatePIN = pin => {
  if(pin.length == 4 || pin.length == 6){
    return pin.match(/\d/g).length == pin.length
  }else{
    return false;
  }
}
```

正则版本牛逼：

```js
let validatePIN = pin => /^(\d{4}|\d{6})$/.test(pin)
```

# 第四十九题、偶数数组获取奇数的索引，奇数数组获取偶数的索引？

示例：

```js
iqTest("2 4 7 8 10") => 3 // Third number is odd, while the rest of the numbers are even
iqTest("1 2 1 1") => 2 // Second number is even, while the rest of the numbers are odd
```

个人完成版本：

```js
let iqTest = num => {
  let arr = num.split(' '),
      evenArr = arr.filter(item => item % 2),
      oddArr = arr.filter(item => !(item % 2))
      
   return evenArr.length == 1?
          1 + arr.indexOf(evenArr[0]) :
          1+ arr.indexOf(oddArr[0])
}
```

# 第五十题、神奇的数字？

```js
digPow(89, 1) should return 1 since 8¹ + 9² = 89 = 89 * 1
digPow(92, 1) should return -1 since there is no k such as 9¹ + 2² equals 92 * k
digPow(695, 2) should return 2 since 6² + 9³ + 5⁴= 1390 = 695 * 2
digPow(46288, 3) should return 51 since 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51
```

个人版本：

```js
let digPow = (n, p) => {
  let sum = 0;

  [...n.toString()].map((item) =>{    
    sum += Math.pow(Number(item),p)
    p++
  })
  return Number.isInteger(sum / n)?
         sum / n:
         - 1;
}
```

# 第五十一题、2个数字求和并且转化成二进制的数？

个人版本：

```js
let addBinary = (a,b) => (a + b).toString(2)
```

# 第五十二题、获取数组中之前所有项的和等于之后所有想的和和的索引，如果没有返回-1？

示例：

```js
Test.assertEquals(findEvenIndex([1,2,3,4,3,2,1]),3, "The array was: [1,2,3,4,3,2,1] \n");
Test.assertEquals(findEvenIndex([1,100,50,-51,1,1]),1, "The array was: [1,100,50,-51,1,1] \n");
Test.assertEquals(findEvenIndex([1,2,3,4,5,6]),-1, "The array was: [1,2,3,4,5,6] \n");
Test.assertEquals(findEvenIndex([20,10,30,10,10,15,35]),3, "The array was: [20,10,30,10,10,15,35] \n");
```

个人版本：

```js
let findEvenIndex = arr => {
  let evenIdx = -1;
   arr.map(((item,idx) =>{
      let sum = 0 , sum1 =0;
      arr.slice(0, idx).map(item => sum += item)
      arr.slice(idx + 1).map(item => sum1 += item)
      if(sum == sum1){
        evenIdx = idx;
      }
   }))
   return evenIdx
}
```

# 第五十三题、字符串中每个英文字符在字母表的位置拼接成一个空格隔开的字符串？

示例：

```js
Test.assertEquals(alphabetPosition("The sunset sets at twelve o' clock."), "20 8 5 19 21 14 19 5 20 19 5 20 19 1 20 20 23 5 12 22 5 15 3 12 15 3 11");
Test.assertEquals(alphabetPosition("The narwhal bacons at midnight."), "20 8 5 14 1 18 23 8 1 12 2 1 3 15 14 19 1 20 13 9 4 14 9 7 8 20");
```

个人完成版本：

```js
const alphabetPosition = text =>{
 let str =  text.toLowerCase().replace(/[^a-z]/g,''),
     letters = ['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z'],
     arr = []
     str.split('').map(item => arr.push(letters.indexOf(item) + 1))
     return arr.join(' ')
}
```

优化进阶版本：

```js
const alphabetPosition = text => text.toUpperCase().replace(/[^A-Z]/g,'').split('').map(item => item.charCodeAt() - 64).join(' ')
```

知识点：

`str.charCodeAt(index)`可以获得其Unicode值,A-Z所对应的的值减去64就可以得到字母表中对应位置

# 第五十四题、获取数组中为true项的个数？

```js
const countSheeps = arr => arr.filter(item => item == true).length
const countSheeps = arr => arr.filter(Boolean).length
```

# 第五十五题、二维数组条件判断？

示例：

```js
Test.assertSimilar(openOrSenior([[45, 12],[55,21],[19, -2],[104, 20]]),['Open', 'Senior', 'Open', 'Senior'])
Test.assertSimilar(openOrSenior([[3, 12],[55,1],[91, -2],[54, 23]]),['Open', 'Open', 'Open', 'Open'])
Test.assertSimilar(openOrSenior([[59, 12],[55,-1],[12, -2],[12, 12]]),['Senior', 'Open', 'Open', 'Open'])
```

个人版本：

```js
const openOrSenior = data => data.map(item => {
 return item[0] >=55 && item[1] > 7?
        'Senior':'Open';
})
```

解构赋值：

```js
const openOrSenior = data => data.map(([age,level]) => age >= 55 && level > 7? 'Senior':'Open')
```

 # 第五十六题、获取一个数字的所有公约数组成的数组？

示例：

```js
divisors(12); // should return [2,3,4,6]
divisors(25); // should return [5]
divisors(13); // should return "13 is prime"
```

个人完成最终版本：

```js
const divisors = num => {
  let res = [];
  for(let i = 2; i < num - 1; i++){
    Number.isInteger(num / i)?res.push(i):'';
  }
  return res.length?res: `${num} is prime`
}
```

# 第五十七题、去除字符串中所有空格？

个人答案：

```js
const noSpace = s => s.replace(/\s/g,'')
```

# 第五十八题、名字获取？

示例：

```js
list([ {name: 'Bart'}, {name: 'Lisa'}, {name: 'Maggie'} ])
// returns 'Bart, Lisa & Maggie'

list([ {name: 'Bart'}, {name: 'Lisa'} ])
// returns 'Bart & Lisa'

list([ {name: 'Bart'} ])
// returns 'Bart'

list([])
// returns ''
```

个人笨比版本：

```js
const list =  names => {
  names  = names.map(item => item['name'])
  let res =[
    ``,
    `${names[0]}`,
    `${names[0]} & ${names[1]}`
  ]
 console.log(names,res[names.length - 2])
  return names.length < 3?
  res[names.length]:
  names.slice(0,names.length - 1).join(', ') + ` & ${names[names.length - 1]}`
}
```

我变强了版本：

```js
const list = names =>{
  let aNames = names.map(item => item['name']),
      lastItem = aNames.pop()
   return aNames.length?
          aNames.join(', ') + ' & ' + lastItem:
          lastItem || '';
}
```

# 第五十九题、二进制转化成10进制数字？

示例：

```js
Testing: [0, 0, 0, 1] ==> 1
Testing: [0, 0, 1, 0] ==> 2
Testing: [0, 1, 0, 1] ==> 5
```

个人完成版本：

```js
const binaryArrayToNumber = arr => parseInt(arr.join(''),2)
```

`toSting()`可以通过设置数值把10进制转换成二进制。

`parseInt()`可以反向转化

# 第六十题、字符串中每个单词首字母拼接+‘ay’放置到单词末尾？

示例：

```js
pigIt('Pig latin is cool'); // igPay atinlay siay oolcay
pigIt('Hello world !');     // elloHay orldway !
```

不会正则的悲哀：

```js
const pigIt = s => {
  s = s.split(' ')
  s =  s.map(item => {
   if( item != '!' && item != '?'){
   return  item + item.slice(0,1) + 'ay'
     }else{ return item }
   })
  return s.join(' ').replace(/( |^)[a-z]/ig,' ').trim()
}
```

正则的优雅：

```js
const pigIt = s => s.replace(/(\w)(\w*)(\s|$)/g,'\$2\$1ay\$3')
```

# 8Ku题目库（二阶段系列）

## 六十二题、根据传递过来的方法，对两个数字进行运算 

```js
const basicOp = (m,v1,v2) => eval(v1+m+v2)
```

#  7Ku题目库（二阶段系列）

## 第六十一题、数组条件过滤

示例：获取数组中长度为4的字符

个人版本：

```js
const friend = fs => fs.filter(item => item.length == 4)
```

# 6Ku题目库（二阶段系列）

# 5Ku题目库（二阶段系列）

