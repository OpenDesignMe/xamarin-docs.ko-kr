---
title: 선택기의 ItemsSource 속성 설정
description: 선택기 뷰는 데이터의 목록에서 텍스트 항목을 선택 하는 컨트롤입니다. 이 문서는 ItemsSource 속성을 설정 하 여 데이터를 사용 하 여 선택기를 채우는 방법 및 사용자가 항목 선택에 응답 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: 8ECF390C-9DB2-4441-B9A3-101AE7E5AEC5
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/11/2017
ms.openlocfilehash: 3f82e4b7d52988bfef9736ace8c476a9cd2da02b
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38994746"
---
# <a name="setting-a-pickers-itemssource-property"></a>선택기의 ItemsSource 속성 설정

_선택기 뷰는 데이터의 목록에서 텍스트 항목을 선택 하는 컨트롤입니다. 이 문서는 ItemsSource 속성을 설정 하 여 데이터를 사용 하 여 선택기를 채우는 방법 및 사용자가 항목 선택에 응답 하는 방법을 설명 합니다._

Xamarin.Forms 2.3.4 향상 되었습니다 합니다 [ `Picker` ](xref:Xamarin.Forms.Picker) 뷰를 설정 하 여 데이터를 입력 하는 기능을 추가 하 여 해당 [ `ItemsSource` ](xref:Xamarin.Forms.Picker.ItemsSource) 속성 합니다 에서선택한항목을검색하고[ `SelectedItem` ](xref:Xamarin.Forms.Picker.SelectedItem) 속성입니다. 선택한 항목에 대 한 텍스트의 색을 설정 하 여 변경할 수 있습니다 또한 합니다 [ `TextColor` ](xref:Xamarin.Forms.Picker.TextColor) 속성을를 [ `Color` ](xref:Xamarin.Forms.Color)합니다.

## <a name="populating-a-picker-with-data"></a>데이터를 사용 하 여 선택 채우기

A [ `Picker` ](xref:Xamarin.Forms.Picker) 설정 하 여 데이터로 채울 수 있습니다 해당 [ `ItemsSource` ](xref:Xamarin.Forms.Picker.ItemsSource) 속성을는 `IList` 컬렉션입니다. 컬렉션의 각 항목의 수 또는 형식에서 파생 해야 `object`합니다. 초기화 하 여 XAML에서 항목을 추가할 수는 `ItemsSource` 속성 항목의 배열:

```xaml
<Picker x:Name="picker" Title="Select a monkey">
  <Picker.ItemsSource>
    <x:Array Type="{x:Type x:String}">
      <x:String>Baboon</x:String>
      <x:String>Capuchin Monkey</x:String>
      <x:String>Blue Monkey</x:String>
      <x:String>Squirrel Monkey</x:String>
      <x:String>Golden Lion Tamarin</x:String>
      <x:String>Howler Monkey</x:String>
      <x:String>Japanese Macaque</x:String>
    </x:Array>
  </Picker.ItemsSource>
</Picker>
```

> [!NOTE]
> 합니다 `x:Array` 요소에는 `Type` 배열에 있는 항목의 유형을 나타내는 특성입니다.

해당 하는 C# 코드는 다음과 같습니다.

```csharp
var monkeyList = new List<string>();
monkeyList.Add("Baboon");
monkeyList.Add("Capuchin Monkey");
monkeyList.Add("Blue Monkey");
monkeyList.Add("Squirrel Monkey");
monkeyList.Add("Golden Lion Tamarin");
monkeyList.Add("Howler Monkey");
monkeyList.Add("Japanese Macaque");

var picker = new Picker { Title = "Select a monkey" };
picker.ItemsSource = monkeyList;
```

## <a name="responding-to-item-selection"></a>항목 선택에 응답

A [ `Picker` ](xref:Xamarin.Forms.Picker) 한 번에 하나씩 선택할 수 있습니다. 사용자가 항목을 선택 합니다 [ `SelectedIndexChanged` ](xref:Xamarin.Forms.Picker.SelectedIndexChanged) 이벤트가 발생 합니다 [ `SelectedIndex` ](xref:Xamarin.Forms.Picker.SelectedIndex) 속성은 목록에서 선택한 항목의 인덱스를 나타내는 정수를 업데이트 및 [ `SelectedItem` ](xref:Xamarin.Forms.Picker.SelectedItem) 속성은 업데이트 된 `object` 은 선택한 항목을 나타내는입니다. 합니다 [ `SelectedIndex` ](xref:Xamarin.Forms.Picker.SelectedIndex) 속성은 사용자가 선택한 항목을 나타내는 0부터 시작 수 있습니다. 선택 된 항목이 있는 경우 때 합니다 [ `Picker` ](xref:Xamarin.Forms.Picker) 먼저 생성 되 고 초기화 하 고, `SelectedIndex` -1이 됩니다.

