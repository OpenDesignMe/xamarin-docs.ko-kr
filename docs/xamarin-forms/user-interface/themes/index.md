---
title: Xamarin.Forms 테마
description: 이 문서에서는 표준 보기에 대 한 특정 시각적 모양을 정의 하는 Xamarin.Forms 테마를 소개 합니다.
ms.prod: xamarin
ms.assetid: 3DFB7C55-69F6-4980-A501-588719143482
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 09/01/2017
ms.openlocfilehash: 0f49eeba072d6aeb7ead40d5d56d4af9e9bf5e27
ms.sourcegitcommit: 632955f8cdb80712abd8dcc30e046cb9c435b922
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38814709"
---
# <a name="xamarinforms-themes"></a>Xamarin.Forms 테마

![](~/media/shared/preview.png "이 API는 현재 미리 보기")

Xamarin.Forms 테마 진화 2016에서 발표 된 및을 사용해 보고 피드백을 제공 하는 고객에 대 한 미리 보기로 제공 됩니다.

테마를 포함 하 여 Xamarin.Forms 응용 프로그램에 추가 됩니다는 **Xamarin.Forms.Theme.Base** (예: 특정 테마를 정의 하는 패키지를 추가 및 Nuget 패키지 Xamarin.Forms.Theme.Light) 다른 응용 프로그램에 대 한 로컬 테마를 정의할 수 있습니다.

참조를 [밝은 테마](light.md) 및 [어두운 테마](dark.md) 페이지를 앱에 추가 하거나 확인 하는 방법에 대 한 지침은 합니다 [예제 사용자 지정 테마](custom.md)합니다.

**중요:** 단계를 따라야 [테마 어셈블리 (아래)를 로드할](#loadtheme) ios 일부 상용구 코드를 추가 하 여 `AppDelegate` Android 및 `MainActivity`합니다. 향후 미리 보기 릴리스에서 개선 됩니다.


## <a name="control-appearance"></a>모양 제어

[Light](light.md) 하 고 [어두운](dark.md) 테마는 모두 표준 컨트롤에 대 한 시각적인 특정 모양을 정의 합니다. 응용 프로그램의 리소스 사전에 테마를 추가 하면 표준 컨트롤의 모양을 변경 됩니다.

다음 XAML 태그 일부 공용 컨트롤을 보여 줍니다.

```xaml
<StackLayout Padding="40">
    <Label Text="Regular label" />
    <Entry Placeholder="type here" />
    <Button Text="OK" />
    <BoxView Color="Yellow" />
    <Switch />
</StackLayout>
```

다음이 스크린샷에서이 컨트롤을 보여 줍니다.

* 적용할 테마 없음
* 밝은 테마 (만 약간의 차이가 있는 테마 없음)
* 어두운 테마

![](images/standard-none-sml.png "테마 설정 사용 하지 않고 컨트롤") ![](images/standard-light-sml.png "밝은 테마를 사용 하 여 컨트롤") ![](images/standard-dark-sml.png "어두운 테마를 사용 하 여 컨트롤")

<a name="styleclass" />

## <a name="styleclass"></a>StyleClass

`StyleClass` 속성 보기의 모양을 테마에서 제공 되는 정의 따라 변경 될 수 있습니다.

[Light](light.md) 및 [어두운](dark.md) 테마는 모두에 세 가지 다른 모양을 정의 `BoxView`: `HorizontalRule`를 `Circle`, 및 `Rounded`합니다. 이 태그를 보여 줍니다 세 가지 다른 `BoxView`적용 하는 다른 스타일 클래스를 사용 하 여 s:

```xaml
<StackLayout Padding="40">
    <BoxView StyleClass="HorizontalRule" />
    <BoxView StyleClass="Circle" />
    <BoxView StyleClass="Rounded" />
</StackLayout>
```

이 렌더링 밝은 영역과 어두운 다음과 같습니다.

![](images/boxview-light-sml.png "밝은 테마 StyleClass와 BoxView") ![](images/boxview-dark-sml.png "BoxView 어두운 테마 StyleClass와")

<a name="builtin" />

## <a name="built-in-classes"></a>기본 제공 클래스

자동으로 스타일을 지정 하는 것 외에도 일반적인 조명 컨트롤과 어두운 테마는 현재 설정 하 여 적용할 수 있는 다음 클래스를 지원 합니다 `StyleClass` 이러한 컨트롤에서:

**BoxView**

* HorizontalRule
* 원
* 반올림

**Image**

* 원
* 반올림
* 미리 보기

**Button**

* 기본
* 기본 연산자
* 성공
* Info
* 경고
* 위험
* 링크
* 작은
* 큰

**레이블**

* 헤더
* 하기
* 본문
* 링크
* 역


## <a name="troubleshooting"></a>문제 해결

<a name="loadtheme" />

### <a name="could-not-load-file-or-assembly-xamarinformsthemelight-or-one-of-its-dependencies"></a>파일이 나 어셈블리 'Xamarin.Forms.Theme.Light' 또는 해당 종속성 중 하나를 로드할 수 없습니다.

미리 보기 릴리스에서 테마 못할 런타임에 로드할 수 있습니다. 이 오류를 해결 하려면 관련 프로젝트에 아래 표시 된 코드를 추가 합니다.

**iOS**

에 **AppDelegate.cs** 후 다음 줄을 추가 합니다. `LoadApplication`

```csharp
var x = typeof(Xamarin.Forms.Themes.DarkThemeResources);
x = typeof(Xamarin.Forms.Themes.LightThemeResources);
x = typeof(Xamarin.Forms.Themes.iOS.UnderlineEffect);
```

**Android**

에 **MainActivity.cs** 후 다음 줄을 추가 합니다. `LoadApplication`

```csharp
var x = typeof(Xamarin.Forms.Themes.DarkThemeResources);
x = typeof(Xamarin.Forms.Themes.LightThemeResources);
x = typeof(Xamarin.Forms.Themes.Android.UnderlineEffect);
```


## <a name="related-links"></a>관련 링크

- [ThemesDemo 샘플](https://github.com/xamarin/xamarin-forms-samples/tree/master/Themes/ThemesDemo)
