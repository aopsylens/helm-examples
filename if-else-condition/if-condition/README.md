# If condition

There `if` condition for dynamic construction change of file

If you want to create some construction in file when variable matches condition:

1. Create some variable in values.yaml, e.g.
```
ingress:
  tls: ""
```

2. Create construction and put some data to it
```
{{- if .Values.ingress.tls }}
  tls:
    - hosts:
        - test.com
      secretName: test
{{- end }}
```

3. Deploy chart with --set flag where you will change your value of variable

If you want to put construction in file, then set `true` to your variable  `--set ingress.tls=true`
`helm upgrade --debug --install --atomic ${CHART_NAME} ${CHART_PATH} --namespace $NAMESPACE --set ingress.tls=true`
If you don't want to put construction in file, then set `false` to your variable `--set ingress.tls=false`
`helm upgrade --debug --install --atomic ${CHART_NAME} ${CHART_PATH} --namespace $NAMESPACE --set ingress.tls=false`