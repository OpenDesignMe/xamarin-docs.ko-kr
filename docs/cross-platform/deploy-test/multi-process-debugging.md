---
title: 다중 프로세스 디버깅
description: 이 문서에서는 Mac용 Visual Studio를 사용하여 동시에 실행되는 여러 프로세스를 디버깅하는 방법을 설명합니다. 예를 들어 이 기능은 모바일 응용 프로그램 및 웹 서비스 프로젝트를 동시에 디버깅하는 데 사용될 수 있습니다.
ms.prod: xamarin
ms.assetid: 852F8AB1-F9E2-4126-9C8A-12500315C599
author: asb3993
ms.author: amburns
ms.date: 03/24/2017
ms.openlocfilehash: d20e6e0fd567d0aa0febe21bfe12a5237049b22a
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34781854"
---
# <a name="multi-process-debugging"></a>다중 프로세스 디버깅

Mac용 Visual Studio에서 개발된 최신 솔루션에는 다양한 플랫폼을 대상으로 하는 여러 프로젝트가 있는 것이 매우 일반적입니다. 예를 들어 솔루션에는 웹 서비스 프로젝트에서 제공하는 데이터에 의존하는 모바일 응용 프로그램 프로젝트가 있을 수 있습니다. 개발자는 이 솔루션을 개발하는 동안 오류를 해결하기 위해 두 프로젝트가 동시에 실행되도록 해야 할 수도 있습니다. [Xamarin의 Cycle 9 릴리스](https://releases.xamarin.com/stable-release-cycle-9/)를 시작으로 이제는 Mac용 Visual Studio가 동시에 실행 중인 여러 프로세스를 디버깅하는 것이 가능합니다. 따라서 실행 중인 둘 이상의 프로젝트에서 중단점을 설정하고, 변수를 검사하고, 스레드를 보는 것이 가능해졌습니다. 이것을 _다중 프로세스 디버깅_이라고 합니다. 

이 가이드에서는 여러 프로세스 디버깅, 여러 프로세스를 디버깅하도록 솔루션을 구성하는 방법, Mac용 Visual Studio로 기존 프로세스에 결합하는 방법을 지원하기 위해 Mac용 Visual Studio에 이뤄진 일부 변경 사항을 다룹니다.

## <a name="requirements"></a>요구 사항

여러 프로세스를 디버깅하려면 Mac용 Visual Studio가 필요합니다.

## <a name="ide-changes"></a>IDE 변경 내용

개발자가 다중 프로세스를 디버깅하는 데 도움이 되도록 Mac용 Visual Studio의 사용자 인터페이스에 몇가지 변경이 이뤄졌습니다. Mac용 Visual Studio에 업데이트된 **디버그 도구 모음**이 있으며, **솔루션 옵션** 폴더에 새 **솔루션 구성** 섹션이 있습니다. 또한 **스레드 패드**는 이제 실행 중인 프로세스와 각 프로세스에 대한 스레드를 표시합니다. Mac용 visual Studio는 또한 **응용 프로그램 출력**과 같은 특정한 것에 대해 각 프로세스에 하나씩 여러 디버그 패드를 표시합니다.

### <a name="solution-configurations"></a>솔루션 구성

기본적으로 Mac용 Visual Studio는 디버그 도구 모음의 **솔루션 구성** 영역에 개별 프로젝트를 표시합니다. 디버깅 세션이 시작될 때 이것은 Mac용 Visual Studio가 디버거를 시작하고 연결할 프로젝트입니다.

Mac용 Visual Studio에서 여러 프로세스를 시작하고 디버깅하려면 _솔루션 구성_을 만드는 것이 필요합니다. 솔루션 구성은 **시작** 단추를 클릭하거나 &#8984;&#8617;(**Cmd-Enter**)을 눌러 디버깅 세션을 시작할 때 솔루션에 어떤 프로젝트가 포함되어야 하는지 설명합니다. 다음 스크린샷은 Mac용 Visual Studio에 있는 여러 솔루션 구성을 가진 솔루션의 예시입니다.

![](multi-process-debugging-images/mpd01-xs.png "여러 솔루션 구성을 가진 솔루션")

### <a name="parts-of-the-debug-toolbar"></a>디버그 도구 모음의 부분

디버그 도구 모음은 팝업 메뉴를 통해 솔루션 구성을 선택할 수 있도록 변경되었습니다. 이 스크린샷은 디버그 도구 모음의 부분을 보여줍니다.

![](multi-process-debugging-images/mpd02-xs.png "디버그 도구 모음의 부분")

1. **솔루션 구성** - 디버그 도구 모음에서 솔루션 구성을 클릭하고 팝업 메뉴에서 해당 구성을 선택하여 솔루션 구성을 설정할 수 있습니다.

    ![](multi-process-debugging-images/mpd03-xs.png "솔루션 구성을 사용한 샘플 팝업")

2. **빌드 대상** - 프로젝트에 대한 빌드 대상을 식별합니다. Mac용 Visual Studio의 이전 버전에서 변경되지 않습니다.
3. **장치 대상** - 솔루션이 실행될 장치를 선택합니다. 각 프로젝트에 대한 별도 장치 또는 에뮬레이터를 식별할 수 있습니다.

    ![](multi-process-debugging-images/mpd04-xs.png "프로젝트에 대한 장치를 표시하는 팝업")

### <a name="multiple-debug-pads"></a>여러 디버그 패드

다중 솔루션 구성을 시작할 때 Mac용 Visual Studio 패드 일부가 각 프로세스에 대해 한 번씩 여러번 나타납니다. 예를 들어 다음 스크린샷은 두 개의 프로젝트를 실행하는 솔루션에 대해 두 **응용 프로그램 출력** 패드를 보여줍니다.

![](multi-process-debugging-images/mpd05-xs.png "솔루션 구성에 대한 출력 패드")

### <a name="multiple-processes-and-the-active-thread"></a>여러 프로세스와 _활성 스레드_

하나의 프로세스에서 중단점을 만나면 그 프로세스는 실행을 일시 중지하고 다른 프로세스는 계속 실행됩니다. 단일 프로세스 시나리오에서 Mac용 Visual Studio는 단일 패드 집합에 있는 스레드, 지역 변수, 응용 프로그램 출력 등의 정보를 쉽게 표시할 수 있습니다. 그러나, 여러 중단점과 잠재적으로 여러 스레드를 사용하는 여러 프로세스가 있을 경우 모든 스레드(와 프로세스)로부터 오는 모든 정보를 한꺼번에 표시하고자 하는 디버깅 세션의 정보는 개발자가 감당하기에 너무나 엄청나다는 것이 판명될 수 있습니다.

이 문제를 다루기 위해 Mac용 Visual Studio는 한 번에 한 스레드의 정보만 표시합니다. 이것을 _활성 스레드_라고 합니다. 중단점에서 일시 중지하는 첫 번째 스레드는 _활성 스레드_로 간주됩니다. 활성 스레드는 개발자가 중점적으로 주의를 기울이는 스레드입니다. **스텝오버**&#8984;&#8617;O(Shift-Cmd-O)와 같은 디버깅 명령이 활성 스레드에 내려집니다.

**스레드 패드**는 솔루션 구성에서 검사 중인 모든 프로세스 및 스레드에 대한 정보를 표시하고 어떤 것이 활성 스레드인지에 관한 시각 신호를 제공합니다.

![](multi-process-debugging-images/mpd06-xs.png "솔루션 구성에 대한 스레드 패드")

스레드는 호스팅하는 프로세스에 의해 그룹화됩니다. 활성 스레드의 프로젝트 이름 및 ID는 굵은 텍스트로 표시되고, 오른쪽을 가리키는 화살표는 활성 스레드 옆에 있는 여백에 나타납니다. 이전 스크린 샷에서 **프로세스 Id 48703**(**FirstProject**)의 **스레드 #1**은 활성 스레드입니다.

여러 프로세스를 디버깅할 때 **스레드 패드**를 사용하여 활성 스레드가 그 프로세스(또는 스레드)에 대한 디버깅 정보를 참조하도록 전환할 수 있습니다. 활성 스레드를 전환하려면 **스레드 패드**에서 원하는 스레드를 선택한 다음, 두 번 클릭합니다.

#### <a name="stepping-through-code-when-multiple-projects-are-stopped"></a>여러 프로젝트가 중지될 때 단계별 진행 코드

두 개 이상의 프로젝트에 중단점이 있을 경우 Mac용 Visual Studio는 두 프로세스를 일시 중지합니다. 그렇게 하는 것은 활성 스레드에 있는 **스텝오버** 코드에만 가능합니다. 다른 프로세스는 범위 변경이 디버거가 활성 스레드에서 포커스를 전환할 수 있도록 할 때까지 일시 중지됩니다. 예를 들어, 두 개의 프로젝트를 디버깅하는 Mac용 Visual Studio의 다음 스크린샷을 살펴보겠습니다.

![](multi-process-debugging-images/mpd09-xs.png  "Mac용 Visual Studio로 두 프로젝트를 디버깅함")

이 스크린샷을 보면 각 솔루션에 자체 중단점이 있습니다. 디버깅이 시작될 때 만나게 될 첫 번째 중단점은 **SecondProject**에서 `MainClass`의 **10줄**에 있습니다. 두 프로젝트 모두에 중단점이 있으므로 각 프로세스가 중지됩니다. 중단점에 도달하면 **스텝오버**를 호출할 때마다 Mac용 Visual Studio가 활성화 스레드에서 코드를 단계별로 실행합니다.

코드 단계별 진행은 활성 스레드에 국한되므로 다른 프로세스가 여전히 중지된 채로 있는 가운데 Mac용 Visual Studio는 코드를 한 번에 한 줄씩 실행해 나갑니다.

이전 스크린샷을 예로 들자면 `for` 루프가 완료될 때 Mac용 Visual Studio는 `MainClass`에서 **11줄**의 중단점을 만날 때까지 **FirstProject**가 실행되게 합니다. 각 **스텝오버** 명령에 대해, 디버거는 Mac용 Visual Studio의 내부 발견적 알고리즘이 활성 스레드를  **SecondProject**로 전환할 때까지 **FirstProject**에서 한 줄씩 실행해 나갑니다.

프로젝트 중 하나에만 중단점이 설정된 경우 그 프로세스만 일시 중지합니다. 다른 프로젝트는 개발자가 일시 중지하거나 중단점이 추가될 때까지 계속 실행됩니다.

### <a name="pausing-and-resuming-a-processes"></a>프로세스 일시 중지 및 다시 시작

프로세스를 마우스 오른쪽 단추로 클릭한 후 상황에 맞는 메뉴에서 **일시 중지** 또는 **다시 시작**을 선택하여 프로세스를 일시 중지하거나 계속할 수 있습니다.

![](multi-process-debugging-images/mpd08-xs.png "스레드 패드에서 일시 중지 또는 다시 시작")

디버그 도구 모음의 모양은 디버깅 중인 프로젝트의 상태에 따라 변경됩니다. 여러 프로젝트가 실행 중이라면, 디버그 도구 모음은 적어도 하나의 프로젝트가 실행 중이고 하나의 프로젝트가 일시 중지된 경우 **일시 중지** 및 **다시 시작** 단추를 모두 표시합니다.

![](multi-process-debugging-images/mpd07-xs.png  "Debug 도구 모음")

**디버그 도구 모음**에서 **일시 중지** 단추를 클릭하면 디버깅 중인 모든 프로세스가 일시 중지하고 **다시 시작** 단추를 클릭하면 모든 일시 중지 된 프로세스가 다시 시작됩니다.

### <a name="debugging-a-second-project"></a>두 번째 프로젝트 디버깅

Mac용 Visual Studio가 첫 번째 프로젝트를 시작하고 나면 두 번째 프로젝트를 디버깅할 수 있습니다. 첫 번째 프로젝트가 시작되면 **솔루션 패드**에서 프로젝트를 **마우스 오른쪽 단추로 클릭*한 다음, **디버깅 항목 시작**을 클릭합니다.

![](multi-process-debugging-images/mpd13-xs.png  "디버깅 항목 시작")

## <a name="creating-a-solution-configuration"></a>솔루션 구성 만들기

_솔루션 구성_은 **시작** 단추로 디버깅 세션을 시작할 때 Mac용 Visual Studio에 어떤 프로젝트를 실행할지 지시합니다. 솔루션 당 둘 이상의 솔루션 구성이 있을 수 있습니다. 따라서 프로젝트를 디버깅할 때 어떤 프로젝트가 실행되도록 할지 지정할 수 있습니다.

Xamaring Studio에서 새 솔루션 구성을 만들려면

1. Mac용 Visual Studio에서 **솔루션 옵션** 대화 상자를 열고 **실행 > 구성**을 선택합니다.

    ![](multi-process-debugging-images/mpd10-xs.png "솔루션 옵션 대화 상자에서 솔루션 구성")

2. **새로** 단추를 클릭하고, 새 솔루션 구성의 이름을 입력한 후, **만들기**를 클릭합니다. 새 솔루션 구성이 **구성** 창에 나타납니다.

    ![](multi-process-debugging-images/mpd11-xs.png  "새 솔루션 구성 이름 지정")

3. 구성 목록에서 새 실행 구성을 선택합니다. **솔루션 옵션** 대화 상자는 솔루션에 있는 프로젝트를 표시합니다. 디버깅 세션을 시작할 때 시작되어야 하는 각 프로젝트를 확인합니다.

    ![](multi-process-debugging-images/mpd12-xs.png "시작할 프로젝트 선택")

이제 **MultipleProjects** 솔루션 구성이 **디버그 도구 모음**에 나타나 개발자가 두 개의 프로젝트를 동시에 디버깅할 수 있게 합니다.

## <a name="summary"></a>요약

이 가이드는 Mac용 Visual Studio에서 여러 프로세스를 디버깅하는 것에 관해 설명합니다. 다중 프로세스 디버깅을 지원하기 위해 IDE에 가해진 몇 가지 변경 내용을 다루고 몇 가지 관련된 동작을 설명합니다.

## <a name="related-links"></a>관련 링크

- [Xamarin Cycle 9 릴리스 정보](https://releases.xamarin.com/stable-release-cycle-9/)
