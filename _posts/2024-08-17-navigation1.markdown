---
layout: post
title: "在SwiftUI中使用编程式导航（一）"
---

# 在 SwiftUI 中，我们一般使用 `NavigationLink` 创建导航链接，用户点击之后，导航到对应页面。但是有时需要不通过直接点击链接进行导航。

## 场景

* 场景一： 调用 api 成功返回数据后自动导航到下个页面。
* 场景二： Menu 菜单中的按钮，点击之后进行导航。

## 实现方式

有三种以上的方式可以实现。我们只讲最简单的一种：使用 `navigationDestination(isPresented:destination:)`



```swift
struct ExampleView: View {
    @State private var isShow = false
    
    var body: some View {
        NavigationStack {
            VStack {
                Button("showTargetView"){
                    isShow = true
                }
            }
            .navigationDestination(isPresented: $isShow) { TargetView() }
        }
    }
}
```

关键有三点：

1. 必须在 NavigationView, NavigationStack, NavigationSplitView 内部使用。上例中是 `NavigationStack`
2. 必须包含一个 State，用来保存状态。上例中是 `isShow`
3. 必须包含一个触发元素，用来切换 State。上例中是 `Button`



当然，还有其它方法，但都不如这种方法简单直观。