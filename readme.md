# Module 10 - ArgoCD & GitOps

Репозиторий содержит конфигурацию для управления инфраструктурой кластера через ArgoCD (App-of-Apps, ApplicationSet, AppProject, Sync Waves и ignoreDifferences).

## Структура проекта
- `bootstrap/root.yaml` — корневое приложение (App-of-Apps).
- `apps/` — манифесты приложений (`podinfo-dev`, `podinfo-prod`, `hello`).
- `appsets/` — генераторы ApplicationSet.
- `install/` — конфигурация для установки ArgoCD.
- `releases/` — файлы параметров (values) для окружений.

## Инструкция по развертыванию

1. Добавляем официальный Helm-репозиторий проекта Argo:
```bash
helm repo add argocd https://github.io
helm repo update
```

2. Устанавливаем ArgoCD одной командой, используя конфигурационный файл из этого репозитория:
```bash
helm install argocd argocd/argo-helm -n argo --create-namespace -f install/argocd-values.yaml
```

3. Запускаем GitOps-конвейер (App-of-Apps). Для этого примените корневой манифест из папки репозитория:
```bash
kubectl apply -f bootstrap/root.yaml
```
