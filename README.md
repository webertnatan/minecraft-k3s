# 🚀 Minecraft no Kubernetes com k3s + ArgoCD (GitOps)

## 📌 Visão Geral

Este projeto demonstra a implementação completa de um ambiente DevOps local utilizando:

- Kubernetes leve (k3s)
- Deploy contínuo com ArgoCD (GitOps)
- Servidor Minecraft containerizado
- Persistência com PVC

---

## 🧱 Arquitetura

GitHub → ArgoCD → Kubernetes → Minecraft → NodePort → Cliente

---

## 💻 Ambiente

- CachyOS (Arch-based)
- Ryzen 7 7735HS
- 16GB RAM
- k3s + containerd

---

## ⚙️ Instalação do k3s

```bash
curl -sfL https://get.k3s.io | sh -
```

---

## ❌ Problema

system validation failed - wrong number of fields

### ✅ Solução

```bash
mount | grep cgroup
systemctl restart k3s
```

---

## 🚀 Instalação ArgoCD

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

---

## 🎮 Deploy Minecraft

Imagem:

```yaml
image: itzg/minecraft-server
```

---

## ⚠️ Problemas resolvidos

- PVC não encontrado
- PVC sendo deletado
- CrashLoopBackOff
- Versão incorreta (26.1)
- Login Microsoft obrigatório

---

## ⚙️ Configuração importante

```yaml
env:
  - name: EULA
    value: "TRUE"
  - name: ONLINE_MODE
    value: "FALSE"
  - name: MEMORY
    value: 2G
  - name: VERSION
    value: "1.20.1"
```

---

## 📡 Acesso

```bash
kubectl get svc -n minecraft
```

Conectar:

```
IP_DO_NODE:PORTA
```

---

## 🧪 Teste final

Servidor iniciado com sucesso:

```
Done (3.998s)! For help, type "help"
```

---

## 🧠 Aprendizados

- PVC é obrigatório para apps stateful
- Logs são essenciais
- ArgoCD precisa de project
- k3s pode falhar com cgroups

---

## 🏆 Resultado

✔ Kubernetes funcionando  
✔ ArgoCD funcionando  
✔ GitOps ativo  
✔ Minecraft rodando  

---

## 🚀 Próximos passos

- Harbor (registry)
- Prometheus + Grafana
- Ingress
- CI/CD
