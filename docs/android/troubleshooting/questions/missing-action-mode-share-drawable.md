---
title: "Android.Support.v7.AppCompat-지정 된 이름과 일치 하는 리소스를 찾을 수: ' android: actionModeShareDrawable' attr"
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 5814069C-FC43-41DE-B5A5-024D05E59929
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/09/2018
ms.openlocfilehash: 07655587642c3e1aa94d035e76f6f6758340546d
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
ms.locfileid: "30774898"
---
# <a name="androidsupportv7appcompat---no-resource-found-that-matches-the-given-name-attr-androidactionmodesharedrawable"></a>Android.Support.v7.AppCompat-지정 된 이름과 일치 하는 리소스를 찾을 수: ' android: actionModeShareDrawable' attr

1. Android 5.0 (API 21) SDK는 Android SDK Manager를 통해 뿐만 아니라 최신 추가 기능을 다운로드 하 고 있는지 확인 합니다.

2. CompileSdkVersion 21로 설정 된 응용 프로그램을 컴파일하는 있는지 확인 하십시오. 필요에 따라 21도로 targetSdkVersion를 설정할 수 있습니다.

3. API 19 같은 이전 버전을 필요한 경우 Nuget 페이지에서 발견 된 각 버전을 다운로드 하십시오.

[https://www.nuget.org/packages/Xamarin.Android.Support.v7.AppCompat/](https://www.nuget.org/packages/Xamarin.Android.Support.v7.AppCompat/)

*참고*: 수동으로 설치한 경우이 패키지 관리자 콘솔을 통해, 또한 같은 버전의 Xamarin.Android.Support.v4가 설치 되었는지 확인

[https://www.nuget.org/packages/Xamarin.Android.Support.v4/](https://www.nuget.org/packages/Xamarin.Android.Support.v4/)

스택 오버플로 참조: [http://stackoverflow.com/questions/26431676/appcompat-v721-0-0-no-resource-found-that-matches-the-given-name-attr-andro](http://stackoverflow.com/questions/26431676/appcompat-v721-0-0-no-resource-found-that-matches-the-given-name-attr-andro)

## <a name="see-also"></a>참고 항목

- [어떤 Android SDK 패키지를 설치해야 하나요?](~/android/troubleshooting/questions/install-android-sdk-packages.md)

