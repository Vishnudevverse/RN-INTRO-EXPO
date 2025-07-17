# Expo Drawer App with TypeScript

A step-by-step guide to bootstrap an Expo project featuring a Drawer navigator and full TypeScript support.

---

## Prerequisites

- Node.js (v14+) and npm  
- expo-cli (optional but recommended)  
- Familiarity with React Native and TypeScript basics  

---

## 1. Create the Expo Project

```bash
npm install -g expo-cli           # (Optional) install Expo CLI globally
npx create-expo-app expoDrawerApp --template blank
cd expoDrawerApp
```

---

## 2. Install React Navigation Drawer

```bash
npx expo install \
  react-native-gesture-handler \
  react-native-reanimated \
  react-native-screens \
  react-native-safe-area-context \
  @react-native-masked-view/masked-view

npm install @react-navigation/native @react-navigation/drawer
```

---

## 3. Add TypeScript

```bash
npm install --save-dev typescript @types/react @types/react-native
```

Optionally, pull in Expo’s TS config helper:

```bash
npx expo install expo-env
```

---

## 4. Configure TypeScript

Initialize a base `tsconfig.json` and then replace its contents:

```bash
tsconfig.json
```

```json
{
  "extends": "expo/tsconfig.base",
  "compilerOptions": {
    "jsx": "react-jsx",
    "strict": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["./*"]
    }
  },
  "exclude": [
    "node_modules",
    "babel.config.js",
    "metro.config.js",
    "jest.config.js"
  ]
}
```

---

## 5. Migrate to TypeScript

Rename your entry point:

```bash
git mv App.js App.tsx
```

---

## 6. Update App.tsx

Paste in this Drawer navigator setup:

```tsx
// App.tsx
import 'react-native-gesture-handler';
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createDrawerNavigator } from '@react-navigation/drawer';
import { View, Text, StyleSheet } from 'react-native';

type RootDrawerParamList = {
  Home: undefined;
  Settings: undefined;
};

const Drawer = createDrawerNavigator<RootDrawerParamList>();

function HomeScreen(): JSX.Element {
  return (
    <View style={styles.container}>
      <Text>Home Screen</Text>
    </View>
  );
}

function SettingsScreen(): JSX.Element {
  return (
    <View style={styles.container}>
      <Text>Settings Screen</Text>
    </View>
  );
}

export default function App(): JSX.Element {
  return (
    <NavigationContainer>
      <Drawer.Navigator initialRouteName="Home">
        <Drawer.Screen name="Home" component={HomeScreen} />
        <Drawer.Screen name="Settings" component={SettingsScreen} />
      </Drawer.Navigator>
    </NavigationContainer>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, alignItems: 'center', justifyContent: 'center' }
});
```

---

## 7. Run & Develop

Start the Expo server:

```bash
npx expo start
```

To add native modules (AdMob, IAP, custom dev client):

```bash
npx expo install expo-ads-admob expo-in-app-purchases expo-dev-client
npx expo run:android
```

---

## 8. Production Builds with EAS

```bash
npm install -g eas-cli
npx eas login
npx eas build:configure
eas build --platform android

Prebuild the native project (this injects the Gradle / AndroidManifest changes those packages require):

npx expo prebuild --platform android
or simply

npx expo run:android
which under the hood does the prebuild + Gradle install.

Build with Gradle (debug or release):

cd android
./gradlew assembleDebug      # for a debug APK
./gradlew assembleRelease    # for a release APK
```
---

## What You’ve Achieved

- A fresh Expo project named **expoDrawerApp**  
- A working **React Navigation Drawer**  
- Full **TypeScript** support with `App.tsx`  

Now you can customize drawer content, styling, and add more screens. Enjoy building!
