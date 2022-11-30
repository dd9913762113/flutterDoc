# flutterDoc

### 1. [Flutter] [大文件上传之随传随处理]（避免占用大量内存）


```
// 初始化一个Http客户端，并加入自定义Header
var req = await HttpClient().putUrl(uri);
headers.forEach((key, value) {
req.headers.add(key, value);
});


// 读文件
var s = await file.open();
var x = 0;
var size = file.lengthSync();
var chunkSize = 65536;
while (x < size) {
    var _len = size - x >= chunkSize  ? chunkSize : size - x;
    val = s.readSync(_len).toList();
    x = x + _len;
    // 处理数据块
    val = proc(val);
    // 加入http发送缓冲区
    req.add(val);
    // 立即发送并清空缓冲区
    await req.flush();
}
await s.close();

// 文件发送完成
await req.close();
// 获取返回数据
final response = await req.done;
// 其它处理逻辑
print("response statusCode: ${resp.statusCode}");
```

