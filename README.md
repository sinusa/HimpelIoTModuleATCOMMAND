# Himpel IoT Module AT COMMAND 메시지 규격

- # 준비
  - ### UART Config
    | 항목       | 설정값       |
    |------------|--------------|
    | Baudrate   | 115200       |
    | Stop Bits  | Stop Bit 1   |
    | Data Bits  | 8 Bit        |
    | Flow Ctrl  | Disable      |

- # AT COMMAND 규칙
  - ## 메시지 필드
  - ### prefix
    | 명령어       | 주체              | 설명                                              |
    |--------------|-------------------|---------------------------------------------------|
    | DEVICEREADY  | Slave             | 연동 준비가 완료되었음을 알림                    |
    | FACRESET     | Master            | 모듈을 공장초기화하고, onboarding 상태로 진입     |
    | ONBOARD      | Master            | 모듈이 onboarding 상태로 진입                    |
    | REQ          | Master / Slave    | 정보 요청, body는 JSON으로 정의                  |
    | SET          | Master / Slave    | 정보 설정, body는 JSON으로 정의                  |
    | RESP         | Master / Slave    | 정보 요청/설정에 대한 응답, body가 있으면 JSON으로 정의 |

  - ### Response
    | 코드 | 설명       |
    |------|------------|
    | OK   | 성공 응답  |
    | NOK  | 실패 응답  |

  - ### Body
    - 발신측의 Command 가 REQ, SET , RESP 인 경우 json 형태의 body 를 포함한다. body 의 마지막 데이터에 반드시 CRLF ( 0x0D, 0x0A ) 를 포함한다.

  - ### Checksum
    - 메시지기 첫 prefix 부터 body 까지의 모든 데이터를 Ad
 
  - ## 메시지 포맷
    <pre>
    ┌────────┬──────────┬───────────────┬──────────────────────┬────────────┐
    │ Prefix │ Command  │ Delimiter " " │        Body?         │  Checksum  │
    └────────┴──────────┴───────────────┴──────────────────────┴────────────┘
    </pre>
