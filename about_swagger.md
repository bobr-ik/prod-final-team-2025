## Описание работы Swagger UI


### **1. Аутентификация**
API использует аутентификацию через API-ключ, который передаётся в заголовке `Authorization`. Для доступа к защищённым эндпоинтам необходимо:
1. Зарегистрироваться через эндпоинт `/users` (если у вас ещё нет аккаунта).
2. Авторизоваться через эндпоинт `/users/auth`, чтобы получить токены доступа (`access_token`) и обновления (`refresh_token`).
3. Использовать `access_token` в заголовке `Authorization` для доступа к защищённым эндпоинтам.

Пример заголовка:
```
Authorization: Bearer <access_token>
```

---

### **2. Основные эндпоинты**

#### **Регистрация пользователя**
- **Эндпоинт**: `POST /users`
- **Описание**: Регистрация нового пользователя.
- **Пример запроса**:
  ```json
  {
    "email": "user@example.com",
    "username": "user123",
    "password": "password123"
  }
  ```
- **Пример ответа**:
  ```json
  {
    "email": "user@example.com",
    "username": "user123",
    "client_id": "550e8400-e29b-41d4-a716-446655440000",
    "access_level": "GUEST"
  }
  ```

---

#### **Аутентификация**
- **Эндпоинт**: `POST /users/auth`
- **Описание**: Получение токенов доступа и обновления.
- **Пример запроса**:
  ```json
  {
    "email": "user@example.com",
    "password": "password123"
  }
  ```
- **Пример ответа**:
  ```json
  {
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expires_in": 3600,
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refresh_expires_in": 86400
  }
  ```

---

#### **Обновление токена**
- **Эндпоинт**: `POST /users/auth/refresh`
- **Описание**: Обновление токена доступа с использованием токена обновления.
- **Пример запроса**:
  ```json
  {
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
  ```
- **Пример ответа**:
  ```json
  {
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expires_in": 3600,
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refresh_expires_in": 86400
  }
  ```

---

### **3. Моковые данные для тестирования**
Для тестирования API можно использовать следующие моковые данные:


#### **Аутентификация**
```json
{
  "email": "admin@example.com",
  "password": "adminadmin"
}
```

```json
{
  "email": "student@example.com",
  "password": "studentstudent"
}
```

---

