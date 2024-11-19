---
layout: post
title: "FileManager.default.fileExists returns false"
---

The `FileManager.default`  has a function to check whether a file exists.

```swift
func fileExists(atPath path: String) -> Bool
```

I used to call the function like this:

```swift
let url = URL(string: "file://some/directory/filename")!

if FileManager.default.fileExists(atPath: url.absoluteString) {
  // do something with the file
}else {
  print("file does not exist.")
}
```

But now I believe I was wrong since the function keeps returning false when I try to test a file that actually exists.

The key is not about the function, but the `url.absoluteString`. I should not use it as the parameter of the `fileExists` function, instead I should use `url.path()`

```swift
func path(percentEncoded: Bool = true) -> String
```

It says the system doesn’t allow certain characters in the URL path component, so URL percent-encodes those characters to create a valid URL. Calling this function with percentEncoded = false removes any percent-encoding and returns the unencoded path.

I didn't see any difference from the path printed in the console, but the fileExists became true after I used the `path()` function.

> here is the [documentation](https://developer.apple.com/documentation/foundation/url/3988473-path)
