# ДЗ 4 · DDL, DML і бізнес-запити: Olist

Типізована схема Olist з PK/FK/CHECK, зміна записів, JOIN, агрегування, сегментація покупців і оцінки продавців.

[Відкрити у Google Colab](https://colab.research.google.com/github/humanistitel/goit-rdb-hw-04/blob/main/Diuryk_hw4_olist.ipynb) · [Завантажити notebook](https://raw.githubusercontent.com/humanistitel/goit-rdb-hw-04/main/Diuryk_hw4_olist.ipynb)

## Запуск

У Colab оберіть CPU та натисніть **Runtime → Run all**. Перша клітинка готує залежності й тимчасовий PostgreSQL 16; остання зупиняє сервер. Перший запуск потребує інтернету. Якщо виконання перервано, запустіть останню клітинку для зупинки сервера.

Локально: Jupyter та Python 3.9–3.12.

## Дані

[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce), Olist, ліцензія [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).

Відсутні CSV завантажуються з [офіційного Kaggle ZIP, версія 2](https://www.kaggle.com/api/v1/datasets/download/olistbr/brazilian-ecommerce?datasetVersionNumber=2), storage version `55151/2669146`. ZIP має 44 717 580 байтів; SHA-256 `967e41e04fc306fe604e2a693f488995a8b41e5047418f8a5c8e4abd6deca784`.

| Таблиця | Записів |
| --- | ---: |
| customers | 99 441 |
| orders | 99 441 |
| order_items | 112 650 |
| products | 32 951 |
| sellers | 3 095 |
| order_reviews | 99 224 |

## Запити

CSV спочатку завантажуються в raw-таблиці; SQL формує типізовані таблиці. Приклади містять INSERT, UPDATE, DELETE, upsert, п’ять типів JOIN, GROUP BY/HAVING та віконні функції.

Сегментація використовує `customer_unique_id` і дату 2018-10-18. Відгук належить замовленню, тому оцінка замовлення з кількома продавцями спільна для них. Порядок округлення оцінок і правила обчислення сум наведено в notebook.
