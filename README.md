# Микросервисное приложение с аутентификацией

## Запуск приложения

Для запуска приложения выполните следующие шаги:

1. Запуск Helm-чартов:
```bash
# Установка auth сервиса
helm upgrade --install dz6-auth ./auth/auth_chart -n auth

# Установка app сервиса
helm upgrade --install dz6 ./app/app_chart -n app
```

2. Проверка статуса подов:
```bash
kubectl get pods -n auth
kubectl get pods -n app
```

3. Добавление записи в hosts для доступа к приложению:
```
# В Windows (PowerShell от администратора)
Add-Content -Path C:\Windows\System32\drivers\etc\hosts -Value "$(minikube ip) arch.homework" -Force

# В Linux/MacOS
echo "$(minikube ip) arch.homework" | sudo tee -a /etc/hosts
```

## Требования

- Kubernetes (Minikube)
- Helm
- Newman: `npm install -g newman` (для запуска тестов)

## Тестирование аутентификации

Эта коллекция проверяет работу аутентификации и авторизации в системе.

### Сценарий тестирования

1. Регистрация первого пользователя (статус 201)
2. Проверка запрета доступа к профилю без авторизации (статус 401/302)
3. Вход первого пользователя и получение cookie сессии
4. Получение профиля первого пользователя (проверка структуры ответа с полями data.id, data.username и др.)
5. Выход из системы
6. Регистрация второго пользователя
7. Вход второго пользователя 
8. Получение профиля второго пользователя
9. Проверка, что второй пользователь не имеет доступа к профилю первого (статус 403/404)

### Проверяемые данные

При получении профиля пользователя проверяется структура ответа:
```json
{
    "data": {
        "id": 11,
        "username": "testuser_...",
        "firstName": "Test",
        "lastName": "User",
        "email": "testuser@example.com"
    }
}
```

### Запуск тестов

```bash
newman run auth_test_collection.json --env-var "baseUrl=http://arch.homework"
``` 