Webpack Module Federation Setup
Step 1: Install Dependencies
Run the following command to install Webpack Module Federation plugin:
npm install @angular-architects/module-federation --save
Step 2: Configure Host Application
Modify the webpack.config.js in the host app to include remote module references:
const { shareAll, withModuleFederationPlugin } = require('@angular-architects/module-federation/webpack');

module.exports = withModuleFederationPlugin({
  remotes: {
    product: "product@http://localhost:4201/remoteEntry.js",
    cart: "cart@http://localhost:4202/remoteEntry.js"
  },
  shared: shareAll({ singleton: true, strictVersion: false, requiredVersion: 'auto' })
});
Step 3: Configure Micro Frontend Applications
Each micro frontend should expose its components by modifying their respective webpack.config.js files:
Example for Product MFE:
const { shareAll, withModuleFederationPlugin } = require('@angular-architects/module-federation/webpack');

module.exports = withModuleFederationPlugin({
  name: 'product',
  filename: 'remoteEntry.js',
  exposes: {
    './ProductModule': './src/app/product/product.module.ts',
  },
  shared: shareAll({ singleton: true, strictVersion: false, requiredVersion: 'auto' })
});
Step 4: Load Micro Frontend Dynamically
In the host app routing module, dynamically load MFEs as follows:
const routes: Routes = [
  { path: 'product', loadChildren: () => import('product/ProductModule').then(m => m.ProductModule) },
  { path: 'cart', loadChildren: () => import('cart/CartModule').then(m => m.CartModule) }
];
Step 5: Running Applications
Start the host and MFEs separately:
ng serve --port 4200  # Host Application
ng serve --port 4201  # Product Micro Frontend
ng serve --port 4202  # Cart Micro Frontend
