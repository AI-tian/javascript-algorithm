# 二进制间距

给定一个正整数 N，找到并返回 N 的二进制表示中两个连续的 1 之间的最长距离。 

如果没有两个连续的 1，返回 0 。

> 输入：22
>
> 输出：2
>
>解释：
>
>22 的二进制是 010110 。
>
>在 22 的二进制表示中，有三个 1，组成两对连续的 1 。
>
>第一对连续的 1 中，两个 1 之间的距离为 2 。
>
>第二对连续的 1 中，两个 1 之间的距离为 1 。
>
>答案取两个距离之中最大的，也就是 2 。

## 思路

> 1. 先将输入的数转换为二进制字符串
>
> 2. 利用正则查找如果有连续的11返回0
> 3. 利用正则查找为1的字符
> 4. 利用正则exec与lastindex方法找到二进制字符串中1所在的位置push给新数组arr；
> 5. 利用Math.max()方法进行比较找到1之间最大的值；

```javascript
        var str = 444;
        var binary = str.toString(2),
            len = binary.length;
            console.log(binary)
        
        if(binary.match(/(1)\1/g) == null){
            //判断如果没有连续的1时返回0
            console.log(0)
        }else{
            var patt = /1/g;//匹配为1的字符
            var arr = [];
            for(var i = 0; i < len; i++){
                if(patt.exec(binary) != null){
                   a = patt.lastIndex - 1;
                   arr.push(a)  
                }
            }
            var last = 0,//最大距离的变量
                first = 0;//索引变量
            //遍历数组
           for(var i = 0; i < arr.length; i++){
                first =  Math.max(first, arr[i]- last - 1);
                last = arr[i];
            }
           console.log(first)
        }
```

# 找出整型数组中乘积最大的三个数

给定一个包含整数的无序数组，要求找出乘积最大的三个数

> 输入 ： [-11,2,4,8,3,7,0,-16]
>
>输出 ：1408
>
>解释
>1. 数组中的3个数依次相乘
>2. -10 * 7 * 29,-10 * 7 * 30 .....
>3. 7 * 29 * 30,7 * 29 * 5......
>4. 29 * 30 * 5,29 * 30 * -10.....
>5. 依次相乘找到最大乘积

## 思路
> 1. 先利用数组的sort方法由低到高排序
> 2. 然后for循环遍历让最大的三个数想乘
> 3. 有数组的最左边出现绝对值大的负数，让最小的两个负数与数组最右边的数想乘
> 4. 如果第一种情况大于第二中情况返回第一种结果
>5. 否则返回第二种情况

```javascript
var arr = [-11,2,4,8,3,7,0,-16];
big_product(arr)
function big_product(origin){
    //由低到高排序
    var srote_arr = origin.sort(function(a,b){
        return a - b;
    });
    var chuange_va1 = 1,
        chuange_va2 = 1,
        arr_elemet = srote_arr.length - 1;
        //遍历找到最大的三个数，使其相乘(第一种情况)
        for(var i = arr_elemet; i > arr_elemet - 3; i--){
            chuange_va1 = chuange_va1 * srote_arr[i]
        }
        //有数组的最左边出现绝对值大的负数，让最小的两个负数与数组最右边的数想乘(第二种情况)
        chuange_va2 = srote_arr[0] * srote_arr[1] * srote_arr[arr_elemet]; 
        // 第一种结果大于第二种结果返回第一种结果否则返回第二种
        if(chuange_va1 > chuange_va2) return chuange_va1;
        return chuange_va2;
}
```

# 计算2的n次幂

输入整数n，输出2的n次幂

> 输入：2
>
> 输出：4
>
> 解释
> 输入n，执行n个2相乘（2的n次方）

## 思路
>1. 利用for遍历输入整数n
>2. 在循环里面执行n次乘2

```javascript
var n = parseInt(window.prompt('input')),
num = 2;
for(var i = 0;i < n;i++){
    console.log(num * 2)
}
```

# 两整数之和

不使用运算符 + 和 - ，计算两整数a、b之和

> 输入： 1、2
> 输出： 3

## 解释
> 当输入两个数，不需要加减符号，输出这两个数的和

## 思路

> 这里不用加减，就要用到二进制来进行计算

> 

```javascript
function getnum(a, b){
   if((a & b) == 0){
       return a|b;
       
   }else{
       return getnum(a ^ b,(a & b)<< 1)
   }  
}
```
# 求n以内的质数

> 输入： 100