> [!NOTE]
> 항목의 선택 동작을 [ `Picker` ](xref:Xamarin.Forms.Picker) 플랫폼 전용을 사용 하 여 iOS에서 사용자 지정할 수 있습니다. 자세한 내용은 [선택 항목 선택 제어](~/xamarin-forms/platform/platform-specifics/consuming/ios.md#picker_update_mode)입니다.

다음 코드 예제에서는 검색 하는 방법을 보여 줍니다.는 [ `SelectedItem` ](xref:Xamarin.Forms.Picker.SelectedItem) 에서 속성 값을 [ `Picker` ](xref:Xamarin.Forms.Picker) XAML에서:

```xaml
<Label Text="{Binding Source={x:Reference picker}, Path=SelectedItem}" />
```

해당 하는 C# 코드는 다음과 같습니다.

```csharp
var monkeyNameLabel = new Label();
monkeyNameLabel.SetBinding(Label.TextProperty, new Binding("SelectedItem", source: picker));
```

이벤트 처리기 수 또한 될 때 실행 되는 [ `SelectedIndexChanged` ](xref:Xamarin.Forms.Picker.SelectedIndexChanged) 이벤트가 발생 합니다.

```csharp
void OnPickerSelectedIndexChanged(object sender, EventArgs e)
{
  var picker = (Picker)sender;
  int selectedIndex = picker.SelectedIndex;

  if (selectedIndex != -1)
  {
    monkeyNameLabel.Text = (string)picker.ItemsSource[selectedIndex];
  }
}
```

이 메서드를 가져옵니다 합니다 [ `SelectedIndex` ](xref:Xamarin.Forms.Picker.SelectedIndex) 속성 값에서 선택한 항목을 검색할 값을 사용 하는 [ `ItemsSource` ](xref:Xamarin.Forms.Picker.ItemsSource) 컬렉션입니다. 이 기능적으로 선택한 항목을 검색 하는 [ `SelectedItem` ](xref:Xamarin.Forms.Picker.SelectedItem) 속성입니다. 각 항목에는 `ItemsSource` 유형의 컬렉션 이므로 `object`, 이므로 캐스팅 되어야 합니다는 `string` 표시에 대 한 합니다.

> [!NOTE]
> A [ `Picker` ](xref:Xamarin.Forms.Picker) 설정 하 여 특정 항목을 표시 하도록 초기화 합니다 [ `SelectedIndex` ](xref:Xamarin.Forms.Picker.SelectedIndex) 또는 [ `SelectedItem` ](xref:Xamarin.Forms.Picker.SelectedItem) 속성입니다. 그러나 초기화 한 후 이러한 속성 설정 해야 합니다 [ `ItemsSource` ](xref:Xamarin.Forms.Picker.ItemsSource) 컬렉션입니다.

## <a name="populating-a-picker-with-data-using-data-binding"></a>데이터 바인딩을 사용 하 여 데이터를 사용 하 여 선택 채우기

A [ `Picker` ](xref:Xamarin.Forms.Picker) 채울 수 있습니다도 데이터 바인딩할 데이터 바인딩을 사용 하 여 해당 [ `ItemsSource` ](xref:Xamarin.Forms.Picker.ItemsSource) 속성을는 `IList` 컬렉션입니다. XAML에서이 통해 합니다 [ `Binding` ](xref:Xamarin.Forms.Xaml.BindingExtension) 태그 확장:

```xaml
<Picker Title="Select a monkey" ItemsSource="{Binding Monkeys}" ItemDisplayBinding="{Binding Name}" />
```

해당 하는 C# 코드는 다음과 같습니다.

```csharp
var picker = new Picker { Title = "Select a monkey" };
picker.SetBinding(Picker.ItemsSourceProperty, "Monkeys");
picker.ItemDisplayBinding = new Binding("Name");
```

[ `ItemsSource` ](xref:Xamarin.Forms.Picker.ItemsSource) 속성 데이터를 바인딩하는 `Monkeys` 반환 하는 연결 된 뷰 모델의 속성을 `IList<Monkey>` 컬렉션. 다음 코드 예제는 `Monkey` 네 가지 속성을 포함 하는 클래스:

```csharp
public class Monkey
{
  public string Name { get; set; }
  public string Location { get; set; }
  public string Details { get; set; }
  public string ImageUrl { get; set; }
}
```

개체의 목록에 바인딩할 때 합니다 [ `Picker` ](xref:Xamarin.Forms.Picker) 각 개체에서 표시할 속성을 알 수 있어야 합니다. 설정 하 여 이렇게 합니다 [ `ItemDisplayBinding` ](xref:Xamarin.Forms.Picker.ItemDisplayBinding) 필요한 속성에 각 개체의 속성입니다. 위의 코드 예제에는 `Picker` 각 표시 하도록 설정 된 `Monkey.Name` 속성 값입니다.

### <a name="responding-to-item-selection"></a>항목 선택에 응답

데이터 바인딩 개체를 설정 하려면 사용할 수는 [ `SelectedItem` ](xref:Xamarin.Forms.Picker.SelectedItem) 속성 값 변경 시:

```xaml
<Picker Title="Select a monkey"
        ItemsSource="{Binding Monkeys}"
        ItemDisplayBinding="{Binding Name}"
        SelectedItem="{Binding SelectedMonkey}" />
<Label Text="{Binding SelectedMonkey.Name}" ... />
<Label Text="{Binding SelectedMonkey.Location}" ... />
<Image Source="{Binding SelectedMonkey.ImageUrl}" ... />
<Label Text="{Binding SelectedMonkey.Details}" ... />
```

해당 하는 C# 코드는 다음과 같습니다.

```csharp
var picker = new Picker { Title = "Select a monkey" };
picker.SetBinding(Picker.ItemsSourceProperty, "Monkeys");
picker.SetBinding(Picker.SelectedItemProperty, "SelectedMonkey");
picker.ItemDisplayBinding = new Binding("Name");

var nameLabel = new Label { ... };
nameLabel.SetBinding(Label.TextProperty, "SelectedMonkey.Name");

var locationLabel = new Label { ... };
locationLabel.SetBinding(Label.TextProperty, "SelectedMonkey.Location");

var image = new Image { ... };
image.SetBinding(Image.SourceProperty, "SelectedMonkey.ImageUrl");

var detailsLabel = new Label();
detailsLabel.SetBinding(Label.TextProperty, "SelectedMonkey.Details");
```

합니다 [ `SelectedItem` ](xref:Xamarin.Forms.Picker.SelectedItem) 속성 데이터를 바인딩하는 `SelectedMonkey` 형식인 연결 된 뷰 모델의 속성 `Monkey`합니다. 사용자 항목에서를 선택 하는 경우에 따라서 합니다 [ `Picker` ](xref:Xamarin.Forms.Picker)의 `SelectedMonkey` 속성이 설정 됩니다 하 여 선택한 `Monkey` 개체입니다. 합니다 `SelectedMonkey` 개체 데이터에서 사용자 인터페이스에 표시 됩니다 [ `Label` ](xref:Xamarin.Forms.Label) 하 고 [ `Image` ](xref:Xamarin.Forms.Image) 뷰:

![](populating-itemssource-images/monkeys.png "선택 항목 선택")

> [!NOTE]
> [ `SelectedItem` ](xref:Xamarin.Forms.Picker.SelectedItem) 하 고 [ `SelectedIndex` ](xref:Xamarin.Forms.Picker.SelectedIndex) 속성 둘 다 기본적으로 양방향 바인딩을 지원 합니다.

## <a name="summary"></a>요약

합니다 [ `Picker` ](xref:Xamarin.Forms.Picker) 뷰는 데이터의 목록에서 텍스트 항목을 선택 하는 컨트롤입니다. 이 문서를 채우는 방법을 설명 된 `Picker` 설정 하 여 데이터를 사용 하 여는 [ `ItemsSource` ](xref:Xamarin.Forms.Picker.ItemsSource) 속성 및 사용자가 항목 선택에 응답 하는 방법. Xamarin.Forms 2.3.4에에서 도입 된,이 접근 방식 상호 작용 하기 위한 권장 방법이 `Picker`합니다.


## <a name="related-links"></a>관련 링크

- [선택기 데모 (샘플)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/PickerDemo/)
- [Monkey 앱 (샘플)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/MonkeyAppPicker/)
- [바인딩할 수 있는 선택 (샘플)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/BindablePicker/)
- [선택기](xref:Xamarin.Forms.Picker)
