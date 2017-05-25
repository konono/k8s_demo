# k8s_demo
k8s deploy for single host machine

## DEMO
sudo apt install ttyrec
git clone https://github.com/konono/k8s_demo
cd conjure-up/demo
ttyplay conjure-up_k8s.tty

### 前提
Ubuntu 16.04 LTSの最新版がインストールされていること

### 最新のパッケージにアップデート
```
sudo apt update
sudo apt upgrade
```

### apparmor lxcコンテナがおかしくなってしまうのでapparmorを今回はOFFにします

```
sudo systemctl stop apparmor.service
sudo update-rc.d -f apparmor remove
sudo systemctl disable apparmor.service
```

### アップデートをしたのでreboot
```
sudo reboot
```

### conjure-upのインストール
```
sudo snap install conjure-up --classic
```

### conjure-upを使ってk8sをdeploy
```
conjure-up kubernetes
```

### tui画面で下記を選択

```
kubernetes core
Deploy new self-hosted controller
localhost
```

### kubectlをホストにインストール

```
snap install kubectl --classic
mkdir -p ~/.kube/
juju scp kubernetes-master/0:config ~/.kube/config
```

### 動作確認

```
kubectl cluster-info
kubectl get pods -o wide --all-namespaces
```

conjure-up はjujuをつかってdeployしていることがわかる

```
juju status
juju config kubernetes-master
juju config kubernetes-worker
```
