## Image 图片

在`SwiftUI`中, 使用 `Image` 渲染图片, Image 可以加载 资源包, 系统图标, UIImage 等图片资源.

####基本用法

1.从资源包内加载图片
```swift
Image("cat")
```

2.加载UIImage图片
```swift
Image(uiImage: UIImage(named: "dog")!)
```

3.加载苹果的 SF Symbols Icon
```SWIFT
Image(systemName: "cloud.heavyrain.fill")
    .font(.largeTitle)
```

####属性设置

内容显示设置
```swift
Image("rome")
    .resizable() // 内容延伸
    .aspectRatio(contentMode: .fit) // 缩放比例
    .frame(width: 250) // 设置宽高
```

图像平铺
```swift
// 完全平铺
Image("logo")
    .resizable(resizingMode: .tile)

// 带边距平铺
Image("logo")
    .resizable(capInsets: EdgeInsets(top: 20, leading: 20, bottom: 20, trailing: 20), resizingMode: .tile)
```

渲染 SF Symbols
```swift
Image(systemName: "cloud.sun.rain.fill")
    .renderingMode(.original) // 渲染模式
    .font(.largeTitle) // 显示大小
    .padding() // 边距
    .background(Color.black) // 背景色
    .clipShape(Circle()) // 边缘效果
```

#### 加载网络图片
SwiftUI有一个专门的AsyncImage，用于从互联网下载和显示远程图像。
其最简单的形式中，你可以只传递一个URL，像这样:
```swift
AsyncImage(url: URL(string: "https://img1.doubanio.com/view/photo/l/public/p2292035027.jpg"))
```
当 URL 为空时或者无效时,  `AsyncImage` 回显示默认灰色占位背景图

AsyncImage 在加载图片时, 不知道图片大小, 所以加载时会占满整个视图. 当图片加载完成后, 渲染成正确的大小. 我们可以设置图像的大小和显示方式，以及使用占位符颜色来避免加载前后大小不一致问题.
```swift
AsyncImage(url: URL(string: "https://img1.doubanio.com/view/photo/l/public/p2292035027.jpg")) { image in
    image.resizable() // 填充
} placeholder: {
    Color.red // 占位背景色
}
.frame(width: 128, height: 128) // 大小
.clipShape(RoundedRectangle(cornerRadius: 25)) // 圆角
```
因为生成的图像和占位符颜色现在都可以调整大小，所以frame()修改器能够确保我们AsyncImage始终保持正确的大小。

如果我们知道图像的比例, 可以通过scale参数来加载图像:

```swift
AsyncImage(url: URL(string: "https://img1.doubanio.com/view/photo/l/public/p2292035027@2x.png"), scale: 2)
```





