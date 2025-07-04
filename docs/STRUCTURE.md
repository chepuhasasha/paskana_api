# Project Structure

This document describes the modules and main files of the NestJS backend.

## auth
- **auth.module.ts** – imports JWT module and provides AuthService.
- **auth.service.ts** – validates users, issues tokens.
- **auth.controller.ts** – endpoints for login and registration.
- **dto/login.dto.ts** – login payload.
- **dto/register.dto.ts** – registration payload.
- **guards/jwt-auth.guard.ts** – protects routes with JWT.
- **strategies/jwt.strategy.ts** – strategy for validating JWT tokens.

## users
- **users.module.ts** – exports UsersService.
- **users.service.ts** – user-related business logic.
- **users.controller.ts** – CRUD API for users.
- **entities/user.entity.ts** – TypeORM entity for users.
- **dto/create-user.dto.ts** – payload for creating users.
- **dto/update-user.dto.ts** – payload for updating users.

## marketplace
- **marketplace.module.ts** – manages marketplace integrations.
- **marketplace.service.ts** – stores tokens and interacts with APIs.
- **marketplace.controller.ts** – endpoints to connect accounts.
- **entities/marketplace-token.entity.ts** – stores API tokens.
- **dto/connect-marketplace.dto.ts** – data to connect a marketplace.
- **dto/update-marketplace.dto.ts** – updates marketplace settings.

## metrics
- **metrics.module.ts** – maintains metric entities.
- **metrics.service.ts** – saves and queries metrics.
- **metrics.controller.ts** – REST API for metrics.
- **entities/order.entity.ts** – order metrics.
- **entities/sale.entity.ts** – sales metrics.
- **entities/stock.entity.ts** – inventory metrics.
- **entities/rating.entity.ts** – rating metrics.
- **dto/query-metrics.dto.ts** – filters for retrieving metrics.

## scheduler
- **scheduler.module.ts** – registers scheduled tasks.
- **scheduler.service.ts** – cron jobs that fetch data.
- **tasks.ts** – placeholder for task definitions.

All files contain only comments to indicate their responsibility.
