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
- Envoy proxy directly redirect logical host via DNS