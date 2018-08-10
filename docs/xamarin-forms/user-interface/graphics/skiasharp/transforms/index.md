---
title: SkiaSharp 변환
description: 이 문서에서는 Xamarin.Forms 응용 프로그램에서 SkiaSharp 그래픽을 표시 하기 위한 변환 하 고 샘플 코드를 사용 하 여이 보여 줍니다.
ms.prod: xamarin
ms.technology: xamarin-skiasharp
ms.assetid: E9BE322E-ECB3-4395-AFE4-4474A0F25551
author: charlespetzold
ms.author: chape
ms.date: 03/10/2017
ms.openlocfilehash: 89aa29d5bf03b1d6f9668ef2aee6ce0c1a277cc5
ms.sourcegitcommit: 12d48cdf99f0d916536d562e137d0e840d818fa1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2018
ms.locfileid: "39615862"
---
# <a name="skiasharp-transforms"></a>SkiaSharp 변환

_SkiaSharp 그래픽을 표시 하기 위한 변환에 알아봅니다_

SkiaSharp의 메서드로 구현 되는 기존 그래픽 변환을 지원 합니다 [ `SKCanvas` ](https://developer.xamarin.com/api/type/SkiaSharp.SKCanvas/) 개체입니다. 변환 좌표 및에서 지정 하는 크기를 변경 하는 수학적으로 `SKCanvas` 그리기 기능으로 그래픽 개체는 렌더링 됩니다. 변환은 애니메이션 또는 반복적인 그래픽 그리기에 대 한 편리한 경우가 많습니다. 몇 가지 기법 &mdash; 비트맵 이나 텍스트를 회전 같은 &mdash; 변환 사용 하지 않고 가능 하지 않습니다.

SkiaSharp 변환 작업을 지원 합니다.

- *변환* 다른 곳에서 shift 좌표로
- *확장* 좌표와 크기를 늘리거나
- *회전* 지점 좌표를 회전 하려면
- *기울이기* 이동할 가로 또는 세로로 조정 사각형은 평행 사변형 되도록

이러한 라고 *affine* 변환 합니다. Affine 변환만 평행선을 항상 보존 및 무한 되도록 좌표 또는 크기를 일으키지 않습니다. 사각형은 평행 사변형 이외의으로 변환 되지 않습니다 및 원 타원 이외의 값으로 변환 되지 됩니다.

SkiaSharp 비 관계 변환 지원 (라고도 *프로젝션* 또는 *관점* 변환) 표준 3-3 하 여 변환 매트릭스를 기반 합니다. 비 관계 변환 사각형을 모든 볼록 사변형 (네 면 그림 모든 내부 각도가 미만의 180도)로 변환할 수 있습니다. 비 affine 변환만 좌표나 크기 무한 되도록 하면 되지만 3D 효과 대 한 중요 합니다.

## <a name="differences-between-skiasharp-and-xamarinforms-transforms"></a>SkiaSharp 및 Xamarin.Forms 변환의 차이점

Xamarin.Forms는 SkiaSharp의 유사한 변환도 지원 합니다. Xamarin.Forms [ `VisualElement` ](xref:Xamarin.Forms.VisualElement) 클래스에는 다음 변환 속성을 정의 합니다.

- `TranslationX` 및 `TranslationY`
- `Scale`
- `Rotation`, `RotationX` 및 `RotationY`

합니다 `RotationX` 및 `RotationY` 속성은 큐브 뷰 변환 하는 의사 3D 효과 만듭니다.

가지 SkiaSharp 변환 및 Xamarin.Forms 변환 간의 몇 가지 중요 한 차이점이 있습니다.

첫 번째 차이점은 SkiaSharp 변환 전체에 적용 된다는 사실을 `SKCanvas` 개인이 Xamarin.Forms 변환을 적용 하는 동안 개체 `VisualElement` 파생 합니다. (Xamarin.Forms 변환을 적용할 수 있습니다 합니다 `SKCanvasView` 개체 자체 `SKCanvasView` 에서 파생 되 `VisualElement`, 하지만 해당 `SKCanvasView`, SkiaSkarp 변환을 적용 합니다.)

왼쪽 위 모퉁이 기준으로 SkiaSharp 변환 되는 `SKCanvas` Xamarin.Forms 변환은의 왼쪽 위 모퉁이 기준으로 하는 동안는 `VisualElement` 적용 되는 합니다. 크기 조정을 적용할 때이 차이점은 중요 하 고 이러한 변환은 항상 특정 시점을 기준으로 하므로 회전 변환 합니다.

매우 큰 차이 SKiaSharp 변환 *메서드* Xamarin.Forms 변환 하는 동안 *속성*합니다. 이것이 구문 차이 외 의미 체계 차이: SkiaSharp 변환 Xamarin.Forms 변환 상태를 설정 하는 동안 작업을 수행 합니다. SkiaSharp 변환에 변환 적용 되기 전에 그려진 그래픽 개체 아니라 이후에 그려지는 그래픽 개체에 적용 됩니다. 반면, Xamarin.Forms 변환 속성을 설정 하는 즉시 이전에 렌더링 된 요소에 적용 됩니다. SkiaSharp 변환은 누적 메서드가 호출 됩니다. Xamarin.Forms 변환 속성을 다른 값으로 설정 된 경우 대체 됩니다.

머리글 아래에 나타나고이 단원의 샘플 프로그램을 모두 **변환** 의 홈 페이지에는 [ **SkiaSharpFormsDemos** ](https://developer.xamarin.com/samples/xamarin-forms/SkiaSharpForms/Demos/) 프로그램인 및는 [ **변형** ](https://github.com/xamarin/xamarin-forms-samples/tree/master/SkiaSharpForms/Demos/Demos/SkiaSharpFormsDemos/Transforms) 솔루션의 폴더입니다.

## <a name="the-translate-transformtranslatemd"></a>[좌표 이동 변환](translate.md)

SkiaSharp 그래픽 이동할 좌표 이동 변환을 사용 하는 방법에 알아봅니다.

## <a name="the-scale-transformscalemd"></a>[배율 변환](scale.md)

다양 한 크기는 개체 크기 조정에 대 한 SkiaSharp 배율 변환을 검색 합니다.

## <a name="the-rotate-transformrotatemd"></a>[회전 변환](rotate.md)

효과 및 애니메이션 SkiaSharp 회전 변환 가능한 살펴봅니다.

## <a name="the-skew-transformskewmd"></a>[기울이기 변환](skew.md)

기울이기 변환에서 SkiaSharp 기운된 그래픽 개체를 만들 수 있습니다 하는 방법을 참조 하세요.

## <a name="matrix-transformsmatrixmd"></a>[매트릭스 변환](matrix.md)

심층 탐구 다양 한 변환 매트릭스를 사용 하 여 SkiaSharp 변환 합니다.

## <a name="touch-manipulationstouchmd"></a>[터치 조작](touch.md)

구현 끌어, 크기 조정 및 회전에 대 한 터치 조작을 사용 하 여 행렬 변환 합니다.

## <a name="non-affine-transformsnon-affinemd"></a>[비아핀(Non-Affine) 변환](non-affine.md)

비 관계 변환 효과 사용 하 여 oridinary 넘어 이동 합니다.

## <a name="3d-rotation3d-rotationmd"></a>[3D 회전](3d-rotation.md)

비 관계 변환을 사용 하 여 3D 공간에서 2D 개체를 회전 합니다.


## <a name="related-links"></a>관련 링크

- [SkiaSharp Api](https://developer.xamarin.com/api/root/SkiaSharp/)
- [SkiaSharpFormsDemos (샘플)](https://developer.xamarin.com/samples/xamarin-forms/SkiaSharpForms/Demos/)
