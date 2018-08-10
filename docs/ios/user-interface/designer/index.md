---
title: Ios 디자이너 사용자 인터페이스 빌드
description: 이 문서에는 iOS 용 Xamarin 디자이너를 사용 하 여 스토리 보드와.xib 파일을 응용 프로그램의 사용자 인터페이스를 만드는 방법을 설명 합니다. 도구의 가용성, 기본 기능, 디자인할 수 있는 컨트롤에 설명 하 고 용도 대 한 연습을 제공 하는 문서에 연결 합니다.
ms.prod: xamarin
ms.assetid: E35EFB69-EBBA-40E3-ADBE-CB8016F17127
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 05/31/2018
ms.openlocfilehash: a931373a6abba3084af3c7aefcdddc903ad1b577
ms.sourcegitcommit: 7a89735aed9ddf89c855fd33928915d72da40c2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36209234"
---
# <a name="building-user-interfaces-with-the-ios-designer"></a>Ios 디자이너 사용자 인터페이스 빌드

_IOS 용 Xamarin 디자이너에는 Mac 및 Visual Studio 용 Visual Studio와 완벽 하 게 통합 하는 iOS 스토리 보드 및 작성기 인터페이스 형식에 대 한 비주얼 디자이너는입니다. 디자이너 iOS 스토리 보드 및.xib 형식과 완전히 호환을 유지 하 Mac 용 Visual Studio 또는 Xcode의 인터페이스 작성기 외에도 Visual Studio에서 파일을 편집할 수 있습니다. 또한 iOS 용 Xamarin 디자이너는 사용자 지정 컨트롤 편집기에서 디자인 타임에 렌더링 하는 등의 고급 기능을 지원 합니다._

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio for Mac](#tab/macos)

[![iOS, Mac 용 Visual Studio의 디자이너](images/designer-vsmac-sml.png "iOS 디자이너")](images/designer-vsmac.png#lightbox)

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

[![Visual Studio의 디자이너 iOS](images/designer-vs.png "iOS 디자이너")](images/designer-vs.png#lightbox)

-----

## <a name="availability"></a>가용성

Visual Studio 2017 windows 및 Mac 용 Visual Studio에서 iOS 용 Xamarin 디자이너 ´ ù.

이 가이드에서 다루는 내용에 대 한 지식이 있다고 가정은 [안내 Xamarin.iOS 시작](~/ios/get-started/index.md)합니다.

## <a name="ios-designer-basicsintroductionmd"></a>[iOS Designer 기본 사항](introduction.md)

이 가이드에서는 Xamarin iOS 디자이너의 기능입니다. 컨트롤을 시각적으로 배치 하려면 디자이너를 사용 하는 방법 및 속성을 편집 하는 방법을 보여 주는 디자이너 기본 사항 설명 합니다.

## <a name="designable-controls-overviewios-designable-controls-overviewmd"></a>[디자인할 수 있는 컨트롤 개요](ios-designable-controls-overview.md)

이 가이드에서 사용자 지정 컨트롤을 깊이에서 찾습니다 생성 되는 방식 및 요구 사항을 디자인 화면에 렌더링할 충족 해야 합니다. 또한 디자인할 수 있는 컨트롤을 사용 하는 경우 발생할 수 있는 일반적인 문제를 디버깅 하는 방법을 보여 줍니다.

## <a name="walkthrough---using-custom-controls-with-ios-designerios-designable-controls-walkthroughmd"></a>[연습-사용자 지정 컨트롤을 사용 하 여 ios 디자이너](ios-designable-controls-walkthrough.md)

이 문서에서는 사용자 지정 컨트롤을 만들고 iOS 디자이너에서 사용 하는 방법을 보여 주는 단계별 연습을 제공 합니다. 디자이너의 도구 상자에서 사용할 수 있는 컨트롤을 끌어서/삭제 보기로 정도의 만들어야 하는 방법을 보여 줍니다. 또한 디자인 타임에 설정 될 수 있는 속성을 만드는 방법 뿐만 아니라 디자인 타임 및 런타임, 올바르게 렌더링 하도록 컨트롤을 구현 하는 방법을 보여 줍니다.

## <a name="auto-layout-with-the-xamarin-ios-designerdesigner-auto-layoutmd"></a>[Xamarin ios 디자이너 자동 레이아웃](designer-auto-layout.md)

이 가이드에서는 iOS 자동 레이아웃 및 iOS 디자이너에서 사용할 수 있는 새 제약 조건 워크플로 소개합니다.
