---
title: TIL-4
date: 2023-10-04
---
When testing an iOS app using [Maestro](https://maestro.mobile.dev/), sometimes [nested elements are not visible](https://maestro.mobile.dev/platform-support/react-native#interacting-with-nested-components-on-ios) by the selectors. It may happen, when you use `TouchableOpacity `, `Pressable`, `TouchableWithoutFeedback` etc. To fix it, pass `accessible={false}` to those components.

You can inspect view hierarchy using [Xcode](https://dasdom.dev/the-view-debugger-in-xcode/) or
```bash
maestro hierarchy
```





