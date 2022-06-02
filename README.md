# Helm Task

## Steps

### In Hello World WebApp folder: open terminal:
- Bulid image from python app by using Dockerfile
```sh
docker build -f Dockerfile -t {docker_id}/webapp-python .
```
- Push image to DockerHub
```sh
docker push {docker_id}/webapp-python
```
- Build Customized Redis Image
```sh
docker pull redis
```
- Tag and Push Customized Redis Image
```sh
docker tag redis {docker_id}/redis
docker push {docker_id}/redis
```
### Helm:
- Create Helm Chart
```sh
helm create python-chart
```
- Check on identation 
```sh
helm lint ./python-chart
```
- Install helm and define release name 
```sh
helm install {Release Name} ./python-chart
```

![Build Status](https://raw.githubusercontent.com/mostafahassan097/Deploy-Python-WebApp-with-Redis-Using-Docker-and-Helm-Chart/main/Imgs/1.png?raw=true)

![Build Status](https://raw.githubusercontent.com/mostafahassan097/Deploy-Python-WebApp-with-Redis-Using-Docker-and-Helm-Chart/main/Imgs/2.png?raw=true)

### Installing kube-prometheous-stack:
- Add helm repo
```sh
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```
- Install Prometheus
```sh
helm install prometheus  prometheus-community/kube-prometheus-stack
```
- Show Services:
```sh
kubectl get svc
```
- Prometheus itself:
```sh
kubectl port-forward svc/prometheus-operated 9090
```
In your browser: 127.0.0.1:9090
![Build Status](https://raw.githubusercontent.com/mostafahassan097/Deploy-Python-WebApp-with-Redis-Using-Docker-and-Helm-Chart/main/Imgs/3.png?raw=true)

- Grafana
```sh
kubectl port-forward deployment/prometheus-grafana 3000
```
In your browser: 127.0.0.1:3000
> Note: grafana-username: admin , grafana-password: prom-operator
![Build Status](https://raw.githubusercontent.com/mostafahassan097/Deploy-Python-WebApp-with-Redis-Using-Docker-and-Helm-Chart/main/Imgs/4.png?raw=true)
![Build Status](https://raw.githubusercontent.com/mostafahassan097/Deploy-Python-WebApp-with-Redis-Using-Docker-and-Helm-Chart/main/Imgs/5.png?raw=true)

