# Авторизация через POST запрос с помощью логина и пароля

## Описание
Этот метод позволяет авторизоваться в системе, отправляя учетные данные пользователя (логин и пароль) через POST запрос на указанный URL.

## Формат запроса
### URL
```
POST https://example.com/api/courier/auth
```

### Заголовки
```
Content-Type: application/json
```

### Тело запроса
```json
{
  "username": "your_username",
  "password": "your_password"
}
```

## Формат ответа
### Успешный ответ (HTTP 200)
Если авторизация прошла успешно, сервер возвращает токен доступа и информацию о пользователе:
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": 123,
    "username": "your_username",
    "email": "your_email@example.com",
    "phone": "+79998887766"
  }
}
```

### Ошибка (HTTP 401)
Если логин или пароль неверны:
```json
{
  "error": "invalid_credentials",
  "message": "Неверный логин или пароль."
}
```