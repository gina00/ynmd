# 方法收集
### 去除字符串左右空格
```
trim(str) {
    return str.replace(/(^\s*)|(\s*$)/g, '')
},
```
### 检测输入的字符串是否合格
```
checkIsNull(str) {
    if (str == '') {
     return true
    }
    var regu = '^[ ]+$'
    var re = new RegExp(regu)
    return re.test(str)
},
``` 

```js
ipAddr: [
          {
            required: true,
            message: '请输入合法IP地址',
            trigger: 'blur',
            pattern: /^(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])\.(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])\.(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])\.(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])$/
          }
        ],
        port: [
          {
            required: true,
            message: '请输入端口，1-65535',
            trigger: 'blur',
            type: 'number',
            min: 1,
            max: 65535
          }
        ],
        
```


### 是否为数字
```
isNumber(val) {
      var regPos = /^\d+(\.\d+)?$/ //非负浮点数
      var regNeg = /^(-(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*)))$/ //负浮点数
      if (regPos.test(val) || regNeg.test(val)) {
        return true
      } else {
        return false
      }
    }
```
### 获取当天日期
```
getNowTime() {
      var now = new Date()
      var year = now.getFullYear() //得到年份
      var month = now.getMonth() //得到月份
      var date = now.getDate() //得到日期
      month = month + 1
      month = month.toString().padStart(2, '0')
      date = date.toString().padStart(2, '0')
      var defaultDate = `${year}-${month}-${date}`
      this.$set(this.formData, 'trackTime', defaultDate)
    }
```
### 判断数组中某一个值是否为false，全部为true时执行，否则不执行
```
mounted(){
	  this.ticketArr=[
		{
		  name:'大师傅',
		  isshow:false
		},
		{
		  name:'的风格',
		  isshow:false
		}
	  ]
	  if(this.ticketArr.findIndex(target=>target.isshow===true)==-1){
		  console.log('验证通过')
	  }else {
		console.log('验证不通过')
	  }
	}
```
### js对象拆分多个对象
```
let obj = {裙子: 5, 上衣: 10, 短裙: 15, 内衣: 20, 内裤: 30}
	// 要求结果如下:
	[
	{name: "裙子", value: 5}
	{name: "上衣", value: 10}
	{name: "短裙", value: 15}
	{name: "内衣", value: 20}
	{name: "内裤", value: 30}
	]
	 let list = [];
	 for(var key in obj){
			var temp = {}
			temp.name = key;
			temp.value = obj[key];
			list.push(temp)
	  }
	  
	 //js属性对象的hasOwnProperty方法
	 判断自身属性是否存在
	 var o = new Object();
	o.prop = 'exists';

	function changeO() {
	  o.newprop = o.prop;
	  delete o.prop;
	}

	o.hasOwnProperty('prop');  // true
	changeO();
	o.hasOwnProperty('prop');  // false
```
### 前端vue问题记录（七）：JS stacktrace（Node内存溢出）
1. `npm install cross-env --save--dev`
2. `npm install increase-memory-limit --save--dev`
3. package.json
 ```
 "scripts": {
    "fix-memory-limit": "cross-env LIMIT=2048 increase-memory-limit"
  },
  "devDependencies": {
    "increase-memory-limit": "^1.0.7",
    "cross-env": "^5.2.0",
    ...
  }
  ```
  
4. `npm run fix-memory-limit`
5. 执行`npm run fix-memory-limit`这句
6. 成功后出现
成功则会出现一下界面
```
cross-env LIMIT=2048 increase-memory-limit
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/eslint' written successfully.
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/eslint.cmd' written successfully.
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/jsondiffpatch' written successfully.
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/jsondiffpatch.cmd' written successfully.
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/sass' written successfully.
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/sass.cmd' written successfully.
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/svgo' written successfully.
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/svgo.cmd' written successfully.
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/vue-cli-service' written successfully.
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/vue-cli-service.cmd' written successfully.
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/xlsx' written successfully.
'C:/E/new-nl-devlop-web/nl-autotestdev/devops-web/nl-devops-web/node_modules/.bin/xlsx.cmd' written successfully.
```
### js——获取数组中的最大值
```
let  arr = [1, 3, 5, 7,10]      
let max = arr.reduce((key1, key2) => {
return key1 = key1 > key2 ? key1 : key2
});
console.log(max)   // 10
```

1. 仅取整数部分`Math.floor()`
2. 小数进一 `Math.ceil()`
3. 四舍五入 `Math.round()`
4. /*js里没有对小数点后控制多少位的函数,想精确到小数后多少位,并四舍五入,如下)*/
 ```
 function round(v,e) 
{ 
    var a=1; 
    for(;e>0;a*=10,e--); 
    for(;e<0;a/=10,e++); 
    return Math.round(v*a)/a; 
}
```

```
let  arr = [1, 3, 5, 7,10]      
let max = arr.reduce((key1, key2) => {
return key1 = key1 > key2 ? key1 : key2
});
console.log(max)   // 10
```
### findIndex() 方法
```
let index = this.allHeaderData.findIndex(item => item.key === params.key)
//findIndex() 方法返回传入一个测试条件(函数)符合条件的数组第一个元素位置
```

### Object.keys(row).reduce

## 删除方法
1. $delete
```js
//删除数组的某个下标
 this.$delete(this.editableTabsCheckRecords, dataIndex)
```
2. 

