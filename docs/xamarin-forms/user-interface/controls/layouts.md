---
title: Xamarin.Forms 레이아웃
description: Xamarin.Forms 레이아웃은 visual 구조로 사용자 인터페이스 컨트롤을 작성 하는 데 사용 됩니다. 이 문서에서는 Xamarin.Forms에 포함 된 레이아웃을 나열 합니다.
ms.prod: xamarin
ms.assetid: F4180997-BA21-453A-9958-D1E2940DF050
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/21/2018
ms.openlocfilehash: 224eb2ee3958e5979382a3dc5e70110fdce51879
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38994604"
---
# <a name="xamarinforms-layouts"></a>Xamarin.Forms 레이아웃

_Xamarin.Forms 레이아웃은 visual 구조로 사용자 인터페이스 컨트롤을 작성 하는 데 사용 됩니다._

합니다 [ `Layout` ](xref:Xamarin.Forms.Layout) 하 고 [ `Layout<T>` ](xref:Xamarin.Forms.Layout`1) Xamarin.Forms의 클래스는 특수 한 하위 뷰 및 기타 레이아웃 컨테이너 역할을 하는 뷰의 합니다. 합니다 `Layout` 자체 클래스에서 파생 되며 [ `View` ](views.md)합니다. `Layout` 파생 클래스에는 일반적으로 Xamarin.Forms 응용 프로그램에서 자식 요소의 크기와 위치를 설정 하기 위한 논리가 포함 됩니다.

[![Xamarin.Forms 레이아웃 형식](layouts-images/layouts-sml.png "Xamarin.Forms 레이아웃 형식을")](layouts-images/layouts.png#lightbox "Xamarin.Forms 레이아웃 형식")

파생 된 클래스는 `Layout` 두 가지 범주로 나눌 수 있습니다.

## <a name="layouts-with-single-content"></a>단일 콘텐츠와 레이아웃

이러한 클래스에서 파생 [ `Layout` ](xref:Xamarin.Forms.Layout)를 정의 하는 [ `Padding` ](xref:Xamarin.Forms.Layout.Padding) 고 [ `IsClippedToBounds` ](xref:Xamarin.Forms.Layout.IsClippedToBounds) 속성입니다.

<a name="contentView" />

### <a name="contentview"></a>ContentView

|     |     |
| --- | --- |
| [`ContentView`](xref:Xamarin.Forms.ContentView) 으로 설정 된 단일 자식이 포함 되어는 [ `Content` ](xref:Xamarin.Forms.ContentView.Content) 속성입니다. 합니다 `Content` 속성에 설정할 수 있습니다 `View` 파생 개체를 비롯 한 다른 `Layout` 파생 합니다. `ContentView` 구조적 요소와 주로 사용 되 고를 기본 클래스로 사용 됩니다 [ `Frame` ](#frame)합니다.<br /><br />[API 설명서](xref:Xamarin.Forms.ContentView) | [![ContentView 예제](layouts-images/ContentView.png "ContentView 예제")](layouts-images/ContentView-Large.png#lightbox "ContentView 예제")<br />[이 페이지에 대 한 C# 코드](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/ContentViewDemoPage.cs) / [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/ContentViewDemoPage.xaml) |
|     |     |

<a named="frame" />

### <a name="frame"></a>프레임

|     |     |
| --- | --- |
| 합니다 [ `Frame` ](xref:Xamarin.Forms.Frame) 클래스에서 파생 됩니다 [ `ContentView` ](#contentView) 자식 주위에 사각형 프레임을 표시 합니다. `Frame` 기본값이 [ `Padding` ](xref:Xamarin.Forms.Layout.Padding) 20의 값도 정의 [ `OutlineColor` ](xref:Xamarin.Forms.Frame.OutlineColor)를 [ `CornerRadius` ](xref:Xamarin.Forms.Frame.CornerRadius), 및 [ `HasShadow` ](xref:Xamarin.Forms.Frame.HasShadow)속성입니다.<br /><br />[API 설명서](xref:Xamarin.Forms.Frame) | [![예제에서는 프레임](layouts-images/Frame.png "예제에서는 프레임")](layouts-images/Frame-Large.png#lightbox "예제 프레임")<br />[이 페이지에 대 한 C# 코드](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/FrameDemoPage.cs) / [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/FrameDemoPage.xaml) |
|     |     |

<a name="scrollView" />

### <a name="scrollview"></a>ScrollView

|     |     |
| --- | --- |
| [`ScrollView`](xref:Xamarin.Forms.ScrollView) 해당 콘텐츠를 스크롤할 수 있습니다. 설정 된 [ `Content` ](xref:Xamarin.Forms.ScrollView.Content) 속성 보기 또는 레이아웃 너무 커서 화면에 맞지 않습니다. (의 콘텐츠를 `ScrollView` 경우가 매우를 [ `StackLayout` ](#stackLayout).) 설정 합니다 [ `Orientation` ](xref:Xamarin.Forms.ScrollView.Orientation) 속성 해야 함을 나타내려면 경우 스크롤 세로, 가로 또는 둘 다.<br /><br />[API 설명서](xref:Xamarin.Forms.ScrollView) / [가이드](~/xamarin-forms/user-interface/layouts/scroll-view.md) / [샘플](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![ScrollView 예제](layouts-images/ScrollView.png "ScrollView 예제")](layouts-images/ScrollView-Large.png#lightbox "ScrollView 예제")<br />[이 페이지에 대 한 C# 코드](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/ScrollViewDemoPage.cs) / [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/ScrollViewDemoPage.xaml) |
|     |     |

### <a name="templatedview"></a>TemplatedView

|     |     |
| --- | --- |
| [`TemplatedView`](xref:Xamarin.Forms.TemplatedView) 컨트롤 템플릿 사용 하 여 콘텐츠를 표시 하 고에 대 한 기본 클래스인 [ `ContentView` ](#contentView)합니다.<br /><br />[API 설명서](xref:Xamarin.Forms.TemplatedView) / [가이드](~/xamarin-forms/app-fundamentals/templates/control-templates/index.md) | [![TemplatedView 예제](layouts-images/TemplatedView.png "TemplatedView 예제")](layouts-images/TemplatedView.png#lightbox "TemplatedView 예제") |
|     |     |

### <a name="contentpresenter"></a>ContentPresenter

|     |     |
| --- | --- |
| [`ContentPresenter`](xref:Xamarin.Forms.ContentPresenter) 내에서 사용 되는 템플릿 기반 보기, 레이아웃 관리자를 [ `ControlTemplate` ](xref:Xamarin.Forms.ControlTemplate) 를 표시 해야 하는 내용을 표시할 위치를 표시 합니다.<br /><br />[API 설명서](xref:Xamarin.Forms.ContentPresenter) / [가이드](~/xamarin-forms/app-fundamentals/templates/control-templates/index.md) | [![ContentPresenter 예제](layouts-images/ContentPresenter.png "ContentPresenter 예제")](layouts-images/ContentPresenter.png#lightbox "ContentPresenter 예제") |
|     |     |

## <a name="layouts-with-multiple-children"></a>여러 자식 요소를 사용 하 여 레이아웃

이러한 클래스에서 파생 [ `Layout<View>` ](xref:Xamarin.Forms.Layout`1)합니다.

