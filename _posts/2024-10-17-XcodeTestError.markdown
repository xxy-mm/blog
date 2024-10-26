---
layout: post
title: "Resolve Xcode Test stuck"
---

I recently added a XCTest target to my existing project in Xcode to improve my code quality. But when I run the test, Xcode went stuck and keeps showing testing on the toolbar. I wait for about 10 minutes and nothing changed. After about half an hour of searching on the web I got the solution.

Here are the steps:

1. In the Xcode menu, go to Product -> Schema -> EditSchema -> Test
2. Under the Test Plans section, you can find your project.
3. There's a small `right arrow` icon after the projects name. Click it.
4. There's an Options button at the right side of the new page. Click it.
5. A popup is shown, and have a select called `Parallelization`
6. Select `Swift Testing Only`
7. The editor may ask you to save the configuration, just save it.
8. Run your test again, and it should work now.

Why this happened?

I've no idea...

But just do it, stop wasting time on the bug.
