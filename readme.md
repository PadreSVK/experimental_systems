# experimental_systems

## Content

this repo contains the centralized system definitions for all experimental systems

all backstage entities will be in namespace `experiments`, for all references use full qualified name <kind>:<namespace>/<name>

> **Note**: All System and Domain entities are centralized in this repository

## Systems

### **Kind: System** (Ecommerce Domain)

* **checkout**
  * name: checkout
  * namespace: experiments
  * title: Checkout System
  * description: A checkout system for processing customer orders and payments
  * owner: experiment-team-alpha
  * domain: ecommerce
  * manager: ferko.alpha

* **basket**
  * name: basket
  * namespace: experiments
  * title: Basket System
  * description: A basket system for managing customer shopping carts
  * owner: experiment-team-bravo
  * domain: ecommerce
  * manager: karol.bravo

* **elis**
  * name: elis
  * namespace: experiments
  * title: ELIS System
  * description: A monolith that should be decomposed into microservices
  * owner: experiment-team-platform
  * domain: ecommerce
  * manager: jozko.platformak

## Structure

```
experimental_systems/
├── catalog-info.yaml (Location entity with wildcard reference)
└── systems/
    ├── checkout.yaml (Checkout system definition)
    ├── basket.yaml (Basket system definition)
    └── elis.yaml (ELIS system definition)
```

## Purpose

This repository serves as the central registry for all system definitions in the experimental namespace, providing:
- Centralized system definitions for consistent catalog management
- Domain organization (currently all systems in ecommerce domain)
- System ownership and management information
- Foundation for organizing components, APIs, and resources by system

## System Repositories

Each system has its own infrastructure repository:

- **Checkout System Repository**: https://github.com/padreSVK/experimental_.checkout-system
  - System-level infrastructure for checkout
  - GitHub repository management, databases, Kubernetes resources

- **Basket System Repository**: https://github.com/padreSVK/experimental_.basket-system
  - System-level infrastructure for basket
  - GitHub repository management, Kafka, Kubernetes resources

## System Model Hierarchy

```
Domain: ecommerce
├── System: checkout
│   ├── Repository: experimental_.checkout-system (infrastructure)
│   └── Repository: experimental_checkout-repository (components & APIs)
├── System: basket
│   ├── Repository: experimental_.basket-system (infrastructure)
│   ├── Repository: experimental_basket-backend (APIs & components)
│   ├── Repository: experimental_basket-mobile (mobile components)
│   └── Repository: experimental_basket-react-component (React library)
└── System: elis
    └── Repository: experimental_.elis-system (monolith to be decomposed)
```

## Adding New Systems

To add a new system to the catalog:

1. Create a new YAML file in `systems/` directory
2. Follow the system definition format:
```yaml
apiVersion: backstage.io/v1alpha1
kind: System
metadata:
  name: <system-name>
  namespace: experiments
  title: <System Title>
  description: <System description>
spec:
  owner: <team-name>
  domain: <domain-name>
  manager: <manager-email>
```
3. The location reference will automatically discover the new system

## Best Practices

- All systems should have a clear owner (team)
- Each system should have a dedicated manager
- Systems should be grouped by logical domains
- System names should be lowercase with hyphens
- Each system should have its own infrastructure repository (experimental_.<system-name>-system)