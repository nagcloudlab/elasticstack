

https://github.com/elastic/helm-charts


## elasticsearch

minikube start --cpus 6 --memory 10240

helm install elasticsearch elastic/elasticsearch -f /home/nag/elasticstack/helm-charts-main/elasticsearch/examples/minikube/values.yaml

kubectl get statefulset elasticsearch-master -w

kubectl get/delete pvc elasticsearch-master-elasticsearch-master-1

kubectl port-forward service/elasticsearch-master 9200




## kibana

helm install kibana-new elastic/kibana

kubectl port-forward service/kibana- 5601