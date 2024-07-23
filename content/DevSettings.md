---
title: DevSettings
date: 2024-07-23
---

I haven't  seen mention of this in online discussions or blog posts, but you can use the `DevSettings.addMenuItem` method to add a custom item to the Dev Menu. This can be helpful during development or debugging.

```
DevSettings.addMenuItem('Show Secret Dev Screen', () => {
  Alert.alert('Showing secret dev screen!');
});
```

If you are using Expo (I be you do), there is a `DevClient.registerDevMenuItems` method.

