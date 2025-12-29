# Ollama Helm
## Documentación de referencia 
https://github.com/otwld/ollama-helm

## Instalación

Añadimos el repo
```
helm repo add otwld https://helm.otwld.com/
helm repo update
```

Creamos el namespace
```
kubectl create ns 80-ollama-pro
```

Instalación

helm upgrade ollama otwld/ollama --namespace ollama --values conf/values.yaml