## js删除对象的某个属性
| 序号 | 方法 | 事件 |
| -- | -- | -- |
| 1 | delete | delete obj.age |
| 2 | （ES6）：Reflect.deleteProperty() | Reflect.deleteProperty(obj,'name') |
```js
// --delete--
const obj = {
  name:'章三',
  age:18
} 
//删除age这个属性
delete obj.age 
console.log(obj). //{name:'章三'}

//Reflect.deleteProperty()
const obj = {
  name:'章三',
  age:18
} 
//删除name这个属性
Reflect.deleteProperty(obj,'name')
console.log(obj)  //{age:18}
```
## js判断对象中是否有某一属性
| 序号 | 方法 | 事件 |
| -- | -- | -- |
| 1 | obj.hasOwnProperty() | obj.hasOwnProperty('name') |
| 2 | !== | obj.name !== undefined |
| 3 | Object.keys | Object.keys(obj).indexOf("name") |
| 4 | ES6 属性名 in 对象 |"name" in obj |
```js
// --obj.hasOwnProperty()--
const obj = {
     name:'章三',
}
console.log(obj.hasOwnProperty('name'));  //true
console.log(obj.hasOwnProperty('age'));   //false

//!==
const obj = {
     name:'章三',
}
console.log(obj.name !== undefined);  //true
console.log(obj.age !== undefined);   //false

//Object.keys
const obj = {
     name:'章三',
}
Object.keys(obj).indexOf("name") // 0
Object.keys(obj).indexOf("age") // -1

//in 对象
const obj = {
     name:'章三',
}
console.log("name" in obj) // true
console.log("age" in obj) // false
```

## es6 特性
1. Set()
```js
//new set()是es6新增的数据结构，类似于数组，但它的一大特性就是所有元素都是唯一的，没有重复的值，我们一般称为集合，Set本身是一个构造函数，用来生成 Set 数据结构。
//使用场景：
//用于数组去重、用于字符串去重、实现并集、交集、和差集

//一、增删改查方法

1. 添加元素-----add()
//添加某个值，返回 Set 结构本身，当添加实例中已经存在的元素，set不会进行处理添加
let list=new Set([5,6,6]);
list.add(1);  // {1}
list.add(2).add(3).add(3);  // 3只被添加了一次
console.log(list) // {5, 6, 1, 2, 3}

2. 删除元素-----delete()
//删除某个值，返回一个布尔值，表示删除是否成功
let list=new Set([1,20,30,40])
list.delete(30)   // true   //删除值为30的元素，有返回true，没有返回false
console.log(list)    // {1, 20, 40}

3. 判断某元素是否存在-------has()
//返回一个布尔值，判断该值是否为Set的成员
let list=new Set([1,2,3,4])
list.has(2)   // 有返回true，没有返回false

4. 清除所有元素------clear()
//清除所有成员，没有返回值
let list=new Set([1,2,3,4])
list.clear()
console.log(list)    // {}

// 二、遍历方法
1. 遍历 keys()
//返回键名的遍历器，相等于返回键值遍历器values()
let list2=new Set(['a','b','c'])
for(let key of list2.keys()){
   console.log(key)//a,b,c
}

2. 遍历 values()
//返回键值的遍历器
let list=new Set(['a','b','c'])
for(let value of list.values()){
console.log(value)//a,b,c
}

3. 遍历 entries()
//返回键值对的遍历器
let list=new Set(['4','5','hello'])
for (let item of list.entries()) {
  console.log(item);
}
// ['4','4']   ['5','5']   ['hello','hello'] 

4. 遍历 forEach()
// 使用回调函数遍历每个成员
let list=new Set(['4','5','hello'])
list.forEach((value, key) => console.log(key + ' : ' + value))
// 4:4    5:5   hello:hello

// 三、使用情形
1. 用于数组去重
2. let arr = [3, 5, 2, 2, 5, 5];
let setArr = new Set(arr)     // 返回set数据结构  Set(3) {3, 5, 2}
let setArrlen = new Set(arr).size //返回 数组长度 3
arr.length>setArrlen //说明原始数组有重复值

//方法一   es6的...解构
let unique1 =  [...setArr ];      //去重转数组后  [3,5,2]

//方法二  Array.from()解析类数组为数组
let unique2 = Array.from(setArr )   //去重转数组后  [3,5,2]

2. 用于字符串去重
 let str = "352255";
let unique = [...new Set(str)].join("");     // 352 

3. 实现并集、交集、和差集
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);

// 并集
let union = new Set([...a, ...b]);
// Set {1, 2, 3, 4}

// 交集
let intersect = new Set([...a].filter(x => b.has(x)));
// set {2, 3}

// （a 相对于 b 的）差集
let difference = new Set([...a].filter(x => !b.has(x)));
// Set {1}
//Array.from(difference)
//[...difference]



```


## JS遍历方法
1. 
2. 去重
```js
const newListLength = new Set(fieldNameArr.map(item => item.fieldName)).size
//new set()是es6新增的数据结构，类似于数组，但它的一大特性就是所有元素都是唯一的，没有重复的值，我们一般称为集合，Set本身是一个构造函数，用来生成 Set 数据结构。
//使用场景：
//用于数组去重、用于字符串去重、实现并集、交集、和差集
```

## 前端请求接口，路径参数为json字符串的传递方式
```js
// 
this.axios
    .post(
        `/autotest-baseconfig/parmsValue/generateRandomValue?json=${encodeURIComponent(
        JSON.stringify(reqParams)
    )}`
).then(response => {
    if (response.respResult === '1') {
        this.randomTypeResult = response.respData
    }
})
```






