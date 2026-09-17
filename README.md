Лабораторна робота 1. Робота з СУБД PostgreSQL та основи SQL
Загальна інформація
Здобувач освіти: Дмитро Кондратюк

Група: ІПЗ-33

Обраний рівень складності: 1-2

Виконання завдань
Список таблиць
SQL
-- Запит для отримання списку таблиць
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'public'
ORDER BY table_name;
Результат: У базі даних створено 8 основних таблиць: categories, customers, employees, order_items, orders, products, regions, suppliers.

<img width="551" height="823" alt="{B8D5E31E-764B-4535-8A85-F296753A1705}" src="https://github.com/user-attachments/assets/6db83ba8-3265-4167-92c9-84dc1c8a7f40" />


РІВЕНЬ 1. ОСНОВНІ ЗАПИТИ
1. Отримати всі записи з таблиці customers.

SQL
SELECT * FROM customers;
Результат: Отримано 15 записів клієнтів, включаючи як фізичних осіб, так і юридичні компанії з різних міст України.

<img width="1289" height="719" alt="{DF5323A3-BE17-4558-8F39-AFBC02E25153}" src="https://github.com/user-attachments/assets/a4dcd252-b684-41f0-9905-371d4f78da90" />


2. Вивести тільки назви товарів і їхні ціни з таблиці products.

SQL
SELECT product_name, unit_price FROM products;
Результат: Виведено перелік з 24 товарів та їхніх цін.   

<img width="549" height="837" alt="{5BAD8BDC-B100-4AB9-B132-F112A3C9C54F}" src="https://github.com/user-attachments/assets/1a07780f-120d-40f7-a932-882a8acba4ce" />


