# Лабораторна робота 1. Робота з СУБД PostgreSQL та основи SQL

## Загальна інформація

**Здобувач освіти:** Кондратюк Дмитро Михайлович
**Група:** Іпз-33
**Обраний рівень складності:** 2 (з елементами демонстрації базового рівня 1)

> ⚠️ **Примітка перед захистом:** усі запити нижче складені на основі стандартної структури навчальної бази `technomart.sql` (таблиці `customers`, `products`, `employees`, `orders`), описаної у методичних вказівках. Перед здачею виконайте кожен запит у Supabase SQL Editor на своєму проєкті, звірте назви стовпців зі своєю реальною схемою (можуть незначно відрізнятись) та додайте власні скріншоти результатів замість плейсхолдерів `[Скріншот]`.

---

## Виконання завдань

## Рівень 1

### 1. Основні SELECT запити

**1.1. Отримати всі записи з таблиці customers**
```sql
SELECT * FROM customers;
```
Результат: виведено повний список клієнтів (фізичні та юридичні особи) з усіма атрибутами.
**1.2. Вивести тільки назви товарів і їхні ціни з таблиці products**
```sql
SELECT product_name, unit_price
FROM products;
```
Результат: отримано скорочений набір даних — лише назва товару та її ціна, без зайвих стовпців.
**1.3. Показати контактні дані всіх співробітників**
```sql
SELECT first_name, last_name, phone, email
FROM employees;
```
Результат: виведено ПІБ, телефон та email кожного співробітника компанії.
<img width="800" height="804" alt="image" src="https://github.com/user-attachments/assets/aa1b962b-a9ab-4b93-92b9-6f270eae1b03" />
### 2. Прості умови WHERE
**2.1. Клієнти з міста Київ**
```sql
SELECT * FROM customers
WHERE city = 'Київ';
```
**2.2. Товари дорожчі за 25000 грн**
```sql
SELECT * FROM products
WHERE unit_price > 25000;
```
**2.3. Замовлення зі статусом 'delivered'**
```sql
SELECT * FROM orders
WHERE status = 'delivered';
```
**2.4. Співробітники відділу продажів**
```sql
SELECT * FROM employees
WHERE position LIKE '%продаж%';
```
<img width="1585" height="608" alt="image" src="https://github.com/user-attachments/assets/4a629402-7833-4144-97d6-d19539482b14" />

### 3. Базове сортування ORDER BY

**3.1. Товари за зростанням ціни**
```sql
SELECT product_name, unit_price
FROM products
ORDER BY unit_price ASC;
```
**3.2. Клієнти в алфавітному порядку**
```sql
SELECT contact_name, city
FROM customers
ORDER BY contact_name;
```
**3.3. Замовлення від найновіших до найстаріших**
```sql
SELECT order_id, order_date
FROM orders
ORDER BY order_date DESC;
```
<img width="1502" height="820" alt="image" src="https://github.com/user-attachments/assets/01768ea1-5f02-4309-8f5c-1f8d7f8df07c" />



### 4. Обмеження результатів LIMIT

**4.1. Перші 10 найдорожчих товарів**
```sql
SELECT product_name, unit_price
FROM products
ORDER BY unit_price DESC
LIMIT 10;
```

`[Скріншот]`

**4.2. 5 останніх замовлень**
```sql
SELECT order_id, order_date
FROM orders
ORDER BY order_date DESC
LIMIT 5;
```

`[Скріншот]`

**4.3. Перші 8 клієнтів в алфавітному порядку**
```sql
SELECT contact_name
FROM customers
ORDER BY contact_name
LIMIT 8;
```

`[Скріншот]`

---

## Рівень 2

### 5. Пошук за зразком з LIKE

**5.1. Клієнти, чиї імена починаються на "Іван"**
```sql
SELECT * FROM customers
WHERE contact_name LIKE 'Іван%';
```

`[Скріншот]`

**5.2. Товари зі словом "phone" або "телефон" у назві**
```sql
SELECT * FROM products
WHERE product_name LIKE '%phone%' OR product_name LIKE '%телефон%';
```

`[Скріншот]`

**Самостійно — 3 власні запити з LIKE:**

```sql
-- Бізнес-логіка: маркетинговий відділ хоче знайти клієнтів
-- з поштою на Gmail для email-розсилки (пошук за закінченням рядка)
SELECT contact_name, email
FROM customers
WHERE email LIKE '%@gmail.com';
```

