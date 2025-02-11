# Подтверждение выполнения задания

## Описание
Этот метод позволяет курьеру подтвердить выполнение задания. Если задание было `from_war`, необходимо отправить массив недовезенных GRM (сам GRM и причина недовоза). Если задание было `to_war`, необходимо перечислить GRM, которые приедут на склад. В одном запросе может быть либо `undelivered_grm`, либо `to_war_grm`.

## Формат запроса
### URL
```
POST https://example.com/api/courier/tasks
```

### Заголовки
```
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Тело запроса
#### from_war
```json
{
  "ref": 12345,
  "action": "confirm",
  "completion_datetime": "2023-10-01T14:30:00Z",
  "undelivered_grm": [
    {
      "grm": "GRM123",
      "reason": "Не выдали на складе"
    },
    {
      "grm": "GRM456",
      "reason": "Получатель отказался"
    }
  ],
  "services": [
    {
      "name": "Общая услуга1",
      "quantity": 1
    }
  ]
}
```
#### to_war
```json
{
  "ref": 12345,
  "action": "confirm",
  "completion_datetime": "2023-10-01T14:30:00Z",
  "to_war_grm": [
    {
      "grm": "GRM789",
      "services": [
        {
          "name": "Услуга1",
          "quantity": 2
        },
        {
          "name": "Услуга2",
          "quantity": 1
        }
      ]
    },
    {
      "grm": "GRM101",
      "services": [
        {
          "name": "Услуга3",
          "quantity": 3
        }
      ]
    }
  ],
  "services": [
    {
      "name": "Общая услуга1",
      "quantity": 1
    }
  ]
}
```

## Формат ответа
### Успешный ответ (HTTP 200)
Если запрос выполнен успешно, возвращается подтверждение выполнения задания:
```json
{
  "status": "success",
  "message": "Задание подтверждено."
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
Если данные запроса некорректны:
```json
{
  "error": "bad_request",
  "message": "Некорректные данные запроса."
}
```

### Ошибка (HTTP 404)
Если услуга с указанным наименованием не найдена:
```json
{
  "error": "service_not_found",
  "message": "Услуга с наименованием '<service_name>' не найдена."
}
```