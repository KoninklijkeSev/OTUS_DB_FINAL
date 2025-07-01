# OTUS_DB_FINAL

## **Проектная работа**
Построить схему базы данных и реализовать свою модель интернет-магазина.

## **Схема**
![scheme](https://github.com/KoninklijkeSev/OTUS_DB_FINAL/blob/main/Screenshot++.jpg)

## **Описание таблиц и полей**

* Продукты (`products`)
	* `id` - ID продукта
	* `products_categories_id` - ID категории
	* `name` - Наименование продукта
	* `description` - Описание продукта
	* `products_suppliers_id` - ID поставщика
	* `products_details_id` - ID деталей

* Детали продукта (`products_details`)
	* `id` - ID деталей
	* `delivery_date` - дата поставки
	* `manufacture_date` - Дата поставки
	* `best_by_date` - Срок годности
	* `expiration_date` - Дата истечения срока годности

* Категории продуктов (`products_categories`)
	* `id` - ID категории
	* `name` - Наименование категории

* Поставщики продуктов (`products_suppliers`)
	* `id` - ID поставщика
	* `name` - Наименование поставщика
	* `address` - Адрес поставщика
	* `phone` - Телефон поставщика
	* `email` - E-mail поставщика
 
* Производители продуктов (`products_manufacturers`)
	* `id` - ID производителя
	* `name` - Наименование производителя
	* `address` - Адрес производителя
	* `phone` - Телефон производителя
	* `email` - E-mail производителя

* Цены продуктов (`products_prices`)
	* `id` - ID цены
	* `product_id` - ID продукта
	* `price` - Цена
	* `discount_price` - Цена скидки
   
* Детали покупки (`sales_details`)
	* `id` - ID деталей прокупки
	* `product_id` - ID продукта
	* `quantity` - Количество

* Покупки (`sales`)
	* `id` - ID покупки
	* `customer_id` - ID покупателя
	* `sales_date` - Дата покупки
	* `sales_detalils_id` - ID деталей покупки

* Покупатели (`customers`)
	* `id` - ID покупателя
	* `name` - Имя покупателя
	* `address` - Адрес покупателя
	* `phone` - Телефон покупателя
	* `email` - E-mail покупателя
  * `customers_categories_id` - ID категорий покупателя
 
* Категории покупателя (`customers_categories`)
	* `id` - ID категории покупателя
	* `name` - Наименование категории
	* `month_id` - ID месяца

 * Месяца (`months`)
	* `id` - ID месяца
	* `name` - Наименование месяца

  * Сводная таблица поставщиков и производителей (`products_suppliers_manufacturers`)
	* `id` - ID поставщиков и производителей
	* `products_suppliers_id` - ID поставщиков продуктов
	* `products_manufacturers_id` - ID производителей продуктов
   
## **Скрипт генерации объектов**

 ```sql
-- Создание таблицы Категорий продуктов (products_categories)
CREATE TABLE products_categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

COMMENT ON COLUMN products_categories.id IS 'ID категории';
COMMENT ON COLUMN products_categories.name IS 'Наименование категории';

-- Создание таблицы Поставщики продуктов (products_suppliers)
CREATE TABLE products_suppliers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(255)
);

COMMENT ON COLUMN products_suppliers.id IS 'ID поставщика';
COMMENT ON COLUMN products_suppliers.name IS 'Наименование поставщика';
COMMENT ON COLUMN products_suppliers.address IS 'Адрес поставщика';
COMMENT ON COLUMN products_suppliers.phone IS 'Телефон поставщика';
COMMENT ON COLUMN products_suppliers.email IS 'E-mail поставщика';

-- Создание таблицы Производители продуктов (products_manufacturers)
CREATE TABLE products_manufacturers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(255)
);

COMMENT ON COLUMN products_manufacturers.id IS 'ID производителя';
COMMENT ON COLUMN products_manufacturers.name IS 'Наименование производителя';
COMMENT ON COLUMN products_manufacturers.address IS 'Адрес производителя';
COMMENT ON COLUMN products_manufacturers.phone IS 'Телефон производителя';
COMMENT ON COLUMN products_manufacturers.email IS 'E-mail производителя';

-- Создание таблицы Детали продукта (products_details)
CREATE TABLE products_details (
    id SERIAL PRIMARY KEY,
    delivery_date DATE,
    manufacture_date DATE,
    best_by_date DATE,
    expiration_date DATE
);

COMMENT ON COLUMN products_details.id IS 'ID деталей';
COMMENT ON COLUMN products_details.delivery_date IS 'Дата поставки';
COMMENT ON COLUMN products_details.manufacture_date IS 'Дата производства';
COMMENT ON COLUMN products_details.best_by_date IS 'Срок годности';
COMMENT ON COLUMN products_details.expiration_date IS 'Дата истечения срока годности';

-- Создание таблицы Сводная таблица поставщиков и производителей (products_suppliers_manufacturers)
CREATE TABLE products_suppliers_manufacturers (
    id SERIAL PRIMARY KEY,
    products_suppliers_id INT NOT NULL,
    products_manufacturers_id INT NOT NULL,
    FOREIGN KEY (products_suppliers_id) REFERENCES products_suppliers(id),
    FOREIGN KEY (products_manufacturers_id) REFERENCES products_manufacturers(id)
);

COMMENT ON COLUMN products_suppliers_manufacturers.id IS 'ID поставщиков и производителей';
COMMENT ON COLUMN products_suppliers_manufacturers.products_suppliers_id IS 'ID поставщиков продуктов';
COMMENT ON COLUMN products_suppliers_manufacturers.products_manufacturers_id IS 'ID производителей продуктов';

-- Создание таблицы Продукты (products)
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    products_categories_id INT NOT NULL,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    products_suppliers_id INT NOT NULL,
    products_details_id INT NOT NULL,
    FOREIGN KEY (products_categories_id) REFERENCES products_categories(id),
    FOREIGN KEY (products_suppliers_id) REFERENCES products_suppliers(id),
    FOREIGN KEY (products_details_id) REFERENCES products_details(id)
);

COMMENT ON COLUMN products.id IS 'ID продукта';
COMMENT ON COLUMN products.products_categories_id IS 'ID категории';
COMMENT ON COLUMN products.name IS 'Наименование продукта';
COMMENT ON COLUMN products.description IS 'Описание продукта';
COMMENT ON COLUMN products.products_suppliers_id IS 'ID поставщика';
COMMENT ON COLUMN products.products_details_id IS 'ID деталей';

-- Создание таблицы Цены продуктов (products_prices)
CREATE TABLE products_prices (
    id SERIAL PRIMARY KEY,
    product_id INT NOT NULL,
    price NUMERIC(10, 2) NOT NULL,
    discount_price NUMERIC(10, 2),
    FOREIGN KEY (product_id) REFERENCES products(id)
);

COMMENT ON COLUMN products_prices.id IS 'ID цены';
COMMENT ON COLUMN products_prices.product_id IS 'ID продукта';
COMMENT ON COLUMN products_prices.price IS 'Цена';
COMMENT ON COLUMN products_prices.discount_price IS 'Цена скидки';

-- Создание таблицы Детали покупки (sales_details)
CREATE TABLE sales_details (
    id SERIAL PRIMARY KEY,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    FOREIGN KEY (product_id) REFERENCES products(id)
);

COMMENT ON COLUMN sales_details.id IS 'ID деталей покупки';
COMMENT ON COLUMN sales_details.product_id IS 'ID продукта';
COMMENT ON COLUMN sales_details.quantity IS 'Количество';

-- Создание таблицы Месяца (months)
CREATE TABLE months (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

COMMENT ON COLUMN months.id IS 'ID месяца';
COMMENT ON COLUMN months.name IS 'Наименование месяца';

-- Создание таблицы Категории покупателя (customers_categories)
CREATE TABLE customers_categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    month_id INT NOT NULL,
    FOREIGN KEY (month_id) REFERENCES months(id)
);

COMMENT ON COLUMN customers_categories.id IS 'ID категории покупателя';
COMMENT ON COLUMN customers_categories.name IS 'Наименование категории';
COMMENT ON COLUMN customers_categories.month_id IS 'ID месяца';


-- Создание таблицы Покупатели (customers)
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(255),
    customers_categories_id INT NOT NULL,
    FOREIGN KEY (customers_categories_id) REFERENCES customers_categories(id)
);

COMMENT ON COLUMN customers.id IS 'ID покупателя';
COMMENT ON COLUMN customers.name IS 'Имя покупателя';
COMMENT ON COLUMN customers.address IS 'Адрес покупателя';
COMMENT ON COLUMN customers.phone IS 'Телефон покупателя';
COMMENT ON COLUMN customers.email IS 'E-mail покупателя';
COMMENT ON COLUMN customers.customers_categories_id IS 'ID категорий покупателя';

-- Создание таблицы Покупки (sales)
CREATE TABLE sales (
    id SERIAL PRIMARY KEY,
    customer_id INT NOT NULL,
    sales_date DATE NOT NULL,
    sales_details_id INT NOT NULL,
    FOREIGN KEY (customer_id) REFERENCES customers(id),
    FOREIGN KEY (sales_details_id) REFERENCES sales_details(id)
);

COMMENT ON COLUMN sales.id IS 'ID покупки';
COMMENT ON COLUMN sales.customer_id IS 'ID покупателя';
COMMENT ON COLUMN sales.sales_date IS 'Дата покупки';
COMMENT ON COLUMN sales.sales_details_id IS 'ID деталей покупки';

-- Добавление уникального ограничения для таблицы products_manufacturers
ALTER TABLE products_manufacturers ADD CONSTRAINT unique_manufacturer_name UNIQUE (name);

-- Добавление уникального ограничения для таблицы products_suppliers
ALTER TABLE products_suppliers ADD CONSTRAINT unique_supplier_name UNIQUE (name);

-- Добавление уникального ограничения для таблицы products_categories
ALTER TABLE products_categories ADD CONSTRAINT unique_category_name UNIQUE (name);

-- Добавление уникального ограничения для таблицы products_suppliers_manufacturers
ALTER TABLE products_suppliers_manufacturers ADD CONSTRAINT unique_supplier_manufacturer UNIQUE (products_suppliers_id, products_manufacturers_id);

--Добавление данных в таблицу
-- Вставка данных в таблицу Категорий продуктов (products_categories)
INSERT INTO products_categories (name) VALUES
('Овощи и фрукты'),
('Молочные продукты'),
('Мясо и рыба'),
('Зерновые продукты'),
('Напитки');

-- Вставка данных в таблицу Поставщики продуктов (products_suppliers)
INSERT INTO products_suppliers (name, address, phone, email) VALUES
('Поставщик Овощей', 'ул. Овощная 1', '1234567890', 'supplier_vegetables@example.com'),
('Поставщик Молочных Продуктов', 'ул. Молочная 2', '0987654321', 'supplier_dairy@example.com'),
('Поставщик Мяса и Рыбы', 'ул. Мясная 3', '1122334455', 'supplier_meat_fish@example.com'),
('Поставщик Зерновых Продуктов', 'ул. Зерновая 4', '5544332211', 'supplier_grains@example.com'),
('Поставщик Напитков', 'ул. Напитковая 5', '6677889900', 'supplier_drinks@example.com');

-- Вставка данных в таблицу Производители продуктов (products_manufacturers)
INSERT INTO products_manufacturers (name, address, phone, email) VALUES
('Производитель Овощей', 'ул. Овощная 10', '1234567890', 'manufacturer_vegetables@example.com'),
('Производитель Молочных Продуктов', 'ул. Молочная 20', '0987654321', 'manufacturer_dairy@example.com'),
('Производитель Мяса и Рыбы', 'ул. Мясная 30', '1122334455', 'manufacturer_meat_fish@example.com'),
('Производитель Зерновых Продуктов', 'ул. Зерновая 40', '5544332211', 'manufacturer_grains@example.com'),
('Производитель Напитков', 'ул. Напитковая 50', '6677889900', 'manufacturer_drinks@example.com');

-- Вставка данных в таблицу Детали продукта (products_details)
INSERT INTO products_details (delivery_date, manufacture_date, best_by_date, expiration_date) VALUES
('2023-10-01', '2023-09-01', '2024-09-01', '2024-10-01'),
('2023-10-02', '2023-09-02', '2024-09-02', '2024-10-02'),
('2023-10-03', '2023-09-03', '2024-09-03', '2024-10-03'),
('2023-10-04', '2023-09-04', '2024-09-04', '2024-10-04'),
('2023-10-05', '2023-09-05', '2024-09-05', '2024-10-05');

-- Вставка данных в таблицу Сводная таблица поставщиков и производителей (products_suppliers_manufacturers)
INSERT INTO products_suppliers_manufacturers (products_suppliers_id, products_manufacturers_id) VALUES
(1, 1), (2, 2), (3, 3), (4, 4), (5, 5);

-- Вставка данных в таблицу Продукты (products)
INSERT INTO products (products_categories_id, name, description, products_suppliers_id, products_details_id) VALUES
(1, 'Яблоки', 'Свежие яблоки из Испании', 1, 1),
(2, 'Молоко', 'Молоко цельное', 2, 2),
(3, 'Говядина', 'Мраморная говядина', 3, 3),
(4, 'Рис', 'Рис басмати', 4, 4),
(5, 'Кола', 'Кола без сахара', 5, 5);

-- Вставка данных в таблицу Цены продуктов (products_prices)
INSERT INTO products_prices (product_id, price, discount_price) VALUES
(1, 100.00, 90.00),
(2, 80.00, 72.00),
(3, 300.00, 270.00),
(4, 50.00, 45.00),
(5, 60.00, 54.00);

-- Вставка данных в таблицу Детали покупки (sales_details)
INSERT INTO sales_details (product_id, quantity) VALUES
(1, 2),
(2, 3),
(3, 1),
(4, 5),
(5, 4);

-- Вставка данных в таблицу Покупатели (customers)
INSERT INTO customers (name, address, phone, email, customers_categories_id) VALUES
('Иван Иванов', 'ул. Покупателей 1', '1234567890', 'ivan@example.com', 1),
('Мария Петрова', 'ул. Покупателей 2', '0987654321', 'maria@example.com', 2),
('Алексей Сидоров', 'ул. Покупателей 3', '1122334455', 'aleksey@example.com', 3),
('Елена Николаева', 'ул. Покупателей 4', '5544332211', 'elena@example.com', 4),
('Дмитрий Васильев', 'ул. Покупателей 5', '6677889900', 'dmitriy@example.com', 5);

-- Вставка данных в таблицу Категории покупателя (customers_categories)
INSERT INTO customers_categories (name, month_id) VALUES
('Овощи и фрукты', 1),
('Молочные продукты', 2),
('Мясо и рыба', 3),
('Зерновые продукты', 4),
('Напитки', 5);

-- Вставка данных в таблицу Месяца (months)
INSERT INTO months (name) VALUES
('Январь'),
('Февраль'),
('Март'),
('Апрель'),
('Май');

-- Вставка данных в таблицу Покупки (sales)
INSERT INTO sales (customer_id, sales_date, sales_details_id) VALUES
(1, '2023-10-01', 1),
(2, '2023-10-02', 2),
(3, '2023-10-03', 3),
(4, '2023-10-04', 4),
(5, '2023-10-05', 5);

## **Примеры хранимых процедур**
## **Хранимая процедура, которая будет собирать данные о продукте, при запросе ID продукта**

--Код процедуры
CREATE OR REPLACE PROCEDURE get_product_info(
    IN product_id INT,
    INOUT product_name VARCHAR(255),
    INOUT category_name VARCHAR(255),
    INOUT product_description TEXT,
    INOUT supplier_name VARCHAR(255),
    INOUT manufacturer_name VARCHAR(255)
)
AS $$
BEGIN
    SELECT
        p.name,
        pc.name,
        p.description,
        ps.name,
        pm.name
    INTO
        product_name,
        category_name,
        product_description,
        supplier_name,
        manufacturer_name
    FROM
        products p
            JOIN
        products_categories pc ON p.products_categories_id = pc.id
            JOIN
        products_suppliers ps ON p.products_suppliers_id = ps.id
            JOIN
        products_suppliers_manufacturers psm ON ps.id = psm.products_suppliers_id
            JOIN
        products_manufacturers pm ON psm.products_manufacturers_id = pm.id
    WHERE
        p.id = product_id;
END;
$$ LANGUAGE plpgsql;

--Вызов процедуры get_product_info, чтобы узнать информацию о продукте с ID = 1
CALL get_product_info(
        1,
        NULL::VARCHAR(255),
        NULL::VARCHAR(255),
        NULL::TEXT,
        NULL::VARCHAR(255),
        NULL::VARCHAR(255)
     );

--Удаление процедуры get_product_info
DROP PROCEDURE IF EXISTS get_product_info(p_product_id INT);

## **Хранимая процедура, которая вносит данные о новом товаре**
--Код процедуры
CREATE OR REPLACE PROCEDURE insert_product_data(
    IN manufacturer_name VARCHAR(255),
    IN manufacturer_address TEXT,
    IN manufacturer_phone VARCHAR(20),
    IN manufacturer_email VARCHAR(255),
    IN supplier_name VARCHAR(255),
    IN supplier_address TEXT,
    IN supplier_phone VARCHAR(20),
    IN supplier_email VARCHAR(255),
    IN delivery_date DATE,
    IN manufacture_date DATE,
    IN best_by_date DATE,
    IN expiration_date DATE,
    IN category_name VARCHAR(255),
    IN product_name VARCHAR(255),
    IN product_description TEXT,
    IN price NUMERIC(10, 2),
    IN discount_price NUMERIC(10, 2)
)
AS $$
DECLARE
    v_manufacturer_id INT;
    v_supplier_id INT;
    v_details_id INT;
    v_product_id INT;
    v_category_id INT;
BEGIN
    -- Вставка или обновление производителя
    INSERT INTO products_manufacturers (name, address, phone, email)
    VALUES (manufacturer_name, manufacturer_address, manufacturer_phone, manufacturer_email)
    ON CONFLICT (name) DO UPDATE SET
                                     address = EXCLUDED.address,
                                     phone = EXCLUDED.phone,
                                     email = EXCLUDED.email
    RETURNING id INTO v_manufacturer_id;

    -- Вставка или обновление поставщика
    INSERT INTO products_suppliers (name, address, phone, email)
    VALUES (supplier_name, supplier_address, supplier_phone, supplier_email)
    ON CONFLICT (name) DO UPDATE SET
                                     address = EXCLUDED.address,
                                     phone = EXCLUDED.phone,
                                     email = EXCLUDED.email
    RETURNING id INTO v_supplier_id;

    -- Вставка деталей продукта
    INSERT INTO products_details (delivery_date, manufacture_date, best_by_date, expiration_date)
    VALUES (delivery_date, manufacture_date, best_by_date, expiration_date)
    RETURNING id INTO v_details_id;

    -- Вставка или получение существующей категории продукта
    INSERT INTO products_categories (name)
    VALUES (category_name)
    ON CONFLICT (name) DO UPDATE SET name = EXCLUDED.name
    RETURNING id INTO v_category_id;

    -- Вставка продукта
    INSERT INTO products (products_categories_id, name, description, products_suppliers_id, products_details_id)
    VALUES (v_category_id, product_name, product_description, v_supplier_id, v_details_id)
    RETURNING id INTO v_product_id;

    -- Вставка цены продукта
    INSERT INTO products_prices (product_id, price, discount_price)
    VALUES (v_product_id, price, discount_price);

    -- Связывание поставщика и производителя
    INSERT INTO products_suppliers_manufacturers (products_suppliers_id, products_manufacturers_id)
    VALUES (v_supplier_id, v_manufacturer_id)
    ON CONFLICT (products_suppliers_id, products_manufacturers_id) DO NOTHING;
END;
$$ LANGUAGE plpgsql;

--Вызов процедуры insert_product_data
CALL insert_product_data(
        'Производитель 99', 'Адрес производителя 99', '1234567890', 'manufacturer99@example.com',
        'Поставщик 99', 'Адрес поставщика 99', '0987654321', 'supplier99@example.com',
        '2023-10-01', '2023-09-01', '2024-09-30', '2024-10-01',
        'Категория 199', 'Продукт 99', 'Описание продукта 99', 100.00, 90.00);

## **Хранимая функция, которая будет проверять, если ли в списке покупок категории товаров на которые у покупателя выбрана скидка**
--Код процедуры
CREATE OR REPLACE FUNCTION check_customer_discount_categories(
    p_customer_id INT,
    p_sale_id INT
)
    RETURNS TABLE (
                      category_name VARCHAR(255),
                      has_discount BOOLEAN
                  )
AS $$
BEGIN
    RETURN QUERY
        SELECT
            pc.name AS category_name,
            CASE WHEN cc.name = pc.name THEN TRUE ELSE FALSE END AS has_discount
        FROM
            sales s
                JOIN
            sales_details sd ON s.sales_details_id = sd.id
                JOIN
            products p ON sd.product_id = p.id
                JOIN
            products_categories pc ON p.products_categories_id = pc.id
                LEFT JOIN
            customers c ON s.customer_id = c.id
                LEFT JOIN
            customers_categories cc ON c.customers_categories_id = cc.id
        WHERE
            s.id = p_sale_id AND s.customer_id = p_customer_id;
END;
$$ LANGUAGE plpgsql;

--Вызов функции check_customer_discount_categories
SELECT check_customer_discount_categories(1, 1);

## **Хранимая функция, которая будет выгружать покупателей**
--Код процедуры
CREATE OR REPLACE FUNCTION export_customers()
    RETURNS TABLE (
                      customer_id INT,
                      customer_name VARCHAR(255),
                      customer_address TEXT,
                      customer_phone VARCHAR(20),
                      customer_email VARCHAR(255),
                      category_name VARCHAR(255),
                      discount_month VARCHAR(255)
                  )
    LANGUAGE plpgsql
AS $$
BEGIN
    RETURN QUERY
        SELECT
            c.id AS customer_id,
            c.name AS customer_name,
            c.address AS customer_address,
            c.phone AS customer_phone,
            c.email AS customer_email,
            cc.name AS category_name,
            m.name AS discount_month
        FROM
            customers c
                JOIN
            customers_categories cc ON c.customers_categories_id = cc.id
                JOIN
            months m ON cc.month_id = m.id
        ORDER BY
            c.id;
END;
$$;

--Вызов функции export_customers
SELECT export_customers();
