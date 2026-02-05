# LifeOS

LifeOS — персональное приложение для планирования задач, расписания и долгосрочных целей.
Проект предназначен для демонстрации навыков проектирования доменной модели и backend-разработки на платформе .NET.

Версия MVP сфокусирована на базовых сценариях планирования:

* задачи
* расписание
* цели

---

## Цель проекта

Цель проекта — показать умение:

* проектировать предметную область,
* работать с реляционной моделью данных,
* разрабатывать REST API на ASP.NET Core,
* использовать Entity Framework Core,
* структурировать приложение по слоям,
* документировать архитектурные решения.

Проект ориентирован на портфолио для стажировки или позиции Junior .NET Developer.

---

## Предметная область

### User

Пользователь системы.

Поля:

* Id : Guid
* Email : string
* DisplayName : string
* Role : UserRole (Guest, User)

---

### TaskItem

Задача пользователя.

Поля:

* Id : Guid
* UserId : Guid
* Title : string
* Description : string?
* DueDate : DateTime?
* Status : TaskStatus (Todo, InProgress, Done)
* Priority : int (1–5)
* CreatedAt : DateTime

Назначение:

* ежедневное планирование,
* отображение в расписании,
* контроль выполнения.

---

### Goal

Долгосрочная цель пользователя.

Поля:

* Id : Guid
* UserId : Guid
* Title : string
* Description : string?
* StartDate : DateTime
* EndDate : DateTime?
* Progress : double (0–100)

Связи:

* одна цель может содержать несколько подцелей (self-referencing one-to-many).

---

### ScheduleItem

Элемент расписания.

Поля:

* Id : Guid
* UserId : Guid
* Title : string
* StartTime : DateTime
* EndTime : DateTime
* Type : ScheduleType (Study, Work, Personal)

---

## Связи между сущностями

* User → TaskItem (one-to-many)
* User → Goal (one-to-many)
* Goal → SubGoals (one-to-many)
* User → ScheduleItem (one-to-many)

---

## API

### Аутентификация

POST /api/auth/register
POST /api/auth/login

---

### Tasks

GET /api/tasks
GET /api/tasks/today
POST /api/tasks
GET /api/tasks/{id}
PUT /api/tasks/{id}
DELETE /api/tasks/{id}

---

### Goals

GET /api/goals
POST /api/goals
GET /api/goals/{id}
PUT /api/goals/{id}

---

### Schedule

GET /api/schedule?date=YYYY-MM-DD
POST /api/schedule

---

## Архитектура

```
/src
  LifeOS.Api            // Controllers, authentication, Swagger
  LifeOS.Application    // Business logic, services, DTOs
  LifeOS.Domain         // Entities, enums
  LifeOS.Infrastructure // EF Core, DbContext, migrations
/tests
  LifeOS.Tests
```

Архитектурный подход:

* разделение ответственности по слоям,
* использование DTO,
* централизованная бизнес-логика,
* миграции базы данных через EF Core.

---

## Технологический стек

* .NET (LTS)
* ASP.NET Core Web API
* Entity Framework Core
* PostgreSQL или SQL Server
* JWT-аутентификация
* Swagger / OpenAPI
* xUnit (unit tests)
* Docker (опционально)

---

## Пользовательский интерфейс (Figma)

Проектирование интерфейса включает:

* дашборд с задачами и расписанием на день,
* список задач с фильтрацией,
* модальные окна создания и редактирования задач,
* экран целей с отображением прогресса,
* экран расписания (day view).

Для каждого экрана предусмотрены состояния:

* пустое состояние,
* состояние загрузки,
* состояние ошибки.

---

## Запуск проекта

1. Клонировать репозиторий
2. Указать строку подключения к базе данных
3. Применить миграции Entity Framework Core
4. Запустить проект LifeOS.Api
5. Открыть Swagger UI

---

## Ценность проекта для портфолио

Проект демонстрирует:

* осмысленное проектирование доменной модели,
* работу с реляционной базой данных,
* реализацию REST API,
* понимание жизненного цикла backend-приложения,
* готовность к расширению функциональности.

---

## Возможные направления развития

* напоминания и фоновые задачи,
* аналитика выполнения задач,
* экспорт расписания,
* поддержка совместных календарей.

---
