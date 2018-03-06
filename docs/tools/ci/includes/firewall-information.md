## <a name="firewall-configuration"></a>방화벽 구성

Xamarin 테스트 클라우드로 전송 될 테스트에 대 한 순서로 테스트를 전송한 컴퓨터 테스트 클라우드 서버와 통신할 수 있어야 합니다. 에 있는 서버에서 네트워크 트래픽을 허용 하도록 방화벽을 구성 해야 **testcloud.xamarin.com** 포트 80 및 443입니다. DNS에서 관리 하는이 끝점 및 IP 주소는 변경 될 수 있습니다. 

일부 경우에는 테스트 (또는 테스트를 실행 하는 장치) 방화벽에 의해 보호 되는 웹 서버와 통신 해야 합니다. 이 시나리오에서는 다음 IP 주소에서 트래픽을 허용 하도록 방화벽을 구성 해야 합니다.

* **195.249.159.238**
* **195.249.159.239**