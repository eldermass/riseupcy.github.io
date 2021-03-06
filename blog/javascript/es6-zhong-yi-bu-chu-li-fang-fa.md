# generator 函数

1. 可用于解决异步的深度嵌套，函数与函数名间加上\* 就能成为generator函数,next\(\) 依次执行yield域，return后结束

   ```text
   function * show(){
    yield 'welcome';
    yield 'to';
    return 'toilet'
   }
   let a = show();
   console.log(a.next()) // {value: "welcome", done: false}
   console.log(a.next()) // {value: "to", done: false}
   console.log(a.next()) // {value: "toilet", done: true}
   ```

2. 可以遍历generator 函数的实例，只不过不会遍历到return的值

   ```text
   function * show(){
    yield 'welcome';
    yield 'to';
    return 'toilet'
   }
   let a = show();
   // 循坏
   for(let val of a) {
    console.log( val )
    //没有return 的值
   }
   // 可解构获取值
   let [c, ...d] = show()
   ```

3. 例子

   \`\`\`

    function \* gen\(\){ let val = yield 'riseupcy'; yield axios.get\(`https://api.github.com/users/${val}`\); return 'over' } let g = gen\(\)

   console.log\(g.next\(\)\) console.log\(g.next\(\).value.then\(res =&gt; {console.log\(res\)}\)\) // 可以控制触发函数的时机，next函数的传值，就是之后的value值 setTimeout\(\(\) =&gt; { console.log\(g.next\(\)\) },2000\)

&lt;/script&gt;

```text
#### Async Await
1. async 可以让一个普通的函数变为promise对象
```

async function fn\(\){ throw new Error\('wrong bbb'\) } fn\(\).then\(res=&gt;{ console.log\('res = '+res\); }\).catch\(err=&gt;{ console.log\(err\) }\)

```text
2. await 配合async使用可以使异步函数同步执行
```

function get\(\){ return new Promise\(\(resolve, reject\) =&gt; { setTimeout\(\(\) =&gt; { resolve\('something'\) }, 1000\) }\) }

async function show\(\){ let res = await get\(\) // 之后的函数都会等待get执行完毕 console.log\(res\) console.log\('after'\) }

show\(\)

```text
3. 在async函数中，其中一个await后的执行出错，之后的函数就不会执行
```

async function fn1\(\){ await Promise.reject\('出问题了'\) // 这里出错，之后的代码就不会执行 let a = await Promise.resolve\('成功了'\) console.log\(a\) } fn1\(\)

```text
> 捕获错误可以解决这个问题
```

async function fn1\(\){ await Promise.reject\('2出问题了'\).catch\(err=&gt;{ console.log\(err\) }\); let a = await Promise.resolve\('2成功了'\) console.log\(a\) } fn1\(\)

```text
> try catch 也行
```

async function fn\(\){ try{ await Promise.reject\('出错了'\)  
}catch\(e\){

```text
}
//前面的代码错误，不影响后续执行
let a = await Promise.resolve('bbb')
return a
```

} fn\(\)

```text
4. 应用实例
```

 async function getData\(username\){ let res = await axios.get\(&lt;code&gt;https://api.github.com/users/${username}&lt;/code&gt;\) let img = document.createElement\(&apos;img&apos;\) img.src = res.data.avatar\_url document.body.appendChild\(img\) console.log\(&apos;&\#x56FE;&\#x7247;&\#x88C5;&\#x5728;&\#x5B8C;&\#x6BD5;&apos;+ img.src \) } getData\(&apos;riseupcy&apos;\)  \`\`\`

