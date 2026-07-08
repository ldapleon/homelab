
---

# `docs/cheatsheets/cli-cheatsheet.md`

```markdown
# Homelab CLI Cheat Sheet

Dieses Cheat Sheet enthält häufige Befehle für Troubleshooting und Betrieb des Homelabs.

---

# kubectl

## Cluster Überblick

```bash
kubectl get nodes -o wide
kubectl get pods -A
kubectl get svc -A
kubectl get ingressroute -A
kubectl get storageclass


Ressourcen in einem Namespace anzeigen:

kubectl get all -n <namespace>
kubectl get pods -n <namespace>
kubectl get svc -n <namespace>
kubectl get events -n <namespace> --sort-by=.lastTimestamp


Pod Details:

kubectl describe pod <pod> -n <namespace>
kubectl logs <pod> -n <namespace>
kubectl logs <pod> -n <namespace> --previous
kubectl logs deployment/<deployment> -n <namespace>


Pods nach Node anzeigen:

kubectl get pods -A -o wide | grep <node-name>

Beispiel:

kubectl get pods -A -o wide | grep talos-cp-1


Deployment / DaemonSet neu starten:

kubectl rollout restart deployment/<name> -n <namespace>
kubectl rollout restart daemonset/<name> -n <namespace>

Beispiel:

kubectl rollout restart daemonset/longhorn-manager -n longhorn-system


Node prüfen:

kubectl describe node <node>
kubectl describe node <node> | grep -i taint
kubectl top nodes
kubectl top pods -A


Taint entfernen:

kubectl taint nodes <node> node-role.kubernetes.io/control-plane:NoSchedule-


PVC / PV prüfen:

kubectl get pvc -A
kubectl get pv
kubectl describe pvc <pvc> -n <namespace>


Namespace hängt auf Terminating:

kubectl describe namespace <namespace>
kubectl get namespace <namespace> -o jsonpath='{.spec.finalizers}{"\n"}'

Finalizer entfernen:

kubectl patch namespace <namespace> \
  --type=json \
  -p='[{"op":"remove","path":"/spec/finalizers"}]'

Nur als letzter Schritt verwenden.


Alle namespaced Ressourcen in einem Namespace finden
kubectl api-resources --verbs=list --namespaced -o name | while read r; do
  kubectl get "$r" -n <namespace> --ignore-not-found
done


Flux CLI


Überblick:

flux get all
flux get sources git
flux get kustomizations
flux get helmreleases -A
Git Source neu synchronisieren
flux reconcile source git flux-system


Kustomization neu synchronisieren:
flux reconcile kustomization <name>

Beispiel:

flux reconcile kustomization storage


HelmRelease neu synchronisieren:
flux reconcile helmrelease <name> -n <namespace>

Beispiel:

flux reconcile helmrelease longhorn -n longhorn-system


Kustomization pausieren und fortsetzen:
flux suspend kustomization <name>
flux resume kustomization <name>

Beispiel:

flux suspend kustomization storage
flux resume kustomization storage


Flux Controller prüfen:
kubectl get pods -n flux-system
kubectl logs deployment/source-controller -n flux-system
kubectl logs deployment/kustomize-controller -n flux-system
kubectl logs deployment/helm-controller -n flux-system
kubectl logs deployment/notification-controller -n flux-system


Helm Releases anzeigen:
helm ls -A
Release Status
helm status <release> -n <namespace>

Beispiel:

helm status longhorn -n longhorn-system
Release entfernen
helm uninstall <release> -n <namespace>

Mit Longhorn vorsichtig umgehen, wenn produktive Daten vorhanden sind.


Talosctl

Talos Version prüfen:
talosctl version -n <node-ip>


Nodes prüfen:
talosctl health
talosctl service -n <node-ip>
talosctl dashboard -n <node-ip>


Extensions anzeigen:
talosctl get extensions -n <node-ip>
Logs / dmesg
talosctl dmesg -n <node-ip>
talosctl logs kubelet -n <node-ip>
talosctl logs containerd -n <node-ip>


Dateien auf Talos prüfen:
talosctl ls /var/lib -n <node-ip>
talosctl ls /var/lib/longhorn -n <node-ip>
talosctl read /etc/hostname -n <node-ip>


Konfiguration anwenden:
talosctl apply-config -n <node-ip> -f talos/clusterconfig/controlplane.yaml
talosctl apply-config -n <node-ip> -f talos/clusterconfig/worker.yaml


Node upgraden:
talosctl upgrade \
  --image <installer-image> \
  -n <node-ip>

Beispiel:

talosctl upgrade \
  --image factory.talos.dev/installer/<schematic-id>:v1.13.5 \
  -n 192.168.188.181

Immer nur einen Node nach dem anderen upgraden.

Reboot
talosctl reboot -n <node-ip>


Cilium CLI

Status:
cilium status
cilium connectivity test
Cilium Pods prüfen

kubectl get pods -n kube-system | grep cilium
kubectl logs -n kube-system daemonset/cilium
kubectl logs -n kube-system deployment/cilium-operator


Cilium Endpoints:
cilium endpoint list
Cilium Services
cilium service list
Cilium Debug
cilium sysdump

Das erzeugt ein Support-Bundle zur Analyse.

Traefik


Traefik Pods:
kubectl get pods -n traefik
kubectl logs deployment/traefik -n traefik


IngressRoutes anzeigen:
kubectl get ingressroute -A
kubectl describe ingressroute <name> -n <namespace>


Services prüfen:
kubectl get svc -n traefik
TLS Secret prüfen
kubectl get secret -A | grep tls


cert-manager


Zertifikate anzeigen:
kubectl get certificates -A
kubectl get certificaterequests -A
kubectl get issuers -A
kubectl get clusterissuers


Zertifikat Details:
kubectl describe certificate <name> -n <namespace>
cert-manager Logs
kubectl logs deployment/cert-manager -n cert-manager
kubectl logs deployment/cert-manager-webhook -n cert-manager
kubectl logs deployment/cert-manager-cainjector -n cert-manager


Longhorn


Pods:
kubectl get pods -n longhorn-system -o wide


HelmRelease:
kubectl get helmrelease -n longhorn-system
flux reconcile helmrelease longhorn -n longhorn-system


StorageClasses:
kubectl get storageclass
PVCs
kubectl get pvc -A
kubectl get pv


Longhorn Nodes:
kubectl get nodes.longhorn.io -n longhorn-system
kubectl get engineimages.longhorn.io -n longhorn-system
kubectl get volumes.longhorn.io -n longhorn-system


Pi-hole / Unbound


Pi-hole Service:
sudo systemctl status pihole-FTL
sudo systemctl restart pihole-FTL


Unbound Service:
sudo systemctl status unbound
sudo systemctl restart unbound
sudo unbound-checkconf


Unbound direkt testen:
dig @127.0.0.1 -p 5335 github.com
DNSSEC testen
dig @127.0.0.1 -p 5335 dnssec-failed.org

Erwartung:

SERVFAIL
DNS vom Client testen
dig github.com
dig pihole.home.arpa
dig longhorn.home.arpa


GitOps Workflow


Normaler Ablauf:
git status
git add .
git commit -m "message"
git push

Danach:

flux reconcile source git flux-system
flux get kustomizations


Typische Troubleshooting-Reihenfolge
Wenn eine App nicht erreichbar ist


DNS prüfen:
dig app.home.arpa


Traefik Route prüfen:
kubectl get ingressroute -A


Service prüfen:
kubectl get svc -n <namespace>


Pods prüfen:
kubectl get pods -n <namespace>


Logs prüfen:
kubectl logs <pod> -n <namespace>