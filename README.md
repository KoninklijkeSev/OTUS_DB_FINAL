# OTUS_DB_FINAL

## **Проектная работа**
Построить схему базы данных и реализовать свою модель интернет-магазина.

## **Схема**
![scheme](https://github.com/KoninklijkeSev/OTUS_DB_FINAL/blob/main/Scheme.jpg)

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
	* `products_price_id` - ID цены продукта

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
-- Создание таблицы производителей продуктов
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

-- Создание таблицы категорий продуктов
CREATE TABLE products_categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

COMMENT ON COLUMN products_categories.id IS 'ID категории';
COMMENT ON COLUMN products_categories.name IS 'Наименование категории';

-- Создание таблицы поставщиков продуктов
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

-- Создание таблицы деталей продуктов
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

-- Создание таблицы продуктов
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    products_categories_id INT,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    products_suppliers_id INT,
    products_details_id INT,
    products_manufacturers_id INT
);

COMMENT ON COLUMN products.id IS 'ID продукта';
COMMENT ON COLUMN products.products_categories_id IS 'ID категории продукта';
COMMENT ON COLUMN products.name IS 'Наименование продукта';
COMMENT ON COLUMN products.description IS 'Описание продукта';
COMMENT ON COLUMN products.products_suppliers_id IS 'ID поставщика продукта';
COMMENT ON COLUMN products.products_details_id IS 'ID деталей продукта';
COMMENT ON COLUMN products.products_manufacturers_id IS 'ID производителя продукта';

-- Создание таблицы цен продуктов
CREATE TABLE products_prices (
    id SERIAL PRIMARY KEY,
    product_id INT,
    price DECIMAL(10, 2) NOT NULL,
    discount_price DECIMAL(10, 2)
);

COMMENT ON COLUMN products_prices.id IS 'ID цены';
COMMENT ON COLUMN products_prices.product_id IS 'ID продукта';
COMMENT ON COLUMN products_prices.price IS 'Цена продукта';
COMMENT ON COLUMN products_prices.discount_price IS 'Цена продукта со скидкой';

-- Создание таблицы категорий покупателей
CREATE TABLE customers_categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    month_id INT
);

COMMENT ON COLUMN customers_categories.id IS 'ID категории покупателя';
COMMENT ON COLUMN customers_categories.name IS 'Наименование категории покупателя';
COMMENT ON COLUMN customers_categories.month_id IS 'ID месяца';

-- Создание таблицы месяцев
CREATE TABLE months (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

COMMENT ON COLUMN months.id IS 'ID месяца';
COMMENT ON COLUMN months.name IS 'Наименование месяца';

-- Создание таблицы покупателей
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    address TEXT,
    phone VARCHAR(20),
    email VARCHAR(255),
    customers_categories_id INT
);

COMMENT ON COLUMN customers.id IS 'ID покупателя';
COMMENT ON COLUMN customers.name IS 'Имя покупателя';
COMMENT ON COLUMN customers.address IS 'Адрес покупателя';
COMMENT ON COLUMN customers.phone IS 'Телефон покупателя';
COMMENT ON COLUMN customers.email IS 'E-mail покупателя';
COMMENT ON COLUMN customers.customers_categories_id IS 'ID категории покупателя';

-- Создание таблицы деталей покупок
CREATE TABLE sales_details (
    id SERIAL PRIMARY KEY,
    product_id INT,
    quantity INT NOT NULL,
    products_price_id INT
);

COMMENT ON COLUMN sales_details.id IS 'ID деталей покупки';
COMMENT ON COLUMN sales_details.product_id IS 'ID продукта';
COMMENT ON COLUMN sales_details.quantity IS 'Количество продукта';
COMMENT ON COLUMN sales_details.products_price_id IS 'ID цены продукта';

-- Создание таблицы покупок
CREATE TABLE sales (
    id SERIAL PRIMARY KEY,
    customer_id INT,
    sales_date DATE NOT NULL,
    sales_details_id INT
);

COMMENT ON COLUMN sales.id IS 'ID покупки';
COMMENT ON COLUMN sales.customer_id IS 'ID покупателя';
COMMENT ON COLUMN sales.sales_date IS 'Дата покупки';
COMMENT ON COLUMN sales.sales_details_id IS 'ID деталей покупки';

-- Создание таблицы сводной таблицы поставщиков и производителей
CREATE TABLE products_suppliers_manufacturers (
    id SERIAL PRIMARY KEY,
    products_suppliers_id INT,
    products_manufacturers_id INT
);

COMMENT ON COLUMN products_suppliers_manufacturers.id IS 'ID поставщиков и производителей';
COMMENT ON COLUMN products_suppliers_manufacturers.products_suppliers_id IS 'ID поставщиков продуктов';
COMMENT ON COLUMN products_suppliers_manufacturers.products_manufacturers_id IS 'ID производителей продуктов';

-- Установка внешних ключей и ограничений

ALTER TABLE products
ADD CONSTRAINT fk_products_categories_id
FOREIGN KEY (products_categories_id) REFERENCES products_categories(id);

ALTER TABLE products
ADD CONSTRAINT fk_products_suppliers_id
FOREIGN KEY (products_suppliers_id) REFERENCES products_suppliers(id);

ALTER TABLE products
ADD CONSTRAINT fk_products_details_id
FOREIGN KEY (products_details_id) REFERENCES products_details(id);

ALTER TABLE products
ADD CONSTRAINT fk_products_manufacturers_id
FOREIGN KEY (products_manufacturers_id) REFERENCES products_manufacturers(id);

ALTER TABLE products_prices
ADD CONSTRAINT fk_product_id
FOREIGN KEY (product_id) REFERENCES products(id);

ALTER TABLE customers_categories
ADD CONSTRAINT fk_month_id
FOREIGN KEY (month_id) REFERENCES months(id);

ALTER TABLE customers
ADD CONSTRAINT fk_customers_categories_id
FOREIGN KEY (customers_categories_id) REFERENCES customers_categories(id);

ALTER TABLE sales_details
ADD CONSTRAINT fk_product_id_sales_details
FOREIGN KEY (product_id) REFERENCES products(id);

ALTER TABLE sales_details
ADD CONSTRAINT fk_products_price_id
FOREIGN KEY (products_price_id) REFERENCES products_prices(id);

ALTER TABLE sales
ADD CONSTRAINT fk_customer_id
FOREIGN KEY (customer_id) REFERENCES customers(id);

ALTER TABLE sales
ADD CONSTRAINT fk_sales_details_id
FOREIGN KEY (sales_details_id) REFERENCES sales_details(id);

ALTER TABLE products_suppliers_manufacturers
ADD CONSTRAINT fk_products_suppliers_id
FOREIGN KEY (products_suppliers_id) REFERENCES products_suppliers(id);

ALTER TABLE products_suppliers_manufacturers
ADD CONSTRAINT fk_products_manufacturers_id
FOREIGN KEY (products_manufacturers_id) REFERENCES products_manufacturers(id);
