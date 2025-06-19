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
	* `id` - ID поставщика
	* `name` - Наименование поставщика
        * `address` - Адрес поставщика
	* `phone` - Телефон поставщика
	* `email` - E-mail поставщика

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
  