> 输出：2、3、5、7、11、13、17、19、23、29、31、37、41、43、47、53、59、61、67、71、73、79、83、89、97。

## 解释

> 当输入100时，输出100以内的质数

## 思路

1. 质数是大于1的自然数中，除了1和它本身以外不再有其他因数
2. 

```javascript
function prime(n) {
    var count = 0;
    for (var i = 1; i < n; i++) {
        for (var j = 0; j <= i; j++) {
            if (i % j == 0) {
                count++;
            }
        }
        if (count == 2) {
            console.log(i)
        }
        count = 0;
    }
          
}
```


# 替换空格

请实现一个函数，把字符串中的每个空格替换成"%20"。

你可以假定输入字符串的长度最大是1000。
注意输出字符串的长度可能大于1000。

样例
> 输入："We are happy."

> 输出："We%20are%20happy."

```javascript
var replaceSpaces = function(str) {
    var arr = str.split("");
    for(var i = 0; i < arr.length; i++){
        if(arr[i] == " "){
            arr[i] = "%20"
        }
    }
   var ret = arr.join("");
   return ret;
}
```

# 找出数组中重复的数字
给定一个长度为 n 的整数数组 nums，数组中所有的数字都在 0∼n−1 的范围内。

数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。

请找出数组中任意一个重复的数字。

注意：如果某些数字不在 0∼n−1 的范围内，或数组中不包含重复数字，则返回 -1；

样例
给定 nums = [2, 3, 5, 4, 3, 2, 6, 7]。

返回 2 或 3。

```javascript
var duplicateInArray = function (nums) {
        var obj = {
            length: 0,
            push: Array.prototype.push
        };
        var arr = [];
        var arr1 = [];
        var ret = 0;
        function pan(n) {
            for (var i = 0; i < n.length; i++) {
                if (n[i] > n.length - 1) {
                    return n[i] > n.length - 1;
                }
            }
        }
        if (nums.length === 0 || pan(nums)) {
            return -1;
        } else {
            for (var i = 0; i < nums.length; i++) {
                if (!obj[nums[i]]) {
                    obj[nums[i]] = 'a';
                    arr.push(nums[i])
                } else {
                    arr1.push(nums[i])
                }
            }
            if (arr.length === nums.length) {
                return -1;
            } else {
                return arr1[0]
            }
        }
    };
```

# 不修改数组找出重复的数字
给定一个长度为 n+1 的数组nums，数组中所有的数均在 1∼n 的范围内，其中 n≥1。

请找出数组中任意一个重复的数，但不能修改输入的数组。

样例
给定 nums = [2, 3, 5, 4, 3, 2, 6, 7]。

返回 2 或 3。

```javascript
var duplicateInArray = function (nums) {
        var obj = {
            length: 0,
            push: Array.prototype.push
        }
        var arr = [];
        for (var i = 0; i < nums.length; i++) {
            if (!obj[nums[i]]) {
                obj[nums[i]] = 'a';
            } else {
                arr.push(nums[i])
            }
        }
        return arr[0];
    };
```
# 二维数组中的查找
在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。

请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

样例
输入数组：

[
  [1,2,8,9]，
  [2,4,9,12]，
  [4,7,10,13]，
  [6,8,11,15]
]

如果输入查找数值为7，则返回true，

如果输入查找数值为5，则返回false。

```javascript
var searchArray = function (array, target) {
    var ret = false;
    var arr = [];
    var arr1 = [];
    for (var i = 0; i < array.length; i++) {
        for (var j = 0; j < array[i].length; j++) {
            if (target == array[i][j]) {
                arr.push(array[i][j])
            } else {
                arr1.push(array[i][j])
            }
        }
    }
    if(arr.length === 0){
        return false;
    }else{
        return true;
    }
};
```
# 从尾到头打印链表
输入一个链表的头结点，按照 从尾到头 的顺序返回节点的值。

返回的结果用数组存储。

```javascript
var printListReversingly = function (head) {
    var arr = [];
    while (head != null) {
        arr.unshift(head.val);
        head = head.next;
    }
    return arr;
}
```
# 斐波那契数列

输入一个整数 n ，求斐波那契数列的第 n 项。

假定从0开始，第0项为0。(n<=39)

样例
输入整数 n=5 

返回 5

```javascript
var Fibonacci = function (n) {
        var one = 0;
        var two = 1;
        var three;
        if (n > 1) {
            for (var i = 1; i < n; i++) {
                three = one + two;
                one = two;
                two = three;
            }
            return three
        }else{
            return 0;
        }
}
```
