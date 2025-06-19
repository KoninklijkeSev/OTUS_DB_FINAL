# OTUS_DB_FINAL

## **Проектная работа**
Построить схему базы данных и реализовать свою модель интернет-магазина.

## **Схема**
![scheme](https://github.com/KoninklijkeSev/OTUS_DB_FINAL/blob/main/Scheme+.jpg)

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
    products_price_id INT NOT NULL,
    FOREIGN KEY (product_id) REFERENCES products(id),
    FOREIGN KEY (products_price_id) REFERENCES products_prices(id)
);

COMMENT ON COLUMN sales_details.id IS 'ID деталей покупки';
COMMENT ON COLUMN sales_details.product_id IS 'ID продукта';
COMMENT ON COLUMN sales_details.quantity IS 'Количество';
COMMENT ON COLUMN sales_details.products_price_id IS 'ID цены продукта';

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

COMMENT ON COLUMN sales.id IS 'ID покупки';
COMMENT ON COLUMN sales.customer_id IS 'ID покупателя';
COMMENT ON COLUMN sales.sales_date IS 'Дата покупки';
COMMENT ON COLUMN sales.sales_detalils_id IS 'ID деталей покупки';

--Добавление индексов
CREATE INDEX idx_products_categories_name ON products_categories(name);

CREATE INDEX idx_products_suppliers_name ON products_suppliers(name);

CREATE INDEX idx_products_manufacturers_name ON products_manufacturers(name);

CREATE INDEX idx_products_suppliers_manufacturers_products_suppliers_id ON products_suppliers_manufacturers(products_suppliers_id);
CREATE INDEX idx_products_suppliers_manufacturers_products_manufacturers_id ON products_suppliers_manufacturers(products_manufacturers_id);

CREATE INDEX idx_products_name ON products(name);
CREATE INDEX idx_products_products_categories_id ON products(products_categories_id);
CREATE INDEX idx_products_products_suppliers_id ON products(products_suppliers_id);
CREATE INDEX idx_products_products_details_id ON products(products_details_id);

CREATE INDEX idx_products_prices_product_id ON products_prices(product_id);

CREATE INDEX idx_sales_details_product_id ON sales_details(product_id);
CREATE INDEX idx_sales_details_products_price_id ON sales_details(products_price_id);

CREATE INDEX idx_customers_name ON customers(name);
CREATE INDEX idx_customers_customers_categories_id ON customers(customers_categories_id);

CREATE INDEX idx_customers_categories_name ON customers_categories(name);
CREATE INDEX idx_customers_categories_month_id ON customers_categories(month_id);

CREATE INDEX idx_months_name ON months(name);

CREATE INDEX idx_sales_customer_id ON sales(customer_id);
CREATE INDEX idx_sales_sales_date ON sales(sales_date);
CREATE INDEX idx_sales_sales_details_id ON sales(sales_details_id);
