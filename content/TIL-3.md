---
title: TIL-3
date: 2023-10-03
---
You can [skip Expo's onboarding screen](https://docs.expo.dev/build-reference/e2e-tests/#using-development-builds-to-speed-up-test-run-time) in the test environment by appending `disableOnboardig=1` to the development server URL.

When using [Maestro](https://maestro.mobile.dev/), you can open the app with the `openLink`:

```yaml
appId: <your_app_id>
---
- launchApp:
    clearState: true
    clearKeychain: true
- openLink: "exp+<your_app_nam>://expo-development-client/?url=http%3A%2F%2F192.168.1.27%3A8081?disableOnboarding=1"
```