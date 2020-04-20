# 在 flutter 使用 js

`dart`中提供了一个 package, [js](https://pub.dev/packages/js), 可以方便地和 js 中的
代码进行互操性。

例如，要使用 js 中的`JSON`对象的功能,

```dart
// json.dart

@JS('JSON')
library JSON;

class JSON {
  @JS('stringify')
  external static String stringify(obj);
}
```

在`library`上的修饰符中的名字为 js 中的全局对象上的对象,
其余的修饰符中的名字，即在此 js 对象的方法或属性.

假设现在我们有一个 js 对象

```dart
@JS()
@anonymous
class Config {
  external bool get useInterceptor;
  external set useInterceptor(bool value);
  external bool get showMenu;
  external set showMenu(bool value);
}

```

那么，我们可以这样使用：

```dart
import './utils/json.dart';

var jsObj = Config()
  ..showMenu = false
  ..useInterceptor = true;
var str = JSON.stringify(jsObj);
print(str);
```

!!!warning

    [只有顶级(class/library)的修饰符上的名字可以使用点操作符](https://github.com/dart-lang/sdk/issues/27926).

```dart hl_lines="1 5"
@JS()
library JSON;

class JSON{
  @JS('JSON.stringify')
  external static String stringify(obj);
}
```

## references

- [stackoverflow: passing-dart-objects-to-js-functions-in-js-interop](https://stackoverflow.com/questions/33394867/passing-dart-objects-to-js-functions-in-js-interop)
- [pub: js](https://pub.dev/packages/js)
