---
title: 플랫폼별 만들기
description: 이 문서는 플랫폼별 통해 효과 노출 하는 방법을 보여 줍니다.
ms.prod: xamarin
ms.assetid: 0D0E6274-6EF2-4D40-BB77-3D8E53BCD24B
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 11/23/2016
ms.openlocfilehash: 1d9f07a089eabedf07bef49c9815fe7e93128f09
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38997258"
---
# <a name="creating-platform-specifics"></a>플랫폼별 만들기

_공급 업체는 자신의 플랫폼별 효과 사용 하 여 만들 수 있습니다. 효과가는 플랫폼별을 통해 노출 되는 특정 기능을 제공 합니다. 결과 코드를 fluent API 및 XAML을 통해 보다 쉽게 사용할 수 있는 효과입니다. 이 문서는 플랫폼별 통해 효과 노출 하는 방법을 보여 줍니다._

## <a name="overview"></a>개요

플랫폼 전용을 만들기 위한 프로세스는 다음과 같습니다.

1. 효과로 특정 기능을 구현 합니다. 자세한 내용은 [효과 만드는](~/xamarin-forms/app-fundamentals/effects/creating.md)합니다.
1. 효과 노출 하는 플랫폼 특정 클래스를 만듭니다. 자세한 내용은 [플랫폼별 클래스를 만드는](#creating)합니다.
1. 플랫폼별 클래스에서 플랫폼별 XAML을 통해 사용할 수 있도록 연결된 된 속성을 구현 합니다. 자세한 내용은 [연결 된 속성 추가](#attached_property)합니다.
1. 플랫폼 관련 클래스에 플랫폼별 코드를 fluent API 통해 사용할 수 있도록 확장 메서드를 구현 합니다. 자세한 내용은 [확장 메서드 추가](#extension_methods)합니다.
1. 효과 플랫폼 특정 효과와 동일한 플랫폼에서 호출 된 경우에 적용 됩니다 있도록 효과 구현을 수정 합니다. 자세한 내용은 [효과 만드는](#creating_the_effect)합니다.

플랫폼 특정 효과 노출 합니다. 결과 XAML 및 fluent 코드 API 통해 효과 보다 쉽게 사용할 수 있습니다.

> [!NOTE]
> 공급 업체 명의 사용 편의성을 위해 자체 플랫폼별을 만들려면이 기술은 사용할지는 예상는 것입니다. 사용자가 자신의 플랫폼별을 만들도록 선택할 수, 하는 동안 유의 만들고 효과 사용 보다 더 많은 코드가 필요 하다는 것입니다.

샘플 응용 프로그램을 보여 줍니다.는 `Shadow` 으로 표시 되는 텍스트에 그림자를 추가 하는 플랫폼별을 [ `Label` ](xref:Xamarin.Forms.Label) 컨트롤:

![](creating-images/screenshots.png "섀도 플랫폼별")

샘플 응용 프로그램으로 구현 된 `Shadow` 이해 하기 쉽도록 각 플랫폼에 플랫폼별입니다. 그러나 각 플랫폼별 효과 구현 외에도 섀도 클래스의 구현은 각 플랫폼에 대해 거의 동일 합니다. 따라서이 가이드 섀도 클래스와 연결 된 미치는 단일 플랫폼의 구현에 중점을 둡니다.

효과 대 한 자세한 내용은 참조 하세요. [효과 사용 하 여 사용자 지정 컨트롤](~/xamarin-forms/app-fundamentals/effects/index.md)합니다.

<a name="creating" />

## <a name="creating-a-platform-specific-class"></a>플랫폼별 클래스 만들기

플랫폼 전용으로 생성 됩니다는 `public static` 클래스:

```csharp
namespace MyCompany.Forms.PlatformConfiguration.iOS
{
  public static Shadow
  {
    ...
  }
}
```

다음 섹션에서는 구현에 설명 된 `Shadow` 플랫폼별 및 관련 된 적용 합니다.

<a name="attached_property" />

### <a name="adding-an-attached-property"></a>연결 된 속성 추가

연결된 된 속성에 추가 되어야 합니다는 `Shadow` 플랫폼별 XAML 통해 사용을 허용 하려면:

```csharp
namespace MyCompany.Forms.PlatformConfiguration.iOS
{
    using System.Linq;
    using Xamarin.Forms;
    using Xamarin.Forms.PlatformConfiguration;
    using FormsElement = Xamarin.Forms.Label;

    public static class Shadow
    {
        const string EffectName = "MyCompany.LabelShadowEffect";

        public static readonly BindableProperty IsShadowedProperty =
            BindableProperty.CreateAttached("IsShadowed",
                                            typeof(bool),
                                            typeof(Shadow),
                                            false,
                                            propertyChanged: OnIsShadowedPropertyChanged);

        public static bool GetIsShadowed(BindableObject element)
        {
            return (bool)element.GetValue(IsShadowedProperty);
        }

        public static void SetIsShadowed(BindableObject element, bool value)
        {
            element.SetValue(IsShadowedProperty, value);
        }

        ...

        static void OnIsShadowedPropertyChanged(BindableObject element, object oldValue, object newValue)
        {
            if ((bool)newValue)
            {
                AttachEffect(element as FormsElement);
            }
            else
            {
                DetachEffect(element as FormsElement);
            }
        }

        static void AttachEffect(FormsElement element)
        {
            IElementController controller = element;
            if (controller == null || controller.EffectIsAttached(EffectName))
            {
                return;
            }
            element.Effects.Add(Effect.Resolve(EffectName));
        }

        static void DetachEffect(FormsElement element)
        {
            IElementController controller = element;
            if (controller == null || !controller.EffectIsAttached(EffectName))
            {
                return;
            }

            var toRemove = element.Effects.FirstOrDefault(e => e.ResolveId == Effect.Resolve(EffectName).ResolveId);
            if (toRemove != null)
            {
                element.Effects.Remove(toRemove);
            }
        }
    }
}
```

`IsShadowed` 연결 된 속성을 추가 하는 데 사용 됩니다 합니다 `MyCompany.LabelShadowEffect` 에 영향을 컨트롤에서 제거는 `Shadow` 클래스에 연결 된. 이 연결 속성 레지스터는 `OnIsShadowedPropertyChanged` 속성의 값이 변경 될 때 실행 되는 메서드. 그러면이 메서드를 호출 합니다는 `AttachEffect` 또는 `DetachEffect` 의 값을 기반으로 하는 메서드를 추가 하 여 효과 제거 합니다 `IsShadowed` 연결 된 속성입니다. 효과 컨트롤을 수정 하 여 컨트롤에서 제거 또는 추가할 [ `Effects` ](xref:Xamarin.Forms.Element.Effects) 컬렉션입니다.

> [!NOTE]
> 그룹 이름 확인 및 적용 구현에 지정 된 고유 식별자를 연결한 값을 지정 하 여 효과 해결는 note 합니다. 자세한 내용은 [효과 만드는](~/xamarin-forms/app-fundamentals/effects/creating.md)합니다.

연결 된 속성에 대 한 자세한 내용은 참조 하세요. [연결 속성](~/xamarin-forms/xaml/attached-properties.md)합니다.

<a name="extension_methods" />

### <a name="adding-extension-methods"></a>확장 메서드를 추가합니다.

확장 메서드를 추가 해야 합니다 `Shadow` 플랫폼별 코드를 fluent API 통해 사용을 허용 하려면:

```csharp
namespace MyCompany.Forms.PlatformConfiguration.iOS
{
    using System.Linq;
    using Xamarin.Forms;
    using Xamarin.Forms.PlatformConfiguration;
    using FormsElement = Xamarin.Forms.Label;

    public static class Shadow
    {
        ...
        public static bool IsShadowed(this IPlatformElementConfiguration<iOS, FormsElement> config)
        {
            return GetIsShadowed(config.Element);
        }

        public static IPlatformElementConfiguration<iOS, FormsElement> SetIsShadowed(this IPlatformElementConfiguration<iOS, FormsElement> config, bool value)
        {
            SetIsShadowed(config.Element, value);
            return config;
        }
        ...
    }
}
```

`IsShadowed` 하 고 `SetIsShadowed` 확장 메서드 호출 get 및 set 접근자에 대 한는 `IsShadowed` 각각 연결 된 속성입니다. 각 확장 메서드가 작동 합니다 `IPlatformElementConfiguration<iOS, FormsElement>` 형식에 플랫폼 전용을 호출할 수 있음을 지정 하는 [ `Label` ](xref:Xamarin.Forms.Label) iOS에서 인스턴스.

<a name="creating_the_effect" />

### <a name="creating-the-effect"></a>효과 만들기

`Shadow` 플랫폼별 추가 `MyCompany.LabelShadowEffect` 에 [ `Label` ](xref:Xamarin.Forms.Label)를 제거 합니다. 다음 코드 예제는 `LabelShadowEffect` iOS 프로젝트에 대 한 구현 합니다.

```csharp
[assembly: ResolutionGroupName("MyCompany")]
[assembly: ExportEffect(typeof(LabelShadowEffect), "LabelShadowEffect")]
namespace ShadowPlatformSpecific.iOS
{
    public class LabelShadowEffect : PlatformEffect
    {
        protected override void OnAttached()
        {
            UpdateShadow();
        }

        protected override void OnDetached()
        {
        }

        protected override void OnElementPropertyChanged(PropertyChangedEventArgs args)
        {
            base.OnElementPropertyChanged(args);

            if (args.PropertyName == Shadow.IsShadowedProperty.PropertyName)
            {
                UpdateShadow();
            }
        }

        void UpdateShadow()
        {
            try
            {
                if (((Label)Element).OnThisPlatform().IsShadowed())
                {
                    Control.Layer.CornerRadius = 5;
                    Control.Layer.ShadowColor = UIColor.Black.CGColor;
                    Control.Layer.ShadowOffset = new CGSize(5, 5);
                    Control.Layer.ShadowOpacity = 1.0f;
                }
                else if (!((Label)Element).OnThisPlatform().IsShadowed())
                {
                    Control.Layer.ShadowOpacity = 0;
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine("Cannot set property on attached control. Error: ", ex.Message);
            }
        }
    }
}
```

`UpdateShadow` 메서드 집합 `Control.Layer` 그림자를 만들기 위한 속성을 제공 하는 합니다 `IsShadowed` 연결된 속성이로 설정 되어 `true`, 제공 및는 `Shadow` 플랫폼별 동일한 플랫폼에서 호출 된는 효과 대 한 구현 됩니다. 이 검사가 수행 되는 `OnThisPlatform` 메서드.

경우는 `Shadow.IsShadowed` 속성 값이 변경 런타임에 적용 해야 그림자를 제거 하 여 응답을 연결 합니다. 따라서 재정의 된 버전의 `OnElementPropertyChanged` 메서드를 호출 하 여 바인딩 가능한 속성 변경에 대응 되는 `UpdateShadow` 메서드.

효과 만드는 방법에 대 한 자세한 내용은 참조 하세요. [효과 만드는](~/xamarin-forms/app-fundamentals/effects/creating.md) 하 고 [연결 된 속성으로 결과 매개 변수 전달](~/xamarin-forms/app-fundamentals/effects/passing-parameters/attached-properties.md)합니다.

## <a name="consuming-a-platform-specific"></a>플랫폼별 사용

합니다 `Shadow` 플랫폼별으로 설정 하 여 XAML에서 사용 되는 `Shadow.IsShadowed` 연결 된 속성을 `boolean` 값:

```xaml
<ContentPage xmlns:ios="clr-namespace:MyCompany.Forms.PlatformConfiguration.iOS" ...>
  ...
  <Label Text="Label Shadow Effect" ios:Shadow.IsShadowed="true" ... />
  ...
</ContentPage>
```

또는 fluent API를 사용 하 여 C#에서 사용할 수 있습니다.

```csharp
using Xamarin.Forms.PlatformConfiguration;
using MyCompany.Forms.PlatformConfiguration.iOS;

...

shadowLabel.On<iOS>().SetIsShadowed(true);
```

플랫폼별 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [소비 플랫폼별](~/xamarin-forms/platform/platform-specifics/consuming/index.md)합니다.

## <a name="summary"></a>요약

이 문서는 플랫폼별 통해 효과 노출 하는 방법을 보여 줍니다. 결과 코드를 fluent API 및 XAML을 통해 보다 쉽게 사용할 수 있는 효과입니다.


## <a name="related-links"></a>관련 링크

- [ShadowPlatformSpecific (샘플)](https://developer.xamarin.com/samples/xamarin-forms/userinterface/shadowplatformspecific/)
- [효과 사용 하 여 사용자 지정 컨트롤](~/xamarin-forms/app-fundamentals/effects/index.md)
- [연결된 속성](~/xamarin-forms/xaml/attached-properties.md)