```sql
-- Бізнес-логіка: пошук усіх товарів бренду Samsung
-- для формування каталогу партнерської акції (пошук за початком рядка)
SELECT product_name, unit_price
FROM products
WHERE product_name LIKE 'Samsung%';
```

```sql
-- Бізнес-логіка: пошук клієнтів, прізвище яких закінчується на "енко" —
-- аналіз частотності поширених українських прізвищ у базі (пошук за вмістом)
SELECT contact_name, city
FROM customers
WHERE contact_name LIKE '%енко';
```

`[Скріншот]` (для кожного із трьох запитів)

### 6. Логічні оператори AND, OR, NOT

**6.1. Товари дорожчі 15000 і дешевші 50000 грн**
```sql
SELECT product_name, unit_price
FROM products
WHERE unit_price > 15000 AND unit_price < 50000;
```

`[Скріншот]`

**6.2. Клієнти з Києва або Львова, юридичні особи**
```sql
SELECT contact_name, city, customer_type
FROM customers
WHERE (city = 'Київ' OR city = 'Львів')
  AND customer_type = 'company';
```

`[Скріншот]`

**Самостійно — 4 власні запити:**

```sql
-- Бізнес-логіка: відбір товарів для акції "розпродаж залишків" —
-- недорогі товари, яких залишилось мало на складі
SELECT product_name, unit_price, units_in_stock
FROM products
WHERE unit_price < 10000 AND units_in_stock < 5;
```

```sql
-- Бізнес-логіка: пошук співробітників, які мають вказаного керівника
-- (тобто НЕ є топ-менеджерами) для списку рядового персоналу
SELECT first_name, last_name, position
FROM employees
WHERE NOT reports_to IS NULL;
```

```sql
-- Бізнес-логіка: замовлення, які або доставлені, або скасовані —
-- для звіту про "завершені" (закриті) замовлення
SELECT order_id, status, order_date
FROM orders
WHERE status = 'delivered' OR status = 'cancelled';
```

```sql
-- Бізнес-логіка: клієнти-фізособи не з великих міст —
-- потенційна аудиторія для регіональної рекламної кампанії
SELECT contact_name, city, customer_type
FROM customers
WHERE customer_type = 'individual'
  AND city != 'Київ'
  AND city != 'Харків';
```

`[Скріншот]` (для кожного із чотирьох запитів)

### 7. Оператори IN, BETWEEN, IS NULL

**7.1. Клієнти з міст Київ, Харків, Одеса, Дніпро**
```sql
SELECT contact_name, city
FROM customers
WHERE city IN ('Київ', 'Харків', 'Одеса', 'Дніпро');
```

`[Скріншот]`

**7.2. Товари в ціновому діапазоні від 10000 до 30000 грн**
```sql
SELECT product_name, unit_price
FROM products
WHERE unit_price BETWEEN 10000 AND 30000;
```

`[Скріншот]`

**Самостійно — по 2 запити для кожного оператора:**

```sql
-- IN (1): бізнес-логіка — вибірка замовлень у "проблемних" статусах
-- для контролю якості обслуговування
SELECT order_id, status
FROM orders
WHERE status IN ('pending', 'cancelled');
```

```sql
-- IN (2): бізнес-логіка — пошук товарів обраних категорій
-- (наприклад, "Смартфони" і "Ноутбуки") для окремої вітрини сайту
SELECT product_name, category_id
FROM products
WHERE category_id IN (1, 3);
```

```sql
-- BETWEEN (1): бізнес-логіка — замовлення за 1 квартал 2024 року
-- для формування квартального звіту продажів
SELECT order_id, order_date
FROM orders
WHERE order_date BETWEEN '2024-01-01' AND '2024-03-31';
```

```sql
-- BETWEEN (2): бізнес-логіка — товари "середнього" цінового сегменту
-- для аналізу найпопулярнішої категорії покупців
SELECT product_name, unit_price
FROM products
WHERE unit_price BETWEEN 5000 AND 15000;
```

```sql
-- IS NULL (1): бізнес-логіка — товари без опису потребують
-- доопрацювання картки товару відділом контенту
SELECT product_name
FROM products
WHERE description IS NULL;
```

```sql
-- IS NOT NULL (2): бізнес-логіка — клієнти-юрособи (мають назву компанії)
-- для розсилки B2B-пропозицій
SELECT contact_name, company_name
FROM customers
WHERE company_name IS NOT NULL;
```

`[Скріншот]` (для кожного із шести запитів)

