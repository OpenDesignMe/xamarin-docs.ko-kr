---
title: 지도의 경로 강조 표시
description: 이 문서에서는 맵에 다중선 오버레이 추가 하는 방법을 설명 합니다. 폴리라인 오버레이 일련의 일반적으로 지도에 경로 표시 하거나 필요한 모든 셰이프를 구성 하는 데 사용 되는 연결 된 선 세그먼트입니다.
ms.prod: xamarin
ms.assetid: FBFDC715-1654-4188-82A0-FC522548BCFF
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 11/29/2017
ms.openlocfilehash: 786f050495d4682b719178f2723c482929544678
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38998723"
---
# <a name="highlighting-a-route-on-a-map"></a>지도의 경로 강조 표시

_이 문서에서는 맵에 다중선 오버레이 추가 하는 방법을 설명 합니다. 폴리라인 오버레이 일련의 일반적으로 지도에 경로 표시 하거나 필요한 모든 셰이프를 구성 하는 데 사용 되는 연결 된 선 세그먼트입니다._

## <a name="overview"></a>개요

오버레이 지도에 계층화 된 그래픽입니다. 오버레이 확대/축소 하는 대로 지도 사용 하 여 크기가 조정 되는 그래픽 그리기 콘텐츠를 지원 합니다. 다음 스크린샷은 맵에 다중선 오버레이 추가 하는 결과 보여 줍니다.

![](polyline-map-overlay-images/screenshots.png)

