# Rook-Ceph

Original Release: https://github.com/rook/rook/releases/tag/v1.0.4

## GKE固有の設定

- FlexVolumeのPathが普通じゃない。

```
        - name: FLEXVOLUME_DIR_PATH
          value: "/home/kubernetes/flexvolume"
```

- ノードプールのデフォルトOS(cos)だとRBD Kernel Moduleが使えないので、Ubuntuを選択する必要がある。

## Defaut storageclassの変更

```
kubectl patch storageclass standard -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"false"}}}'
kubectl patch storageclass rook-ceph-block -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```