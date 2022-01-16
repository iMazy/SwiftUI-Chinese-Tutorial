# 标签文本 

### Text

#### 基础使用
 Text 作为 SwiftUI 中一个基本的控件, 等价于 UIKit 中的 UILabel, 但它可以用更少的代码，实现 UIKit 中对文本的复杂操作。

```
Text("Hello SwiftUI") // 设置文本内容
    .lineLimit(3) // 限制行数
    .truncationMode(.middle) // 截断方式
    .frame(maxWidth: .infinity, alignment: .leading) // 设置大小
    .font(.largeTitle) // 设置字体
    .background(Color.blue) // 背景色  
    .foregroundColor(.white) // 前景色(文字颜色)
    .lineSpacing(5) // 行间距
    .padding(.all, 15) // 外边距
    .border(Color.blue, width: 5) //  边框
    .rotationEffect(.init(degrees: 45), anchor: .center) // 旋转
    .blur(radius: 1) // 模糊
    .multilineTextAlignment(.center) // 文本对齐方式, 例如.center、 或.trailing
    .textSelection(.enabled) // 是否显示选中操作
        
```

#### 文本格式

```
// 字符串
let possibles: [String] = ["A", "B", "C", "D"]
var body: some View {
    Text(ingredients, format: .list(type: .and)) // B, D, C, and A
}

// 数字
let rolls: [Int] = Int.random(in: 1...6)
var body: some View {
    Text(rolls, format: .list(memberStyle: .number, type: .and)) // 4, 3, 2, and 6
}

// 距离或重量等测量值
let length = Measurement(value: 225, unit: UnitLength.centimeters)
var body: some View {
    Text(length, format: .measurement(width: .wide)) // 7.4 feet
}

//  货币的格式化
var body: some View {
    Text(72.3, format: .currency(code: "CAD")) // CA$72.30
}

// 如果需要支持 iOS 14 和 13，您可以改用该formatter参数

static let taskDateFormat: DateFormatter = {
    let formatter = DateFormatter()
    formatter.dateStyle = .long
    return formatter
}()

let dueDate = Date()
var body: some View {
    Text("Task due date: \(dueDate, formatter: Self.taskDateFormat)") //  Task due date: Jan 16, 2022
}

```

#### 如何在文本中的字母之间添加间距

SwiftUI 为我们提供了两个修饰符来控制文本视图中的字符间距，允许我们根据您的需要使字母间距更紧密或更远。
两个修饰符是tracking() 和 kerning(): 都在字母之间添加间距，但是跟踪会拉开连字，而紧缩不会，紧缩会留下一些尾随空格，而跟踪不会。

```
Text("Hello World")
    .tracking(20) // H  e l l  o    W o  r l d
```

tracking() 和 kerning() 的区别

```
Text("ffi")
    .font(.custom("AmericanTypewriter", size: 72))
    .kerning(100) // 显示结果:  f   fi
    
Text("ffi")
    .font(.custom("AmericanTypewriter", size: 72))
    .tracking(100) // 显示结果: f   f   i
```


#### 日期格式化
SwiftUI 的文本视图带有两个特定的日期格式化程序, 一个处理单个日期，一个处理日期范围。

单个日期
```
 // show just the date
Text(Date().addingTimeInterval(600), style: .date) // Jan 16, 2022

 // show just the time
 Text(Date().addingTimeInterval(600), style: .time) // 18:12 PM

// show the relative distance from now, automatically updating
Text(Date().addingTimeInterval(600), style: .relative) // 8 min, 12 sec

// make a timer style, automatically updating
Text(Date().addingTimeInterval(600), style: .timer) // 8:12
```

日期范围
```
Text(Date()...Date().addingTimeInterval(600)) // 2:37-2.47 PM
```

#### 使用 redacted() 将内容标记为占位符
SwiftUI 允许我们在视图中将文本标记为占位符，这意味着它会被渲染，但会被灰色遮盖以显示它不是最终内容。这是通过redacted(reason:)修饰符提供的，以及unredacted()可用于根据需要覆盖编辑的修饰符。

```
Text("This is placeholder text")
    .font(.title)
    .redacted(reason: .placeholder)
```

#### SwiftUI 渲染 Markdown 内容

iOS 15后, SwiftUI 内置了对渲染 Markdown 的支持，包括粗体、斜体、链接等。我觉得写这个几乎是愚蠢的，因为老实说它不需要做任何工作——它实际上是内置在 SwiftUI 的Text视图中.

```
VStack {
    Text("This is regular text.")
    Text("* This is **bold** text, this is *italic* text, and this is ***bold, italic*** text.")
    Text("~~A strikethrough example~~")
    Text("`Monospaced works too`")
    Text("Visit Apple: [click here](https://apple.com)")
}
```

### Field
- TextField 文本输入框     
- SecureField 密码输入框

```
@State private var name = "Mazy"
@State private var password = "***"

var body: some View {
TextField("Shout your name at me", text: $name) // $0: 占位字符 $1: 输入的内容
        .textFieldStyle(.roundedBorder) // 边框样式
        .textCase(.uppercase) // 大小写
        .padding(.horizontal) // 边距
                    
    SecureField("请输入密码", text: $password) // $0: 占位字符 $1: 输入的内容
                      .textFieldStyle(.roundedBorder) // 类型
}
                     

```

### Label

```
// 使用 SF 符号
Label("Your account", systemImage: "folder.circle") 

// 使用自己的图像
Label("Welcome to the app", image: "star")

// font()您可以使用修饰符并行缩放文本和图标
Label("Your account", systemImage: "person.crop.circle")
    .font(.title)
        
// 可以通过使用 `labelStyle()` 修饰符来控制标签的显示方式，如下所示：.titleOnly  .iconOnly   .titleAndIcon

Label("Text Only", systemImage: "heart")
    .font(.title)
    .labelStyle(.titleOnly)

Label("Icon Only", systemImage: "star")
    .font(.title)
    .labelStyle(.iconOnly)

Label("Both", systemImage: "paperplane")
    .font(.title)
    .labelStyle(.titleAndIcon)
```


