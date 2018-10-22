---
layout: post
title: React Native Series 1 "Getting Started"!
---

Pada tutorial kali ini kita akan belajar tentang bagaimana cara membuat react-native project. Sebenernya dokumentasi dari facebook tentang react native sangat lengkap dan mudah untuk di ikuti. Namun saya menulis tutorial ini untuk mengingatkan diri saya tentang step by stepnya

Disini saya gunakan MacOs dan target applikasi yang akan terinstal di Android

Pertama sekali 

```bash
brew install watchman
```

install rn cli globally 
```bash
npm install -g react-native-cli
```

init react native project
```bash
react-native init [project_name]
```

for run on android
```bash
react-native run-android
```

Untuk run adbnya
Silahkan masuk ke adb
```bash
./adb devices
```

Jika muncul unable to load script from assets index.android.bundle
```bash
./adb reverse tcp:8081 tcp:8081
```
