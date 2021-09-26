# Create ConfigMaps/Secrets from files

In Kubernetes for creating configmap from file you use command:

```
kubectl create configmap game-config --from-file=configure-pod-container/configmap/
```

In Helm you can create directory called `files` and put any files in it for creating manifests with these files from `templates` directory.

Examples

Create `files` directory along with `templates` directory

If you need to create configmap with some bash script called `script.sh`:
1) Create file `script.sh` in `files` directory
2) Create file `configmap-script.yaml` in `templates` directory
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: script
data:
  script.sh: |-
{{- $.Files.Get "files/script.sh"  | nindent 4 -}}   
```

If you need to put some data from file to configmap
1) Create file `data.txt` in `files` directory
2) Create file `configmap-data.yaml` in `templates` directory
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: data
data:
  data.txt: {{ .Files.Get "files/data.txt" | quote }}  
```