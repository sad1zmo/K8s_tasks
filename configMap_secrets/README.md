Создание секртеа для докер регистри:

kubectl create secret docker-registry regcred --docker-server=registry.rebrainme.com --docker-username=pull-creds --docker-password=glpat-vnpL_iv7WxdzB2QQuKEE -o yaml > regcred.yaml
kubectl apply -f regcred.yaml

получить секрет в человекочитаемом виде:

kubectl get secrets regcred -o jsonpath='{.data.*}' | base64 -d