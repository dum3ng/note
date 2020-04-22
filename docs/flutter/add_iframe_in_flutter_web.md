# 在 flutter web 中添加 iframe

文章见： [https://flatteredwithflutter.com/flutter-web-and-iframe/](https://flatteredwithflutter.com/flutter-web-and-iframe/)

代码如下：

```dart
import 'dart:html';
import 'dart:ui' as ui;

class _MyWidgetState extends State<MyWidget> {

  @override
  void initState() {
    super.initState();

    final IFrameElement _iframeElement = IFrameElement();

    _iframeElement.height = '500';
    _iframeElement.width = '500';
    _iframeElement.src = 'https://bing.com';
    _iframeElement.style.border = 'none';

    // ignore: undefined_prefixed_name
    ui.platformViewRegistry.registerViewFactory(
      'iframeElement',
      (int viewId) => _iframeElement,
    );

  }

  @override
  Widget build(BuildContext context) {
    Widget _iframeWidget;
    _iframeWidget = HtmlElementView(
      viewType: 'iframeElement',
      key: UniqueKey(),
    );
    return Container(
      child: _iframeWidget
    )
  }

}

```
