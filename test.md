```mermaid        
classDiagram
    class Животное {
        +String имя
        +void есть()
    }
    class Собака {
        +void лаять()
    }
    Животное <|-- Собака
```


```python
a = float(input("Введите первое число: "))
b = float(input("Введите второе число: "))
operation = input("Выберите операцию (+, -, *, /): ")

if operation == "+":
    print(f"Результат: {a + b}")
elif operation == "-":
    print(f"Результат: {a - b}")
elif operation == "*":
    print(f"Результат: {a * b}")
elif operation == "/":
    if b != 0:
        print(f"Результат: {a / b}")
    else:
        print("Ошибка: деление на ноль!")
else:
    print("Неверная операция!")
```

dj[sjdbladjkbfjsvljahvbdfljavf;hqv;hfe


```mermaid
gantt
    title Проект разработки ПО "Вектор"
    dateFormat  YYYY-MM-DD
    axisFormat  %d/%m
    todayMarker off

    section Подготовка
    Анализ требований       :a1, 2024-01-01, 15d
    Техническое проектирование :a2, after a1, 10d
    Выбор технологий       :a3, after a2, 5d

    section Разработка
    Модуль авторизации     :b1, 2024-01-20, 20d
    API ядра системы       :b2, after a2, 25d
    Интерфейс администратора :b3, after b1, 15d
    Тестирование API       :crit, b4, after b2, 10d

    section Интеграция
    Настройка CI/CD        :c1, after b4, 7d
    Сборка релиза          :crit, c2, after c1, 5d
    Деплой на staging      :c3, after c2, 3d

    section Документация
    Техническая документация :d1, after a3, 12d
    Руководство пользователя :d2, 2024-02-10, 14d

    section Тестирование
    Юнит-тесты            :e1, after b1, 10d
    Интеграционные тесты  :e2, after b4, 12d
    Нагрузочное тестирование :crit, e3, after e2, 8d
```

```mermaid
sequenceDiagram
    participant Client as Клиент (Web)
    participant Auth as AuthService
    participant Order as OrderSystem
    participant Payment as PaymentGateway
    participant Logistics as LogisticsAPI
    participant Notify as NotificationService

    %% 1. Аутентификация
    Client ->> Auth: POST /login (credentials)
    Auth -->> Client: JWT Token

    %% 2. Создание заказа
    Client ->> Order: POST /orders (JWT, items)
    Order ->> Auth: GET /validate (JWT)
    Auth -->> Order: UserID
    Order ->> Payment: Reserve funds (UserID, amount)
    Payment -->> Order: PaymentID (pending)
    Order ->> Logistics: Create shipment (items)
    Logistics -->> Order: TrackingID
    Order -->> Client: OrderID, TrackingID

    %% 3. Подтверждение платежа
    Payment ->> Order: PATCH /orders/{id} (status=paid)
    Order ->> Logistics: Confirm shipment (TrackingID)
    Logistics ->> Order: ETA (days)
    Order ->> Notify: Send email (UserID, "Order paid")
    Notify -->> Order: OK

    %% 4. Логистика
    Logistics ->> Notify: Send SMS (UserID, "Shipped")
    Notify -->> Logistics: OK
    Client ->> Logistics: GET /track/{id}
    Logistics -->> Client: Shipment status
```
