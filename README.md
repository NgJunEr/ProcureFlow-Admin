# ProcureFlow Admin - Procurement Management System

![Laravel Version](https://img.shields.io/badge/Laravel-10.x-FF2D20?style=flat-square&logo=laravel)
![PHP Version](https://img.shields.io/badge/PHP-8.1+-777BB4?style=flat-square&logo=php)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=flat-square&logo=postgresql)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)

ProcureFlow Admin is a role-based procurement management system designed for engineering companies to streamline supplier management, customer relations, and purchase requisition processes.

## Table of Contents
- [Project Overview](#project-overview)
- [Features](#features)
- [Database Schema](#database-schema)
- [Technology Stack](#technology-stack)

## Project Overview

ProcureFlow Admin addresses the procurement management needs of engineering firms by providing:

1. **Centralized Information Management**
2. **Streamlined Purchase Requisition Workflow**
3. **Role-Based Access Control**
4. **Supplier and Customer Relationship Management**
5. **Product Cost and Profit Tracking**

The system serves three primary roles:
- **Managers**: Oversee PR approvals and financial reporting
- **Sales Department**: Manage customer information and relationships
- **Purchasing Department**: Handle supplier relations and product sourcing

## Features

### Manager Role
- 🚀 **Create/Approve PRs**  
  Create purchase requisitions linking suppliers/customers, add products, approve requests
- 📊 **Financial Reports**  
  View profit reports: ∑(selling_price - buying_price) × quantity
- 👥 **User Management**  
  Add/edit staff accounts and assign roles
- 🔍 **Audit Trail**  
  Track all system activities and changes
- **Workflow**: Create PR → Select supplier/customer → Add products → Approve

### Sales Department
- 👥 **Customer Management**  
  Add/edit customer records with company/contact details
- 🔍 **Customer PRs**  
  View all PRs related to specific customers
- 📋 **Export Data**  
  Export customer lists to CSV/PDF
- 📅 **Engagement History**  
  Track customer interactions and order history
- **Workflow**: Add customer → View their PRs → Export contact list

### Purchasing Department
- 🏭 **Supplier Management**  
  Add/edit supplier profiles and contact info
- 📦 **Product Catalog**  
  Maintain product database with prices and MOQ
- 🔍 **Supplier PRs**  
  View all PRs from specific suppliers
- 📊 **Performance Monitoring**  
  Track supplier reliability and delivery times
- **Workflow**: Add supplier → Update products → View supplier PRs

## Database Schema

```sql
CREATE TABLE suppliers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    contact VARCHAR(255) NOT NULL,
    note TEXT,
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);

CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    company_name VARCHAR(255) NOT NULL,
    contact_name VARCHAR(255) NOT NULL,
    note TEXT,
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);

CREATE TABLE prs (
    id SERIAL PRIMARY KEY,
    date DATE NOT NULL,
    supplier_id INTEGER REFERENCES suppliers(id),
    customer_id INTEGER REFERENCES customers(id),
    customer_po VARCHAR(255) NOT NULL,
    status VARCHAR(20) DEFAULT 'pending',
    note TEXT,
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);

CREATE TABLE pr_products (
    id SERIAL PRIMARY KEY,
    pr_id INTEGER REFERENCES prs(id) ON DELETE CASCADE,
    product_name VARCHAR(255) NOT NULL,
    quantity INTEGER NOT NULL,
    moq VARCHAR(50) NOT NULL,
    buying_price NUMERIC(10, 3) NOT NULL,
    selling_price NUMERIC(10, 3) NOT NULL,
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);
```

## Technology Stack

### Backend
- **Framework**: Laravel 10.x
- **Database**: PostgreSQL 16
- **Authentication**: Laravel Breeze
- **API**: RESTful architecture

### Frontend
- **Templating**: Blade Components
- **Styling**: Tailwind CSS + FlowbiteUI
- **Interactivity**: Laravel Livewire

### Development & Operations
- **Version Control**: Git & GitHub
- **Database Management**: pgAdmin 4
- **Deployment**: Laravel Forge
- **CI/CD**: GitHub Actions

### Key Packages
```bash
npm install flowbite
```
