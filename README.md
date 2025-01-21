# Ecommerce App with Micro Frontends and NgRx Integration

## Table of Contents

1. **Introduction**
2. **Micro Frontend Architecture Overview**
3. **Technology Stack**
4. **Workflow and Integration Steps**
5. **Host and Micro Frontend Setup**
6. **NgRx State Management**
7. **Lazy Loading and Routing**
8. **Cross-App Communication**
9. **State Persistence**
10. **Testing Strategy**
11. **Deployment and Scaling**
12. **Best Practices**

---

## 1. Introduction

The Ecommerce App follows a **Micro Frontend Architecture**, allowing different business features (e.g., Product Catalog, Cart, Checkout) to be independently developed, deployed, and maintained. This approach enhances scalability, team autonomy, and allows for easier technology upgrades without affecting the entire application.

Micro frontends enable teams to work on smaller, decoupled codebases, making it easier to add new features and maintain existing ones. Each micro frontend in this application represents a business domain and operates independently while being integrated into a unified host shell application.

This architecture leverages Webpack Module Federation, which allows sharing dependencies and runtime module loading, thus optimizing performance and reducing redundancy. The NgRx state management library is used to ensure predictable data flow and synchronization across multiple micro frontends, providing features such as state persistence, actions, and side-effect management.

**Benefits of Micro Frontend Architecture:**

- **Independent Deployment:** Micro frontends can be deployed independently, reducing the risk of full application failure.
- **Scalability:** Enables horizontal scaling by distributing workloads across different teams.
- **Technology Flexibility:** Different micro frontends can adopt different frameworks or versions.
- **Improved Maintainability:** Easier debugging and enhancements due to smaller, focused codebases.
- **Team Autonomy:** Different teams can work on individual micro frontends with minimal dependencies.

**Key Features Implemented:**

- **Micro Frontend Modules:**
  - Product Catalog Micro Frontend
  - Cart Micro Frontend
  - Checkout Micro Frontend
- **Shared State Management with NgRx:**
  - Centralized state handling for user interactions.
  - Ensuring synchronization across micro frontends.
- **Lazy Loading and Dynamic Imports:**
  - Improved performance by loading micro frontends only when needed.
- **Authentication and Security:**
  - JWT-based authentication to securely manage user sessions across all micro frontends.
- **Continuous Integration and Deployment:**
  - Automated builds and deployments using Docker and Kubernetes.

---

## 2. Micro Frontend Architecture Overview

### **Architecture Components**

**Host Application (Shell):**
- Provides global layout, authentication, and routing.
- Dynamically loads micro frontends.
- Handles shared dependencies like styles, NgRx Store, and authentication tokens.

**Product Micro Frontend (MFE):**
- Responsible for product listing and detail views.
- Interacts with shared NgRx store for cart updates.

**Cart Micro Frontend (MFE):**
- Manages cart operations.
- Syncs cart data with the backend API.

**Checkout Micro Frontend (MFE):**
- Handles order placement and payment integration.
- Communicates with external payment gateways.

---

### **Detailed Component Diagram**
```
              +---------------------------------------------------+
               |                 Host Application (Shell)           |
               |  - Provides global layout & authentication         |
               |  - Dynamically loads micro frontends                |
               |  - Handles shared dependencies (NgRx, styles)       |
               +---------------------------------------------------+
                                   |
        -----------------------------------------------------------
        |                         |                              |
+---------------------+  +---------------------+  +---------------------+
|  Product MFE        |  |  Cart MFE            |  |  Checkout MFE         |
|  - Product listing  |  |  - Manage cart       |  |  - Handle payment     |
|  - Product details  |  |  - Sync with API     |  |  - External gateways  |
+---------------------+  +---------------------+  +---------------------+
```

---

## 3. Technology Stack

- **Frontend:** Angular 19
- **State Management:** NgRx Store, Effects
- **Micro Frontend Integration:** Webpack Module Federation
- **Backend:** Node.js, Express, PostgreSQL
- **Deployment:** Docker, Kubernetes
- **Authentication:** JWT, OAuth2

---

## 4. Workflow and Integration Steps

1. Set up Angular projects for host and micro frontends.
2. Configure Module Federation for dynamic loading.
3. Implement NgRx Store for state management.
4. Define communication strategies across MFEs.
5. Integrate authentication and authorization mechanisms.
6. Deploy using Docker containers.

---

## 5. Webpack Module Federation Setup

**Step 1: Install Dependencies**
```bash
npm install @angular-architects/module-federation --save
```

**Step 2: Configure Host Application**
```js
const { shareAll, withModuleFederationPlugin } = require('@angular-architects/module-federation/webpack');

module.exports = withModuleFederationPlugin({
  remotes: {
    product: "product@http://localhost:4201/remoteEntry.js",
    cart: "cart@http://localhost:4202/remoteEntry.js"
  },
  shared: shareAll({ singleton: true, strictVersion: false, requiredVersion: 'auto' })
});
```

**Step 3: Configure Micro Frontend Applications**
```js
module.exports = withModuleFederationPlugin({
  name: 'product',
  filename: 'remoteEntry.js',
  exposes: {
    './ProductModule': './src/app/product/product.module.ts',
  },
  shared: shareAll({ singleton: true, strictVersion: false, requiredVersion: 'auto' })
});
```

**Step 4: Load Micro Frontend Dynamically**
```ts
const routes: Routes = [
  { path: 'product', loadChildren: () => import('product/ProductModule').then(m => m.ProductModule) },
  { path: 'cart', loadChildren: () => import('cart/CartModule').then(m => m.CartModule) }
];
```

**Step 5: Running Applications**
```bash
ng serve --port 4200  # Host Application
ng serve --port 4201  # Product Micro Frontend
ng serve --port 4202  # Cart Micro Frontend
```

---

## 6. Conclusion

By implementing Micro Frontend Architecture with NgRx, this Ecommerce App achieves scalability, maintainability, and flexibility, ensuring seamless user experiences and efficient development workflows.

