# 文件操作

操作关系 FileReader -&gt; Blob -&gt; ArrayBuffer

## FileReader

```javascript
function getFile() {
  let file = document.getElementById("file");
  let reader = new FileReader();
  // 获取file文件的Blob对象
  let fileblob = file.files[0];
  reader.readAsDataURL(fileblob);
  // 操作完之后，在reader.result中获取结果
  reader.onload = function() {
    console.log(reader);
    document.getElementById("fuck").innerHTML = `<img src='${this.result}'/>`;
    console.log(this.result);
  };
}
```

## Blob

```typescript
let blob = new Blob(); // 参数 [ArrayBuffer | ArrayBufferView | String | Blob, source], MIMEtype

function downLoadFile(res) {
  const ele = document.createElement("a");
  ele.setAttribute(
    "href",
    window.URL.createObjectURL(new Blob([document.querySelector("#text").innerHTML], { type: "text/plain" }))
  ); //设置下载文件的url地址
  ele.setAttribute("download", "download"); //用于设置下载文件的文件名
  ele.click();
}
```

## ArrayBuffer

