---
title: "[임베디드 기초] 4강 - GPIO"
date: 2023-08-17
categories: [Dev, Embedded]
tags: [embedded_basic]
render_with_liquid: false
---

## 환경 구축

- 환경 구축 완료되는 시점 : 컴파일 + HelloWorld가 출력되는 상황 + 디버깅이 되는 상황

  

STM32 Cube IDE를 쓰는 이유?  

1. 무료.
2. ST제품은 세팅만으로 기본 코드가 완성됨

  

* * *

## STM32CubeIDE 프로젝트 생성

![](/assets/img/Embedded_Basic/04/image.png)

  

  

### STM32F103C8T6 칩 선택하기

PRODUCT INFO에서 칩에 대한 선택을 하고, 리스트에서 동일한 모델명을 갖는 애를 찾으면 된다.

추가로, 칩 선택 후 우측 상단에서 데이터 시트도 다운 받을 수 있음.

![](/assets/img/Embedded_Basic/04/image2.png)![](/assets/img/Embedded_Basic/04/image3.png)![](/assets/img/Embedded_Basic/04/image4.png)

  

## STM32F103C8T6 데이터 시트 까보기

칩은 암묵적으로 검정색 점이 있는 곳이 1번 핀이다.

칩에도 자세히 보면 점이 있다.

![](/assets/img/Embedded_Basic/04/image5.png)![](/assets/img/Embedded_Basic/04/image6.png)

  

자, 이제 다시  IDE로 넘어와서 Next를 누르면 아래와 같은 창이 뜨는데, 이름을 기입하고 Finish를 누른다.

![](/assets/img/Embedded_Basic/04/image7.png)  

  

perspective now? 라는 다이얼로그가 뜨면 Yes를 누르고 기다린다.

![](/assets/img/Embedded_Basic/04/image8.png)  

  

그럼 이렇게 생긴 유아이가 뜨고, 각 핀별로 기능을 쉽게 할당할 수 있다!

![](/assets/img/Embedded_Basic/04/image9.png)  

  

## 

* * *

## 이제 보드를 연결해보자

![](/assets/img/Embedded_Basic/04/54301FEA-BCC1-48E7-9F73-6D13447979B9.jpg)

ST Link로 연결하면 전원도 함께 들어간다. 이렇게 연결하면 된다.

  

## 코드를 보자

ST 로그인을 안하면 아래와 같이 메세지가 뜨면서 코드가 생성이 안된다.

ST 계정 생성을 하고 로그인 한 뒤 Project > Generate Code를 선택한다.

![](/assets/img/Embedded_Basic/04/image10.png)![](/assets/img/Embedded_Basic/04/image11.png)  

  

  

###  main.c 열어보기

![](/assets/img/Embedded_Basic/04/image12.png)  

코드를 짤 때 주의할 점이 있는데, USER Code Begin Includes와 End Includes 사이에 내 코드를 넣어야 한다. 💥다른데에 넣으면 안된다!💥

ioc에서 GPIO설정 등을 바꾸고 `Ctrl`+`S`로 저장을 하고 제너레이트 코드하게되면 코드를 자동으로 만들어주는데, 저 위치에 넣은 코드가 아니면 다 날아간다.

그리고 주석을 한글로 달면 깨진다.   

  

## 맨 처음 타는 코드인 HAL\_Init()에서부터 디버깅 해보기

main() 함수에 있는 HAL\_Init() 함수 위치에 중단점을 찍고 디버그 버튼을 눌러서 디버깅을 해보자.

다이얼로그가 뜨면 OK를 누르고, 새로운 버전이 있는 것 같다~ 하면 NO, 그 다음에 파일 포함 여부에서는 OK를 누른다.

![](/assets/img/Embedded_Basic/04/image13.png) 

→ 만약 ST Link가 연결이 안되어있으면 이런 에러가 뜬다.

![](/assets/img/Embedded_Basic/04/image14.png)

 → OK를 누르면 업데이트하도록 다이얼로그가 뜨고, 그 창에서 ST Link 업데이트를 진행하면 이 에러는 사라진다.

  

(만약 나중에 STLink  Utility를 이용해 업데이트 하는 방법이 필요하다면 4강의 STDLink 커넥션하기를 다시 보자.)

이러한 에러를 다 해결하고 나면 디버깅 뷰로 바뀐다.

  

## 핀 세팅하기

ioc를 더블클릭해서 핀세팅 뷰로 바꾸고, System Core > SYS를 선택한다.

그리고 

![](/assets/img/Embedded_Basic/04/image15.png)![](/assets/img/Embedded_Basic/04/image16.png)![](/assets/img/Embedded_Basic/04/99a40e2f-047c-4956-ae74-4e4a534e8049.png)  

보통 시리얼 와이어를 선호한다. → 핀 2개만 이용해서(핀을 아껴서) 컨트롤 가능해서.

그럼 이렇게 우측 뷰에서 핀에 하이라이트가 된다. (이것이 바로 이 IDE의 장점!!!)

  

  

그리고 저장을 하고 Code generate를 하자.

  

디버깅을 해보기 위해서, 아까 말했던 HAL\_Init(), SystemClock\_Config() 에 중단점을 찍고,

while(1) 반복문 안에는 헬로월드를 찍을 수 없으니, HAL\_Delay를 통해 딜레이를 줘보자. 그 결과는 아래와 같다.

