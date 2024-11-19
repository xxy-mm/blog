---
layout: post
title: "startAccessingSecurityScopedResource returns false"
---

I am developing an app recently. I saved some file in the apps documents folder, and read them in a feature time like below:

```swift
 let gotAccess = fileURL.startAccessingSecurityScopedResource()
 guard gotAccess else {
      return "Can't access audio file"
  }
  // do something with the file
  handle(fileURL)
```

When I run it on simulator, everything works as expected. But when I run it on my iphone, the gotAccess keeps returning false, what happened?

My iphone11's os version is 18.1, and so is my simulator.

I searched a lot and finally find out the answer:

the `startAccessingSecurityScopedResource` will return false if the url is in your apps security scope. In my case, I stored the file in the app's document directory:

```swift
FileManager.default.urls(for: .documentDirectory, in: .userDomainMask).first!
```

The directory is owned by my app, since its my apps own directory. Visiting files in the app's own directory does not need to call the `startAccessingSecurityScopedResource`, and when you do so, the method will simply return `false`!

But why my simulator returns true? Anyone knows?