3. Показати контактні дані всіх співробітників (ім'я, прізвище, телефон, email).   

SQL
SELECT first_name, last_name, phone, email FROM employees;
Результат: Виведено контактну інформацію 8 співробітників інтернет-магазину.   

<img width="1054" height="764" alt="{4BF4486D-4DC4-4F33-B0D3-9DA4911F0CC4}" src="https://github.com/user-attachments/assets/cc9aef2a-8984-4d09-b30b-7859bd87f60c" />


4. Знайти всіх клієнтів з міста Київ.

SQL
SELECT * FROM customers WHERE city = 'Київ';
Результат: Отримано записи 4 клієнтів, які проживають або мають офіс у Києві.

<img width="1526" height="609" alt="{0D10B143-4399-44DC-ABA9-656CED1800B7}" src="https://github.com/user-attachments/assets/7845a1da-35e7-4e0a-ac55-e3754620bcd9" />


5. Вивести товари, які коштують більше 25000 грн.

SQL
SELECT * FROM products WHERE unit_price > 25000;
Результат: Виведено список преміальних товарів (13 позицій), ціна яких перевищує вказаний поріг.

<img width="1572" height="780" alt="{3095CA64-4EBF-40E5-96F2-ED61FDA4947E}" src="https://github.com/user-attachments/assets/551c02fc-f257-4459-ad15-968adbf3c721" />


6. Показати всі замовлення зі статусом 'delivered'.

SQL
SELECT * FROM orders WHERE order_status = 'delivered';
Результат: Отримано 26 виконаних та доставлених замовлень.

<img width="1597" height="833" alt="{031250F6-096D-4079-A411-35B47E271332}" src="https://github.com/user-attachments/assets/6798b3e5-4024-4652-b310-55bd9e573f89" />


7. Знайти співробітників, які працюють у відділі продажів (посада містить слово "продаж").

SQL
SELECT * FROM employees WHERE title LIKE '%продаж%';
Результат: Отримано 3 записи менеджерів та 1 директора з продажу.

<img width="1501" height="493" alt="{B7050FBA-6201-49F7-A31B-A9711B45CA2E}" src="https://github.com/user-attachments/assets/5ef70868-164f-43ef-9416-fbdd16ddbe73" />

8. Відсортувати товари за зростанням ціни.

SQL
SELECT * FROM products ORDER BY unit_price ASC;
Результат: Товари відсортовано від найдешевшого (Зарядний кабель за 699 грн) до найдорожчого.

<img width="1658" height="830" alt="{F8039C0A-C539-4008-8208-1353217EF3EE}" src="https://github.com/user-attachments/assets/899a4377-dcf0-43fd-a30e-b75a18ba1d49" />


9. Показати клієнтів в алфавітному порядку за іменем контактної особи.

SQL
SELECT * FROM customers ORDER BY contact_name ASC;
Результат: Список клієнтів відсортовано від "Білоус Дмитро..." до "Шевченко Віктор...".

<img width="1622" height="760" alt="{C09B0E0E-DD16-4311-AE6A-366BD65E9EB0}" src="https://github.com/user-attachments/assets/4b5e1781-c70e-4cab-b5b2-25fcaeef78be" />


10. Вивести замовлення від найновіших до найстаріших.

SQL
SELECT * FROM orders ORDER BY order_date DESC;
Результат: Замовлення відсортовано у зворотному хронологічному порядку.

<img width="1639" height="836" alt="{8C67A4AC-BE95-49D0-BF33-DB93703DA745}" src="https://github.com/user-attachments/assets/69707cc4-a914-48f2-92b8-17d8b8fe38a7" />


11. Показати перші 10 найдорожчих товарів.

SQL
SELECT * FROM products ORDER BY unit_price DESC LIMIT 10;
Результат: Виведено топ-10 товарів з максимальною ціною (очолює список LG OLED C3).

<img width="1638" height="643" alt="{89D87830-6B82-467B-A828-3E7F6556FD2A}" src="https://github.com/user-attachments/assets/e39c1c56-5f0f-47c2-aeb1-41c118752ef7" />


12. Вивести 5 останніх замовлень (за датою).

SQL
SELECT * FROM orders ORDER BY order_date DESC LIMIT 5;
Результат: Отримано 5 найсвіжіших замовлень, зроблених у серпні 2024 року.

<img width="1537" height="544" alt="{B33EA143-2138-451F-B8A0-83A249AC5479}" src="https://github.com/user-attachments/assets/5f7b4a75-10d3-44ed-8c02-95e102fcb6ea" />


13. Отримати перших 8 клієнтів в алфавітному порядку.

SQL
SELECT * FROM customers ORDER BY contact_name ASC LIMIT 8;
Результат: Виведено перші 8 рядків з відсортованого списку контактних осіб.

<img width="1605" height="574" alt="{336EB800-4ED2-4F8A-9D8F-CA7F3C690FC7}" src="https://github.com/user-attachments/assets/5ab3d046-44f6-4f57-9798-2dd2d041ba57" />


РІВЕНЬ 2. СКЛАДНІ УМОВИ ТА ОПЕРАТОРИ
14. Знайти всіх клієнтів, чиї імена починаються на "Іван".

SQL
SELECT * FROM customers WHERE contact_name LIKE 'Іван%';
Результат: Знайдено клієнтку Іванову Марію.

<img width="1576" height="389" alt="{3F6566E4-86C3-4F7E-8E74-691652C2944E}" src="https://github.com/user-attachments/assets/52bcfa8c-84e6-44dc-8d58-f94b2e65997d" />


15. Вивести товари, в назві яких є слово "phone" або "телефон".

SQL
SELECT * FROM products 
WHERE LOWER(product_name) LIKE '%phone%' 
   OR LOWER(product_name) LIKE '%телефон%';
Результат: Виведено смартфони iPhone.

<img width="1590" height="395" alt="{D3239A25-249B-4323-904C-4172B5D26D55}" src="https://github.com/user-attachments/assets/e2bbe977-1f2c-446e-94ff-ddda371b6a71" />


16. Самостійно: 3 власні запити з використанням LIKE (початок, кінець, містить).

SQL
-- Пошук за початком: Категорії, що починаються на "Смарт"
SELECT * FROM categories WHERE category_name LIKE 'Смарт%';

-- Пошук за кінцем: Клієнти, що використовують пошту Gmail
SELECT * FROM customers WHERE email LIKE '%@gmail.com';

-- Пошук за вмістом: Товари з роздільною здатністю 4K в описі
SELECT * FROM products WHERE description LIKE '%4K%';
Результат: Запити успішно відфільтрували категорії смартфонів/розумного дому, користувачів Gmail та відповідні телевізори.

<img width="1550" height="497" alt="{C26259DA-E4A1-42F1-A322-2461855B664D}" src="https://github.com/user-attachments/assets/8e8a7677-9f99-4259-b48f-0fb78d62eac2" />


17. Знайти товари дорожчі за 15000 грн і дешевші за 50000 грн.

SQL
SELECT * FROM products WHERE unit_price > 15000 AND unit_price < 50000;
Результат: Отримано 15 позицій у середньому преміум-сегменті.

<img width="1672" height="762" alt="{9003F7FB-CE92-4F99-9DAD-D332A1D4EE20}" src="https://github.com/user-attachments/assets/f781205d-6996-4711-8e6e-12775c8cc989" />


18. Вивести клієнтів з Києва або Львова, які є юридичними особами.

SQL
SELECT * FROM customers 
WHERE city IN ('Київ', 'Львів') AND customer_type = 'company';
Результат: Виведено компанії ТОВ "Бізнес Сістемс", ТОВ "Медіа Продакшн" та ПАТ "Фінанс Груп".

<img width="1628" height="458" alt="{D3361B91-A635-4F52-B5B6-9167F5EA5B45}" src="https://github.com/user-attachments/assets/6c7b01a4-1379-4fe4-b0ce-7a80530c1974" />


19. Самостійно: 4 власні запити з комбінаціями логічних операторів.

SQL
-- Товари, яких мало на складі АБО замовлено багато
SELECT * FROM products WHERE units_in_stock < 5 OR units_on_order >= 10;

-- Співробітники з Києва із зарплатою від 25000
SELECT * FROM employees WHERE city = 'Київ' AND salary >= 25000;

-- Замовлення не доставлені, але з дорогою доставкою
SELECT * FROM orders WHERE NOT order_status = 'delivered' AND freight > 200;

-- Смартфони, які коштують дешевше 20000 АБО їх багато на складі
SELECT * FROM products WHERE category_id = 1 AND (unit_price < 20000 OR units_in_stock > 20);
Результат: Отримано логічно відфільтровані вибірки з різних таблиць з використанням AND, OR, NOT.

<img width="1641" height="393" alt="{0500FE29-A60E-4DC9-93E1-2F6162048AD2}" src="https://github.com/user-attachments/assets/b2215647-2af1-49d2-97d3-4d9a71063ea8" />


20. Вивести клієнтів з міст Київ, Харків, Одеса, Дніпро.

SQL
SELECT * FROM customers WHERE city IN ('Київ', 'Харків', 'Одеса', 'Дніпро');
Результат: Виведено 13 клієнтів із міст-мільйонників.

<img width="1618" height="690" alt="{548C4551-762E-4E31-BA04-9716644E24A0}" src="https://github.com/user-attachments/assets/01e9ad95-6619-42d9-ace4-4bd9134b4e8e" />


21. Знайти товари в ціновому діапазоні від 10000 до 30000 грн.

SQL
SELECT * FROM products WHERE unit_price BETWEEN 10000 AND 30000;
Результат: Виведено 12 товарів середньої цінової категорії.

<img width="1643" height="720" alt="{97F0241E-D1D5-4676-9651-2E96A8A2965E}" src="https://github.com/user-attachments/assets/83a5b703-1f18-4cab-9704-75460536373f" />


22. Самостійно: по 2 запити для операторів IN, BETWEEN, IS NULL / IS NOT NULL.

SQL
-- IN (1): Замовлення, відправлені Новою Поштою або УкрПоштою
SELECT * FROM orders WHERE ship_via IN ('Нова Пошта', 'УкрПошта');
-- IN (2): Співробітники певних регіонів
SELECT * FROM employees WHERE region_id IN (2, 3, 25);

-- BETWEEN (1): Замовлення за перший квартал 2024 року
SELECT * FROM orders WHERE order_date BETWEEN '2024-01-01' AND '2024-03-31';
-- BETWEEN (2): Зарплати в діапазоні 20-30 тис.
SELECT * FROM employees WHERE salary BETWEEN 20000 AND 30000;

-- IS NULL: Клієнти-фізичні особи (без назви компанії)
SELECT * FROM customers WHERE company_name IS NULL;
-- IS NOT NULL: Підлеглі (мають керівника)
SELECT * FROM employees WHERE reports_to IS NOT NULL;
Результат: Відпрацьовано роботу специфічних операторів діапазонів та перевірки на порожнечу (NULL).

<img width="1549" height="537" alt="{A7E650FD-D85E-45EF-BB1F-ABEC85568B4C}" src="https://github.com/user-attachments/assets/2a4e750d-05eb-42ed-86ec-e6ba8b9e5181" />


23. Самостійно: 5 складних запитів (поєднання різних умов).

SQL
-- 1) Доступні на складі товари певних категорій в ціновому діапазоні
SELECT * FROM products 
WHERE category_id IN (1, 2, 7) AND unit_price BETWEEN 15000 AND 40000 AND units_in_stock > 0;

