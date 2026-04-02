# 🚀 Convair — Android Build Engine

Reusable GitHub Actions workflow for building **Expo → Android** apps without EAS.

## Features

- **APK** (installable) + **AAB** (Play Store) builds
- Native **Gradle** build (no EAS dependency)
- **Keystore signing** via secrets (reuse your EAS keystore)
- **Diawi** upload with install link
- **Caching** (npm + Gradle) for faster builds
- **Zero cost** — runs on GitHub Actions free tier

## Usage

In your app repository, create `.github/workflows/build.yml`:

```yaml
name: Build Android

on:
  push:
    branches: [main]

jobs:
  build:
    uses: jgpjuniorj/convair/.github/workflows/android-build.yml@main
    with:
      node-version: "18"
    secrets:
      KEYSTORE_BASE64: ${{ secrets.KEYSTORE_BASE64 }}
      KEYSTORE_PASSWORD: ${{ secrets.KEYSTORE_PASSWORD }}
      KEY_ALIAS: ${{ secrets.KEY_ALIAS }}
      KEY_PASSWORD: ${{ secrets.KEY_PASSWORD }}
      DIAWI_TOKEN: ${{ secrets.DIAWI_TOKEN }}
      ENV_FILE: ${{ secrets.ENV_FILE }}
```

## Required Secrets

| Secret | Description |
|--------|-------------|
| `KEYSTORE_BASE64` | Your `.jks` keystore, base64 encoded |
| `KEYSTORE_PASSWORD` | Keystore password |
| `KEY_ALIAS` | Key alias |
| `KEY_PASSWORD` | Key password |
| `DIAWI_TOKEN` | _(optional)_ Diawi API token |
| `ENV_FILE` | _(optional)_ `.env` contents, base64 encoded |

## Inputs

| Input | Default | Description |
|-------|---------|-------------|
| `node-version` | `18` | Node.js version |
| `java-version` | `17` | Java/JDK version |
| `expo-sdk` | `52` | Expo SDK (cache key) |
| `build-apk` | `true` | Build APK |
| `build-aab` | `true` | Build AAB |
| `upload-diawi` | `false` | Upload to Diawi |
