```jsx
eas build -p android --profile preview
```

```jsx
{
  "cli": {
    "version": ">= 3.17.1"
  },
  "build": {
    "preview": {
      "android": {
        "buildType": "apk"
      }
    },
    "preview2": {
      "android": {
        "gradleCommand": ":app:assembleRelease"
      }
    },
    "preview3": {
      "developmentClient": true
    },
    "production": {}
  }
}
```

```jsx
// eas.json
{
  "cli": {
    "version": ">= 3.17.1"
  },
  "build": {
    "preview": {
      "android": {
        "buildType": "apk"
      }
    },
    "production": {}
  }
}
```

Link: [[React Native]]

npx run android 
npx react-native  build-android --mode-release
