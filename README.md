# System requirements

- A 64-bit Mac running 10.12+.

- Xcode 8+

- The OS X 10.12 SDK. Run

> $ ls `xcode-select -p`/Platforms/MacOSX.platform/Developer/SDKs
> to check whether you have it. Building with a newer SDK works too, but the releases currently use the 10.12 SDK.

# Install depot_tools
- Clone the depot_tools repository:

> $ git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git

Add depot_tools to the end of your PATH (you will probably want to put this in your ~/.bash_profile or ~/.zshrc). Assuming you cloned depot_tools to /path/to/depot_tools (note: you must use the absolute path or Python will not be able to find infra tools):

> $ export PATH="$PATH:/path/to/depot_tools"

# glient sync
> gclient sync

# Xcode Project 생성
Xcode는 iOS 플랫폼 용으로 개발할 때 선호되는 기본 IDE입니다.

Xcode 프로젝트 생성

GN이 Xcode 프로젝트 파일을 생성하게하려면 --ide=xcode 실행시 인수를 전달하십시오 gn gen. 그러면 all.xcworkspace 지정된 출력 디렉토리에 이름이 지정된 파일이 생성됩니다 .

예:
> gn gen out/ios --args='target_os="ios" target_cpu="arm64"' --ide=xcode   
> open -a Xcode.app out/ios/all.xcworkspace

Xcode로 컴파일 및 실행

Xcode로 컴파일은 지원되지 않습니다! 우리가 대신하는 일은 Xcode에서 닌자를 실행하는 스크립트를 사용하여 컴파일하는 것입니다. 이는 생성 된 프로젝트의 빌드 단계에서 사용자 정의 실행 스크립트 조치로 수행됩니다. 이 스크립트는 명령 행에서 빌드 할 때처럼 닌자를 호출합니다.

이를 통해 Ninja의 빌드 속도를 희생하지 않고도 Xcode에서 iOS 개발자에게 익숙한 일반적인 배포 / 디버깅 워크 플로에 액세스 할 수 있습니다.

# iOS 빌드
> src/tools_webrtc/ios/build_ios_libs.sh