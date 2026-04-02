# REST API – Регистрация пользователя

## HTTP Method + URL

POST /api/v1/users/register

---

## Входные параметры

| Поле | Тип | Обязательное | Ограничения |
|---|---|---:|---|
| firstName | string | Да | 1–100 символов |
| lastName | string | Да | 1–100 символов |
| userName | string | Да | уникальный, 1–50 символов |
| password | string | Да | 8 символов, заглавная + строчная + цифра + спецсимвол |
| recaptchaToken | string | Да | токен Google reCAPTCHA v2 ("I'm not a robot") |

---

## Ограничения для пароля

Пароль должен содержать:

- минимум 8 символов
- одну цифру
- одну заглавную букву
- одну строчную букву
- один специальный символ

---

## Успешный ответ

HTTP 201 Created

```json
{
  "message": "User Register Successfully.",
  "userName": "ivan",
  "status": "REGISTERED"
}
```

---

## Ошибки

### 400 Bad Request

```json
{
  "errorCode": "INVALID_PASSWORD",
  "message": "Passwords must have at least one non alphanumeric character, one digit ('0'-'9'), one uppercase ('A'-'Z'), one lowercase ('a'-'z'), one special character and Password must be eight characters or longer.",
  "field": "password"
}
```

---

### 409 Conflict

```json
{
  "errorCode": "USER_ALREADY_EXISTS",
  "message": "User exists!"
}
```

---

### 400 Bad Request – reCAPTCHA

```json
{
  "errorCode": "RECAPTCHA_REQUIRED",
  "message": "Please verify reCaptcha to register!"
}
```

---

## Пример запроса

```json
{
  "firstName": "ivan",
  "lastName": "ivanov",
  "userName": "ivan",
  "password": "Password@123",
  "recaptchaToken": "03AFcWeA..."
}
```
