kubectl get pods -A -o | grep "노드풀 이름"

kubentl get nodes -o wide 

kubectl cordon 노드풀 노드풀 (여러개가 있을 경우에)

kubentl get nodes -o wide 
#기존의 노드풀은 스케줄 disabled가 걸림

kubectl drain  