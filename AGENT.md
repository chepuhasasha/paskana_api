# AGENT.md

## Цель

Создай модуль `agent` в проекте NestJS. Этот модуль реализует агрегацию данных с маркетплейсов (Ozon, Wildberries и др.) по расписанию. Он получает данные по API, нормализует и сохраняет в базу.

## Требования

- Framework: NestJS
- Язык: TypeScript
- ORM: TypeORM
- База данных: PostgreSQL
- Модули в проекте: `user`, `auth`, `marketplace`, `metrics`

## Структура модуля `agent`

Создай следующую файловую структуру:

```
src/agent/
├── agent.module.ts
├── agent.service.ts
├── agent.scheduler.ts
├── tasks/
│   ├── ozon.task.ts
│   └── wb.task.ts
└── utils/
    └── normalize.ts
```

## agent.module.ts

Импортирует: `AgentService`, `AgentScheduler`, все задачи из `tasks/`.
Экспортирует: ничего.

## agent.service.ts

Публичные методы:

- `runForAllUsers()`: собирает данные по всем пользователям и аккаунтам
- `runForUser(userId: string)`: вручную запускает сбор данных для одного пользователя

Использует `MarketplaceService` для получения токенов.

## agent.scheduler.ts

Планировщик задач с использованием `@nestjs/schedule`.

- Расписание: каждые 30 минут
- Метод: вызывает `agentService.runForAllUsers()`

## tasks/\*.task.ts

Каждый `.task.ts` — логика взаимодействия с конкретным API:

### ozon.task.ts

- Получение заказов (`/v3/posting/fbs/list`)
- Получение остатков (`/v1/product/info/stocks`)

### wb.task.ts

- Получение заказов (`/api/v1/supplier/orders`)
- Получение остатков (`/api/v1/supplier/stocks`)

Методы должны возвращать массивы нормализованных DTO.

## utils/normalize.ts

Функции, приводящие сырые ответы от маркетплейсов к единому формату DTO:

- `normalizeOrders(raw): OrderDTO[]`
- `normalizeStock(raw): StockDTO[]`

## DTO

Определи базовые DTO:

```ts
interface OrderDTO {
  marketplace: "ozon" | "wb";
  orderId: string;
  sku: string;
  quantity: number;
  price: number;
  date: Date;
  userId: string;
}

interface StockDTO {
  marketplace: "ozon" | "wb";
  sku: string;
  quantity: number;
  warehouseId: string;
  date: Date;
  userId: string;
}
```

## Взаимодействие с другими модулями

- `MarketplaceService.getTokens(userId): MarketplaceToken[]`
- `MetricsService.saveOrders(orders: OrderDTO[])`
- `MetricsService.saveStocks(stocks: StockDTO[])`

## Цель генерации

Сгенерируй всю указанную структуру с заготовками функций и экспортов, чтобы можно было сразу приступить к реализации бизнес-логики.
