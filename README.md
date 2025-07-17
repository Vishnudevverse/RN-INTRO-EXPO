Here’s the **complete CLI command sequence** to spin up your Expo Drawer app **and** convert it to TypeScript (`.tsx`), including all necessary libraries:

```bash
# 1️⃣ (Optional) Install Expo CLI globally
npm install -g expo-cli

# 2️⃣ Create a new blank Expo project
npx create-expo-app expoDrawerApp --template blank
cd expoDrawerApp

# 3️⃣ Install React Navigation Drawer dependencies
npx expo install \
  react-native-gesture-handler \
  react-native-reanimated \
  react-native-screens \
  react-native-safe-area-context \
  @react-native-masked-view/masked-view
npm install \
  @react-navigation/native \
  @react-navigation/drawer

# 4️⃣ Install TypeScript and type definitions
npm install --save-dev typescript @types/react @types/react-native

# 5️⃣ (Optional) Expo TS config helper
npx expo install expo-env

# 6️⃣ Initialize a tsconfig.json
#    You can simply run:
npx tsc --init --pretty --jsx react-jsx

#    Then replace its contents with:
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

```bash
# 7️⃣ Rename App.js → App.tsx
git mv App.js App.tsx

# 8️⃣ Replace App.tsx contents with the TSX Drawer code below

# 9️⃣ Start the app in Expo Go (JS‑only preview)
npx expo start

# 🔟 When you need native modules (AdMob, IAP), install:
npx expo install expo-ads-admob expo-in-app-purchases expo-dev-client

# 1️⃣1️⃣ Build & install custom dev client on Android
npx expo run:android

# 1️⃣2️⃣ For production builds with EAS:
npm install -g eas-cli
npx eas login
npx eas build:configure
eas build --platform android
```

---

### 📄 Your new **App.tsx**:

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
  container: { flex: 1, alignItems: 'center', justifyContent: 'center' },
});
```

---

You’re now set up with:

1. **`expoDrawerApp`** project
2. **React Navigation Drawer**
3. **TypeScript (`.tsx`)** support

Let me know if you’d like any further tweaks!
