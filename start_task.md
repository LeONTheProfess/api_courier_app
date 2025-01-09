# Запрос начала выполнения задания

## Описание
Этот метод позволяет курьеру сообщить системе, что он начал выполнение задание (с указанным `ref`).

## Формат запроса
### URL
```
POST https://example.com/api/courier/tasks
```

### Заголовки
```json
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Тело запроса
```json
{
  "ref": 12345,
  "action": "start"
}
```

## Формат ответа
### Успешный ответ (HTTP 200)
Если запрос выполнен успешно, возвращается подтверждение начала задания:
```json
{
  "status": "success",
  "message": "Задание начато."
}
```

### Ошибка (HTTP 403)
Если токен доступа недействителен:
```json
{
  "error": "access_denied",
  "message": "Токен доступа недействителен."
}
```

### Ошибка (HTTP 404)
Если задание с указанным `ref` не найдено:
```json
{
  "error": "task_not_found",
  "message": "Задание с указанным ref не найдено."
}
```

### Ошибка (HTTP 400)
Если задание уже начато или завершено:
```json
{
  "error": "task_already_started",
  "message": "Задание уже начато или завершено."
}
``` 