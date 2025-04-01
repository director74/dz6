# dz6 Приложение для проверки авторизации через Apigateway 

Для запуска проекта использовать команды

```bash
helm dependency build
helm install -n app dz6 ./
```

Также необходимо заполнить данные для подключения postgresql
в файле values.yaml в секции global.postgresql.auth