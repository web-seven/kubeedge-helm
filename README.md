Cleanup Edge Side
```bash
sudo rm -R /etc/kubeedge/
sudo rm -R /var/lib/edged/
sudo rm -R /var/lib/kubeedge/
docker rm -f $(docker ps -a -q)
kubectl delete ns kubeedge
```

Install Cloud Side
```bash
kubectl create ns kubeedge
helm -n kubeedge upgrade --install cloudcore ./charts/cloudcore/
```

Start Edge Side
```bash
kubectl get secret -nkubeedge tokensecret -o=jsonpath='{.data.tokendata}' | base64 -d
sudo edgecore --config edgecore_default.yaml
```