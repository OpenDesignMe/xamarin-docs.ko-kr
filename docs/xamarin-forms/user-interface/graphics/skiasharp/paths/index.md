---
title: SkiaSharp 선 및 경로
description: 이 문서에서는 Xamarin.Forms 응용 프로그램에서 줄 및 그래픽 경로 그릴 SkiaSharp 사용 방법에 설명 하 고 샘플 코드를 사용 하 여이 보여 줍니다.
ms.prod: xamarin
ms.assetid: 316A15FE-383D-4D06-8641-BAC7EE7474CA
ms.technology: xamarin-skiasharp
author: charlespetzold
ms.author: chape
ms.date: 03/10/2017
ms.openlocfilehash: 9febfabb7b44b1ec09abda4b352691b37565cb48
ms.sourcegitcommit: 12d48cdf99f0d916536d562e137d0e840d818fa1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2018
ms.locfileid: "39615137"
---
# <a name="skiasharp-lines-and-paths"></a>SkiaSharp 선 및 경로

_SkiaSharp 선 및 그래픽 경로 그릴 사용_

합니다 [이전 섹션](~/xamarin-forms/user-interface/graphics/skiasharp/basics/index.md) 설명 하는 SkiaSharp `SKCanvas` 클래스 사각형, 타원, 그릴 모서리가 둥근된 사각형을 그릴 수 있는 여러 메서드가 포함 됩니다. 이 섹션 및 이후 섹션 만들기 및 렌더링을 사용 하 여 연결 된 다양 한 클래스 처리 *그래픽 경로*합니다.

그래픽 경로 줄 고 SkiaSharp 곡선 그리기는 가장 일반적인된 방법입니다. 이 섹션에서는 사용 하 여는 `SKPath` 직선 그리기 작은 직선의 컬렉션을 사용 하는 개체 (호출을 *다중선*) 수학적으로 정의할 수 있는 곡선을 그리는 합니다. 이후 섹션에서 지원 되는 곡선의 다양 한 종류에 설명 합니다 `SKPath`합니다.

머리글 아래에 나타나고이 단원의 샘플 프로그램을 모두 **선 및 경로** 의 홈 페이지에는 [ **SkiaSharpFormsDemos** ](https://developer.xamarin.com/samples/xamarin-forms/SkiaSharpForms/Demos/) 프로그램인 및는 [ **경로** ](https://github.com/xamarin/xamarin-forms-samples/tree/master/SkiaSharpForms/Demos/Demos/SkiaSharpFormsDemos/Paths) 솔루션의 폴더입니다.

## <a name="lines-and-stroke-capslinesmd"></a>[선 및 스트로크 단면](lines.md)

SkiaSharp 다른 스트로크 단면을 사용 하 여 선을 그리는 데 사용 하는 방법에 알아봅니다.

## <a name="path-basicspathsmd"></a>[경로 기본 사항](paths.md)

선 및 곡선을 결합 하는 데 SkiaSharp SKPath 개체를 탐색 합니다.

## <a name="the-path-fill-typesfill-typesmd"></a>[경로 채우기 유형](fill-types.md)

SkiaSharp 경로 채우기 유형으로 가능한 다른 결과 검색 합니다.

## <a name="polylines-and-parametric-equationspolylinesmd"></a>[폴리라인 및 파라메트릭 수식](polylines.md)

SkiaSharp 사용 하 여 렌더링 줄 매개 방정식을 사용 하 여 정의할 수 있습니다.

## <a name="dots-and-dashesdotsmd"></a>[점 및 대시](dots.md)

SkiaSharp에서 점선과 파선 선 그리기의 복잡성을 마스터입니다.

## <a name="finger-paintingfinger-paintmd"></a>[손가락으로 그리기](finger-paint.md)

캔버스에 그릴 손가락을 사용 합니다.


## <a name="related-links"></a>관련 링크

- [SkiaSharp Api](https://developer.xamarin.com/api/root/SkiaSharp/)
- [SkiaSharpFormsDemos (샘플)](https://developer.xamarin.com/samples/xamarin-forms/SkiaSharpForms/Demos/)
