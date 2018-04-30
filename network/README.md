네트워크
==========================

### 1. 서비스 운영중에 특정 ip 을 block 하면 어떻게 해야 할까요? (가능한 방법을 모두 말해주세요.)

### 답변

제 경험에 기준해서 말씀드리면 dos성 공격을 받고있었고 netstat로 확인해보니 syn_recv 상태를 가지는 중복 세션들이 많이 생성되는 상황이여서 syn_flooding이 의심스러웠는데, 그때는 방화벽을 따로 갖추고 있던 상황이 아니라서 iptable을 이용해서 중복 세션들을 drop 시켰습니다. 
방화벽서버에서 차단 하는 방법도 있습니다.

웹서버 자체에서도 차단 하는 방법도 있습니다. 그런데 웹서버에서 차단 하는 경우에는 웹서버 까지 공격세션들이 접근하면서 부하가 많이 걸려서 가장 좋은 방법은 방화벽 > iptable > 웹서버 순인것 같습니다.

### 1-2 방화벽, iptable, 웹서버, 애플리케이션 외에는 없을까요?

osi 7계층에서 L2 L3 L4 L7 에서 switch를 이용해서 ip를 차단할 수 있으며 L4에서는 iptables를 사용할 수 있고 L7에서는 웹서버 nginx나 apache에서 그리고 was에서도 ip블락을 할수 있습니다.

또한 HAProxy와 같은 프록시를 이용해서 ip를 차단할 수 있습니다.


    OSI 7 
    7 : web server(nginx, apache), was(tomcat), proxy(HAProxy)
    4 : iptable, windows firewall, switch
    3 : switch
    2 : switch

참고자료 

[HAProxy란](http://d2.naver.com/helloworld/284659m)