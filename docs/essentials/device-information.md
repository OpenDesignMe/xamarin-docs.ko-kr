---
title: 'Xamarin.Essentials: 장치 정보'
description: 이 문서에서 응용 프로그램에서 실행 되는 장치에 대 한 정보를 제공 하는 Xamarin.Essentials DeviceInfo 클래스를 설명 합니다.
ms.assetid: A1AC5373-926A-4FB6-8D7D-4B87EB8EB522
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 18fe081372cc190e5ead2045f36d63652f8702c3
ms.sourcegitcommit: 51c274f37369d8965b68ff587e1c2d9865f85da7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2018
ms.locfileid: "39353804"
---
# <a name="xamarinessentials-device-information"></a>Xamarin.Essentials: 장치 정보

![시험판 버전 NuGet](~/media/shared/pre-release.png)

합니다 **DeviceInfo** 클래스는 응용 프로그램에서 실행 되는 장치에 대 한 정보를 제공 합니다.

## <a name="using-deviceinfo"></a>DeviceInfo를 사용 하 여

클래스에서 Xamarin.Essentials에 대 한 참조를 추가 합니다.

```csharp
using Xamarin.Essentials;
```

다음 정보는 API를 통해 노출 됩니다.

```csharp
// Device Model (SMG-950U, iPhone10,6)
var device = DeviceInfo.Model;

// Manufacturer (Samsung)
var manufacturer = DeviceInfo.Manufacturer;

// Device Name (Motz's iPhone)
var deviceName = DeviceInfo.Name;

// Operating System Version Number (7.0)
var version = DeviceInfo.VersionString;

// Platform (Android)
var platform = DeviceInfo.Platform;

// Idiom (Phone)
var idiom = DeviceInfo.Idiom;

// Device Type (Physical)
var deviceType = DeviceInfo.DeviceType;
```

## <a name="platformsxrefxamarinessentialsdeviceinfoplatforms"></a>[플랫폼](xref:Xamarin.Essentials.DeviceInfo.Platforms)

`DeviceInfo.Platform` 운영 체제에 매핑되는 상수 문자열을 상호 연결 합니다. 값으로 확인할 수 있습니다는 `Platforms` 클래스:

- **DeviceInfo.Platforms.iOS** -iOS
- **DeviceInfo.Platforms.Android** -Android
- **DeviceInfo.Platforms.UWP** – UWP
- **DeviceInfo.Platforms.Unsupported** 지원 되지 않는 –

## <a name="idiomsxrefxamarinessentialsdeviceinfoidioms"></a>[관용구](xref:Xamarin.Essentials.DeviceInfo.Idioms)

`DeviceInfo.Idiom` 상관 관계를 지정 응용 프로그램 종류의 장치에 매핑하는 상수 문자열에서 실행 됩니다. 값으로 확인할 수 있습니다는 `Idioms` 클래스:

- **DeviceInfo.Idioms.Phone** -휴대폰
- **DeviceInfo.Idioms.Tablet** – 태블릿
- **DeviceInfo.Idioms.Desktop** – 데스크톱
- **DeviceInfo.Idioms.TV** – TV
- **DeviceInfo.Idioms.Unsupported** 지원 되지 않는 –

## <a name="device-type"></a>장치 유형

`DeviceInfo.DeviceType` 응용 프로그램을 실제 또는 가상 장치에서 실행 되 고 있는지 확인 하는 열거형을 상호 연결 합니다. 가상 장치 시뮬레이터 또는 에뮬레이터입니다.

## <a name="platform-implementation-specifics"></a>플랫폼 구현 세부 정보

# <a name="iostabios"></a>[iOS](#tab/ios)

iOS 개발자가 특정 iOS 장치의 이름을 API를 노출 하지 않습니다. 하드웨어 식별자와 같은 반환 되는 대신 _iPhone10, 6_ iPhone X 참조 하는 합니다. 이러한 식별자 매핑을 Apple에서 제공 되지 않지만에서 찾을 수 있습니다 [iPhone Wiki](https://www.theiphonewiki.com/wiki/Models) (공식 아닌 원본 소스).

--------------

## <a name="api"></a>API

- [DeviceInfo 소스 코드](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/DeviceInfo)
- [DeviceInfo API 설명서](xref:Xamarin.Essentials.DeviceInfo)
