# Story 1.2: MySQL Database Connection & Environment Configuration

## Overview
Configured persistent MySQL 8.x connectivity, HikariCP connection pooling, and Hibernate JPA properties for the **Atomic Payment Engine**, restoring full Spring Boot `DataSource` auto-configuration.

## Database Provisioning
- **Database Name:** `atomic_ledger_db`
- **Character Set & Collation:** `utf8mb4` / `utf8mb4_unicode_ci` (full 4-byte Unicode storage with case-insensitive UCA sorting and uniqueness checks)

## Security & Connection Pooling (`application.properties`)
- **Secret Management:** Database credentials are injected at runtime via environment variables (`${DB_USERNAME:root}` and `${DB_PASSWORD}`) so no plaintext secrets are committed to version control.
- **HikariCP Pool (`AtomicLedgerHikariPool`):** Configured with `maximum-pool-size=10`, `minimum-idle=5`, and `connection-timeout=30000` ms.
- **JPA & Transaction Hygiene:** Enabled `ddl-auto=update` for schema evolution and set `spring.jpa.open-in-view=false` so database connections are released immediately after `@Transactional` service boundaries complete rather than lingering during HTTP serialization.

## Verification
- Removed the temporary `DataSourceAutoConfiguration` exclusion from `BackendApplication.java`.
- Confirmed `AtomicLedgerHikariPool` initialized cleanly against MySQL and `GET /actuator/health` returned `"status": "UP"` with the `db` health indicator active.