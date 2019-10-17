# 模拟Promise

1. 模拟Promise的基础实现，加深对Promise的理解

   ```text
   class Promise2{
    constructor(fn){
        let _this = this
        this.state = ''
        this.res_success = null
        this.res_error = null
        this.queue = []
        fn((...args) => {
            _this.state = 'success'
            _this.res_success = args
            _this.queue.forEach( val => {
                val.fn1(...args)
            })
        }, (...args) => {
            _this.state = 'error'
            _this.res_error = args
            _this.queue.forEach(val => {
                val.fn2(...args)
            })
        })
    }
    then(fn1, fn2){
        if(this.state == 'success'){
            fn1(...this.res_success)
        }else if(this.state == 'error'){
            fn2(...this.res_error)
        }else{
            //在没界定状态前，先储存函数
            this.queue.push({fn1, fn2})
        }
    }
   }
   ```

   > 测试一下代码
   >
   > \`\`\` let p = new Promise2\(\(resolve,reject\)=&gt;{ setTimeout\(\(\)=&gt;{ resolve\(123\) },1000\) }\)

p.then\(res=&gt;{ console.log\(res\) }\)

```text
2. 模拟一下Promise.all的实现
```

Promise2.all = function\(arr\){ let result = \[\] return new Promise2\(function \(resolve,reject\){ let i = 0 next\(\) function next\(\){ arr\[i\].then\(function \(res\){ result.push\(res\) i++ if\(i == arr.length\){ resolve\(result\) }else{ next\(\) } },reject\) } }\) }

```text
> 测试promise.all
```

let p1 = new Promise2\(\(resolve,reject\)=&gt;{ setTimeout\(\(\)=&gt;{ resolve\(11\) },1000\) }\) let p2 = new Promise2\(\(resolve,reject\)=&gt;{ setTimeout\(\(\)=&gt;{ resolve\(22\) },1000\) }\) Promise2.all\(\[p1,p2\]\).then\(res=&gt;{ console.log\(res\) }\) \`\`\`

