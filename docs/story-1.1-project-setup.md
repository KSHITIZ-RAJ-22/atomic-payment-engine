# Story 1.1: Spring Boot Project Initialization & Layered Architecture

## Overview
Initialized the core backend service for the **Atomic Payment Engine** using an enterprise 7-layer package architecture.

## Tech Stack & Environment
- **Language:** Java 25 (`jdk-25.0.5.1`)
- **Framework:** Spring Boot 4.2.0
- **Build Tool:** Maven (via Maven Wrapper `./mvnw`)
- **Core Starters:** WebMVC, Data JPA, Validation, Actuator, MySQL Connector/J, Lombok

## Layered Package Architecture (`com.kshitiz.atomicledger`)
- `config` — Security, CORS, OpenAPI, and JPA auditing configurations
- `controller` — REST API endpoints (HTTP request/response boundary)
- `service` — Core payment logic, concurrency locks, and double-entry ledger rules
- `repository` — Spring Data JPA interfaces for MySQL persistence
- `entity` — JPA database entity mappings
- `dto` — Request and response payloads isolated from persistence models
- `exception` — Custom domain exceptions and global `@RestControllerAdvice` handlers

## Technical Notes & Verification
- **Temporary Database Bypass:** `DataSourceAutoConfiguration` (`org.springframework.boot.jdbc.autoconfigure.DataSourceAutoConfiguration`) is temporarily excluded in `BackendApplication` until MySQL datasource properties are configured in **Story 1.2**.
- **Verification:** Confirmed clean Maven build and embedded Apache Tomcat startup on port `8080`.