# TCP/IP

[작성자: 노희재]
</br>
</br>
</br>
💡   이번 발표에선 TCP/IP 를 더욱 자세히 알아보며
TCP/IP 의 흐름과 오류 제어 방식 등에 대해 다루어 보겠습니다.
</br>
</br>
</br>
# TCP/IP 란?

인터넷에서 컴퓨터들이 서로 정보를 주고 받는데에 쓰이는 프로토콜의 집합
</br>
</br>
</br>

# TCP/IP Updated 의 모델
![스크린샷_2022-01-24_오후_10 59 00](https://user-images.githubusercontent.com/85618700/150996561-4f6ba5b5-232e-4fe7-ae13-5881938d6be3.png)
</br>

현대의 인터넷에서 가장 많이 사용되는 TCP/IP Updated 모델은 5개의 계층으로 이루어져 있습니다.
</br>
</br>

1. encoding 과 decoding 이 이루어지는 물리 계층
2. 같은 네트워크에 있는 여러대의 컴퓨터들이 데이터를 주고 받기 위해 필요한 데이터 링크 계층
3. routing, forwarding, segmentation 이 이루어지는 네트워크 계층
4. 최종 목적지인 프로세스까지 데이터가 도달하게 하기 위해 port 번호를 붙이는 전송 계층
5. 응용 프로세스와 직접 관계하여 응용 서비스를 수행하는 응용 계층

</br>
</br>

여기서 TCP/IP 는 각각

IP - 3계층, TCP - 4계층에서 이루어집니다.
</br>
</br>
</br>

# IP

Internet Protocol 의 약자.

소스 IP 와 목적지 IP 를 주어 양끝단의 호스트간의 통신을 책임집니다.

IP 의 특징은 신뢰성 및 흐름 제어 기능이 전혀 없기 때문에

신뢰성을 확보하려면 TCP 와 같은 상위 트랜스포트 계층에 의존해야 합니다.

목적지까지의 Routing 경로를 찾아주는 것이 IP 의 핵심 기능입니다.
</br>
</br>
</br>

# TCP
Transmission Control Protocol 의 약자.   
근거리 통신망이나 인트라넷, 인터넷에 연결된 컴퓨터에서   
실행되는 프로그램 간에 안정적으로, 순서대로, 에러 없이 교환 할 수 있게 합니다.

</br>
</br>

## 3-way Handshake

TCP 통신을 시작하기 전에,

연결을 성립할 준비가 되었는지 검증하는 과정을 말합니다.

![스크린샷_2022-01-25_오전_12 24 21](https://user-images.githubusercontent.com/85618700/150996609-d65d8831-a97f-4718-a57a-ce40facfab8b.png)

</br>
</br>

## 4-way Handshake

TCP 통신을 끝내기 전에,

연결을 해제할 준비가 되었는지 검증하는 과정을 말합니다.

![스크린샷_2022-01-25_오전_1 57 17](https://user-images.githubusercontent.com/85618700/150996586-88138a71-ddd9-4734-9491-5b51fec3841d.png)

</br>
</br>

## 제어

*Acknowledgement

지금까지 보내거나 받은 데이터량을 체크하여 상대방에게 보내는 것을 말합니다.

만약 송/수신자가 300번째 데이터를 받았다면 301번째 데이터를 보내라는 뜻으로 1을 추가하여 301을 보냅니다.

*Negative Acknowledgement

통신 제어용 신호로, 데이터 수신에 에러가 있었음을 확인하는 신호입니다.

*Window Size

한 번에 받을 수 있는 데이터의 양을 말하며 3-way Handshake 때 수신자 측이 정합니다.
</br>
</br>

1. 흐름 제어
    
    데이터의 손실이나 불필요한 송신/수신을 막기 위해
    
    수신자에 따라 송신자의 데이터 전송량을 조절하는 것을 말합니다.
    
    분할된 데이터에는 고유한 번호가 부여 되는데,
    
    이를 바탕으로 데이터가 제대로 전달됐는지 알 수 있기 때문에
    
    데이터 신뢰도가 높지만 속도는 떨어지는 특징을 가집니다.
    
    Stop and Wait, Sliding Window 등이 있습니다.
    
    - Stop and Wait
        
        매번 전송한 패킷에 대한 확인 응답을 받아야 그 다음 패킷을 전송할 수 있기 때문에
        
        비효율적이라는 단점이 있습니다.
        
    - Sliding Window
        
        수신측에서 설정한 윈도우 크기만큼 송신측에서 확인 응답 없이
        
        세그먼트를 전송할 수 있게 하여 데이터 흐름을 동적으로 조절하는 방식입니다.
        
        송신측에서 ACK 프레임을 수신하지 않더라도 여러개의 프레임을 연속으로 전송할 수 있습니다.
        
        </br>
        </br>
    
2. 오류 제어
    
    통신 과정에서 발생한 오류 검출과
    
    데이터가 손실되었다면 재전송을 통해 복구시키는 것을 말합니다.
    
    Stop and Wait ARQ, Go-Back-n ARQ 등이 있습니다.
    
    - Stop and Wait ARQ
        
        송신 측에서 1개의 프레임을 송신하고, 수신측에서 수신된 프레임의 에러 유무에 따라
        
        ACK 혹은 NAK(Negative Acknowledgement) 를 보내는 방식입니다.
        
        식별을 위해 데이터 프레임과 ACK 프레임은 각각 0, 1 번호를 번갈아가며 부여합니다.
        
        수신측에 데이터를 받지 못했을 경우 NAK 를 보내고,
        
        NAK 를 받은 송신측은 데이터를 재전송합니다.
        
        만약 데이터나 ACK 가 분실되었을 경우 일정 간격의 시간을 두고
        
        타임아웃이 되면 송신측은 데이터를 재전송합니다.
        
    - Go-Back-n ARQ
        
        전송된 프레임이 손상되거나 분실된 경우,
        
        그리고 ACK 패킷의 손실로 인한 TIME-OUT 이 발생한 경우,
        
        확인된 마지막 프레임 이후로 모든 프레임을 재전송합니다.
        
        슬라이딩 윈도우는 연속적인 프레임 전송 기법으로
        
        전송측은 전송된 프레임의 복사본을 가지고 있어야 하며, ACK 와 NAK 모두 각각 구별해야 합니다.
        
        - 재전송 되는 경우를 정리해보자면
            1. 전송측은 NAK 프레임을 받았을 경우, NAK 프레임 번호부터 데이터를 재전송합니다.
            2. 수신측은 원하는 프레임이 아닐 경우, 데이터를 모두 폐기 처분합니다.
            3. TIME-OUT 의 경우, 마지막 ACK 된 데이터부터 재전송합니다.

</br>
</br>
        
3. 혼잡 제어
    
    만약 한 라우터에 데이터가 몰릴 경우
    
    자신에게 온 데이터를 모두 처리 할 수 없게 됩니다.
    
    이런 경우 호스트들은 또 다시 재전송을 하고 혼잡도를 가중시켜
    
    오버플로우나 데이터 손실을 유발하는데, 이를 막기 위해
    
    송신측에서 데이터 전송 속도를 줄이는 것을 말합니다.
    
    AIMD, Slow Start, Fast Retransmit, Fast Recovery 등이 있습니다.
    
    - AIMD (Additive Increase Multicative Decrease)
        
        합 증가/곱 감소 알고리즘이라고 합니다.
        
        처음에 패킷 하나를 보내는 것으로 시작하여 전송한 패킷이 문제 없이 도착하면 Window Size 를 1씩 증가시키며 전송하는 방법입니다.
        
        만약 패킷 전송을 실패하거나 TIME-OUT 이 발생하면 Window Size 를 절반으로 감소 시킵니다.
        
        네트워크가 혼잡해지고 나서야 대역폭을 줄이는 방식이라는 단점과
        
        네트워크 수용량 면에서는 효율적으로 동작하지만
        
        처음 전송 속도를 올리는데에 시간이 길다는 단점이 있습니다.
        
    - Slow Start
        
        AIMD 와 마찬가지로 패킷을 하나씩 보내는 것부터 시작하지만
        
        이 방식은 패킷이 문제 없이 도착하면 ACK 패킷마다 Window Size 를 1씩 늘리고
        
        혼잡 현상이 발생하면 Window Size 를 1씩 떨어뜨립니다.
        
        처음에는 네트워크 수용량을 예측할 수 있는 정보가 없지만,
        
        한 번 혼잡 현상이 발생하였던 Window Size 의 절반까지는 이전처럼 지수 함수 꼴로 증가시키고
        
        그 이후부터는 완만하게 1씩 증가시키는 방식입니다.
        
        Slow Start 라는 이름을 사용하지만, 매 전송마다 2배씩 증가하기 때문에
        
        전송되어지는 데이터의 크기는 지수함수의 모습으로 증가합니다.
        
        </br>
        </br>
        </br>
        
# 👋 마치는 말
OSI 7 Layer 발표 때 생략했던 부분들을 다룰 수 있어서 좋았습니다!   
하지만 역시나 네트워크는 팔 수록 많은 지식이 딸려오기 때문에,,   
최대한 자세히 다뤄보려 했지만 이번 시간에도 생략했던 부분들이 있습니다.   
새롭게 알게된 단어들은 꼭 한 번 훑어보시길 바라요!   
</br>
</br>
</br>