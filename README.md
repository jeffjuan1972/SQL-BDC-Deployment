# SQL-Server-BDC-單一節點佈署
### 硬體基本規格
1. VM : 8 core CPU, 16GB RAM , 100GB Disk Ubuntu20.04
2. VM : 4 core CPU, 8GB RAM, 100GB Disk Windows Server 2019 std

### 01 Windows 主機
1. 安裝 Chrome
2. 開啟 Chrome，下載 PowerShell script file: WindowsTools.ps1
3. 執行 WindowsTools.ps1 (右鍵點選 Run with PowerShell)
4. 複製 ssh public key 至測試主機自建資料夾 ssh_key
5. 開啟命令提示字元，連線 ubuntu 主機
```
  ssh -i <ssh key file path> account@ip
  EX : ssh -i C:\Users\jeffjuan\Desktop\ssh_key\vm0710-u_key.pem jeffjuan@65.52.172.51
```
 
### 02 Ubuntu
1. Patch Unbuntu
```
sudo apt update && sudo apt upgrade -y
sudo systemctl reboot
```
2. 下載安裝 k8s 指令
```
curl -O https://raw.githubusercontent.com/jeffjuan1972/SQL-BDC-Deployment/main/single-node-kubeadm.sh
```
3. 安裝 kubernetes
```
sudo chmod +x single-node-kubeadm.sh
sudo ./single-node-kubeadm.sh
```
4. 安裝完成後，測試 docker
```
sudo docker —version
```
5. 測試 kubernetes
```
sudo kubectl get nodes
```
6. Pull docker image 指令
```
curl -O https://raw.githubusercontent.com/jeffjuan1972/SQL-BDC-Deployment/main/PrePull-Docker-images.sh
```
7. 執行指令下載bdc需要的docker image 
```
sudo chmod +x PrePull-Docker-images.sh
sudo ./PrePull-Docker-images.sh
```
### 03 建置 PV

#### BDC 相關image
mssql-app-service-proxy
mssql-control-watchdog
mssql-controller
mssql-dns
mssql-hadoop
mssql-mleap-serving-runtime
mssql-mlserver-py-runtime
mssql-mlserver-r-runtime
mssql-monitor-collectd
mssql-monitor-elasticsearch
mssql-monitor-fluentbit
mssql-monitor-grafana
mssql-monitor-influxdb
mssql-monitor-kibana
mssql-monitor-telegraf
mssql-security-knox
mssql-security-support
mssql-server-controller
mssql-server-data
mssql-ha-operator
mssql-ha-supervisor
mssql-service-proxy
mssql-ssis-app-runtime

相關工具下載：
### 1. WindowsTools.ps1
在 Windows 主機下載安裝以下工具
  <li>azure-data-studio</li>
  <li>azure-cli</li>
  <li>kubernetes-cli</li>
  <li>curl</li>
  <li>putty</li>
  <li>notepadplusplus</li>
  <li>7zip</li>
  <li>qlserver-cmdlineutils</li>
 
### 2. single-node-kubeadm.sh
 安裝 Kubernetes 指令
 
### 3. PrePull-Docker-images.sh
 下載所有 BDC 需要的 Docker images 

### 4. setup-volumes-agent.sh
   為 persistant volumes 建立 volumes