경우는 [ `Map` ](xref:Xamarin.Forms.Maps.Map) iOS에서 Xamarin.Forms 응용 프로그램에서 컨트롤이 렌더링 되는 `MapRenderer` 클래스가 인스턴스화되면 네이티브를 다시 인스턴스화하는 `MKMapView` 제어 합니다. Android 플랫폼에는 `MapRenderer` 클래스에는 네이티브 인스턴스화합니다 `MapView` 컨트롤입니다. Windows 플랫폼 (UWP (유니버설)을 합니다 `MapRenderer` 클래스에는 네이티브 인스턴스화합니다 `MapControl`합니다. 렌더링 프로세스에 대 한 사용자 지정 렌더러를 만들어 플랫폼별 맵 사용자 지정을 구현 하 여 활용 취할 수 있습니다는 `Map` 각 플랫폼에서 합니다. 이 수행 하는 프로세스는 다음과 같습니다.

1. [만들](#Creating_the_Custom_Map) Xamarin.Forms 사용자 지정 지도입니다.
1. [사용할](#Consuming_the_Custom_Map) Xamarin.Forms에서 사용자 지정 맵.
1. [사용자 지정](#Customizing_the_Map) 각 플랫폼에서 맵에 대 한 사용자 지정 렌더러를 만들어 맵.

> [!NOTE]
> [`Xamarin.Forms.Maps`](xref:Xamarin.Forms.Maps) 초기화 하 고 사용 하기 전에 구성 해야 합니다. 자세한 내용은 [`Maps Control`](~/xamarin-forms/user-interface/map.md)를 참조하세요.

사용자 지정 렌더러를 사용 하 여 지도 사용자 지정 하는 방법에 대 한 내용은 [지도 핀 사용자 지정](~/xamarin-forms/app-fundamentals/custom-renderer/map/customized-pin.md)합니다.

<a name="Creating_the_Custom_Map" />

### <a name="creating-the-custom-map"></a>사용자 지정 맵 만들기

서브 클래스를 만든 합니다 [ `Map` ](xref:Xamarin.Forms.Maps.Map) 추가 하는 클래스는 `RouteCoordinates` 속성:

```csharp
public class CustomMap : Map
{
  public List<Position> RouteCoordinates { get; set; }

  public CustomMap ()
  {
    RouteCoordinates = new List<Position> ();
  }
}
```

`RouteCoordinates` 속성 경로를 강조 표시를 정의 하는 좌표 컬렉션을 저장 합니다.

<a name="Consuming_the_Custom_Map" />

### <a name="consuming-the-custom-map"></a>사용자 지정 맵 사용

사용 된 `CustomMap` XAML 페이지 인스턴스에서 해당 인스턴스를 선언 하 여 제어 합니다.

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:MapOverlay;assembly=MapOverlay"
             x:Class="MapOverlay.MapPage">
    <ContentPage.Content>
        <local:CustomMap x:Name="customMap" MapType="Street" WidthRequest="{x:Static local:App.ScreenWidth}" HeightRequest="{x:Static local:App.ScreenHeight}" />
    </ContentPage.Content>
</ContentPage>
```

또는 사용을 `CustomMap` C# 페이지 인스턴스에서 해당 인스턴스를 선언 하 여 제어 합니다.

```csharp
public class MapPageCS : ContentPage
{
    public MapPageCS ()
    {
        var customMap = new CustomMap {
            MapType = MapType.Street,
            WidthRequest = App.ScreenWidth,
            HeightRequest = App.ScreenHeight
        };
        ...
        Content = customMap;
    }
}
```

초기화는 `CustomMap` 필요에 따라 제어 합니다.

```csharp
public partial class MapPage : ContentPage
{
  public MapPage ()
  {
    ...
    customMap.RouteCoordinates.Add (new Position (37.785559, -122.396728));
    customMap.RouteCoordinates.Add (new Position (37.780624, -122.390541));
    customMap.RouteCoordinates.Add (new Position (37.777113, -122.394983));
    customMap.RouteCoordinates.Add (new Position (37.776831, -122.394627));

    customMap.MoveToRegion (MapSpan.FromCenterAndRadius (new Position (37.79752, -122.40183), Distance.FromMiles (1.0)));
  }
}
```

이 초기화는 일련의 강조 표시 하려면 지도에서 경로 정의 하려면 위도 및 경도 좌표를 지정 합니다. 사용 하 여 지도의 보기를 배치 합니다는 [ `MoveToRegion` ](xref:Xamarin.Forms.Maps.Map.MoveToRegion*) 메서드를 만들어 위치 및 지도 확대/축소 수준을 변경 하는 [ `MapSpan` ](xref:Xamarin.Forms.Maps.MapSpan) 에서 [ `Position` ](xref:Xamarin.Forms.Maps.Position) 와 [ `Distance` ](xref:Xamarin.Forms.Maps.Distance)합니다.

<a name="Customizing_the_Map" />

### <a name="customizing-the-map"></a>지도 사용자 지정

사용자 지정 렌더러는 이제 맵에 다중선 오버레이 추가 하려면 각 응용 프로그램 프로젝트에 추가 되어야 합니다.

#### <a name="creating-the-custom-renderer-on-ios"></a>IOS에서 사용자 지정 렌더러 만들기

서브 클래스를 만든 합니다 `MapRenderer` 클래스를 재정의 해당 `OnElementChanged` 다중선 오버레이 추가 하는 방법.

```csharp
[assembly: ExportRenderer(typeof(CustomMap), typeof(CustomMapRenderer))]
namespace MapOverlay.iOS
{
    public class CustomMapRenderer : MapRenderer
    {
        MKPolylineRenderer polylineRenderer;

        protected override void OnElementChanged(ElementChangedEventArgs<View> e)
        {
            base.OnElementChanged(e);

            if (e.OldElement != null) {
                var nativeMap = Control as MKMapView;
                if (nativeMap != null) {
                    nativeMap.RemoveOverlays(nativeMap.Overlays);
                    nativeMap.OverlayRenderer = null;
                    polylineRenderer = null;
                }
            }

            if (e.NewElement != null) {
                var formsMap = (CustomMap)e.NewElement;
                var nativeMap = Control as MKMapView;
                nativeMap.OverlayRenderer = GetOverlayRenderer;

                CLLocationCoordinate2D[] coords = new CLLocationCoordinate2D[formsMap.RouteCoordinates.Count];
                int index = 0;
                foreach (var position in formsMap.RouteCoordinates)
                {
                    coords[index] = new CLLocationCoordinate2D(position.Latitude, position.Longitude);
                    index++;
                }

                var routeOverlay = MKPolyline.FromCoordinates(coords);
                nativeMap.AddOverlay(routeOverlay);
            }
        }
        ...
    }
}

```

이 메서드는 사용자 지정 렌더러가 새 Xamarin.Forms 요소에 연결할 때 다음 구성에서 수행 합니다.

- `MKMapView.OverlayRenderer` 해당 대리자를 설정 합니다.
- 위도 및 경도 좌표 컬렉션에서 검색 되는 `CustomMap.RouteCoordinates` 속성의 배열로 저장 `CLLocationCoordinate2D` 인스턴스.
- 다중선 정적 호출 하 여 만든 `MKPolyline.FromCoordinates` 및 각 점의 위도 지정 하는 메서드.
- 다중선은 호출 하 여 지도에 추가 된 `MKMapView.AddOverlay` 메서드.

그런 다음 구현 된 `GetOverlayRenderer` 오버레이의 렌더링을 사용자 지정 하는 방법:

```csharp
public class CustomMapRenderer : MapRenderer
{
  MKPolylineRenderer polylineRenderer;
  ...

  MKOverlayRenderer GetOverlayRenderer(MKMapView mapView, IMKOverlay overlayWrapper)
  {
      if (polylineRenderer == null && !Equals(overlayWrapper, null)) {
          var overlay = Runtime.GetNSObject(overlayWrapper.Handle) as IMKOverlay;
          polylineRenderer = new MKPolylineRenderer(overlay as MKPolyline) {
              FillColor = UIColor.Blue,
              StrokeColor = UIColor.Red,
              LineWidth = 3,
              Alpha = 0.4f
          };
      }
      return polylineRenderer;
  }
}
```

#### <a name="creating-the-custom-renderer-on-android"></a>Android에서 사용자 지정 렌더러 만들기

서브 클래스를 만든 합니다 `MapRenderer` 클래스 재정의 및 해당 `OnElementChanged` 및 `OnMapReady` 다중선 오버레이 추가 하는 방법:

```csharp
[assembly: ExportRenderer(typeof(CustomMap), typeof(CustomMapRenderer))]
namespace MapOverlay.Droid
{
    public class CustomMapRenderer : MapRenderer
    {
        List<Position> routeCoordinates;

        public CustomMapRenderer(Context context) : base(context)
        {
        }

        protected override void OnElementChanged(Xamarin.Forms.Platform.Android.ElementChangedEventArgs<Map> e)
        {
            base.OnElementChanged(e);

            if (e.OldElement != null)
            {
                // Unsubscribe
            }

            if (e.NewElement != null)
            {
                var formsMap = (CustomMap)e.NewElement;
                routeCoordinates = formsMap.RouteCoordinates;
                Control.GetMapAsync(this);
            }
        }

        protected override void OnMapReady(Android.Gms.Maps.GoogleMap map)
        {
            base.OnMapReady(map);

            var polylineOptions = new PolylineOptions();
            polylineOptions.InvokeColor(0x66FF0000);

            foreach (var position in routeCoordinates)
            {
                polylineOptions.Add(new LatLng(position.Latitude, position.Longitude));
            }

            NativeMap.AddPolyline(polylineOptions);
        }
    }
}
```

합니다 `OnElementChanged` 위도 및 경도 좌표에서의 컬렉션을 검색 하는 메서드는 `CustomMap.RouteCoordinates` 속성 멤버 변수에 저장 합니다. 그런 다음 호출 하는 `MapView.GetMapAsync` 메서드를 기본 `GoogleMap` 사용자 지정 렌더러가 새 Xamarin.Forms 요소에 연결할 때 제공한 보기로 연결 됩니다. 한 번 합니다 `GoogleMap` 인스턴스 수를 `OnMapReady` 메서드를 호출할를 인스턴스화하여 다중선 만들어지는 `PolylineOptions` 및 각 점의 위도 지정 하는 개체. 호출 하 여 맵에 다중선은 다음 추가 `NativeMap.AddPolyline` 메서드.

#### <a name="creating-the-custom-renderer-on-the-universal-windows-platform"></a>유니버설 Windows 플랫폼에서 사용자 지정 렌더러 만들기

서브 클래스를 만든 합니다 `MapRenderer` 클래스를 재정의 해당 `OnElementChanged` 다중선 오버레이 추가 하는 방법.

```csharp
[assembly: ExportRenderer(typeof(CustomMap), typeof(CustomMapRenderer))]
namespace MapOverlay.UWP
{
    public class CustomMapRenderer : MapRenderer
    {
        protected override void OnElementChanged(ElementChangedEventArgs<Map> e)
        {
            base.OnElementChanged(e);

            if (e.OldElement != null)
            {
                // Unsubscribe
            }

            if (e.NewElement != null)
            {
                var formsMap = (CustomMap)e.NewElement;
                var nativeMap = Control as MapControl;

                var coordinates = new List<BasicGeoposition>();
                foreach (var position in formsMap.RouteCoordinates)
                {
                    coordinates.Add(new BasicGeoposition() { Latitude = position.Latitude, Longitude = position.Longitude });
                }

                var polyline = new MapPolyline();
                polyline.StrokeColor = Windows.UI.Color.FromArgb(128, 255, 0, 0);
                polyline.StrokeThickness = 5;
                polyline.Path = new Geopath(coordinates);
                nativeMap.MapElements.Add(polyline);
            }
        }
    }
}
```

이 메서드는 사용자 지정 렌더러가 새 Xamarin.Forms 요소에 연결할 때 다음과 같은 작업을 수행 합니다.

- 위도 및 경도 좌표 컬렉션에서 검색 되는 `CustomMap.RouteCoordinates` 속성 및 변환할를 `List` 의 `BasicGeoposition` 좌표입니다.
- 다중선 인스턴스화하여 생성 되는 `MapPolyline` 개체입니다. 합니다 `MapPolygon` 클래스로 설정 하 여 지도에 선을 표시 하려면 해당 `Path` 속성을를 `Geopath` 줄 좌표가 포함 된 개체입니다.
- 다중선 추가 하 여 지도에 렌더링 되는 `MapControl.MapElements` 컬렉션입니다.

## <a name="summary"></a>요약

이 문서에는 폴리라인 오버레이 지도에 경로 표시 하거나 필요한 모든 셰이프를 구성 하는 지도를 추가 하는 방법을 설명 합니다.


## <a name="related-links"></a>관련 링크

- [다중선 맵 Ovlerlay (샘플)](https://developer.xamarin.com/samples/xamarin-forms/customrenderers/map/polyline/)
- [지도 핀 사용자 지정](~/xamarin-forms/app-fundamentals/custom-renderer/map/customized-pin.md)
- [Xamarin.Forms.Maps](xref:Xamarin.Forms.Maps)
