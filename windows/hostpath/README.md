## 1. create a pod with hostpath mount(C: disk) on windows
```console
kubectl create -f https://raw.githubusercontent.com/andyzhangx/Demo/master/windows/hostpath/busybox-hostpath.yaml
```

#### watch the status of pod until its Status changed from `Pending` to `Running`
```console
watch kubectl describe po busybox-hostpath
```

## 2. enter the pod container to do validation
```console
kubectl exec -it busybox-hostpath -- cmd

C:\>d:

D:\>dir

 Directory of D:\

09/25/2017  06:29 AM    <DIR>          .
09/25/2017  06:29 AM    <DIR>          ..
               0 File(s)              0 bytes
               2 Dir(s)  97,325,273,088 bytes free
```

## 3. copy some files from pod
```console
kubectl cp busybox-hostpath:/k/kubeletstart.ps1 /tmp/kubeletstart.ps1
```

#### hostPath issues
 - [hostpath.type as `DirectoryOrCreate` does not work on windows](https://github.com/kubernetes/kubernetes/issues/62121)
 - [Deleting pod that had mount a host directory, does not let a new pod mount that directory](https://github.com/kubernetes/kubernetes/issues/68603)
 
| k8s version | fixed version |
| ---- | ---- |
| v1.9 | 1.9.7 |
| v1.10 | 1.10.2 |
| v1.11 | 1.11.0 |
 
