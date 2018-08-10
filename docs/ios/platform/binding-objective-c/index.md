---
title: IOS 라이브러리 바인딩
description: 이 문서에서는 C# 바인딩을 만들 Objective-c 코드를 Xamarin.iOS 응용 프로그램에서 네이티브 라이브러리 및 CocoaPods를 사용할 수 있도록 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: EBDC50DC-B44B-4003-AB2B-1EEB868A5E01
ms.technology: xamarin-ios
ms.custom: xamu-video
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/18/2017
ms.openlocfilehash: 75c8f9a2eea080c3da031366b314d94929080811
ms.sourcegitcommit: ec50c626613f2f9af51a9f4a52781129bcbf3fcb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37855223"
---
# <a name="binding-ios-libraries"></a>IOS 라이브러리 바인딩

Xamarin.iOS 및 Xamarin.Mac CocoaPods 및 Objective-c 라이브러리 바인딩 방법을 알아보려면 다음이 링크를 수행 합니다.

- [**개요** ](~/cross-platform/macios/binding/overview.md) -
  바인딩이 작동 하는 방법에 대해 설명 합니다.
- [**Objective-c 라이브러리 바인딩** ](~/cross-platform/macios/binding/objective-c-libraries.md) -
  Xamarin 프로젝트에서 사용 하기 위한 Objective-c 라이브러리를 바인딩하는 방법에 대 한 지침입니다.
- [**입력 정의 참조 가이드** ](~/cross-platform/macios/binding/binding-types-reference.md) -
  모든 바인딩 생성 프로세스를 추진 하는 바인딩 작성자가 사용할 수 있는 특성에 설명 합니다.

## <a name="objective-sharpiecross-platformmaciosbindingobjective-sharpieindexmd"></a>[Objective Sharpie](~/cross-platform/macios/binding/objective-sharpie/index.md)

목표 Sharpie는 바인딩의 첫 번째 패스를 부트스트랩 하는 데는 명령줄 도구입니다.
공용 API에 매핑할 네이티브 라이브러리의 헤더 파일을 구문 분석 하 여 작동 합니다 [바인딩 정의](~/cross-platform/macios/binding/objective-c-libraries.md) (그렇지 않은 경우 수동으로 수행 되는 프로세스). 목표 Sharpie 자체적으로 바인딩을 만들지 않습니다 하지만 시작 하는 데 도움이!

목표 Sharpie 3.0 Cocoapods를 직접 바인딩하는 기능을 도입 되었습니다!

## <a name="walkthrough---binding-an-ios-objective-c-librarywalkthroughmd"></a>[연습-iOS Objective-c 라이브러리 바인딩](walkthrough.md)

이 페이지에서는 오픈 소스를 사용 하 여 iOS 바인딩 프로젝트 만들기의 단계별 연습은 [ **InfColorPicker** ](https://github.com/InfinitApps/InfColorPicker) 예로 Objective C 프로젝트입니다. 합니다 **InfColorPicker** 라이브러리는 사용자가 색 선택 영역을 보다 친숙 한 만들기, HSB 표현에 따라 색을 선택할 수 있는 재사용 가능한 뷰 컨트롤러를 제공 합니다.
목표 Sharpie 바인딩 프로세스를 지원 하기 위해 사용 됩니다.

## <a name="xamarin-university-lightning-lecture"></a>Xamarin University 번개 강의

> [!VIDEO https://youtube.com/embed/ZUoPLcmnf1o]

**iOS 바인딩 C/c + +에서에서 [Xamarin University](https://university.xamarin.com/)**

## <a name="related-links"></a>관련 링크

- [Objective-C 바인딩](~/cross-platform/macios/binding/index.md)
- [Mac 바인딩](~/mac/platform/binding.md)
- [Objective-c 바인딩 라이브러리를 빌드할 Xamarin University 과정:](https://university.xamarin.com/classes/track/all#building-an-objective-c-bindings-library)
- [Xamarin University 과정: 목표 Sharpie 사용 하 여 Objective-c 바인딩 라이브러리를 빌드](https://university.xamarin.com/classes/track/all#build-an-objective-c-bindings-library-with-objective-sharpie)