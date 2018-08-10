---
title: XAML 태그 확장
description: 문서 요소 리터럴 텍스트 문자열 이외의 원본에서 설정할 수 있도록 하 여 전원 및 XAML의 유연성을 확장 하기 Xamarin.Forms XAML 태그 확장을 사용 하는 방법에 설명 합니다.
ms.prod: xamarin
ms.assetid: EB06C8B7-3FD5-47B7-A09C-A13063BD110F
ms.technology: xamarin-forms
author: charlespetzold
ms.author: chape
ms.date: 01/05/2018
ms.openlocfilehash: d507ff3c74de6bb4ea36c1a7b7dc2cd5dd60823b
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38996742"
---
# <a name="xaml-markup-extensions"></a>XAML 태그 확장

XAML 태그 확장 요소 리터럴 텍스트 문자열 이외의 원본에서 설정할 수 있도록 하 여 성능과 유연성 XAML의를 확장할 수 있습니다.

설정 일반적으로 예를 들어 합니다 `Color` 속성의 `BoxView` 같이:

```xaml
<BoxView Color="Blue" />
```

또는 16 진수 RGB 색 값으로 설정할 수 있습니다.

```xaml
<BoxView Color="#FF0080" />
```

두 경우 모두에서 텍스트 문자열을 설정 합니다 `Color` 특성으로 변환 됩니다는 `Color` 값을 [ `ColorTypeConverter` ](xref:Xamarin.Forms.ColorTypeConverter) 클래스입니다.

설정 하려면 대신 좋습니다를 `Color` 리소스 사전에 저장 된 값 또는 사용자가 만든 하는 클래스의 정적 속성의 값 또는 형식 속성을 특성 `Color` 페이지의 다른 요소에서 생성 된 또는 색상, 채도 및 명도 값을 구분 합니다.

이러한 옵션은 모두 XAML 태그 확장을 사용 하 여 있을 수 있습니다. 그러나 구 "태그 확장" 하다 고 걱정할: XAML 태그 확장은 *하지* XML에 대 한 확장입니다. XAML 태그 확장을 사용 하더라도 XAML은 항상 xml이 유효한 XML입니다.

태그 확장은 실제로 다른 방식으로 요소 특성을 표현 하 합니다. XAML 태그 확장은 중괄호로 묶은 특성 설정을 일반적으로 식별할 수 있습니다:

```xaml
<BoxView Color="{StaticResource themeColor}" />
```

중괄호 안에 있는 모든 특성 설정이 *항상* XAML 태그 확장 합니다. 그러나 볼 수 있듯이 XAML 태그 확장 중괄호를 사용 하지 않고 참조할 수도 있습니다.

이 문서는 두 부분으로 구분 됩니다.

## <a name="consuming-xaml-markup-extensionsconsumingmd"></a>[XAML 태그 확장 사용](consuming.md)  

Xamarin.Forms에 정의 된 XAML 태그 확장을 사용 합니다.

## <a name="creating-xaml-markup-extensionscreatingmd"></a>[XAML 태그 확장 만들기](creating.md)

사용자 고유의 사용자 지정 XAML 태그 확장을 작성 합니다.



## <a name="related-links"></a>관련 링크

- [태그 확장 (샘플)](https://developer.xamarin.com/samples/xamarin-forms/XAML/MarkupExtensions/)
- [Xamarin.Forms 책에서 XAML 태그 확장 장](~/xamarin-forms/creating-mobile-apps-xamarin-forms/summaries/chapter10.md)
- [리소스 사전](~/xamarin-forms/xaml/resource-dictionaries.md)
- [동적 스타일](~/xamarin-forms/user-interface/styles/dynamic.md)
- [데이터 바인딩](~/xamarin-forms/app-fundamentals/data-binding/index.md)
