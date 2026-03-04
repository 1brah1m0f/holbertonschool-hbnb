# HBnB Evolution - Technical Documentation

## Introduction
This document serves as the technical blueprint for the HBnB Evolution project. It outlines the system architecture, business logic design, and interaction flows necessary for implementation. The application follows a layered architecture to ensure scalability and maintainability.

---

## 1. High-Level Package Diagram (Task 0)
The application is structured into three main layers: Presentation, Business Logic, and Persistence. Communication between the Presentation and Business Logic layers is managed via the **Facade Pattern** to decouple dependencies.

### Diagram
```mermaid
classDiagram
    %% Relationships
    PresentationLayer ..> BusinessLogicLayer : Uses (via Facade)
    BusinessLogicLayer ..> PersistenceLayer : Persists/Retrieves Data

    %% Presentation Layer
    namespace PresentationLayer {
        class ServiceAPI {
            +handle_request()
            +return_response()
        }
    }

    %% Business Logic Layer
    namespace BusinessLogicLayer {
        class HBnBFacade {
            +register_user()
            +create_place()
            +add_review()
            +get_places()
        }
        class BusinessModels {
            User
            Place
            Review
            Amenity
        }
    }

    %% Persistence Layer
    namespace PersistenceLayer {
        class DataRepository {
            +save()
            +update()
            +delete()
            +get_by_id()
        }
    }

    HBnBFacade --> BusinessModels : Manages