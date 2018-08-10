---
title: 개발자 ID를 사용하여 Xamarin.Mac 앱 서명
description: 이 문서에서는 Mac App Store 외부에 배포될 수 있도록 개발자 ID를 사용하여 Xamarin.Mac 앱을 서명하는 방법을 설명합니다. 코드 서명 옵션 및 빌드를 설명합니다.
ms.prod: xamarin
ms.assetid: cf7b733b-e08f-4f56-a233-264b29ee4c97
ms.technology: xamarin-mac
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/14/2017
ms.openlocfilehash: 130766ef7f9ab8e311db97a7209f4ec62a2ceee4
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34792306"
---
# <a name="signing-xamarinmac-apps-with-a-developer-id"></a>개발자 ID를 사용하여 Xamarin.Mac 앱 서명

개발자가 macOS 사용자에게 직접 앱을 배포하려는 경우 Apple에서는 **게이트키퍼**가 설정된 macOS 시스템에 설치할 수 있도록 개발자 ID로 앱을 코드 서명할 것을 권장합니다. 앱이 서명되지 않은 경우 **게이트키퍼**는 사용자가 앱을 설치하지 못하게 차단하고 경고 메시지를 표시합니다(시작할 때 Control 키를 길게 눌러 이 제한을 무시할 수 있음).

Apple 웹 사이트에서 [개발자 ID 및 게이트키퍼](https://developer.apple.com/resources/developer-id/) 및 [Mac 앱 스토어 외부에 배포](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html)에 대해 자세히 알아보세요.

## <a name="code-signing-options"></a>코드 서명 옵션

사용자에게 직접 배포할(Mac 앱 스토어를 통하지 않고) 앱을 빌드하려면 **개발자 ID**를 사용하도록 **서명 설정**을 지정합니다. **릴리스** 구성을 편집합니다.

 [![](signing-images/config02.png "Mac 서명 옵션")](signing-images/config02.png#lightbox)


## <a name="build"></a>빌드

빌드하기 전에, 올바른 구성을 선택하고 **Mac 빌드** 설정에서 설치 패키지를 만듭니다.

[![](signing-images/config03.png "빌드 옵션")](signing-images/config03.png#lightbox)

개발자가 앱을 빌드하는 동안 두 인증서를 사용하라는 메시지가 표시됩니다.

 [![](signing-images/image57.png "키 집합 액세스 허용")](signing-images/image57.png#lightbox)

 [![](signing-images/image58.png "키 집합 액세스 허용")](signing-images/image58.png#lightbox)

응용 프로그램을 빌드한 후 개발자는 프로젝트를 마우스 오른쪽 단추로 클릭하고 **상위 폴더 열기**를 선택하여 패키지 파일을 찾습니다(`bin/Release` 디렉터리에서). 이 패키지 파일에는 응용 프로그램 설치 관리자가 포함되어 있으므로 아무 macOS 사용자에게 설치용으로 배포할 수 있습니다.

 [![](signing-images/image59.png "찾기에서 앱 패키지 선택")](signing-images/image59.png#lightbox)

## <a name="related-links"></a>관련 링크

- [설치](~//mac/get-started/installation.md)
- [Hello, Mac 샘플](~//mac/get-started/hello-mac.md)
- [Mac 앱 스토어에서 앱 배포](https://developer.apple.com/devcenter/mac/checklist/)
- [도구 가이드: 앱 코드 서명](https://developer.apple.com/library/mac/#documentation/ToolsLanguages/Conceptual/OSXWorkflowGuide/CodeSigning/CodeSigning.html)
- [개발자 ID 및 게이트키퍼](https://developer.apple.com/resources/developer-id/)