### 8. Комбінування умов

**Самостійно — 5 складних запитів:**

```sql
-- 1. LIKE + AND: бізнес-логіка — пошук недорогих аксесуарів Apple
-- (чохли, кабелі тощо) для блоку "супутні товари"
SELECT product_name, unit_price
FROM products
WHERE product_name LIKE '%Apple%'
  AND unit_price < 5000;
```

```sql
-- 2. BETWEEN + IN: бізнес-логіка — замовлення певних клієнтів
-- за конкретний період для їх персональної історії покупок
SELECT order_id, customer_id, order_date
FROM orders
WHERE order_date BETWEEN '2024-06-01' AND '2024-08-31'
  AND customer_id IN (1, 2, 3);
```

```sql
-- 3. LIKE + OR + AND: бізнес-логіка — товари бренду Samsung або Apple,
-- які ще є в наявності на складі
SELECT product_name, unit_price, units_in_stock
FROM products
WHERE (product_name LIKE '%Samsung%' OR product_name LIKE '%Apple%')
  AND units_in_stock > 0;
```

```sql
-- 4. IS NULL + LIKE: бізнес-логіка — клієнти-фізособи (без company_name)
-- з електронною поштою на gmail — сегмент для персональних email-акцій
SELECT contact_name, email
FROM customers
WHERE company_name IS NULL
  AND email LIKE '%@gmail.com';
```

```sql
-- 5. NOT LIKE + BETWEEN: бізнес-логіка — основні (не аксесуарні) товари
-- середнього і високого цінового сегменту для флагманської вітрини
SELECT product_name, unit_price
FROM products
WHERE product_name NOT LIKE '%чохол%'
  AND unit_price BETWEEN 20000 AND 60000;
```

`[Скріншот]` (для кожного із п'яти запитів)

### 9. Складне сортування та пагінація

**Самостійно — 3 запити з сортуванням за кількома полями:**

```sql
-- 1. Бізнес-логіка: каталог товарів, згрупований по категоріях,
-- а всередині категорії — від дорожчих до дешевших
SELECT category_id, product_name, unit_price
FROM products
ORDER BY category_id ASC, unit_price DESC;
```

```sql
-- 2. Бізнес-логіка: список клієнтів для CRM — спочатку компанії,
-- потім фізособи, і за містом всередині кожного типу
SELECT contact_name, city, customer_type
FROM customers
ORDER BY customer_type DESC, city ASC;
```

```sql
-- 3. Бізнес-логіка: звіт про замовлення — за статусом,
-- а в межах статусу — від найновіших до найстаріших
SELECT order_id, status, order_date
FROM orders
ORDER BY status ASC, order_date DESC;
```

**Самостійно — 2 запити з OFFSET для пагінації:**

```sql
-- Сторінка 2 каталогу товарів (записи 11-20), відсортовано за назвою
SELECT product_name, unit_price
FROM products
ORDER BY product_name
LIMIT 10 OFFSET 10;
```

```sql
-- Сторінка 3 списку клієнтів (записи 21-30), відсортовано за іменем
SELECT contact_name, city
FROM customers
ORDER BY contact_name
LIMIT 10 OFFSET 20;
```

`[Скріншот]` (для кожного із п'яти запитів)

---

## Висновки

У ході виконання лабораторної роботи було встановлено з'єднання з хмарною СУБД PostgreSQL на платформі Supabase та відпрацьовано основні можливості команди `SELECT`: вибірку стовпців, фільтрацію за допомогою `WHERE` (оператори порівняння, `LIKE`, `AND`/`OR`/`NOT`, `IN`, `BETWEEN`, `IS NULL`), сортування `ORDER BY` (у тому числі за кількома полями) та обмеження вибірки через `LIMIT`/`OFFSET` для пагінації.

Виконано всі завдання рівня 1 (базові SELECT, WHERE, ORDER BY, LIMIT) та рівня 2 (LIKE, логічні оператори, IN/BETWEEN/IS NULL, комбіновані умови, складне сортування і пагінація), включно з самостійно сформульованими запитами з поясненням бізнес-логіки кожного з них.

**Самооцінка:** 4 (добре)

**Обґрунтування:** виконано всі вимоги рівня 2 в повному обсязі, запити супроводжено коментарями та поясненням бізнес-логіки. Для оцінки "відмінно" додатково потрібно виконати завдання рівня 3 (вкладені логічні умови з дужками, комплексні аналітичні звіти, дослідження закономірностей у даних).
