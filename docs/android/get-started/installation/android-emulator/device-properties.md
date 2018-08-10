---
title: Android 가상 장치 속성 편집
description: 이 문서에서는 Android Device Manager를 사용하여 Android 가상 장치의 프로필 속성을 편집하는 방법을 설명합니다.
ms.prod: xamarin
ms.assetid: 3E33C136-8042-4184-A40C-3200D8CD99CB
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 05/30/2018
ms.openlocfilehash: 75ac85c67825e5db1b663d00f10eee6d093bfc1f
ms.sourcegitcommit: a7febc19102209b21e0696256c324f366faa444e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34733814"
---
# <a name="editing-android-virtual-device-properties"></a>Android 가상 장치 속성 편집

_이 문서에서는 Android Device Manager를 사용하여 Android 가상 장치의 프로필 속성을 편집하는 방법을 설명합니다._


# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

**Android Device Manager**는 개별 Android 가상 장치 프로필 속성의 편집을 지원합니다. **새 장치** 및 **장치 편집기** 화면에서 첫 번째 열에는 가상 장치 속성이 나열되고, 두 번째 열에는 각 속성의 해당 값이 나열됩니다(이 예제에 표시된 것처럼). 

[![새 장치 화면 예제](device-properties-images/win/01-new-device-editor-sml.png)](device-properties-images/win/01-new-device-editor.png#lightbox)

속성을 선택하면 속성에 대한 자세한 설명이 오른쪽에 표시됩니다. *하드웨어 프로필 속성* 및 *AVD 속성*을 수정할 수 있습니다. 하드웨어 프로필 속성(예: `hw.ramSize` 및 `hw.accelerometer`)은 에뮬레이트된 장치의 물리적 특성을 나타냅니다. 이러한 특성에는 화면 크기, 사용 가능한 RAM의 양, 가속도계의 유무가 포함됩니다. AVD 속성은 실행되는 AVD의 작업을 나타냅니다. 예를 들어 AVD 속성을 구성하여 AVD에서 개발 컴퓨터의 그래픽 카드를 렌더링에 사용하는 방식을 지정할 수 있습니다.

다음 지침에 따라 속성을 변경할 수 있습니다.

-   부울 속성을 변경하려면 부울 속성의 오른쪽에 있는 확인 표시를 클릭합니다.

    ![부울 속성 변경](device-properties-images/win/02-boolean-value.png)

-   *열거형*(enumerated) 속성을 변경하려면 속성의 오른쪽에 있는 아래쪽 화살표를 클릭하고 새 값을 선택합니다.

    ![열거형 속성 변경](device-properties-images/win/04-enum-value.png)

-   정수 또는 문자열 속성을 변경하려면 값 열에서 현재 문자열 또는 정수 설정을 두 번 클릭하고 새 값을 입력합니다.

    ![정수 속성 변경](device-properties-images/win/03-integer-value.png)


# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio for Mac](#tab/vsmac)

**Android Device Manager**는 개별 Android 가상 장치 프로필 속성의 편집을 지원합니다. **새 장치** 및 **장치 편집기** 화면에서 첫 번째 열에는 가상 장치 속성이 나열되고, 두 번째 열에는 각 속성의 해당 값이 나열됩니다(이 예제에 표시된 것처럼). 

[![새 장치 화면 예제](device-properties-images/mac/01-new-device-editor-sml.png)](device-properties-images/mac/01-new-device-editor.png#lightbox)

속성을 선택하면 속성에 대한 자세한 설명이 오른쪽에 표시됩니다. *하드웨어 프로필 속성* 및 *AVD 속성*을 수정할 수 있습니다. 하드웨어 프로필 속성(예: `hw.ramSize` 및 `hw.accelerometer`)은 에뮬레이트된 장치의 물리적 특성을 나타냅니다. 이러한 특성에는 화면 크기, 사용 가능한 RAM의 양, 가속도계의 유무가 포함됩니다. AVD 속성은 실행되는 AVD의 작업을 나타냅니다. 예를 들어 AVD 속성을 구성하여 AVD에서 개발 컴퓨터의 그래픽 카드를 렌더링에 사용하는 방식을 지정할 수 있습니다.

다음 지침에 따라 속성을 변경할 수 있습니다.

-   부울 속성을 변경하려면 부울 속성의 오른쪽에 있는 확인 표시를 클릭합니다.

    ![부울 속성 변경](device-properties-images/mac/02-boolean-value.png)

-   *열거형*(enumerated) 속성을 변경하려면 속성의 오른쪽에 있는 풀 다운 메뉴를 클릭하고 새 값을 선택합니다.

    ![열거형 속성 변경](device-properties-images/mac/04-enum-value.png)

-   정수 또는 문자열 속성을 변경하려면 값 열에서 현재 문자열 또는 정수 설정을 두 번 클릭하고 새 값을 입력합니다.

    ![정수 속성 변경](device-properties-images/mac/03-integer-value.png)

-----

다음 표에는 **새 장치** 및 **장치 편집기** 화면에 나오는 속성에 대한 자세한 설명이 나와 있습니다.

[!include[](~/android/includes/emulator-properties.md)]

이러한 속성에 대한 자세한 내용은 [하드웨어 프로필 속성](https://developer.android.com/studio/run/managing-avds.html#hpproperties)을 참조하세요.

