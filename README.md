🛒 **E-COMMERCE ANALYTICS ENGINE (Using SQL, Python & MySQL)**


An interactive and insight-driven e-commerce analytics pipeline built using Python, SQL (MySQL), and Pandas to monitor product data, user behavior, order performance, and revenue insights — enabling smarter, data-driven business decisions for online retail.

📄 **Description**
•This analytics engine provides a comprehensive overview of e-commerce operations by analyzing product catalogs, user profiles, cart/order data, and category trends.
•Python was used to extract data from multiple public REST APIs (FakeStore API, DummyJSON, JSONPlaceholder), transform and clean it, and load it into a structured MySQL database — a complete ETL pipeline.
•The system highlights key metrics such as total products, total users, total orders, revenue, and category-level breakdowns, while generating exportable CSV and JSON reports for use in dashboards or further analysis.

💻 **SQL Analysis & Data Processing**
Structured and executed SQL queries to transform raw API data into meaningful business insights, supporting report generation and decision-making.
Key Contributions:

• Extracted and aggregated product data to measure overall catalog volume, category distribution, and rating performance across multiple API sources.
• Performed financial analysis by calculating total revenue from all orders using SUM(total_price) to track platform cash flow.
• Analyzed category-level statistics — product count, average price, minimum and maximum prices — to identify top-performing segments.
• Evaluated product rating trends to surface the highest-rated items and understand quality distribution across the catalog.
• Conducted price range analysis to bucket products into affordability segments for targeted pricing decisions.
• Measured source-level data volume by tracking records from each API source (fakestoreapi, dummyjson, jsonplaceholder) to ensure pipeline health.
• Processed and cleaned multi-source datasets using SQL functions like JOIN, GROUP BY, COUNT, SUM, AVG, ROUND, and ON DUPLICATE KEY UPDATE for idempotent data loading.


📊 **Key Insights & Reports Generated**

• 📊 Category Breakdown Report — Product count and price stats per category (CSV)
• ⭐ Top Rated Products Report — Highest-rated products ranked by rating and count (CSV)
• 💰 Price Distribution Report — Products bucketed by price range (budget / mid / premium)
• 🌐 Source Stats Report — Record count by API data source
• 📁 Full Analytics JSON — All KPIs exported as a single structured JSON file (daily)


💳 **Key KPI Metrics**

• 🛍️ Total Products — Aggregated across FakeStore and DummyJSON APIs
• 👥 Total Users — Combined from FakeStore and JSONPlaceholder
• 📦 Total Orders — Derived from cart data fetched via API
• 💰 Total Revenue — Summed from all order totals in the database
• ⭐ Average Rating — Computed per product and per category
• 🏷️ Price Range Distribution — Budget / Mid-range / Premium segmentation


🔄 **ETL Pipeline Architecture**
Extract →

• fetch_fakestore_products() — Pulls all products from FakeStore REST API
• fetch_dummyjson_products() — Paginated fetch (30/page) from DummyJSON API
• fetch_fakestore_users() + fetch_jsonplaceholder_users() — Dual-source user data
• fetch_fakestore_carts() — Cart/order data extraction

Transform →

• Field normalization (title truncation, price rounding, email lowercasing)
• ID collision prevention (DummyJSON IDs offset by +1000, JSONPlaceholder by +100)
• Category standardization (lowercase, stripped whitespace)
• Data type validation and null-safe defaults

Load →

INSERT ... ON DUPLICATE KEY UPDATE for idempotent upserts into MySQL
ETL run logs stored in etl_logs table (timestamp, table name, status, record count)


🗄️ **Database Schema**
TableKey Columnsproductsid, title, price, category, rating, rating_count, source_apiusersid, username, email, phone, cityordersid, user_id, total_price, products_count, source_apietl_logsid, run_time, table_name, status, records

🎛️ Interactive CLI Menu
╔══════════════════════════════════════════╗
║    E-Commerce Analytics Engine          ║
╠══════════════════════════════════════════╣
║  1. ETL Run      (APIs → Database)       ║
║  2. Report Gen   (Database → CSV/JSON)   ║
║  3. Full Run     (ETL + Report)          ║
║  4. Scheduler    (Daily 8 AM auto-run)   ║
║  5. Exit                                 ║
╚══════════════════════════════════════════╝

🌟 **Features**
📈 Business Impact & Insights

• 💰 Revenue Tracking — Monitor total order value and identify high-revenue product categories
• 🛍️ Catalog Intelligence — Understand product mix, pricing tiers, and rating quality
• 👥 User Analytics — Track user base growth across multiple data sources
• 🌐 Multi-Source Pipeline — Unified analytics across 3 different REST APIs
• 📊 Operational Efficiency — Automated daily ETL + report generation via scheduler
• 🔄 Idempotent Loads — Safe re-runs with ON DUPLICATE KEY UPDATE — no duplicate data


🎯 **Goal of the Project**
To build a robust and automated e-commerce analytics engine that:

• Fetches and unifies product, user, and order data from multiple APIs
• Cleans and normalizes raw data into a structured MySQL database
• Generates daily analytics reports (CSV + JSON) for business use
• Supports real-time KPI monitoring via the CLI summary dashboard
• Provides a scheduler for fully automated, hands-off daily pipeline runs


📂 **Project Structure**
ecommerce_analytics/
│
├── main.py                        # CLI entry point & scheduler
├── config.py                      # DB config & API base URLs
├── requirements.txt               # requests, pandas, mysql-connector, schedule
│
├── api/
│   ├── fetch_products.py          # FakeStore + DummyJSON product fetchers
│   └── fetch_users.py             # FakeStore + JSONPlaceholder user & cart fetchers
│
├── database/
│   ├── db_connection.py           # MySQL connection manager
│   └── schema.sql                 # Table definitions (products, users, orders, logs)
│
├── services/
│   ├── analytics_service.py       # KPI query functions (revenue, category stats, etc.)
│   └── etl_service.py             # Full ETL orchestration (extract → transform → load)
│
├── reports/
│   └── report_generator.py        # CSV + JSON export & console summary printer
│
├── exports/                       # Auto-generated daily report files
└── logs/                          # ETL run logs directory

📂 **Data Sources**
External REST APIs (Public / Free)
Includes:

• Product details (title, price, category, rating, stock)
• User information (username, email, phone, city)
• Cart/order data (user_id, product list, total price)
• Multi-source tagging (source_api field for traceability)

API                        Data
FakeStoreAPI           Products, Users, Carts
DummyJSON              Extended product catalog
JSONPlaceholder        Additional user data
