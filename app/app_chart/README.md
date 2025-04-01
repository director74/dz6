# dz6 Сервис, в котором проверяется прохождение аутентификации через другой dz6-auth сервис и вывод данных о пользователе

Для запуска проекта использовать команды

```bash
helm dependency build
helm install -n app dz6 ./
```

Также необходимо заполнить данные для подключения postgresql
в файле values.yaml в секции global.postgresql.auth