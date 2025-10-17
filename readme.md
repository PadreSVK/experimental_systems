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
```yaml
spec:
    useApisFromSystems: 
    - finis # compliant, external cost (VPN), branch supply, not pickup orders, invoicing&crediting from orders
    - bonus-portal # product and brand information
    - ledger # order data  for pairing and cash register closures, pre payments
```

* **purchase**
  * name: purchase
  * namespace: experiments
  * title: purchase System
  * description: purchase system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: jozko.financak
```yaml
spec:
    useApisFromSystems: 
    - finis # documents
```

* **artemis**
  * name: artemis
  * namespace: experiments
  * title: artemis System
  * description: artemis system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak
```yaml
spec:
    useApisFromSystems: 
    - finis # user department employee hierarchy
```

* **pricing**
  * name: pricing
  * namespace: experiments
  * title: pricing System
  * description: pricing system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak

* **RO e-transport**
  * name: ro-e-transport
  * namespace: experiments
  * title: RO e-transport System
  * description: RO e-transport system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak

* **e-filling**
  * name: e-filling
  * namespace: experiments
  * title: e-filling System
  * description: e-filling system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak
```yaml
spec:
    useApisFromSystems: 
    - finis # document request
```

* **bonus-portal**
  * name: e-filling
  * namespace: experiments
  * title: e-filling System
  * description: e-filling system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak
```yaml
spec:
    useApisFromSystems: 
    - finis # documents
```

* **sheu**
  * name: sheu
  * namespace: experiments
  * title: sheu System
  * description: sheu system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak
```yaml
spec:
    useApisFromSystems: 
    - pricing # XX prices
    - finis # document + prices
    - ro-e-transport # XX prices
```

* **availability**
  * name: availability
  * namespace: experiments
  * title: availability System
  * description: availability system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak

* **saf-t**
  * name: saf-t
  * namespace: experiments
  * title: saf-t System
  * description: saf-t system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak

* **e-invoicing**
  * name: e-invoicing
  * namespace: experiments
  * title: e-invoicing System
  * description: e-invoicing system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak

* **exchange-rates**
  * name: exchange-rates
  * namespace: experiments
  * title: exchange-rates System
  * description: exchange-rates system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak
```yaml
spec:
    useApisFromSystems: 
    - finis #...
```

* **catalog**
  * name: catalog
  * namespace: experiments
  * title: catalog System
  * description: catalog system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak
```yaml
spec:
    useApisFromSystems: 
    - finis # product infromation
```


* **ledger**
  * name: ledger
  * namespace: experiments
  * title: ledger System
  * description: ledger system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: ferko.financak
```yaml
spec:
    useApisFromSystems: 
    - finis # payments
```

* **FinIS**
  * name: finis
  * namespace: experiments
  * title: FinIS System
  * description: FinIS system
  * owner: experiment-finance-alpha
  * domain: finance
  * manager: jozko.financak
```yaml
spec:
    useApisFromSystems: 
    - bonus-portal # documents
    - e-filling # documents
    - sheu # document + prices
    - purchase # document & companies
    - pricing #stock document prices
    - availability # stock amount
    - saf-t # documents, customers, payments
    - e-invoicing # documents
    - ledger # documents
```

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