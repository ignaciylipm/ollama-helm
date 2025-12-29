# Ollama Helm
## Documentación de referencia 
https://github.com/otwld/ollama-helm
https://github.com/ollama/ollama/blob/main/docs/api.md#generate-a-completion

| Actor                                              | Qué hace                                                                                                                                                                                                                                                                             | Qué **no** hace                                                                                                                             |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **Ollama**                                         | - Mantiene un **runtime/servidor de inferencia** para LLMs. <br> - Empaqueta y distribuye modelos optimizados para CPU/GPU (`.llama`, ggml). <br> - Mantiene la **library oficial** (`https://ollama.com/library`). <br> - Administra memoria, carga de modelos y backend (CPU/GPU). | - No entrena los modelos. <br> - No crea modelos nuevos desde cero. <br> - No modifica el contenido de los modelos originales.              |
| **Autores del modelo** (Meta, Mistral, Phi, Qwen…) | - Crean y entrenan los modelos. <br> - Publican pesos originales y especificaciones.                                                                                                                                                                                                 | - No optimizan para Ollama por defecto (Ollama hace la adaptación). <br> - No administra servidores de inferencia de terceros.              |
| **Tú / Usuario**                                   | - Descargas modelos (`ollama pull`). <br> - Ejecutas inferencia (`ollama run`, REST API). <br> - Configuras CPU/GPU, pods en Kubernetes, memoria.                                                                                                                                    | - No necesitas preocuparte de entrenar. <br> - No tienes que lidiar con compatibilidad CUDA/ggml manualmente si usas los modelos oficiales. |


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
```
helm install ollama otwld/ollama --namespace 80-ollama-pro  --values conf/values.yaml
```

Upgrade
```
helm upgrade ollama otwld/ollama --namespace 80-ollama-pro  --values conf/values.yaml
```

## Otros

En el arranque del pod se puede observar
```
 Couldn't find '/root/.ollama/id_ed25519'. Generating new private key.                                                                                                                                                                                  │
Your new public key is ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIEPxewNZ2PfCe6CbJhSqePuCf3liZYCf2a90ZkzUCGvF 
```

## API

Listar modelos
```
curl 10.167.17.10:11434/api/tags
```