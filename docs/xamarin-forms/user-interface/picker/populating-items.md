---
title: 선택기 항목 컬렉션에 데이터 추가
description: 선택기 뷰는 데이터의 목록에서 텍스트 항목을 선택 하는 컨트롤입니다. 이 문서에는 항목 컬렉션에 추가 하 여 데이터를 사용 하 여 선택기를 채우는 방법 및 사용자가 항목 선택에 응답 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: 3C840F64-A430-457D-A4B2-3D7AF46F9DBE
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/11/2017
ms.openlocfilehash: 8d911108d7d72586a37a3281803eab9c0841f16c
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38997112"
---
# <a name="adding-data-to-a-pickers-items-collection"></a>선택기 항목 컬렉션에 데이터 추가

_선택기 뷰는 데이터의 목록에서 텍스트 항목을 선택 하는 컨트롤입니다. 이 문서에는 항목 컬렉션에 추가 하 여 데이터를 사용 하 여 선택기를 채우는 방법 및 사용자가 항목 선택에 응답 하는 방법을 설명 합니다._

## <a name="populating-a-picker-with-data"></a>데이터를 사용 하 여 선택 채우기

전에 Xamarin.Forms 2.3.4 채우는 프로세스는 [ `Picker` ](xref:Xamarin.Forms.Picker) 데이터를 사용 하 여 읽기 전용으로 표시할 데이터를 추가 하려면 되었습니다 [ `Items` ](xref:Xamarin.Forms.Picker.Items) 컬렉션 형식인 `IList<string>`. 컬렉션의 각 항목 유형 이어야 `string`합니다. 초기화 하 여 XAML에서 항목을 추가할 수는 `Items` 속성의 목록 사용 하 여 `x:String` 항목:

```xaml
<Picker Title="Select a monkey">
  <Picker.Items>
    <x:String>Baboon</x:String>
    <x:String>Capuchin Monkey</x:String>
    <x:String>Blue Monkey</x:String>
    <x:String>Squirrel Monkey</x:String>
    <x:String>Golden Lion Tamarin</x:String>
    <x:String>Howler Monkey</x:String>
    <x:String>Japanese Macaque</x:String>
  </Picker.Items>
</Picker>
```

해당 하는 C# 코드는 다음과 같습니다.

```csharp
var picker = new Picker { Title = "Select a monkey" };
picker.Items.Add("Baboon");
picker.Items.Add("Capuchin Monkey");
picker.Items.Add("Blue Monkey");
picker.Items.Add("Squirrel Monkey");
picker.Items.Add("Golden Lion Tamarin");
picker.Items.Add("Howler Monkey");
picker.Items.Add("Japanese Macaque");
```

사용 하 여 데이터를 추가 하는 것 외에도 합니다 `Items.Add` 메서드를 데이터도 컬렉션에 사용 하 여 삽입할 수는 `Items.Insert` 메서드.

## <a name="responding-to-item-selection"></a>항목 선택에 응답

A [ `Picker` ](xref:Xamarin.Forms.Picker) 한 번에 하나씩 선택할 수 있습니다. 사용자가 항목을 선택 합니다 [ `SelectedIndexChanged` ](xref:Xamarin.Forms.Picker.SelectedIndexChanged) 이벤트 발생 및 [ `SelectedIndex` ](xref:Xamarin.Forms.Picker.SelectedIndex) 속성은 목록에서 선택한 항목의 인덱스를 나타내는 정수를 업데이트 합니다. `SelectedIndex` 속성은 사용자가 선택한 항목을 나타내는 0부터 시작 수 있습니다. 선택 된 항목이 있는 경우 때 합니다 `Picker` 먼저 생성 되 고 초기화 하 고, `SelectedIndex` -1이 됩니다.

> [!NOTE]
> 항목의 선택 동작을 [ `Picker` ](xref:Xamarin.Forms.Picker) 플랫폼 전용을 사용 하 여 iOS에서 사용자 지정할 수 있습니다. 자세한 내용은 [선택 항목 선택 제어](~/xamarin-forms/platform/platform-specifics/consuming/ios.md#picker_update_mode)입니다.

다음 코드 예제는 `OnPickerSelectedIndexChanged` 이벤트 처리기 메서드를 될 때 실행 되는 [ `SelectedIndexChanged` ](xref:Xamarin.Forms.Picker.SelectedIndexChanged) 이벤트 발생:

```csharp
void OnPickerSelectedIndexChanged(object sender, EventArgs e)
{
  var picker = (Picker)sender;
  int selectedIndex = picker.SelectedIndex;

  if (selectedIndex != -1)
  {
    monkeyNameLabel.Text = picker.Items[selectedIndex];
  }
}
```

이 메서드를 가져옵니다 합니다 [ `SelectedIndex` ](xref:Xamarin.Forms.Picker.SelectedIndex) 속성 값에서 선택한 항목을 검색할 값을 사용 하는 [ `Items` ](xref:Xamarin.Forms.Picker.Items) 컬렉션입니다. 각 항목 때문에 `Items` 컬렉션은는 `string`, 하 여 표시할 수 있습니다를 [ `Label` ](xref:Xamarin.Forms.Label) 캐스팅 하지 않고도 합니다.

> [!NOTE]
> A [ `Picker` ](xref:Xamarin.Forms.Picker) 설정 하 여 특정 항목을 표시 하도록 초기화 합니다 [ `SelectedIndex` ](xref:Xamarin.Forms.Picker.SelectedIndex) 속성입니다. 그러나 합니다 `SelectedIndex` 초기화 한 후 속성을 설정 해야 합니다 [ `Items` ](xref:Xamarin.Forms.Picker.Items) 컬렉션입니다.

## <a name="summary"></a>요약

합니다 [ `Picker` ](xref:Xamarin.Forms.Picker) 뷰는 데이터의 목록에서 텍스트 항목을 선택 하는 컨트롤입니다. 이 문서를 채우는 방법을 설명 된 `Picker` 추가 하 여 데이터를 사용 하 여는 [ `Items` ](xref:Xamarin.Forms.Picker.Items) 컬렉션 및 사용자가 항목 선택에 응답 하는 방법. 이 사용 하기 위한 프로세스는 `Picker` Xamarin.Forms 2.3.4 전에 합니다.


## <a name="related-links"></a>관련 링크

- [선택기 데모 (샘플)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/PickerDemo/)
- [선택기](xref:Xamarin.Forms.Picker)
