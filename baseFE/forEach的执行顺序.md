建议：尽量不要用forEach循环异步函数
```
var a = [1]
var a = [1]
a.forEach((item, index) => {
    setTimeOut(()=>{

    }, 0)
})
console.log("1")

new Promise(resolve=>{
   setTimeout(()=>console.log("1"),200)
   resolve(true)
}).then(res=> setTimeout(()=>console.log("2"),50))
```