-- 2) Фізичні особи з Києва або Львова зі вказаною поштою
SELECT * FROM customers 
WHERE email LIKE '%@%' AND customer_type = 'individual' AND (city = 'Київ' OR city = 'Львів');

-- 3) Недоставлені серпневі замовлення з дорогою доставкою
SELECT * FROM orders 
WHERE order_status IN ('pending', 'processing') AND order_date BETWEEN '2024-08-01' AND '2024-08-31' AND freight > 150;

-- 4) Менеджери із середньою зарплатою, які комусь підпорядковуються
SELECT * FROM employees 
WHERE title LIKE '%Менеджер%' AND salary BETWEEN 20000 AND 30000 AND reports_to IS NOT NULL;

-- 5) Активні товари брендів Samsung або Apple дорожчі за 20000 грн
SELECT * FROM products 
WHERE (product_name LIKE '%Samsung%' OR product_name LIKE '%Apple%') AND discontinued = false AND unit_price > 20000;
Результат: Успішно виконано складні багатофакторні фільтрації.

<img width="1643" height="499" alt="{352F5BA1-C7D3-4873-A308-B1CA7D60EEDB}" src="https://github.com/user-attachments/assets/6b07cc48-87c3-4e71-aeeb-e9a100238eb2" />

24. Самостійно: 3 запити з сортуванням за кількома полями та 2 з OFFSET.