<a name="stackLayout" />

### <a name="stacklayout"></a>StackLayout

|     |     |
| --- | --- |
| [`StackLayout`](xref:Xamarin.Forms.StackLayout) 가로 또는 세로로에 따라 스택에 자식 요소를 배치 합니다 [ `Orientation` ](xref:Xamarin.Forms.StackLayout.Orientation) 속성입니다. 합니다 [ `Spacing` ](xref:Xamarin.Forms.StackLayout.Spacing) 속성 자식 사이의 간격을 제어 되며 기본값은 6입니다.<br /><br />[API 설명서](xref:Xamarin.Forms.StackLayout) / [가이드](~/xamarin-forms/user-interface/layouts/stack-layout.md) / [샘플](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/)| [![예제 StackLayout](layouts-images/StackLayout.png "StackLayout 예제")](layouts-images/StackLayout-Large.png#lightbox "StackLayout 예제")<br />[이 페이지에 대 한 C# 코드](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/StackLayoutDemoPage.cs) / [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/StackLayoutDemoPage.xaml) |
|     |     |

<a name="grid" />

### <a name="grid"></a>표

|     |     |
| --- | --- |
| [`Grid`](xref:Xamarin.Forms.Grid) 행 및 열 표에 해당 자식 요소를 배치합니다. 자식의 위치를 사용 하 여 표시 됩니다는 [연결 된 속성](~/xamarin-forms/xaml/attached-properties.md) [ `Row` ](xref:Xamarin.Forms.Grid.RowProperty)를 [ `Column` ](xref:Xamarin.Forms.Grid.ColumnProperty)를 [ `RowSpan` ](xref:Xamarin.Forms.Grid.RowSpanProperty), 및 [ `ColumnSpan` ](xref:Xamarin.Forms.Grid.ColumnSpanProperty)합니다.<br /><br />[API 설명서](xref:Xamarin.Forms.Grid) / [가이드](~/xamarin-forms/user-interface/layouts/grid.md) / [샘플](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![그리드 예제](layouts-images/Grid.png "그리드 예제")](layouts-images/Grid-Large.png#lightbox "Grid 예제")<br />[이 페이지에 대 한 C# 코드](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/GridDemoPage.cs) / [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/GridDemoPage.xaml) |
|     |     |

### <a name="absolutelayout"></a>AbsoluteLayout

|     |     |
| --- | --- |
| [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) 자식 요소를 부모를 기준으로 특정 위치에 배치 됩니다. 자식의 위치를 사용 하 여 표시 됩니다는 [연결 된 속성](~/xamarin-forms/xaml/attached-properties.md) [ `LayoutBounds` ](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) 하 고 [ `LayoutFlags` ](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty)합니다. `AbsoluteLayout` 뷰의 위치에 애니메이션을 적용 하는 데 유용 합니다.<br /><br />[API 설명서](xref:Xamarin.Forms.AbsoluteLayout) / [가이드](~/xamarin-forms/user-interface/layouts/absolute-layout.md) / [샘플](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![AbsoluteLayout 예제](layouts-images/AbsoluteLayout.png "AbsoluteLayout 예제")](layouts-images/AbsoluteLayout-Large.png#lightbox "AbsoluteLayout 예제")<br />[이 페이지에 대 한 C# 코드](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/AbsoluteLayoutdDemoPage.cs) / [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/AbsoluteLayoutDemoPage.xaml) 사용 하 여 [코드 숨김](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/AbsoluteLayoutDemoPage.xaml.cs) |
|     |     |

### <a name="relativelayout"></a>RelativeLayout

|     |     |
| --- | --- |
| [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 에 상대적인 자식 요소를 배치 합니다 `RelativeLayout` 자체 또는 해당 형제입니다. 자식의 위치를 사용 하 여 표시 됩니다는 [연결 된 속성](~/xamarin-forms/xaml/attached-properties.md) 형식의 개체에 설정 된 [ `Constraint` ](xref:Xamarin.Forms.Constraint) 하 고 [ `BoundsConstraint` ](xref:Xamarin.Forms.Constraint)합니다.<br /><br />[API 설명서](xref:Xamarin.Forms.RelativeLayout) / [가이드](~/xamarin-forms/user-interface/layouts/relative-layout.md) / [샘플](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![RelativeLayout 예제](layouts-images/RelativeLayout.png "RelativeLayout 예제")](layouts-images/RelativeLayout-Large.png#lightbox "RelativeLayout 예제")<br />[이 페이지에 대 한 C# 코드](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/RelativeLayoutDemoPage.cs) / [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/RelativeLayoutDemoPage.xaml) |
|     |     |

### <a name="flexlayout"></a>FlexLayout

|     |     |
| --- | --- |
| [`FlexLayout`](xref:Xamarin.Forms.FlexLayout) CSS를 기반으로 [유연한 상자 레이아웃 모듈](http://www.w3.org/TR/css-flexbox-1/)일반적으로 알려진 _레이아웃 flex_ 또는 _flex 박스_합니다. `FlexLayout` 여섯 개의 바인딩 가능한 속성 및 누적 하거나 많은 맞춤 및 방향 옵션을 사용 하 여 래핑된 자식을 사용할 수 있는 5 개의 연결 된 바인딩 가능 속성을 정의 합니다.<br /><br />[API 설명서](xref:Xamarin.Forms.FlexLayout) / [가이드](~/xamarin-forms/user-interface/layouts/flex-layout.md) / [샘플](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/FlexLayoutDemos/) | [![FlexLayout 예제](layouts-images/FlexLayout.png "FlexLayout 예제")](layouts-images/FlexLayout-Large.png#lightbox "FlexLayout 예제")<br />[이 페이지에 대 한 C# 코드](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/FlexLayoutDemoPage.cs) / [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/FlexLayoutDemoPage.xaml) |
|     |     |

## <a name="related-links"></a>관련 링크

- [Xamarin.Forms 소개](~/xamarin-forms/get-started/introduction-to-xamarin-forms.md)
- [Xamarin.Forms FormsGallery 샘플](https://developer.xamarin.com/samples/FormsGallery/)
- [Xamarin.Forms 샘플](https://developer.xamarin.com/samples/xamarin-forms/all/)
- [Xamarin.Forms API 설명서](https://docs.microsoft.com/dotnet/api/xamarin.forms?view=xamarin-forms)
