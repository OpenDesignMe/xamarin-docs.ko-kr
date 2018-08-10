---
title: Xamarin.Forms 데이터 템플릿 소개
description: Xamarin.Forms 데이터 템플릿은 지원 되는 컨트롤에 데이터를 정의 하는 기능을 제공 합니다. 이 문서에서는 데이터 템플릿이 필요한 이유를 검사를 소개 합니다.
ms.prod: xamarin
ms.assetid: 4ED4ACF4-BE4A-44ED-8EAF-C03947B8663B
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 09/11/2017
ms.openlocfilehash: 129ce7a04b93bfb3cb1b9a1639aee61cd56d09d5
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38998921"
---
# <a name="introduction-to-xamarinforms-data-templates"></a>Xamarin.Forms 데이터 템플릿 소개

_Xamarin.Forms 데이터 템플릿은 지원 되는 컨트롤에 데이터를 정의 하는 기능을 제공 합니다. 이 문서에서는 데이터 템플릿이 필요한 이유를 검사를 소개 합니다._

고려해 야는 [ `ListView` ](xref:Xamarin.Forms.ListView) 컬렉션을 표시 하는 `Person` 개체입니다. 다음 코드 예제에서는의 정의 보여 줍니다.는 `Person` 클래스:

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    public string Location { get; set; }
}
```

합니다 `Person` 클래스 정의 `Name`를 `Age`, 및 `Location` 속성을 설정할 수 있습니다는 `Person` 개체가 만들어집니다. 합니다 [ `ListView` ](xref:Xamarin.Forms.ListView) 의 컬렉션을 표시 하는 데 사용 됩니다 `Person` 다음 XAML 코드 예제 에서처럼 개체:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:DataTemplates"
             ...>
    <StackLayout Margin="20">
        ...
        <ListView Margin="0,20,0,0">
            <ListView.ItemsSource>
                <x:Array Type="{x:Type local:Person}">
                    <local:Person Name="Steve" Age="21" Location="USA" />
                    <local:Person Name="John" Age="37" Location="USA" />
                    <local:Person Name="Tom" Age="42" Location="UK" />
                    <local:Person Name="Lucas" Age="29" Location="Germany" />
                    <local:Person Name="Tariq" Age="39" Location="UK" />
                    <local:Person Name="Jane" Age="30" Location="USA" />
                </x:Array>
            </ListView.ItemsSource>
        </ListView>
    </StackLayout>
</ContentPage>
```

에 항목을 추가 합니다 [ `ListView` ](xref:Xamarin.Forms.ListView) 초기화 하 여 XAML에서는 [ `ItemsSource` ](xref:Xamarin.Forms.ItemsView`1.ItemsSource) 배열에서 속성 `Person` 인스턴스.

> [!NOTE]
> 합니다 `x:Array` 요소에는 `Type` 배열에 있는 항목의 유형을 나타내는 특성입니다.

초기화 하는 다음 코드 예제에서 해당 C# 페이지가 표시 됩니다는 [ `ItemsSource` ](xref:Xamarin.Forms.ItemsView`1.ItemsSource) 속성을 `List` 의 `Person` 인스턴스:

```csharp
public WithoutDataTemplatePageCS()
{
    ...
    var people = new List<Person>
    {
        new Person { Name = "Steve", Age = 21, Location = "USA" },
        new Person { Name = "John", Age = 37, Location = "USA" },
        new Person { Name = "Tom", Age = 42, Location = "UK" },
        new Person { Name = "Lucas", Age = 29, Location = "Germany" },
        new Person { Name = "Tariq", Age = 39, Location = "UK" },
        new Person { Name = "Jane", Age = 30, Location = "USA" }
    };

    Content = new StackLayout
    {
        Margin = new Thickness(20),
        Children = {
            ...
            new ListView { ItemsSource = people, Margin = new Thickness(0, 20, 0, 0) }
        }
    };
}
```

합니다 [ `ListView` ](xref:Xamarin.Forms.ListView) 호출 `ToString` 컬렉션의 개체를 표시 하는 경우. 있기 때문에 없습니다 `Person.ToString` 재정의 `ToString` 다음 스크린샷에 표시 된 것 처럼 각 개체의 형식 이름을 반환 합니다.

![](introduction-images/no-data-template.png "데이터 템플릿 없이 ListView")

합니다 `Person` 개체를 재정의할 수는 `ToString` 다음 코드 예제와 같이 의미 있는 데이터를 표시 하는 메서드:

```csharp
public class Person
{
  ...
  public override string ToString ()
  {
    return Name;
  }
}
```

이 인해 합니다 [ `ListView` ](xref:Xamarin.Forms.ListView) 표시 된 `Person.Name` 다음 스크린샷에 표시 된 것 처럼 컬렉션에서 각 개체에 대 한 속성 값:

![](introduction-images/override-tostring.png "데이터 템플릿 사용 하 여 ListView")