SQL
-- Сортування 1: Товари за категорією, а в межах категорії - від найдорожчого
SELECT * FROM products ORDER BY category_id ASC, unit_price DESC;

-- Сортування 2: Співробітники за містом, потім за прізвищем
SELECT * FROM employees ORDER BY city ASC, last_name ASC;

-- Сортування 3: Замовлення за статусом, потім за датою спадання
SELECT * FROM orders ORDER BY order_status ASC, order_date DESC;

-- Пагінація 1: Пропустити 10 товарів, показати наступні 5 (сторінка 3 при розмірі 5)
SELECT * FROM products ORDER BY product_id LIMIT 5 OFFSET 10;

-- Пагінація 2: Пропустити перших 5 клієнтів, показати наступних 5
SELECT * FROM customers ORDER BY customer_id LIMIT 5 OFFSET 5;
Результат: Дані успішно відсортовано та продемонстровано механізм пагінації (сторінкового вивостю).

<img width="1609" height="469" alt="{B589895A-F306-48E6-A523-A7209D4C7967}" src="https://github.com/user-attachments/assets/8880c8a3-d042-4579-97c8-c3e93305d2ec" />


Висновки
Самооцінка: 5
Обгрунтування: В ході виконання лабораторної роботи було створено з'єднання з базою даних, досліджено структуру таблиць та зв'язків інтернет-магазину. Успішно відпрацьовано побудову базових SELECT-запитів, фільтрацію за точними значеннями (WHERE), шаблонами (LIKE), діапазонами (BETWEEN) та списками (IN). Створено складні комбіновані запити з використанням логічних операторів. Засвоєно механізми сортування (ORDER BY) та обмеження кількості рядків разом з пагінацією (LIMIT / OFFSET). Всі поставлені завдання Рівня 1-2 виконані коректно.
