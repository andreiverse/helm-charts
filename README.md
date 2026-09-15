# helm-charts

## qbittorrent and qui

this helm chart has qui and qbittorrent, refer to the default `values.yaml` file, for storage, here's an example for using host paths:

```yaml
persistence:
    config:
    enabled: true
    size: 1Gi
    accessMode: ReadWriteOnce
    hostPath: /mnt/hdd01/qbittorrent/config
    downloads:
    enabled: true
    size: 100Gi
    accessMode: ReadWriteMany
    hostPath: /mnt/hdd01/qbittorrent/downloads
```

make sure to set affinitty if using host path:

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
        - matchExpressions:
            - key: kubernetes.io/hostname
              operator: In
              values:
                - server.andrei.lan
```

#### post install qui

1. login with the temporary password from qbittorrent pod
2. disable localhost auth
3. add the instance to qui as localhost:8080 with no auth