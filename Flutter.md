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

### 2. [Flutter] 带图标的Text - IconText

```
import 'package:flutter/material.dart';

/// icon text
class IconText extends StatelessWidget {
  final String text;
  final Widget icon;
  final double iconSize;
  final Axis direction;
  /// icon padding
  final EdgeInsetsGeometry padding;
  final TextStyle style;
  final int maxLines;
  final bool softWrap;
  final TextOverflow overflow;
  final TextAlign textAlign;

  const IconText(this.text,
      {Key key,
        this.icon,
        this.iconSize,
        this.direction = Axis.horizontal,
        this.style,
        this.maxLines,
        this.softWrap,
        this.padding,
        this.textAlign,
        this.overflow = TextOverflow.ellipsis})
      : assert(direction != null),
        assert(overflow != null),
        super(key: key);

  @override
  Widget build(BuildContext context) {
    final _style = DefaultTextStyle.of(context).style.merge(style);
    return icon == null
        ? Text(text ?? '', style: _style)
        : text == null || text.isEmpty
        ? (padding == null ? icon : Padding(padding: padding, child: icon))
        : RichText(
      text: TextSpan(style: _style,
          children: [
        WidgetSpan(
            child: IconTheme(
              data: IconThemeData(
                  size: iconSize ??
                      (_style == null || _style.fontSize == null
                          ? 16
                          : _style.fontSize + 1),
                  color: _style == null ? null : _style.color),
              child: padding == null
                  ? icon
                  : Padding(
                padding: padding,
                child: icon,
              ),
            )),
        TextSpan(
            text: direction == Axis.horizontal ? text : "\n$text"),
      ]),
      maxLines: maxLines,
      softWrap: softWrap ?? true,
      overflow: overflow ?? TextOverflow.clip,
      textAlign: textAlign ?? (direction == Axis.horizontal ? TextAlign.start : TextAlign.center),
    );
  }
}

```

### 3.


### 4.


### 5.


### 6.


