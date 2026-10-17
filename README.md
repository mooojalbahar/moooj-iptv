name: Build Android APK

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.24.x'
          channel: 'stable'
      - run: flutter pub get
      - run: flutter build apk --release --split-per-abi
      - name: Upload APK Artifact
        uses: actions/upload-artifact@v4
        with:
          name: IPTV-Player-Release
          path: build/app/outputs/flutter-apk/*.apk
