---
layout: post
title: "Set the app's background in swiftUI"
---

I found it difficult to change the whole app's background, especially when you use something like `NavigationSplitView` or `List`. Simply setting the background of these views using `.background` does not work as expected. After hours of searching, I finally found the solution.

Consider we are going to change the background of a `List`:

```swift
struct AudioItemListView: View {
  private var items = ["a", "b", "c"]
  var body: some View {
    List {
      ForEach(items) { item in
        Text(item)
 }
 }
    // won't work
 .background(Color.red)
 }
}
```

The above `.background` modifier will not take effect because SwiftUI sets the scroll content background automatically. You should first remove that background.

```swift
struct AudioItemListView: View {
  private var items = ["a", "b", "c"]
  var body: some View {
    List {
      ForEach(items) { item in
        Text(item)
 }
 }
    // hide the scroll content background
 .scrollContentBackground(.hidden)
    // will work now
 .background(Color.red)
 }
}
```

After setting the background of the `List`, you may find the background of the rows in the list does not change together. This is because the row has its own modifier for the job: `listRowBackground`

```swift
struct AudioItemListView: View {
  private var items = ["a", "b", "c"]
  var body: some View {
    List {
      ForEach(items) { item in
        Text(item)
          // list row background
 .listRowBackground(Color.blue)
 }
 }
    // hide the scroll content background
 .scrollContentBackground(.hidden)
    // will work now
 .background(Color.red)
 }
}
```

Since the `listRowBackground` accepts a View not a Color as its argument, you can't pass `.blue` directly, passing `Color.blue` which represents a View instead.

If you want to change the background to an Image, it's all the same.

```swift
struct AudioItemListView: View {
  private var items = ["a", "b", "c"]
  var body: some View {
    List {
      ForEach(items) { item in
          Text(item)
            // list row background
 .listRowBackground(Color.blue)
 }
 }
    // hide the scroll content background
 .scrollContentBackground(.hidden)
    // the background can also accept a View as parameter
 .background {
      Image("youImageName")
 .resizable()
 .scaledToFill()
 .frame(width: UIScreen.main.bounds.width, height: .infinity)
 .ignoresSafeArea()
 }
 }
}

```

The above code will work if you have an image in your assets. The `frame` modifier is necessary to prevent big images from expanding the container.

You can add as many backgrounds as you wish using ZStack, as long as the background images/colors are not completely opaque.

```swift
 .background {
    ZStack{
      Image("youImageName")
 .resizable()
 .scaledToFill()
 .frame(width: UIScreen.main.bounds.width, height: .infinity)
 .ignoresSafeArea()
 Color.blue.opacity(0.3)
 .ignoresSafeArea()
 }
}
```

But you should notice that setting the background on one page will not affect other pages. You need to set the background for each page.

Leave your comment if there is any better solution~
