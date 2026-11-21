# Data-Fundamentals-ERD-Diagram-Asign-1
ERD Diagram of Witle Online Retail System - Understanding the relationships and database-design, entity-relationship-diagram, relational-diagram and data-modelling.

# CONTENTS
## 1 What is Cardinality?
## 2 Entities & Attributes at a Glance
## 3 What Did I Learn?
## 4 What Tools Did I Use?
## 5 Conclusions
## 6 Insights 

# 1 WHAT IS CARDINALITY?
Cardinality answers: How many of this can relate to how many of that? It is the numbers on the line between two tables. We read it from left to right, then right to left.1.1 One-to-One (1:1).

# 2 ENTITIES & ATTRIBUTES AT A GLANCE
Every entity has a Primary Key (PK). Every relationship has a Foreign Key (FK).Customer - PK: customer_id - FK: -
Delivery_Address - PK: address_id - FK: customer_id
Category - PK: category_id - FK: -
Supplier - PK: supplier_id - FK: -
Product - PK: product_id - FK: category_id, supplier_id
Order - PK: order_id - FK: customer_id
OrderItem - PK: order_id + product_id - FK: order_id, product_id
Payment - PK: payment_id - FK: order_id (UNIQUE)
Delivery - PK: delivery_id - FK: order_id (UNIQUE), address_id4 

## 3 WHAT DID I LEARN?
Business rules become relationships. 'A customer can have many addresses' is not just a sentence - it becomes 1 to Many. Every rule in the brief turned into a line on the diagram.Never leave a Many-to-Many hanging. Order to Product cannot be stored directly. I resolved it with OrderItem, OrderID + ProductID as the composite key. Hardest part, most important.1 to 1 is about control, not just design. One Order to One Payment and One Order to One Delivery stop fraud. Separate what can grow. Anything a customer can have MANY of needs its own table - otherwise you duplicate the customer or lose data. 

## 4 WHAT TOOLS DID I USE?
diagrams.net (Draw.io) - to draw the ERD. Entities, attributes, PKs / FKs, Crow's Foot notation, all 8 relationships. 
Exports to PDF for GitHub to write up the relationships explained in plain language.dbdiagram.io - to test that tables, keys and relationships make sense when written as code.GitHub - to publish the project: ERD image + README.md + relationships explained.

## 5 CONCLUSIONS
In conclusion, the WitleShop ERD meets every requirement in the brief. It covers all 6 areas the business asked for - Customers, Products, Orders, Payments, Deliveries and Suppliers - using 9 entities: Customer, Delivery_Address, Category, Supplier, Product, Order, OrderItem, Payment and Delivery.Every entity has a primary key, every relationship has a foreign key, and every relationship shows its cardinality: 1 to 1, 1 to Many, and Many to Many. The one Many to Many in the system - Order to Product - is fully resolved with the OrderItem junction table, so no relationship is left unresolved.

## 6 INSIGHTS - WHAT THE ERD REVEALS
Customer is the centre of the whole system. Everything traces back to Customer - addresses, orders, payments, deliveries. If Customer data is wrong, every report downstream is wrong.OrderItem is where the money is made. Customer and Order tell you WHO bought. OrderItem tells you WHAT they bought, HOW MANY, and at WHAT PRICE. Without it, WitleShop cannot answer: 'What did we actually sell today?'1 to 1 relationships are fraud controls, not just design. One Order to One Payment stops double-charging and missing payments. One Order to One Delivery stops a parcel being sent twice or lost. In an audit, I would test these two first.The Delivery Address rule is an anti-fraud control. Delivery must link to one of the customer's OWN registered addresses. That one rule stops an attacker changing the delivery address to their house and stealing the order. 
