# Reference
https://malwareanalysis.tistory.com/280

# What is service mesh?
- Infrastructure layer as auth, security, routing
- Istio is used for service mesh with K8S
# Istio
- Service mesh controller 
## Istio architecture
- Data Plane / Control Plane
- Controll Ingress traffic into Istio service mesh
### Data Plane
- in charge of **network connection between micro services**
- Sidecar pattern. Envoy proxy handle all requests first between micro services
- Envoy proxy
### Control Plane
- in charge of **Envoy proxy routing configuration**
- **Envoy proxy controll DNS routing and endpoint**
  (eg. localhost:8080 -> envoy proxy listener A -> envoy.io)
## Istio injection
- enable envoy proxy for specific pod
```bash
istio-injection=enabled
```
## Istio DNS capture
- DNS request redirect to Envoy Proxy
- Envoy proxy directly redirect logical host via DNSㅑ

| **항목**                 | **Istio 미사용 시 (기본 Kubernetes)**                | **Istio 사용 시 (Sidecar + DNS Capture + Mesh)**        |
| ---------------------- | ---------------------------------------------- | ---------------------------------------------------- |
| **DNS 해석**             | CoreDNS가 외부 도메인(example.com)을 upstream DNS로 전달 | Envoy가 자체적으로 해석하거나 ServiceEntry를 통해 처리               |
| **트래픽 흐름**             | 앱 → CoreDNS → 외부 IP로 직접 요청                     | 앱 → Envoy sidecar → (xDS 라우팅) → 외부 서비스               |
| **라우팅 제어**             | 없음 (기본 IP-level 연결)                            | 가능 (VirtualService, DestinationRule로 host 기반 제어)     |
| **mTLS 적용**            | 불가능                                            | 가능 (외부 서비스에도 적용 가능, 단 MESH_EXTERNAL)                 |
| **모니터링/Telemetry**     | 불가                                             | 가능 (Envoy를 통과하므로 트래픽 가시화 가능)                         |
| **실패 시 행동 제어 (재시도 등)** | 불가                                             | 가능 (Retry, Timeout, Circuit Breaking 등 설정 가능)        |
| **ServiceEntry 필요 여부** | 필요 없음                                          | 필요 (Envoy가 외부 도메인을 인식하도록 설정해야 함)                     |
| **보안 정책 적용**           | 불가                                             | 가능 (AuthorizationPolicy, PeerAuthentication 등 사용 가능) |