# RPC: Remote Procedure Call

- RPC가 뭔가요?
  - RPC(Remote Procedure Call)은 네트워크에 대한 세부사항을 자세히 모르는 상황에서 원격지에 있는 프로시저(함수)를 호출하고 응답을 받는 등의 작업을 할 수 있게 만들어주는 프로토콜 또는 추상화된 호출 행위 자체를 일컬어 RPC라고 불러요.

- RPC는 어떻게 구현되나요?
  - 실제 구현 방식은 대체로 복잡하며, 다양한 구성요소가 맞물려 포함되어 있기 때문에 흔히 “RPC 프레임워크"라고 부릅니다.
  - 하지만 본질적으로 네트워크 문제의 실제 구현은 메시지를 주고 받는 것 입니다. 그렇기에 RPC의 구성요소는 심플하게는 **"메시지의 형식"(Wire Format)**과 **"메시지를 주고받는 방법"(Wire Protocol)**으로 해부해 볼 수 있습니다.
    - Wire Format은 메시지의 실제 물리적인 표현 즉, [[Codec]]을 의미합니다. 메시지 인코딩 형식으로 분류해보면 크게 텍스트 기반 RPC와 바이너리 기반 RPC를 나눠볼 수 있습니다.
      - 텍스트 기반 RPC의 예시로는 [[JSON-RPC]]가 있습니다. JSON-RPC에선 (특정 스키마를 만족하는) JSON 텍스트가 Wire Format에 해당합니다.
      - 바이너리 기반 RPC의 예시로는 [[gRPC]]가 있습니다. gRPC 통신에선 [[Protocol Buffers]]로 인코딩된 메시지를 주고받습니다.
    - Wire Protocol은 전체 RPC 프로토콜 구현에서 가장 핵심이 되는 부분으로, 어떤 계층에서 어떤 메시지를 어떤 순서로... 즉, RPC가 “어떻게” 동작하는 가에 대한 구현 세부사항에 해당합니다.
      - 언급한 gRPC에 대한 설명은 엄밀하지 않습니다. gRPC 통신에선 "일반적으로" [[Protocol Buffers]]로 인코딩된 메시지를 주고받긴 하지만 항상 그런것은 아닙니다.
        - [[gRPC]]로 주고 받는 메시지의 형식은 [JSON 텍스트일 수도 있습니다](https://grpc.io/blog/grpc-with-json/).
        - [[gRPC]]의 경우 범용목적 RPC 프로토콜로써 설계되었기 때문에 인코딩 방식에 대해 불가지론적 입니다. gRPC의 Wire Protocol 정의에 해당하는 [gRPC-over-HTTP2](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-HTTP2.md)와 [gRPC-Web](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-WEB.md) 스펙에서는 [[Protocol Buffers]]에 대해 직접적으로 언급하지 않습니다.
        - [[gRPC]] 사용자는 실제 메시지 인코딩을 [[Protocol Buffers]]로 하던 [[JSON]]으로 하던 [[MessagePack]]으로 하던 [[FlatBuffers]]로 하던 [[XML]]로 하던 텍스트건 바이너리건 자유롭게 선택할 수 있으며, [[Protocol Buffers]]를 사용하지 않더라도 [[gRPC]] 프로토콜 자체의 이점을 얻을 수 있습니다.
      - 메시지가 인코딩 되는 방식을 결정하는 것과 프로토콜 세부사항에서 독립적인 “물리계층의 문제"로 정의할 수 있습니다. 메시지 형식이 정해져있는지, 느슨한 연관을 가지는지, 아무 의견이 없는지 여부는 특정 RPC 프로토콜이 풀고자 하는 문제 영역에 맞게 전략적으로 선택됩니다.
      - 양방향 스트리밍이나 메시지 부분 전송 같이 다양한 영역에 걸쳐 광범위한 설계가 필요한 문제를 해결하기 위해 때때로 구성에 대한 강한 의견을 가지는 경우가 있습니다. 모든 선택에는 트레이드오프가 따르며 모든 문제에 대해 절대적인 비교우위를 가지는 디자인은 없습니다.

- RPC 프레임워크의 디자인 고려사항
  - 물리 계층에서 푸는 문제
    - 압축률: 메시지를 더 작게 만들 수록 전송해야하는 트래픽이 더 작아진다.
    - 인코딩/디코딩에 필요한 자원: 압축 과정을 더 싸게 만들 수록 처리할 수 있는 트래픽이 더 많아진다.
  - 네트워크에서 푸는 문제
    - 트랜스포트 뭐 써야하지? over [[TCP]]? [[UDP]]? [[HTTP]]? [[QUIC]]?
    - 멀티플렉싱, 요청 신뢰성, 혼잡 제어 등 어떤 네트워크 기능을 요구하는가
    - 플랫폼에 포함된 네트워크 기능을 쓰는가, 저수준에서 자체적으로 구현하는가
      - 예시: gRPC-over-HTTP2는 [[HTTP2]]의 세부사항을 이용해서 커스텀 프로토콜을 정의함. 이 경우 [[HTTP2]]의 최적화 기법들을 활용하면서 필요한 부분을 커스터마이징 할 수 있지만 기존 [[HTTP]] 의미론을 따르지 않기 때문에 이식성이 매우 떨어지게 됨
  - 애플리케이션에서 푸는 문제
    - 언어: 자체 [[DSL]]을 제공하면 플랫폼 독립적일 수 있으나 프로그래밍 언어와 멀수록 추가 학습비용을 수반
    - 통합: 실제 코드 호출 수준으로 추상화하기 위한 코드(Stub) 생성과 동기화 전략
      - 예시: 애초에 [[프로그래밍 언어]]를 직접 사용하거나, 언어에서 제공하는 매크로 시스템을 사용하면 더 효과적으로 통합 할 수 있지 않을까?
    - 런타임: 그래서 실제 실행환경, 플랫폼에서 어떻게 가장 효과적으로 구현 가능한가?
      - 예시: 웹에선 [[HTTP2]] 세부사항를 제어할 수 있는 API가 없기 때문에 gRPC-over-HTTP2 를 구현할 수 없으며 대안으로 (엄청나게 비효율적인 호환용 프로토콜인) gRPC-Web을 구현해서 사용함

- 인터페이스 언어([[IDL]])와의 상관관계
  - 인터페이스 언어 자체가 특정 RPC 프로토콜에서 요구하는 제약사항들을 설명하기 위해 존재하거나 깊은 연관관계를 가지는 경우가 많지만, 대부분의 경우 언어로써 독립적입니다.
    - 특정 RPC 프레임워크의 [[IDL]]이 원래 의도하지 않는 용도로 사용하는 예시
      - [[Twirp]]: [[Protocol Buffers]] [[IDL]]과 [[직렬화]] 형식을 사용하는 독립적인 RPC 프레임워크입니다. [[gRPC]]와 아무런 연관이 없습니다.
      - [[Avro]]: [[직렬화]] 형식은 자체적으로 정의하지만 [[IDL]]로는 [[JSON]] 기반 스키마 언어를 씁니다.
      - [[MessagePack-RPC]]: [[MessagePack]] 기반의 RPC 프레임워크이지만, [[IDL]]은 [[Thrift]] 것을 가져다 씁니다.
    - 이 밖에도 아예 RPC가 아닌 다른 목적으로 사용되는 경우가 많이 있으나 너무 많아서 생략

- 대표적인 RPC 프레임워크 (스펙과 프레임워크가 명확히 존재하는 것만 명시)
  - [[JSON-RPC]]
    - [JSON-RPC v2 Spec](https://www.jsonrpc.org/specification)
  - [[gRPC]]
    - [gRPC-over-HTTP2](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-HTTP2.md)
    - [gRPC-Web](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-WEB.md)
  - [[Thrift]]
    - [Thrift Protocol Spec](https://github.com/apache/thrift/blob/master/doc/specs/thrift-protocol-spec.md)
  - [[GraphQL]]
    - [GraphQL-over-HTTP](https://github.com/graphql/graphql-over-http/blob/main/spec/GraphQLOverHTTP.md)
    - [GraphQL-over-WebSocket](https://github.com/enisdenjo/graphql-ws/blob/master/PROTOCOL.md)
  - [[MessagePack-RPC]]
    - [MessagePack-RPC Spec](https://github.com/msgpack-rpc/msgpack-rpc/blob/master/spec.md)
  - [[Avro]]
    - [Avro Protocol Declaration](https://avro.apache.org/docs/current/spec.html#Protocol+Declaration)
  - [[Twirp]]
    - [Twirp Wire Protocol v7](https://twitchtv.github.io/twirp/docs/spec_v7.html)