![](/assets/img/Embedded_Basic/04/image17.png)  

  

임베디는 운영체제가 없는 코드를 짜게 되고, 우리가 직접 운영체제를 짜게 되는데

임베디드는 while문 하나, 루프 하나에서 다 돈다고 보면 된다.

우리는 직접 운영체제를 짜기 때문에 컴파일러가 다르다.

  

## GPIO를 제어해보자.

우선 회로도를 한 번 보자. (회로도는 키트 구매자에게 제공되는 pdf라서 첨부하지 않았습니다.)

  

가운데 나와있는 CPU 회로도를 보면 1~24번 핀까지 그려져 있는데, 저 핀이 우측 데이터 시트에서 봤던 핀 번호랑 동일한거다.

![](/assets/img/Embedded_Basic/04/image18.png)![](/assets/img/Embedded_Basic/04/image5.png)  

  

LED를 한 번 연결해볼건데, LED는 핀 중 PC13이라는 GPIO를 제어하면 되고, LED는 보드상에서 D2라는 표시가 되어있는 곳에 있다.

D2는 아래 그림에 표시해두었다.

![](/assets/img/Embedded_Basic/04/image19.png)![](/assets/img/Embedded_Basic/04/image20.png)  

  

### 이제 PC13이라는 핀을 제어해보자.

PC13핀을 누르고 GPIO\_Output을 할당한다.

카테고리에서 GPIO를 선택하고, 해당 핀을 선택하면 하단에 Configuration을 설정할 수 있게 된다.  

그럼 아래 그림과 같이 항목을 선택해준다. 각 항목이 선택된 이유는 다음 강의에서 설명해주신다고 함.

![](/assets/img/Embedded_Basic/04/image21.png) →![](/assets/img/Embedded_Basic/04/image22.png)→ ![](/assets/img/Embedded_Basic/04/image23.png)

  

그 다음 세이브하고 제너레이트 코드한다.

(시청자 질문) DMA도 예외로 볼 수 있지 않냐?

DMA로 와도 내부 인터럽트로 확인이 가능하다.

startup\_stm32f103c8tx.s를 보면 어셈블리 코드가 있고

stm32f1xx\_It.c를 보면 인터럽트 함수가 있다. 이 코드에 핸들러가 있다고 치면, 어셈블리 코드에 매핑이 되어있다.

이건 나중에~ 설명해준다고 하심

  

  

### 핀 제어 코드

HAL\_GPIO\_WritePin() 함수를 이용해 핀을 제어할 것이다.

```cpp
HAL_GPIO_WritePin(GPIOx, GPIO_Pin, PinState);

```

- `GPIOx` : 핀 그룹
- `GPIO_Pin` : 핀 넘버
- `PinState` : 할당할 핀의 상태

어떤 값을 적어줘야 하는지는 헤더파일을 보면 되는데, 헤더쪽에는 아래와 같이 정의가 되어있다. (아까 내가 추가하고 빌드해서 생긴 코드!)

```cpp
/* Private defines -----------------------------------------------------------*/
#define GPIO_LED_Pin GPIO_PIN_13
#define GPIO_LED_GPIO_Port GPIOC

```

  

저기 적혀있는 GPIO\_PIN\_13도 어딘가에 디파인되어있는 애다.

그리고 모두 비트연산을 하고있는 것이다. 

```cpp
#define GPIO_PIN_13 ((uint16_t)0x2000) /* Pin 13 selected */
```

  

![](/assets/img/Embedded_Basic/04/image24.png)
</br>
 → 0x2000을 헥사로 까보면 13번째 비트에 1이 들어가있는걸 볼 수 있다.  

  

그래서 결과적으로 추가할 코드는 아래와 같다

```cpp
while (1)
{
    HAL_GPIO_WritePin(GPIO_LED_GPIO_Port, GPIO_LED_Pin, 1/* HIGH */);
    HAL_Delay(100);
    HAL_GPIO_WritePin(GPIO_LED_GPIO_Port, GPIO_LED_Pin, 0/* LOW */);
    HAL_Delay(100);
}
```

  

### 결과물!

![](/assets/img/Embedded_Basic/04/ezgif.com-video-to-gif.gif)  

  

## GPIO Input을 이용해 스위치로 LED 컨트롤하기

우선 회로도를 보면, PA0이라는 핀을 Input으로 사용하겠다고 표시해두었다.

ioc로 가서 PA0에 GPIO\_Input을 할당한다.

그리고 아래와 같이 Configuration을 설정하고 저장한다.

![](/assets/img/Embedded_Basic/04/image19.png)![](/assets/img/Embedded_Basic/04/image25.png)

### 루프 내 코드

```cpp
if (!HAL_GPIO_ReadPin(GPIO_SW_GPIO_Port, GPIO_SW_Pin)) {
    HAL_GPIO_WritePin(GPIO_LED_GPIO_Port, GPIO_LED_Pin, 0/* LOW */);
}
else {
    HAL_GPIO_WritePin(GPIO_LED_GPIO_Port, GPIO_LED_Pin, 1/* HIGH */);
}
HAL_Delay(100);

```

  

### 결과! 

![](/assets/img/Embedded_Basic/04/ezgif.com-video-to-gif2.gif) 

다음 시간에는 코드 분석을 해보고, 라이브러리 안쓰고 직접도 해보고~ 할 것이ㅏㄷ.
