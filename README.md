# Twiva: Social E-commerce Platform (Contribution Case Study)

> **Note:** This repository is a case study. It contains **no source code, credentials, or client data**. The original codebase is proprietary and private.

## Overview

Twiva is a large-scale social e-commerce platform where influencers promote products and customers buy through them. I worked on it as a **Laravel backend developer** and also as a **QA tester** for the mobile app and the website.

| | |
|---|---|
| **Project** | [new.twiva.com](https://new.twiva.com/) |
| **Role** | Backend Developer (Laravel / PHP) and QA Tester |
| **Period** | October 2024 - March 2025 (6 months) |
| **Work setup** | Fully remote, in a large multi-developer team |
| **Stack** | PHP, Laravel, MySQL, Tailwind CSS, JavaScript |

### About the project

- The biggest project at my company.
- The platform is connected to **AliExpress**, the global e-commerce marketplace, through a dedicated **`AliExpress` module** that links Twiva to the AliExpress website.
- More than **7 years old**. It was first built by another team, then taken over by my company, which has maintained it for about **5 years**.
- Many developers have worked on it over the years, so I had to read and understand a large existing codebase before changing it.

## My Contributions

### 1. Invoice page with PDF export
Built the invoice feature for customer orders.
- Shows the full payment details and the order total, **including shipping**.
- Customers can **print the invoice or download it as a PDF file**.
- PDF generation uses a PDF library. [Add the library name if you find it in your old notes or commits]

### 2. Abandoned-cart reminder emails
Built a reminder flow for customers who add products to their cart, close the app, and never finish the purchase.
- The customer receives a reminder email **after 1 day, after 1 week, and after 1 month** while the cart still has items.
- Reminders **stop automatically** once the customer completes the purchase or removes the products from the cart.
- The email has a clean, branded layout and lists the products left in the cart.
- **Approach:** I defined the user flow and the business rules first (when to send, when to stop), and only then wrote the code.

### 3. Multilingual fix for the AI support chatbot
The AI chatbot used by the support team **always answered in English**, whatever language the customer wrote in.
- The AI model available at that time had limited capabilities, so I could not rely on it alone to follow a language rule.
- **Solution:** I added a **dynamic variable** to the fixed prompt. The AI detects the customer's language from the message and fills the variable, and the prompt then tells the AI to answer in that language.
- **Result:** The bot replies in the same language the customer uses.

### 4. FlexPay payment integration
Worked on a short task to add **FlexPay**, a third-party payment API, to the platform.
- Integrated it using my experience with APIs and by reading the **official documentation**.

### 5. Admin panel improvements
While working, I found **four problems in the admin panel** and proposed fixes to the project manager, who approved them:
- Better **search filters**.
- Clearer **display of data** in the tables.
- **One-click access** from the tables to the accounts of **businesses, influencers and buyers**, for every user type and every kind of order.

### 6. Frontend price display
Improved how prices and numbers are shown so they are **cleaner, better organized and easier to read**.

### 7. QA testing
Tested the **mobile app and the website** as a regular user, going through the full flows.
- Sent **detailed written reports with screenshots** for the problems I found.
- Suggested **improvements to the user experience**.

## Architecture

The backend is a **modular monolith** built with Laravel. Each business domain lives in its own **module**, with its own routes, controllers, entities, repositories, migrations, tests and service provider. Inside the modules, the code follows **clean architecture** principles with the **Repository Pattern**.

```
Route  ->  Controller  ->  Service (in several modules)  ->  Repository  ->  Entity / DB
           (Http layer)     (business logic)                  (data access)
```

- Modules keep domains separated, so many developers can work on different features without touching each other's code.
- Business logic goes in services and repositories, so controllers stay thin: validate input, call the logic, return a response.
- Background work uses **Jobs, Events, Listeners, Mail and Notifications** (for example the order emails and the cart reminders).

### Project structure

The project has **21 modules**. Each module is a small, self-contained part of the application with its own folders. Below is the full structure (folder names only).

```
twiva-new/
  Modules/                      # one module per business domain
    Admin/
      Config, Console, Database, Entities, Events, Http, Imports, Listeners, Providers, Repositories, Resources, Routes, Tests
    AliExpress/
      Config, Console, Database, Entities, Exceptions, Http, Imports, Jobs, Providers, Repositories, Resources, Routes, Services, Tests
    Business/
      Config, Console, Database, Entities, Http, Providers, Repository, Resources, Routes, Tests
    Buyer/
      Config, Console, Database, Entities, Http, Notifications, Providers, Repositories, Resources, Routes, Rules, Tests
    Campaign/
      Config, Console, Database, Entities, Enums, Http, Providers, Repository, Resources, Routes, Rules, Tests
    Categories/
      Config, Console, Database, Entities, Http, Providers, Resources, Routes, Tests
    Chat/
      Config, Console, Database, Entities, Http, Jobs, Notifications, Providers, Resources, Routes, Tests, Transformers
    Coupon/
      Config, Console, Database, Entities, Http, Providers, Resources, Routes, Tests
    Front/
      Config, Console, Database, Entities, Http, Providers, Resources, Routes, Tests
    Home/
      Config, Console, Database, Entities, Helper, Http, Providers, Resources, Routes, Tests
    Influencer/
      Config, Console, Database, Entities, Exports, Http, Providers, Repositories, Resources, Routes, Tests
    Notification/
      Config, Console, Database, Emails, Entities, Http, Mail, Notifications, Providers, Repository, Resources, Routes, Tests
    Order/
      Config, Console, Database, Entities, Events, Http, Imports, Jobs, Listeners, Mail, Notifications, Providers, Repositories, Resources, Respositories, Routes, Tests, Traits
    Partner/
      Config, Console, Database, Entities, Enums, Http, Providers, Repositories, Resources, Routes, Tests
    Payment/
      Config, Console, Database, Entities, Http, Jobs, Providers, Resources, Routes, Services, Tests, certificates
    Platform/
      Config, Console, Database, Entities, Http, Jobs, Providers, Repositories, Resources, Routes, Rules, Services, Tests, Transformers
    Products/
      Config, Console, Database, Entities, Http, Providers, Repositories, Resources, Routes, Services, Tests, Traits, Transformers
    Shop/
      Config, Console, Database, Entities, Http, Providers, Repositories, Resources, Routes, Services, Tests
    System/
      Config, Console, Database, Entities, Http, Providers, Resources, Routes, Tests
    ToUpModule/
      Config, Console, Database, Entities, Http, Providers, Resources, Routes, Tests
    User/
      Config, Console, Database, Entities, Events, Helper, Http, Jobs, Listeners, Providers, Repository, Resources, Routes, Services, Tests, Transformers
  app/
    Casts, Console, Exceptions, Exports, Http, Jobs, Providers, View
    Console/Commands, Http/Controllers, Http/Middleware, View/Components
  config/
  database/
    factories, seeders
  resources/
    css, js, lang, views
  routes/
  tests/
    Feature, Unit
  lang/, documents/, bootstrap/, public/ (admin assets, images, css, js)
```

## Working Conditions

I did this work while **studying full-time at university**, working **fully remotely**, and living in a country with **heavy internet restrictions**, where many websites and services were blocked and needed proxies to access. I still delivered features on time and kept communicating with the team.

## What I Learned

- How to work on a **very large, long-lived project** with many developers and learn its structure quickly.
- To **design the user flow and business logic first**, before writing code (the cart reminders are a good example).
- To read **third-party API documentation** and integrate it safely (FlexPay).
- To work around the limits of an AI model with **prompt design**.
- How to **test as a real user** and write reports other people can act on.
- How to stay productive in a **fully remote team** while handling university pressure and unreliable internet access.

## Links

- Project: [new.twiva.com](https://new.twiva.com/)
- GitHub: [github.com/Waddi3](https://github.com/Waddi3/)
- LinkedIn: [Waddia Almohammad](https://www.linkedin.com/in/waddia-almohammad-95262a426)
- Email: [waddiaalmohammad1@gmail.com]