`Person.ToString` 재정의 구성 된 형식된 문자열을 반환할 수는 `Name`, `Age`, 및 `Location` 속성입니다. 그러나이 방법은 제한적인된 제어 데이터의 각 항목의 모양 제공합니다. 유연성을 높이려면를 [ `DataTemplate` ](xref:Xamarin.Forms.DataTemplate) 만들어질 수 데이터의 모양을 정의 하는 합니다.

## <a name="creating-a-datatemplate"></a>DataTemplate 만들기

A [ `DataTemplate` ](xref:Xamarin.Forms.DataTemplate) 데이터의 모양을 지정 하는 데 사용 되 고 일반적으로 데이터 바인딩을 사용 하 여 데이터를 표시 합니다. 개체의 컬렉션에서 데이터를 표시할 때의 일반적인 사용 시나리오는 한 [ `ListView` ](xref:Xamarin.Forms.ListView)합니다. 예를 들어 경우는 `ListView` 의 컬렉션에 바인딩된 `Person` 개체를 `ListView.ItemTemplate` 속성으로 설정 됩니다는 `DataTemplate` 각각의 모양을 정의 하는 `Person` 개체는 `ListView`. 합니다 `DataTemplate` 의 각 속성 값에 바인딩되는 요소가 포함 됩니다 `Person` 개체입니다. 데이터 바인딩에 대한 자세한 내용은 [데이터 바인딩 기본](~/xamarin-forms/xaml/xaml-basics/data-binding-basics.md)을 참조하세요.

A [ `DataTemplate` ](xref:Xamarin.Forms.DataTemplate) 다음 속성에 대 한 값으로 사용할 수 있습니다.

- [`ListView.HeaderTemplate`](xref:Xamarin.Forms.ListView.HeaderTemplate)
- [`ListView.FooterTemplate`](xref:Xamarin.Forms.ListView.FooterTemplate)
- [`ListView.GroupHeaderTemplate`](xref:Xamarin.Forms.ListView.GroupHeaderTemplate)
- [`ItemsView.ItemTemplate`](xref:Xamarin.Forms.ItemsView`1)에 의해 상속 되는 [ `ListView` ](xref:Xamarin.Forms.ListView)합니다.
- [`MultiPage.ItemTemplate`](xref:Xamarin.Forms.MultiPage`1)에 상속 됩니다 [ `CarouselPage` ](xref:Xamarin.Forms.CarouselPage)합니다 [ `MasterDetailPage` ](xref:Xamarin.Forms.MasterDetailPage), 및 [ `TabbedPage` ](xref:Xamarin.Forms.TabbedPage)합니다.

> [!NOTE]
> 있지만 합니다 [ `TableView` ](xref:Xamarin.Forms.TableView) 사용 하면 [ `Cell` ](xref:Xamarin.Forms.Cell) 개체를 사용 하지 않는 [ `DataTemplate` ](xref:Xamarin.Forms.DataTemplate)합니다. 데이터 바인딩을 항상에서 직접 설정 되므로이 `Cell` 개체입니다.

A [ `DataTemplate` ](xref:Xamarin.Forms.DataTemplate) 위에 나열 된 속성의 직계 자식 이라고 하는 배치 되는 *인라인 템플릿*합니다. 또는 `DataTemplate` 제어 수준, 페이지 수준 또는 응용 프로그램 수준 리소스로 정의할 수 있습니다. 정의할 위치를 선택는 [ `DataTemplate` ](xref:Xamarin.Forms.DataTemplate) 사용할 수 있는 영향을 줍니다.

- A [ `DataTemplate` ](xref:Xamarin.Forms.DataTemplate) 정의 컨트롤에서 수준 에서만 적용할 수 있습니다 컨트롤입니다.
- A [ `DataTemplate` ](xref:Xamarin.Forms.DataTemplate) 정의 페이지에서 수준 페이지의 여러 유효한 컨트롤에 적용 수 있습니다.
- A [ `DataTemplate` ](xref:Xamarin.Forms.DataTemplate) 응용 프로그램 수준에서 정의 된 응용 프로그램 전체에서 유효한 적용할된 컨트롤 수 있습니다.

데이터 템플릿 보기 계층 구조의 하위 우선 공유할 때를 더 높은 정의 `x:Key` 특성입니다. 예를 들어, 페이지 수준 데이터 템플릿을 응용 프로그램 수준 데이터 템플릿을 덮어쓸 수 있습니다 및 페이지 수준 데이터 템플릿을 제어 수준 데이터 템플릿 또는 인라인 데이터 템플릿을 덮어쓸 수 있습니다.


## <a name="related-links"></a>관련 링크

- [셀 모양](~/xamarin-forms/user-interface/listview/customizing-cell-appearance.md)
- [데이터 템플릿 (샘플)](https://developer.xamarin.com/samples/xamarin-forms/templates/datatemplates/)
- [데이터 템플릿](xref:Xamarin.Forms.DataTemplate)
