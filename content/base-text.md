# Text 文本 

### Text
> Text 作为 SwiftUI 中一个基本的控件, 等价于 UIKit 中的 UILabel, 但它可以用更少的代码，实现 UIKit 中对文本的复杂操作。

```
Text("Hello SwiftUI") // 设置文本内容
        .frame(maxWidth: .infinity, alignment: .leading) // 设置大小
        .font(.largeTitle) // 设置字体
        .background(Color.blue) // 背景色
        .foregroundColor(.white) // 前景色(文字颜色)
        .lineSpacing(5) // 行间距
        .padding(.all, 15) // 外边距
        .border(Color.blue, width: 5) //  边框
        .rotationEffect(.init(degrees: 45), anchor: .center) // 旋转
        .blur(radius: 1) // 模糊
```
---
### Field
- TextField 文本输入框     
- SecureField 密码输入框

```
TextField("请输入用户名", text: $username) // $0: 占位字符 $1: 输入的内容
                 .textFieldStyle(RoundedBorderTextFieldStyle()) // 类型
                 
SecureField("请输入密码", text: $password) // $0: 占位字符 $1: 输入的内容
                    .textFieldStyle(RoundedBorderTextFieldStyle()) // 类型
```

