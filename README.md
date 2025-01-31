# Cinema

This is an example of an **N-layer architecture** based on **ASP.NET Core MVC**.  
The project is structured into multiple layers, each fulfilling a specific role in the system.

## Solution Structure

```bash
├── MyCinema.Domain
│   ├── Entities
│   ├── ValueObjects
│   ├── Interfaces
│   └── Services (Domain-specific, if needed)
├── MyCinema.Application
│   ├── DTOs
│   ├── Interfaces
│   ├── Services (Use Cases)
│   └── Validation
├── MyCinema.Infrastructure
│   ├── Data
│   │   ├── Context
│   │   └── Repositories
│   ├── Services (External integrations, HttpClients, etc.)
│   ├── Config
│   └── Migrations (If using EF Core)
├── MyCinema.Web (ASP.NET Core MVC)
│   ├── Controllers
│   ├── Views
│   ├── wwwroot
│   ├── Program.cs
│   └── appsettings.json
└── tests
    └── MyCinema.Tests
        ├── Domain.Tests
        ├── Application.Tests
        └── Infrastructure.Tests
```

## Dependencies

```bash
Web (MyCinema.Web)
  │
  └── Application (MyCinema.Application)
        │
        ├── Domain (MyCinema.Domain)
        │
        └── Infrastructure (MyCinema.Infrastructure)
```

## Explanation

- **Web Layer**  
  Calls the **Application Layer** (services, handlers).

- **Application Layer**  
  - Depends on **Domain Layer** (business logic and entities).  
  - Communicates with **Infrastructure Layer** through interfaces.

- **Domain Layer**  
  - The core of the application, independent of other layers.

- **Infrastructure Layer**  
  - Implements the interfaces defined in **Application Layer**.  
  - Can use **Domain Layer** (e.g., for database entity mappings).

## Architecture Diagram (Mermaid)

```mermaid
graph TD
    A[Web (MyCinema.Web)] -->|Calls| B[Application (MyCinema.Application)]
    B -->|Uses| C[Domain (MyCinema.Domain)]
    B -->|Interfaces with| D[Infrastructure (MyCinema.Infrastructure)]
    C -->|May use| D
```

## Project Principles

- **Separation of Concerns**  
  Each layer has a clear responsibility, ensuring modularity.

- **Domain-Centric Approach**  
  The **Domain Layer** is independent and contains core business logic.

- **Dependency Injection (DI)**  
  - **Application Layer** only knows about **Domain Layer** and interfaces for **Infrastructure Layer**.  
  - **Infrastructure Layer** provides implementations for these interfaces.

- **Scalability & Maintainability**  
  - Easily extendable with new features.  
  - Allows smooth integration with different data sources or external APIs.

## Getting Started

1. Open the solution:  
   ```bash
   MyCinema.sln
   ```

2. Build all projects:  
   ```bash
   dotnet build
   ```

3. Run the application:  
   ```bash
   dotnet run --project MyCinema.Web
   ```
