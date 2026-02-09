---
name: auto_fix_terminal
description: Automatically diagnose and fix common terminal command failures using proxy and safe recovery strategies.
---

<!--
scope: terminal
version: 1.1
-->

# Auto Fix Terminal Skill

## When to Use

Use this skill when a terminal command fails and the failure may be caused by:

- Network restrictions or blocked connections
- Package registry access issues
- Corrupted cache or incomplete dependency downloads

## Supported Commands

### JavaScript / Node.js

- npm install
- npm ci
- pnpm install
- yarn install

### Git

- git clone
- git pull
- git fetch
- git submodule update

### Python

- pip install
- pipx install
- poetry install

### Rust / Go

- cargo build
- cargo fetch
- go mod download

### Flutter / Dart

- flutter pub get
- flutter doctor
- dart pub get

### Mobile / Native

- pod install
- gradlew build
- gradle build
- xcodebuild

### System / CLI

- brew install
- brew update
- curl
- wget

## Diagnosis Rules

Treat the failure as network-related if the command output contains:

- timeout / ETIMEDOUT
- connection reset / ECONNRESET
- TLS / SSL / handshake
- failed to fetch / unable to access
- network is unreachable

## Auto Fix Strategy

### Step 1: Retry with Proxy

Retry the same command once with the following environment variables enabled:

- http_proxy=http://127.0.0.1:7890
- https_proxy=http://127.0.0.1:7890
- all_proxy=socks5://127.0.0.1:7890

After retrying, always remove the proxy environment variables.

### Step 2: Ecosystem-Specific Fixes

If the proxy retry still fails, apply **only one** fix based on the command type.

#### Node.js

- Clear cache:

```sh
npm cache clean --force
pnpm store prune
```

- Retry the original install command once.

#### Flutter / Dart

- Repair pub cache:

```bash
flutter pub cache repair
```

- Retry `flutter pub get`.

#### CocoaPods

- Update specs:

```bash
pod repo update
```

#### Rust

- Retry with sparse registry:

```bash
CARGO_REGISTRIES_CRATES_IO_PROTOCOL=sparse
```

#### Go

- Set module proxy mirror:

```bash
go env -w GOPROXY=https://goproxy.cn,direct
```

## Safety Rules

- Do not repeat the same fix more than once.
- Never enter infinite retry loops.
- Prefer minimal and reversible fixes.
- Do not modify global configuration unless necessary.
- Explain the fix before executing it.

## Example

If the user runs:

```bash
flutter pub get
```

And the command fails due to a network error, the agent should:

1. Retry with proxy enabled.
2. If it still fails, run `flutter pub cache repair`.
3. Retry `flutter pub get` once.

## Notes

- Proxy address can be adjusted to match the local environment.
- This skill is designed for AI Agent collaboration, not blind retries.
