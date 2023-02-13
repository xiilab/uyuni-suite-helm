# uyuni-suite-helm

## clone repository 

```
git clone https://github.com/xiilab/uyuni-suite-helm.git
```

## change value.yaml

```yaml
uyuni:
  common:
    nameOverride: ""
    fullnameOverride: ""

    serviceAccount:
      # Specifies whether a service account should be created
      create: false
      # Annotations to add to the service account
      annotations: { }
      # The name of the service account to use.
      # If not set and create is true, a name is generated using the fullname template
      name: ""

    # 호스트 네임이 있을때 적용
    ingress:
      # true : 호스트 네임 / false : 아이피로 접속
      enabled: false
      className: "nginx"
      annotations: { }
      # kubernetes.io/ingress.class: nginx.conf
      # kubernetes.io/tls-acme: "true"
      hosts:
        - host: test.uyuni-suite.xiilab.com
          paths: []
      tls: [ ]
      #  - secretName: chart-example-tls
      #    hosts:
      #      - chart-example.local

    # 접속 포트 설정
    service:
      type: NodePort
      nodePort: "30100"
   
    # 키클락 설정
    keycloak:
      url: "http://192.168.1.235:30051/auth"
      # 폐쇄망에서 키클락 호스트가 있을경우에 사용
      hostAliases: []




  # 프론트엔드 설정
  frontend:
    replicaCount: 1

    image:
      repository: xiilab/uyuni-suite-frontend
      pullPolicy: IfNotPresent
      # Overrides the image tag whose default is the chart appVersion.
      tag: "0.4.38-stag"

    imagePullSecrets: []
    podAnnotations: {}
    podSecurityContext: {}
    # fsGroup: 2000
    securityContext: {}

```


## install

```
helm install -f values.yaml .
```


