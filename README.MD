# Inventory Management System

Inventory Management System is a desktop application built with Python (Tkinter) and SQLite for small retail or wholesale businesses. It provides a complete workflow for managing employees, suppliers, products (with SKU, GST, MRP), customers, sales, returns/refunds and reporting. The app includes invoice generation (PDF + QR), charting, Excel/PDF exports, low-stock alerts, and simple user management with Admin/Employee roles.

> Note: This repository contains a single-file GUI app (INVENTORY 14.py). The app stores data in a local SQLite database (`inventory14.db`) and includes helper features and data export options.

## Features

- User authentication (Admin / Employee)
- Employee CRUD + user account sync (auto password generation)
- Suppliers & Customers CRUD, with basic validation (email/phone)
- Products CRUD (SKU auto-generation, supplier link, qty, unit price, GST, MRP, reorder level)
- Sales: cart-based checkout, per-item discounts (Flat / Percent), invoice generation (PDF) with embedded QR
- Returns / Refunds with validation to avoid over-refunding; updates stock
- Reports dashboard (Admin-only)
  - Monthly & Daily sales trends (embedded Matplotlib charts)
  - Top products, Supplier comparison, Product sales share (pie), Profit reports and analysis
  - Export charts and reports to PNG/JPEG/PDF/Excel
- Export table data to Excel and PDF (product lists, sales, profit reports)
- Low stock alerts and a dedicated Alerts dialog
- Bulk communication hooks: send emails (SMTP) and SMS placeholder
- Lightweight — single-file GUI + SQLite DB (no heavy server setup)

## Requirements

- Python 3.8+
- Libraries (install via pip):
  - tkinter (usually included with Python)
  - pillow
  - reportlab
  - pandas
  - matplotlib
  - openpyxl
  - tkcalendar
  - matplotlib.backends.backend_tkagg (comes with matplotlib)
  - (optional) any SMTP credentials for sending emails

Install dependencies:
```bash
pip install pillow reportlab pandas matplotlib openpyxl tkcalendar
```

## Quick start

1. Place the script `INVENTORY 14.py` and optional logo files (`logo.png`, `logo2.png`) in a folder.
2. Run the app:
```bash
python "INVENTORY 14.py"
```
(Notice the filename contains a space — keep quotes or rename the file to remove the space.)

3. On first run the script creates an SQLite database `inventory14.db` and seeds a default admin user:
   - Username: `admin`
   - Password: `admin123`

4. Log in as admin to access all sections. Create employees, suppliers and products. Use Sales to create invoices.

## Important paths / files

- Database: `inventory14.db` (created automatically in the same folder)
- Default invoice/save dialogs open a save-as dialog so you choose location
- Temporary exported charts may be saved as temporary files when generating PDF reports

## Notes & Caveats

- Passwords are stored in plain text in the database. This is insecure for production — consider hashing (bcrypt/argon2) if this is used in any real environment.
- The email "send_bulk_mail" uses plain SMTP credentials and currently includes an example credential string in the code. Replace with valid credentials and secure Secrets handling (do not hardcode passwords).
- Phone and email validation is basic and limited: only Gmail and Yahoo are accepted (`@gmail.com` / `@yahoo.com`) and phone format is restricted to Indian 10-digit numbers starting with 6–9. Adjust rules as needed.
- DB migrations are minimal (some PRAGMA/ALTER statements are present). Backup the DB before manual schema edits.
- The app is single-user (desktop). Concurrent multi-user access could lead to SQLite locking issues if multiple instances modify the DB simultaneously.

## UX / Functionality Highlights

- Auto-generated IDs for employees, suppliers, customers and products.
- Auto-calculation of MRP from unit price + GST.
- Per-product and per-cart discount support.
- Invoice PDF includes a QR code with invoice summary.
- Reports provide export to PDF/Excel and have embedded Matplotlib charts.
- Low-stock alerts and a dedicated Alerts dialog make reordering easy.

## Suggested improvements / TODO (if you want to extend)

- Secure passwords (hashing) and support password resets.
- Role-based UI control for more granular permissions.
- Use environment variables or a config file for SMTP credentials.
- Add product images and display them on invoices.
- Improve email/SMS templates and integrate with a real SMS provider.
- Add unit tests and modularize code into smaller modules/packages.
- Improve internationalization / currency formatting for other locales.

## File structure (single-file project)

- INVENTORY 14.py — main application (GUI + DB + all features)
- inventory14.db — created at runtime
- logo.png, logo2.png — optional UI logos you can add to the app folder

## License

This project is provided as-is. You can add a license (e.g., MIT) if you wish to open-source it. The README suggests improvements and security considerations; treat credentials and personal data carefully.

---

If you'd like, I can:
- Rename and split the single script into modules (models, views, helpers) and produce a multi-file project structure.
- Create a requirements.txt file.
- Replace hardcoded SMTP credentials with a secure config (example .env) and show how to use python-dotenv.
- Produce a short user guide (screenshots and walkthrough) or an installer (PyInstaller spec).
