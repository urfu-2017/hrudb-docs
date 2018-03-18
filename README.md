# HruDB

## Адрес

https://hrudb.herokuapp.com/

## Документация

```sh
# Добавление/перезаписывание записи по ключу:
#   <key>   - строка в формате [a-z_-0-9]+
#   <value> - строка длинной не более 1048576 символов
#   <token> - заранее полученный авторизационный токен
PUT /storage/<key> <value> HTTP/1.1
Authorization: <token>
Content-Type: plain/text
→ 201 Сreated или 400 Bad Request

# По одному ключу можно положить несколько значений методом POST
POST /storage/<key> <value> HTTP/1.1
Authorization: <token>
Content-Type: plain/text
→ 204 No content или 400 Bad Request

# Получение последней записи по ключу
GET /storage/<key> HTTP/1.1
Authorization: <token>
→ 200 OK <value> или 400 Bad Request, или 404 Not Found

# Получение всех записей по ключу
#  from     - моложе указанного таймстемпа (new Date().getTime())
#  to       - старше указанного таймстемпа (new Date().getTime())
#  sort     – упорядоченные по дате (date, по умолчанию) или по алфавиту (alph)
#  limit    – в указанном количестве (по умолчанию, Infinity)
#  offset   – с отступ от начала выборки (по умолчанию, 0)
GET /storage/<key>/all?[from][to][sort][limit][offset] HTTP/1.1
Authorization: <token>
→ 200 OK [<value1>, <value2>, ...] или 200 OK [], или 400 Bad Request

# Удаление записи/записей по ключу
DELETE /storage/<key> <value> HTTP/1.1
Authorization: <token>
→ 204 No content

# Ошибки приходят в JSON формате
# {
#     "error": {
#         "statusCode": 400,
#         "message": "Bad request"
#     }
# }
```
