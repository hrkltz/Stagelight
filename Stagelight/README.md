# Stagelight / Stagelight

1. Create the Project
2. Add following Frameworks:
  1. llama.xcframework (Source: https://github.com/ggml-org/llama.cpp/releases/download/b5141/llama-b5141-xcframework.zip)
  2. Metal.framework
  3. Accelerate.framework
3. Set llama.cpp to Embed & Sign
4. Sign llama.cpp once
  1. Extract your Developer Account information: `security find-identity -p codesigning -v`
  2. Get Your Name (TeamID) (Output should look like `1) 1234567890ABCDEF1234567890ABCDEF12345678 "Apple Development: Your Name (TEAMID)"`)
  3. Sign the xcframework: `codesign --force --deep --sign "Apple Development: Your Name (TEAMID)" /path/to/llama.xcframework`
  4. Remove Quarantine Flag (activated by Gatekeeper): `xattr -rd com.apple.quarantine /path/to/llama.xcframework`
5. Extract the llama.swift example source code
6. Allow Outgoing Connections (Client)
  1. adding the following to Stagelight.entitlements
```xml
<key>com.apple.security.network.client</key>
<true/>
```
  2. Remove “Sign in with Apple” entitlement (Xcode → Target → Signing & Capabilities)
