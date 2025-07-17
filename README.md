# (Optional) Install Expo CLI globally so you can use `expo` directly
npm install -g expo-cli

# 1️⃣ Create a fresh blank Expo app (no expo-router)
npx create-expo-app expoDrawerApp --template blank
cd expoDrawerApp

# 2️⃣ Install React Navigation “native” dependencies via Expo
npx expo install \
  react-native-gesture-handler \
  react-native-reanimated \
  react-native-screens \
  react-native-safe-area-context \
  @react-native-masked-view/masked-view

# 3️⃣ Install the React Navigation libraries
npm install \
  @react-navigation/native \
  @react-navigation/drawer

# 4️⃣ (Optional) If/when you add native modules like AdMob or IAP:
npx expo install \
  expo-ads-admob \
  expo-in-app-purchases \
  expo-dev-client

# 5️⃣ Start the Metro bundler and preview in Expo Go (JS‑only features)
npx expo start

# 6️⃣ Build & install your custom dev client on Android (for native features)
npx expo run:android

# 7️⃣ (Optional) For production / Play Store builds with EAS:
npm install -g eas-cli
npx eas login
npx eas build:configure
eas build --platform android
