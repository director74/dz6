# dz6-auth Backend for frontends. Apigateway

Для запуска проекта использовать команды

```bash
helm dependency build
helm install -n auth dz6-auth ./
```

Также необходимо заполнить данные для подключения postgresql
в файле values.yaml в секции global.postgresql.auth