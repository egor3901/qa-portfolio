# SQL для QA-тестировщика (Junior)

Этот файл содержит примеры SQL-запросов и задания для начинающего QA-тестировщика. Его можно использовать как часть портфолио.

---

## 1️⃣ Создание таблиц

### Таблица пользователей
```sql
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100),
    CreatedAt DATE
);
```

### Таблица заказов
```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    UserID INT,
    ProductName VARCHAR(100),
    Quantity INT,
    Price DECIMAL(10,2),
    OrderDate DATE,
    FOREIGN KEY (UserID) REFERENCES Users(UserID)
);
```

---

## 2️⃣ Примеры данных (INSERT)

```sql
INSERT INTO Users VALUES
(1, 'Alice', 'Smith', 'alice@example.com', '2023-01-10'),
(2, 'Bob', 'Johnson', 'bob@example.com', '2023-02-15'),
(3, 'Charlie', 'Brown', 'charlie@example.com', '2023-03-20');

INSERT INTO Orders VALUES
(101, 1, 'Laptop', 1, 1200.00, '2023-04-01'),
(102, 1, 'Mouse', 2, 25.50, '2023-04-03'),
(103, 2, 'Keyboard', 1, 80.00, '2023-04-05'),
(104, 3, 'Monitor', 2, 300.00, '2023-04-07');
```

---

## 3️⃣ Примеры запросов

### a) Выборка всех пользователей
```sql
SELECT * FROM Users;
```

### b) Пользователи, созданные после 2023-01-31
```sql
SELECT *
FROM Users
WHERE CreatedAt > '2023-01-31';
```

### c) Количество заказов каждого пользователя
```sql
SELECT u.FirstName, u.LastName, COUNT(o.OrderID) AS OrdersCount
FROM Users u
LEFT JOIN Orders o ON u.UserID = o.UserID
GROUP BY u.FirstName, u.LastName;
```

### d) Общая сумма заказов для каждого пользователя
```sql
SELECT u.FirstName, u.LastName, SUM(o.Quantity * o.Price) AS TotalSpent
FROM Users u
JOIN Orders o ON u.UserID = o.UserID
GROUP BY u.FirstName, u.LastName;
```

### e) Топ-5 самых дорогих заказов
```sql
SELECT *
FROM Orders
ORDER BY Price DESC
LIMIT 5;
```

---

## 4️⃣ Задания для практики

1. Выбрать всех пользователей, у которых имя начинается на "A".
2. Найти среднюю цену заказа для каждого продукта.
3. Вывести пользователей, которые ещё не сделали ни одного заказа.
4. Найти все заказы за последний месяц.
5. Создать запрос для изменения email пользователя по ID.
6. Вывести список продуктов с суммарным количеством заказов.
7. Найти пользователей с максимальной суммой покупок.

---

## 5️⃣ Советы для QA

- Проверяйте данные на граничные значения и пустые поля.
- Используйте `JOIN` для проверки связей между таблицами.
- Пишите запросы так, чтобы их легко проверять тестами.
- Используйте `LIMIT` и `ORDER BY` для удобства анализа.
- Добавляйте комментарии в SQL-запросы для лучшей читаемости.

---



