# User Manaual

# 1. 주요사양

## 1.1 Fetures/주요 특장점

| 항목 | 내용 |
| --- | --- |
| MCU | ARM CORTEX-M0(48Mhz,32bit() |
| Motor | Coreless DC Motor |
| 입력 전압 | 7~13V |
| 통신 속도 | 9600bpx ~ 115200bps |
| 위치 해상도 | 4096 |
| 서모 전류 | Idle : 30mA
Rated : 380mA
Stall : 1.6A |
| 통신 방식 | RS-485 |
| Stroke | 27mm(최대 30mm) |
| Rated Load | 12N~100N |
| 최대 허용 부하 |  정격 부하의 2배 |
| Duty Cycle | under 50%(정격 부하 시) |
| 위치 정밀도 | 단방향 ±0.03mm
양방향 ±0.06mm |
| 전류 feedback 오차 | ±15%(at over 50mA) |
| 위치 센서 | Potentiomenter |
| 크기 | 57.4(L) x 29.9(W)x15(H)mm |
| 무게 | 45~52g |
| Protocol | 자체 Protocol
Modbus RTU |
| 기어비 | 10:1(12F,20F,35F) / 20:1(55F) / 50:1(100F) |
| 기구 백래쉬 | 0.03mm |

<aside>
⚠️ 사용 시 주의사항
1. 제품 동작시 로드(Rod)에 무리한 힘으로 누르지 마십시오
2. 모터의 수명을 위해 정격 부하 이하의 조건에서 사용하여 주시기 바랍니다.
3. Duty Cycle 50%이하로 설정하여 주십시오

</aside>

<aside>
🚫 서보모터에 정격 전압에 맞게 전원인가를 하여 주십시오

</aside>

## 1.2 성능 그래프

![Untitled](User%20Manaual/Untitled.png)

# 2. Data Map

| 주소 | Size | 이름 | 접근 | 기본값 | 범위 |
| --- | --- | --- | --- | --- | --- |
| 0x00 | 2 | https://www.notion.so/User-Manaual-43e386946af54c429a275d71357cfd6c | R | - | - |
| 0x02 | 1 | Version of Firmware | R |  |  |
| 0x03 | 1 | ID | RW | 0 | 0~254 |
| 0x04 | 1 | Baud Rate | RW | 32 | 9600~115200 |
| 0x06 | 2 | Short Stroke Limit | RW | 0 | 0~4096 |
| 0x08 | 2 | Long Stroke Limit | RW | 3686 | 0~4096 |
| 0x0a | 1 | Protocol Type | RW | 1 | 0~1 |
| 0x0d | 1 | Min Voltage Limit | R | 70 |  |
| 0x0e | 1 | Max Voltage Limit | R | 130 |  |
| 0x10 | 1 | Feedback Return Mode | RW | 1 | 0~2 |
| 0x11 | 1 | Alarm LED | RW | 33 | 0~255 |
| 0x12 | 1 | Alarm Shutdown | RW | 33 | 0~255 |
| 0x13 | 1 | Start Compliance Margin | RW | 개별 SPEC | 0~255 |
| 0x14 | 1 | End Complicance Margin | RW | 기본값 | 0~255 |
| 0x15 | 2 | Speed Limit | RW | 1023 | 0~1023 |
| 0x18 | 2 | Calibration Short Stroke | R | 개별 SPEC |  |
| 0x1a | 2 | Calibration Long Stroke | R | 개별 SPEC |  |
| 0x21 | 1 | Acceleration Rate | RW | 개별 SPEC | 0~255 |
| 0x22 | 1 | Deceleration Rate | RW | 개별 SPEC | 0~255 |
| 0x23 | 1 | Current I Gain | RW | 개별 SPEC | 0~255 |
| 0x24 | 1 | Current P Gain | RW | 개별 SPEC | 0~255 |
| 0x25 | 1 | Speed D Gain | RW | 개별 SPEC | 0~255 |
| 0x26 | 1 | Speed I Gain | RW | 개별 SPEC | 0~255 |
| 0x27 | 1 | Speed P Gain | RW | 개별 SPEC | 0~255 |
| 0x2e | 1 | MIn Position Calibration | RW | 개별 SPEC | 0~255 |
| 0x2f | 1 | Max Position Calibration | RW | 개별 SPEC | 0~255 |
| 0x34 | 2 | Current Limit | RW | 800 | 0~1600 |
|  |  |  |  |  |  |

## 2.3 RAM 영역

| 주소 | 크기(byte) | 명칭 | 접근 | 기본값 | 범위 |
| --- | --- | --- | --- | --- | --- |
| 0x80 | 1 | Force On/Off | RW | 0 | 0~1 |
| 0x81 | 1 | LED | RW | 0 | 0~255 |
| 0x86 | 2 | Goal Position | RW | 0 | 0~4095 |
| 0x88 | 2 | Goal Speed | RW | Speed Limit | 0~1023 |
| 0x8a | 2 | Goal Current | RW | Current Limit | 0~1600 |
| 0x8c | 2 | Present Position | R |  | 0~4095 |
| 0x8e | 2 | Present Current | R |  | 0~1023 |
| /0x90 | 2 | Present Motor Operating Rate | R |  | 0~1600 |
| 0x92 | 1 | Present Voltage | R |  | 0~255 |
| 0x96 | 1 | Moving | R |  | 0~1 |

## 2.4 Data Description

### Model Number

Actuator의 모델 번호입니다.

모델을 구별하고 인지하기 위해 사용됩니다

### Version of Firmware

펌웨어 버전 정보가 저장되어 현재  Actuator의 Firmware 버전이 최신인지 확인하여 최신 Firmware로 유지하도록 합니다.

### ID

통신 상에서 복수의  Actuator를 사용할 경우 각각 식별하기 위한 고유 번호 입니다.

**IR Protocl**
0~253까지 사용 가능하며, 254는 브로드캐스트 ID로 특수하게 사용됩니다.

**Modbus RTU**
1~247까지 사용 가능하며, 0은 브로드캐스트 ID로 특수하게 사용됩니다.

브로드캐스트 ID로 통신을 전송하면 모든 창치에 명령을 내릴 수 있습니다.

<aside>
⚠️ 연결된 Actuator의 ID를 중복되어 사용하지 않도록 주의 해야 합니다. ID가 중복되면 통신 중 Packet 충돌로 인하여 정상적인 통신이 이루어지지 않습니다.

</aside>

### Baudrate

Actuator를 제어하기 위한 통신 속도 입니다.

통신 속도를 변경하고자 할 때에는 Actuator의 시스템을 재 시작 해야 합니다.
단위는 bps로 Bit per seconds의 약자로 초당 전송가능한 bit의 수를 의미한다.

| 설정값 | 통신속도(bps) |
| --- | --- |
| 16(0x010) | 115200 |
| 32(0x20) | 57600 |
| 48(0x30) | 38400 |
| 64(0x20) | 19200 |
| 128(0x80) | 9600 |

<aside>
⚠️ Firmware Version 1.5이하에서는 38400bps는 지원하지 않습니다

</aside>

### Short/Long Stroke Limit

Short Stroke(A)또는 Long Stroke(C)상태의 한계 위치 값으로 Goal Position의 최대/최소 값이 됩니다. Goal Position값이 Short Stroke Limit 값보다 작을 경우 또는 Long Stroke Limit 값보다 클 경우 Stroke
Limit값으로 치환됩니다

![Untitled](User%20Manaual%2043e386946af54c429a275d71357cfd6c/Untitled%201.png)

### Protocol Type

통신 Protocol 방식을 선택합니다.

| 설정값 | Protocol | 설명] |
| --- | --- | --- |
| 0(0x00) | Own Protocol | 자체 통신 Protocol |
| 1(0x10) | Modbus RTU | 산업용 RS485 표준 통신 Protocol |

<aside>
⚠️ Firmware Version 1.5이하에서는 Own Protocol만 지원 하며, 해당 파라메터가 존재하지 않습니다.

</aside>

### High/Low Volatge Limit

### Motor Operating Rate

### Feedback Return Mode

### Alarm Led

### Alarm Shutdown

### Start/End Compliance Margin

### Speed Limit

# 3. 조립 예시

# 4. 유지보수

# 5. 참고자료

🧰
