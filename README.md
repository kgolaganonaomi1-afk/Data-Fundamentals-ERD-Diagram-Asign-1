# Witle Academy Data-Fundamentals: ERD-Diagram - Assignment 1

## 🗺️ Data-Fundamentals - ERD-Diagram overview:
ERD Diagram of Witle Online Retail System - Understanding the relationships and database-design, entity-relationship-diagram, relational-diagram and data-modelling.

# CONTENTS
###### 1 What is Cardinality?
###### 2 Entities & Attributes at a Glance
###### 3 What Did I Learn?
###### 4 What Tools Did I Use?
###### 5 Conclusions
###### 6 Insights 

# 1 WHAT IS CARDINALITY?
Cardinality answers: How many of this can relate to how many of that? It is the numbers on the line between two tables. We read it from left to right, then right to left.1.1 One-to-One (1:1).

## 📦 The dataset
The full dataset contains 9 CSV files.

| File | Rows | Description |
| ----------------------- | ------- | ---------------------------------------------------- |
| `customers.csv` | 1,400 | One row per customer - name, channel, segment, province, credit limit, assigned sales,representative  |
| `products.csv` | 23 | One row per SKU - product line, pack size, list price, unit cost  |
| `sales_orders.csv` | 45,144 |  One row per order - customer, order date, delivery date, channel, sales representative |
| `sales_lines.csv` | 168,172 | One row per order line - SKU, units, unit price, discount, line revenue, cost of goods  |
| `ar_ledger` | 48,144 |  One row per customer invoice - amount, due date, amount settled, settlement date |
| `reps.csv` | 18 | Sales representatives - territory, monthly target |
| `rep_visits.csv` | 9,400 | Visits made by sales representatives to customers, with the outcome |
| `trade_promotions` | 640 | Promotional support given to a customer on a SKU |
| `vendors.csv` | 74 | Suppliers - type, payment terms |

## How the tables connect.

• sales_orders.customer_id → customers.customer_id

• sales_orders.order_id → sales_lines.order_id

• sales_lines.sku → products.sku

• sales_orders.rep_id and customers.rep_id → reps.rep_id

• ar_ledger.customer_id → customers.customer_id

• rep_visits.customer_id and trade_promotions.customer_id → customers.customer_id

# 2 ENTITIES & ATTRIBUTES AT A GLANCE

The 9 entities:

*1. Customer* - CustomerID (PK), Full Name, Email (unique), Phone, Date Registered
*2. Address* - AddressID (PK), CustomerID (FK), Street, City, Postal Code
*3. Category* - CategoryID (PK), Category Name
*4. Supplier* - SupplierID (PK), Supplier Name, Contact, Email
*5. Product* - ProductID (PK), Name, Description, Price, Stock, CategoryID (FK), SupplierID (FK)
*6. Order* - OrderID (PK), CustomerID (FK), Order Date, Status, Total Amount
*7. OrderItem* - OrderID (FK) + ProductID (FK) together as PK, Quantity, Unit Price
*8. Payment* - PaymentID (PK), OrderID (FK unique), Payment Date, Method, Status, Amount Paid
*9. Delivery* - DeliveryID (PK), OrderID (FK unique), AddressID (FK), Delivery Date, Status, Courier, Tracking No

Every entity has a Primary Key (PK). 
Every relationship has a Foreign Key (FK).

Customer - PK: customer_id - FK: -
Delivery_Address - PK: address_id - FK: customer_id
Category - PK: category_id - FK: -
Supplier - PK: supplier_id - FK: -
Product - PK: product_id - FK: category_id, supplier_id
Order - PK: order_id - FK: customer_id
OrderItem - PK: order_id + product_id - FK: order_id, product_id
Payment - PK: payment_id - FK: order_id (UNIQUE)
Delivery - PK: delivery_id - FK: order_id (UNIQUE), address_id4 

## 📘 3 WHAT DID I LEARN?
Business rules become relationships. 'A customer can have many addresses' is not just a sentence - it becomes 1 to Many. Every rule in the brief turned into a line on the diagram.Never leave a Many-to-Many hanging. Order to Product cannot be stored directly. I resolved it with OrderItem, OrderID + ProductID as the composite key. Hardest part, most important.1 to 1 is about control, not just design. One Order to One Payment and One Order to One Delivery stop fraud. Separate what can grow. Anything a customer can have MANY of needs its own table - otherwise you duplicate the customer or lose data. 

## 4 WHAT TOOLS DID I USE?
diagrams.net (Draw.io) - to draw the ERD. Entities, attributes, PKs / FKs, Crow's Foot notation, all 8 relationships. 
Exports to PDF for GitHub to write up the relationships explained in plain language.dbdiagram.io - to test that tables, keys and relationships make sense when written as code.GitHub - to publish the project: ERD image + README.md + relationships explained.

## 5 CONCLUSIONS
In conclusion, the WitleShop ERD meets every requirement in the brief. It covers all 6 areas the business asked for - Customers, Products, Orders, Payments, Deliveries and Suppliers - using 9 entities: Customer, Delivery_Address, Category, Supplier, Product, Order, OrderItem, Payment and Delivery.Every entity has a primary key, every relationship has a foreign key, and every relationship shows its cardinality: 1 to 1, 1 to Many, and Many to Many. The one Many to Many in the system - Order to Product - is fully resolved with the OrderItem junction table, so no relationship is left unresolved.


## 6 🔍 Key insights (What the ERF Reveals)

Customer is the centre of the whole system. Everything traces back to Customer - addresses, orders, payments, deliveries. If Customer data is wrong, every report downstream is wrong.OrderItem is where the money is made. Customer and Order tell you WHO bought. OrderItem tells you WHAT they bought, HOW MANY, and at WHAT PRICE. Without it, WitleShop cannot answer: 'What did we actually sell today?'1 to 1 relationships are fraud controls, not just design. One Order to One Payment stops double-charging and missing payments. One Order to One Delivery stops a parcel being sent twice or lost. In an audit, I would test these two first.The Delivery Address rule is an anti-fraud control. Delivery must link to one of the customer's OWN registered addresses. That one rule stops an attacker changing the delivery address to their house and stealing the order. 

----


## 📬 References

🔗[DAX function reference](https://learn.microsoft.com/dax/)

📘[Nova Retail Group — Sales Analytics by Clarence Mantiya](https://github.com/Clarence-Mantiya/test-project2/blob/main/README.md?plain=1) for Github layout


---

## ⭐ Let's Connect

- 💼 LinkedIn: https://www.linkedin.com/in/kgolagano-naomi-selebano/
- 📧 Email: kgolaganonaomi1@gmail.com
