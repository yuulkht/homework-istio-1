# ДЗ 1 по Istio. Промышленное развертывание промышленных приложений.

## Выполнила Кухтина Юлия Егоровна, БПИ224

## Выполненные шаги

### 1. Установила Istio
скачала отсюда архив `https://github.com/istio/istio/releases/tag/1.28.1`, распаковала, добавила в path папку `bin`
```
istioctl install --set profile=demo -y # установка
kubectl label namespace default istio-injection=enabled # включить инъекцию сайдкара для namespace default
```
![установка](screenshots/1.png)

### 2. Создала helmfile.yaml
```
releases:
  - name: currency
    namespace: default
    chart: ./muffin-currency-chart
    values:
      - ./muffin-currency-chart/values.yaml

  - name: wallet
    namespace: default
    chart: ./muffin-wallet-chart
    values:
      - ./muffin-wallet-chart/values.yaml
```

запуск:
```
helm sync
```