# E-Commerce-Database-Management-System
# Project Summary
Name: Simple E-Commerce Database Management System
Purpose: Store and manage users, products, categories, orders, payments and basic inventory for a small online shop.
Goals:Keep normalized relational schema (3NF) for clarity and correctness.
Support basic e-commerce workflows: browse products, create orders, manage stock, process payments, view sales reports.
Provide example queries and transactional procedures for order creation and stock handling.

# ER Overview (ASCII)
users --< orders --< order_items >-- products --< product_images
                 |
               payments

products >-- categories (many-to-many via product_categories)

# Indexing & Performance Tips
Index products(sku), orders(user_id, created_at), order_items(order_id).
Use partial indexes for active orders if dataset large.
For heavy reporting, extract daily aggregates into summary tables.
Use advisory locks or row-level locks when doing concurrent inventory updates. The sample functions use a simple approach — for production prefer SELECT ... FOR UPDATE on inventory rows.

# Security & Data Integrity Notes
Never store plaintext passwords; use a secure hashing function (bcrypt/argon2) — DB stores password_hash.
Sanitize inputs in app layer before passing to DB. Prefer prepared statements / parameterized queries.
Use transactions for multi-step operations (order creation + inventory updates + payment).
Keep sensitive payment data off your DB unless PCI-compliant; store provider transaction IDs only.

# Suggested Next Steps / Extensions
Add product options/variants (size/color) with separate SKUs.
Add promotions/discounts table and coupon redemptions.
Implement soft-deletes (is_active flags) for products/users.
Add audit/log table for order status changes.
Create REST API (FastAPI/Flask/Express) and a simple dashboard to exercise the DB.
