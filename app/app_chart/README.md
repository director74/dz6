# dz6 Backend for frontends. Apigateway

Для запуска проекта использовать команды

```bash
helm dependency build
helm install dz6 ./
```

Также необходимо заполнить данные для подключения postgresql
в файле values.yaml в секции global.postgresql.auth