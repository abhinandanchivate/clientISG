# Angular Training Student Manual (Angular 19)

## **Introduction**
Welcome to the Angular Training course for version 19! This manual will guide you through the key concepts, practical exercises, and foundational knowledge needed to build modern Angular applications effectively. By the end of this course, you will be able to set up Angular projects, create components, implement data binding, utilize services, leverage Angular 19 features, and much more.

---

## **Day 1: Angular Initial Setup & Important Topics**

### **What is Angular CLI and Project Setup?**
Angular CLI (Command Line Interface) is a powerful tool to initialize, develop, scaffold, and maintain Angular applications easily. 

### **Where is it used?**
Angular CLI is used for generating Angular applications, managing dependencies, compiling code, and serving the project locally.

### **How to Implement?**

1. **Setting Up the Environment:**
   - Download and install Node.js (latest LTS version).
   - Verify installation:
     ```sh
     node -v
     npm -v
     ```
   - Install Angular CLI 19 globally:
     ```sh
     npm install -g @angular/cli@19
     ```
   - Verify Angular CLI installation:
     ```sh
     ng version
     ```

2. **Creating a New Angular Project:**
   - Run the following command to create a new Angular project:
     ```sh
     ng new my-angular-app --routing --style=scss
     ```
   - Choose routing and styling options.

3. **Understanding Project Structure:**
   - Important files overview:
     ```sh
     ├── src
     │   ├── app
     │   ├── assets
     │   ├── environments
     │   ├── index.html
     │   ├── main.ts
     │   ├── styles.scss
     ├── angular.json
     ├── package.json
     ├── README.md
     ```

4. **Running the Application:**
   - Start the application:
     ```sh
     ng serve --open
     ```

### **What happens when we run the `ng serve` command?**
When the `ng serve` command is executed, the following process occurs:

1. **Compilation:**
   - Angular CLI compiles the TypeScript files into JavaScript using Webpack.
   - It also compiles HTML and CSS files.
   - Any syntax errors or missing dependencies will be displayed in the terminal.

2. **Development Server Setup:**
   - A local development server is started using Webpack Dev Server.
   - The default server runs at `http://localhost:4200/`.

3. **Hot Module Replacement (HMR):**
   - Angular enables HMR, allowing real-time updates without a full page reload.
   - Any code changes are reflected instantly.

4. **Asset Optimization:**
   - Webpack bundles JavaScript, CSS, and other assets for efficient loading.

5. **Application Bootstrapping:**
   - The `index.html` file loads the compiled JavaScript files.
   - Angular bootstraps the root module (`AppModule`) and initializes the application.

6. **Live Reload:**
   - The browser automatically reloads when changes are detected in the code.

**Command Breakdown:**
   ```sh
   ng serve --port=4300 --open
   ```
   - `--port=4300`: Runs the application on port 4300 instead of the default 4200.
   - `--open`: Automatically opens the default browser with the application.

---
# Angular Training Student Manual (Angular 19)

## **Introduction**
Welcome to the Angular Training course for version 19! This manual will guide you through the key concepts, practical exercises, and foundational knowledge needed to build modern Angular applications effectively. By the end of this course, you will be able to set up Angular projects, create components, implement data binding, utilize services, leverage Angular 19 features, and much more.

---

## **Day 2: Angular Components**

### **What are Angular Components?**
Angular components are the fundamental building blocks of an Angular application. Each component consists of an HTML template, CSS for styling, and TypeScript logic. Components help encapsulate functionality and allow reusability throughout the application.

### **Where are they used?**
- UI development of Angular applications.
- Implementing modular functionality.
- Handling user interactions and data display.
- Component-based architecture for scalability and maintainability.

### **Anatomy of an Angular Component**
An Angular component consists of three primary parts:

1. **HTML (Template):** Defines the view of the component.
   Example:
   ```html
   <h1>{{ title }}</h1>
   <button (click)="changeTitle()">Change Title</button>
   ```

2. **CSS (Presentation):** Handles the styling of the component.
   Example:
   ```css
   h1 {
     color: blue;
     font-size: 24px;
   }
   ```

3. **TypeScript (Controller):** Contains the business logic of the component.
   Example:
   ```typescript
   import { Component } from '@angular/core';

   @Component({
     selector: 'app-my-component',
     templateUrl: './my-component.component.html',
     styleUrls: ['./my-component.component.css']
   })
   export class MyComponent {
     title = 'Hello Angular';
     
     changeTitle() {
       this.title = 'Angular is Awesome!';
     }
   }
   ```

### **Creating Components**

To generate a new component using Angular CLI:
```sh
ng generate component my-component
```

This command creates the following files:
```
my-component/
├── my-component.component.html
├── my-component.component.css
├── my-component.component.ts
├── my-component.component.spec.ts
```

### **Component Decoration**
Angular uses decorators to define metadata for components. The `@Component` decorator is used to specify:
- `selector`: Defines the custom HTML tag to use the component.
- `templateUrl`: Links to the HTML template.
- `styleUrls`: Links to the CSS file(s).

Example:
```typescript
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
```

### **Root and Subcomponents**
In an Angular application:

- The **root component** is the top-level component (usually `AppComponent`).
- **Subcomponents** are child components that are used inside the root component.

Example:

In `app.component.html`:
```html
<app-header></app-header>
<app-content></app-content>
<app-footer></app-footer>
```

Each subcomponent is responsible for a specific section of the UI.

### **Smart and Dumb Components**

1. **Smart Components:**
   - Handle business logic and manage data.
   - Communicate with services to fetch or update data.
   - Example:
     ```typescript
     import { Component } from '@angular/core';
     import { DataService } from './data.service';
     
     @Component({
       selector: 'app-smart',
       template: `<app-dumb [data]="items"></app-dumb>`
     })
     export class SmartComponent {
       items = [];
       constructor(private dataService: DataService) {
         this.items = this.dataService.getData();
       }
     }
     ```

2. **Dumb Components:**
   - Focus on presentation logic only.
   - Receive data via `@Input()` and emit events via `@Output()`.
   - Example:
     ```typescript
     import { Component, Input } from '@angular/core';
     
     @Component({
       selector: 'app-dumb',
       template: `<ul><li *ngFor="let item of data">{{ item }}</li></ul>`
     })
     export class DumbComponent {
       @Input() data: string[] = [];
     }
     ```



### **Real-world Examples of Components**

Angular applications are often composed of several modular components to enhance maintainability and scalability. Below are common real-world examples of Angular components and their responsibilities:

1. **Header Component:**
   - Contains the application header, including branding, navigation menus, and user profile options.
   - Example:
     ```html
     <header>
       <nav>
         <ul>
           <li><a routerLink="/home">Home</a></li>
           <li><a routerLink="/about">About</a></li>
         </ul>
       </nav>
     </header>
     ```
     ```typescript
     import { Component } from '@angular/core';

     @Component({
       selector: 'app-header',
       templateUrl: './header.component.html',
       styleUrls: ['./header.component.css']
     })
     export class HeaderComponent {}
     ```

2. **Sidebar Component:**
   - Provides navigation links to various sections of the application.
   - Example:
     ```html
     <aside>
       <ul>
         <li><a routerLink="/dashboard">Dashboard</a></li>
         <li><a routerLink="/settings">Settings</a></li>
       </ul>
     </aside>
     ```
     ```typescript
     import { Component } from '@angular/core';

     @Component({
       selector: 'app-sidebar',
       templateUrl: './sidebar.component.html',
       styleUrls: ['./sidebar.component.css']
     })
     export class SidebarComponent {}
     ```

3. **Content Component:**
   - Responsible for displaying the dynamic content of the application based on user interactions.
   - Example:
     ```html
     <section>
       <h1>{{ contentTitle }}</h1>
       <p>{{ contentDescription }}</p>
     </section>
     ```
     ```typescript
     import { Component } from '@angular/core';

     @Component({
       selector: 'app-content',
       templateUrl: './content.component.html',
       styleUrls: ['./content.component.css']
     })
     export class ContentComponent {
       contentTitle = 'Welcome to Angular';
       contentDescription = 'Learn how to build scalable applications';
     }
     ```

4. **Footer Component:**
   - Displays the application footer with legal information and quick links.
   - Example:
     ```html
     <footer>
       <p>&copy; 2024 My Angular App</p>
     </footer>
     ```
     ```typescript
     import { Component } from '@angular/core';

     @Component({
       selector: 'app-footer',
       templateUrl: './footer.component.html',
       styleUrls: ['./footer.component.css']
     })
     export class FooterComponent {}
     ```

### **Example usage in the root component:**
```html
<app-header></app-header>
<app-sidebar></app-sidebar>
<app-content></app-content>
<app-footer></app-footer>
```

### **Real-world Examples of Components**

Angular applications are often composed of several modular components to enhance maintainability and scalability. Below are common real-world examples of Angular components and their responsibilities:

1. **Header Component:**
   - Contains the application header, including branding, navigation menus, and user profile options.
   - Example:
     ```html
     <header>
       <nav>
         <ul>
           <li><a routerLink="/home">Home</a></li>
           <li><a routerLink="/about">About</a></li>
         </ul>
       </nav>
     </header>
     ```
     ```typescript
     import { Component } from '@angular/core';

     @Component({
       selector: 'app-header',
       templateUrl: './header.component.html',
       styleUrls: ['./header.component.css']
     })
     export class HeaderComponent {}
     ```

2. **Sidebar Component:**
   - Provides navigation links to various sections of the application.
   - Example:
     ```html
     <aside>
       <ul>
         <li><a routerLink="/dashboard">Dashboard</a></li>
         <li><a routerLink="/settings">Settings</a></li>
       </ul>
     </aside>
     ```
     ```typescript
     import { Component } from '@angular/core';

     @Component({
       selector: 'app-sidebar',
       templateUrl: './sidebar.component.html',
       styleUrls: ['./sidebar.component.css']
     })
     export class SidebarComponent {}
     ```

3. **Content Component:**
   - Responsible for displaying the dynamic content of the application based on user interactions.
   - Example:
     ```html
     <section>
       <h1>{{ contentTitle }}</h1>
       <p>{{ contentDescription }}</p>
     </section>
     ```
     ```typescript
     import { Component } from '@angular/core';

     @Component({
       selector: 'app-content',
       templateUrl: './content.component.html',
       styleUrls: ['./content.component.css']
     })
     export class ContentComponent {
       contentTitle = 'Welcome to Angular';
       contentDescription = 'Learn how to build scalable applications';
     }
     ```

4. **Footer Component:**
   - Displays the application footer with legal information and quick links.
   - Example:
     ```html
     <footer>
       <p>&copy; 2024 My Angular App</p>
     </footer>
     ```
     ```typescript
     import { Component } from '@angular/core';

     @Component({
       selector: 'app-footer',
       templateUrl: './footer.component.html',
       styleUrls: ['./footer.component.css']
     })
     export class FooterComponent {}
     ```

### **Example usage in the root component:**
```html
<app-header></app-header>
<app-sidebar></app-sidebar>
<app-content></app-content>
<app-footer></app-footer>
```

---

### **Angular Binding**

1. **String Interpolation:**
   - Allows binding of component data to the template using double curly braces `{{ }}`.
   - Example:
     ```html
     <p>{{ title }}</p>
     ```
     ```typescript
     export class AppComponent {
       title = 'Angular Binding Example';
     }
     ```

2. **Property Binding vs. Interpolation:**
   - Property binding uses square brackets `[ ]` to bind data to an element property.
   - Example:
     ```html
     <input [value]="title" />
     ```

3. **Event Binding and Data Transfer:**
   - Event binding listens to user events like click, input, etc.
   - Example:
     ```html
     <button (click)="onClick()">Click Me</button>
     ```
     ```typescript
     export class AppComponent {
       onClick() {
         alert('Button Clicked!');
       }
     }
     ```

4. **Two-Way Binding with ngModel:**
   - Combines property and event binding to keep data in sync.
   - Example:
     ```html
     <input [(ngModel)]="name" />
     <p>Hello {{ name }}</p>
     ```

5. **Class and Style Binding:**
   - Dynamically applies classes and styles.
   - Example:
     ```html
     <div [class.highlight]="isHighlighted">Highlighted Text</div>
     <p [style.color]="color">Styled Text</p>
     ```

6. **Combining All Bindings with Forms:**
   - Example:
     ```html
     <form>
       <input [(ngModel)]="user.name" placeholder="Enter name" />
       <button (click)="submitForm()">Submit</button>
     </form>
     ```
     ```typescript
     export class AppComponent {
       user = { name: '' };

       submitForm() {
         console.log('User:', this.user.name);
       }
     }
     ```

# Student Guide: Directives in Angular

## 1. Introduction to Directives in Angular
Directives in Angular are powerful features that allow developers to extend the functionality of HTML elements. They help in manipulating the DOM, applying styling dynamically, and reusing logic across components.

### Types of Directives
1. **Structural Directives** - Modify the structure of the DOM.
2. **Attribute Directives** - Change the appearance or behavior of an element.
3. **Custom Directives** - User-defined directives to meet specific requirements.

---

## 2. Structural Directives
Structural directives are used to add, remove, or manipulate elements in the DOM. They typically start with an asterisk `*`.

### 2.1 `*ngIf`
**Description:**
- Conditionally add or remove an element based on a boolean expression.

**Example:**
```html
<div *ngIf="isLoggedIn">
  Welcome, User!
</div>
```
**Key Points:**
- Use the `else` clause for fallback content.
- Angular removes the element from the DOM if the condition is `false`.

---

### 2.2 `*ngFor`
**Description:**
- Iterates over an array and renders elements dynamically.

**Example:**
```html
<ul>
  <li *ngFor="let item of items; let i = index">
    {{ i + 1 }}. {{ item }}
  </li>
</ul>
```
**Key Points:**
- Provides local variables such as `index`, `first`, `last`, etc.
- Efficient for dynamic lists.

---

### 2.3 `*ngSwitch`
**Description:**
- Acts like a switch statement to conditionally display elements.

**Example:**
```html
<div [ngSwitch]="status">
  <p *ngSwitchCase="'active'">Active</p>
  <p *ngSwitchCase="'inactive'">Inactive</p>
  <p *ngSwitchDefault>Unknown Status</p>
</div>
```
**Key Points:**
- Provides `ngSwitchCase` and `ngSwitchDefault`.

---

## 3. Attribute Directives
Attribute directives alter the behavior or appearance of elements.

### 3.1 `ngStyle`
**Description:**
- Dynamically applies CSS styles to an element.

**Example:**
```html
<p [ngStyle]="{'color': textColor, 'font-size': fontSize + 'px'}">
  Styled text
</p>
```
**Key Points:**
- Accepts an object of key-value pairs.

---

### 3.2 `ngClass`
**Description:**
- Conditionally apply classes to an element.

**Example:**
```html
<p [ngClass]="{'active': isActive, 'disabled': !isActive}">
  Conditional Class
</p>
```
**Key Points:**
- Can assign an object, array, or string of class names.

---

## 4. Custom Directives
Custom directives allow developers to extend Angular functionality by creating their own directives.

### 4.1 Creating a Custom Directive

**Step 1:** Generate the directive using Angular CLI.
```sh
ng generate directive highlight
```

**Step 2:** Implement the directive.
```typescript
import { Directive, ElementRef, Renderer2, HostListener } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(private el: ElementRef, private renderer: Renderer2) {}

  @HostListener('mouseenter') onMouseEnter() {
    this.renderer.setStyle(this.el.nativeElement, 'backgroundColor', 'yellow');
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.renderer.setStyle(this.el.nativeElement, 'backgroundColor', 'white');
  }
}
```

**Step 3:** Use the directive in an HTML template.
```html
<p appHighlight>Hover over me to see the effect!</p>
```

**Key Points:**
- Use `ElementRef` to interact with DOM elements.
- Use `Renderer2` to apply styles safely.
- Use `@HostListener` to listen to DOM events.

---

### 4.2 Input and Output in Directives
**Example:**
```typescript
@Input() highlightColor: string = 'yellow';
@Output() colorChanged = new EventEmitter<string>();
```

---

## 5. Summary
- Structural directives like `*ngIf`, `*ngFor`, and `*ngSwitch` help in dynamically managing the DOM.
- Attribute directives like `ngStyle` and `ngClass` apply styling and class manipulation.
- Custom directives enable adding reusable functionality across components.

---

## 6. Practice Exercises
1. Implement an Angular component that dynamically adds/removes an item using `*ngIf` and `*ngFor`.
2. Create a custom directive that changes text color when clicked.
3. Use `ngClass` and `ngStyle` to apply dynamic styling to a list of items.

# Angular Services and Dependency Injection

## 1. Introduction to Services
Angular services are a fundamental concept used to share data and logic across components without duplication. They provide a centralized way to manage state, communicate between components, and handle business logic.

### Key Benefits of Using Services
- Promotes code reusability and maintainability.
- Facilitates sharing of data across components.
- Provides a centralized location for business logic.
- Enables dependency injection for better testability.

## 2. Creating an Angular Service
To create a service, use the Angular CLI command:
```sh
ng generate service data
```
This command creates `data.service.ts` with the following structure:

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  private data: any[] = [];

  constructor() {}

  addData(item: any) {
    this.data.push(item);
  }

  getData() {
    return this.data;
  }
}
```

## 3. Registering Services in `app.module.ts`
Angular services are registered using the `providedIn` property within the `@Injectable` decorator or manually in the `providers` array inside `app.module.ts`:

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { DataService } from './data.service';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [DataService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## 4. Injecting Services into Components
To use a service in a component, inject it in the constructor:

```typescript
import { Component } from '@angular/core';
import { DataService } from './data.service';

@Component({
  selector: 'app-root',
  template: `<h1>Angular Services</h1>`
})
export class AppComponent {
  constructor(private dataService: DataService) {
    this.dataService.addData('Angular Service Example');
    console.log(this.dataService.getData());
  }
}
```

---

# Day 5: Angular Pipes

## 1. Introduction to Pipes
Pipes are used to transform data in Angular templates. They help format data such as dates, numbers, and strings.

## 2. Built-in Pipes
Angular provides several built-in pipes, including:
- **DatePipe** - Formats date values.
- **UpperCasePipe** - Converts text to uppercase.
- **LowerCasePipe** - Converts text to lowercase.
- **CurrencyPipe** - Formats currency values.

### Example Usage:
```html
<p>{{ today | date:'fullDate' }}</p>
<p>{{ amount | currency:'USD' }}</p>
```

## 3. Parameterized Pipes
Built-in pipes can accept parameters for customization.

```html
<p>{{ value | number:'1.2-2' }}</p>
<p>{{ today | date:'short' }}</p>
```

## 4. Creating Custom Pipes
To create a custom pipe, use Angular CLI:
```sh
ng generate pipe filter
```
Example custom filter pipe:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filter'
})
export class FilterPipe implements PipeTransform {
  transform(items: any[], searchText: string): any[] {
    if (!items || !searchText) {
      return items;
    }
    return items.filter(item => item.name.toLowerCase().includes(searchText.toLowerCase()));
  }
}
```

### Using the Custom Pipe:
```html
<li *ngFor="let item of items | filter:'angular'">{{ item.name }}</li>
```

## 5. Async Pipes
Async pipes automatically subscribe to observables and promises.

```html
<p>{{ dataObservable | async }}</p>
```

## 6. Chaining Pipes
Pipes can be chained together:
```html
<p>{{ user.name | uppercase | slice:0:5 }}</p>
```

---

# Angular Routing

## 1. Introduction to Routing
Angular's routing module helps in navigating between different views or components within the application.

## 2. Setting Up Routing
### Steps to Set Up Routing:
1. Create a routing module:
   ```sh
   ng generate module app-routing --flat --module=app
   ```

2. Define routes in `app-routing.module.ts`:
   ```typescript
   import { NgModule } from '@angular/core';
   import { RouterModule, Routes } from '@angular/router';
   import { HomeComponent } from './home/home.component';
   import { AboutComponent } from './about/about.component';

   const routes: Routes = [
     { path: 'home', component: HomeComponent },
     { path: 'about', component: AboutComponent },
     { path: '', redirectTo: '/home', pathMatch: 'full' }
   ];

   @NgModule({
     imports: [RouterModule.forRoot(routes)],
     exports: [RouterModule]
   })
   export class AppRoutingModule {}
   ```

## 3. Navigation Paths and `routerLink`
Navigation between routes can be done using the `routerLink` directive.

```html
<nav>
  <a routerLink="/home">Home</a>
  <a routerLink="/about">About</a>
</nav>
<router-outlet></router-outlet>
```

## 4. Passing and Fetching Parameters
Parameters can be passed through routes:

### Passing Parameters:
```html
<a [routerLink]="['/product', product.id]">View Product</a>
```

### Fetching Parameters:
```typescript
import { ActivatedRoute } from '@angular/router';

constructor(private route: ActivatedRoute) {
  this.route.params.subscribe(params => {
    console.log(params['id']);
  });
}
```

## 5. Implementing Route Guards
Route guards help control access to routes based on conditions.

### Creating a Guard:
```sh
ng generate guard auth
```

### Implementing Guard Logic:
```typescript
import { Injectable } from '@angular/core';
import { CanActivate } from '@angular/router';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  canActivate(): boolean {
    return !!localStorage.getItem('user');
  }
}
```

### Applying Guard to Routes:
```typescript
{ path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] }
```

# Angular HTTP Requests - Student Manual

## 1. Introduction
Angular provides a powerful `HttpClientModule` that simplifies communication with backend services via HTTP requests. This manual will guide you through the core functionalities, including performing CRUD operations, handling headers, transforming responses, and managing errors.

---

## 2. Setting Up `HttpClientModule`
To use the `HttpClient` service, you must first import the `HttpClientModule` in your Angular project.

### Steps to Set Up:
1. Install Angular (if not already installed):
    ```bash
    npm install -g @angular/cli
    ng new my-angular-app
    cd my-angular-app
    ```

2. Open `src/app/app.module.ts` and add:
    ```typescript
    import { HttpClientModule } from '@angular/common/http';

    @NgModule({
      declarations: [],
      imports: [
        HttpClientModule  // Import HttpClientModule here
      ],
      providers: [],
      bootstrap: []
    })
    export class AppModule { }
    ```

---

## 3. Performing HTTP Requests
Angular's `HttpClient` allows the execution of various HTTP methods such as `GET`, `POST`, `PUT`, and `DELETE`.

### 3.1 Performing GET Requests
Used to retrieve data from a server.

```typescript
import { HttpClient } from '@angular/common/http';
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-example',
  templateUrl: './example.component.html'
})
export class ExampleComponent implements OnInit {
  constructor(private http: HttpClient) {}

  ngOnInit() {
    this.http.get('https://api.example.com/data').subscribe(response => {
      console.log(response);
    });
  }
}
```

### 3.2 Performing POST Requests
Used to send data to a server.

```typescript
const payload = { name: 'John', age: 30 };
this.http.post('https://api.example.com/data', payload).subscribe(response => {
  console.log(response);
});
```

### 3.3 Performing PUT Requests
Used to update existing data.

```typescript
const updatedData = { name: 'John', age: 31 };
this.http.put('https://api.example.com/data/1', updatedData).subscribe(response => {
  console.log(response);
});
```

### 3.4 Performing DELETE Requests
Used to remove data from the server.

```typescript
this.http.delete('https://api.example.com/data/1').subscribe(response => {
  console.log('Data deleted:', response);
});
```

---

## 4. Handling HTTP Headers
You can add custom headers to your HTTP requests using `HttpHeaders`.

```typescript
import { HttpHeaders } from '@angular/common/http';

const headers = new HttpHeaders({
  'Content-Type': 'application/json',
  'Authorization': 'Bearer your-token-here'
});

this.http.get('https://api.example.com/data', { headers }).subscribe(response => {
  console.log(response);
});
```

---

## 5. Transforming HTTP Responses
Response transformation can be done using RxJS operators such as `map`.

```typescript
import { map } from 'rxjs/operators';

this.http.get('https://api.example.com/data')
  .pipe(
    map(response => response['items'])
  )
  .subscribe(items => {
    console.log(items);
  });
```

---

## 6. Error Handling
Handling errors gracefully ensures a better user experience. Use RxJS `catchError` to manage errors.

```typescript
import { catchError } from 'rxjs/operators';
import { throwError } from 'rxjs';

this.http.get('https://api.example.com/data')
  .pipe(
    catchError(error => {
      console.error('Error occurred:', error);
      return throwError(() => new Error('Something went wrong'));
    })
  )
  .subscribe(response => {
    console.log(response);
  });
```

---

## 7. Common Use Cases

1. **Fetching Data on Component Load:**
    - Use `ngOnInit()` lifecycle hook to fetch data on component initialization.
    
2. **Form Submissions:**
    - Send `POST` requests with form data to the backend.
    
3. **Polling API:**
    - Use RxJS `interval()` to poll an API periodically.
    
4. **Caching API Responses:**
    - Store frequently accessed data in services to minimize redundant requests.

---

## 8. Summary
- Import and configure `HttpClientModule` in `app.module.ts`.
- Use `HttpClient` to perform HTTP operations.
- Manage headers and response transformations.
- Implement robust error handling using RxJS.

---

## 9. Practice Exercises
1. Create a service to fetch users from an API and display them in a list.
2. Implement a form submission that sends data to an API.
3. Handle API response errors and show user-friendly messages.

---

## 10. Additional Resources
- [Angular Official Documentation](https://angular.io/guide/http)
- [RxJS Operators](https://rxjs.dev/guide/operators)


# Angular Observables and RxJS

## Introduction
Angular leverages **Observables** and **RxJS (Reactive Extensions for JavaScript)** to handle asynchronous operations efficiently. Observables provide powerful features like event handling, data transformation, and error handling.

---

## 1. Observables: Creating and Subscribing

### What is an Observable?
An Observable is a data stream that emits values over time. It can emit multiple values and allows subscribers to react to these emissions.

### Creating Observables
Observables can be created using various methods provided by RxJS:

#### Example 1: Creating an Observable from scratch
```typescript
import { Observable } from 'rxjs';

const myObservable = new Observable(observer => {
  observer.next('First value');
  observer.next('Second value');
  observer.complete();
});
```

#### Example 2: Using `of` and `from`
```typescript
import { of, from } from 'rxjs';

const observable1 = of(1, 2, 3, 4, 5);
const observable2 = from([10, 20, 30, 40]);
```

### Subscribing to Observables
To consume an observable, use the `subscribe` method.

```typescript
myObservable.subscribe(
  value => console.log(value),   // Handle emitted values
  error => console.error(error), // Handle errors
  () => console.log('Completed') // Handle completion
);
```

---

## 2. RxJS Operators and Subjects

### Common RxJS Operators
Operators are functions that allow us to transform, filter, and manipulate data streams. Some commonly used operators include:

#### 2.1 Transforming Data
- **map:** Apply a function to each emitted value.

```typescript
import { of } from 'rxjs';
import { map } from 'rxjs/operators';

of(1, 2, 3).pipe(
  map(value => value * 10)
).subscribe(console.log);
```

- **filter:** Filter emitted values based on a condition.

```typescript
import { filter } from 'rxjs/operators';

of(1, 2, 3, 4, 5).pipe(
  filter(value => value % 2 === 0)
).subscribe(console.log);
```

#### 2.2 Combination Operators
- **merge:** Combine multiple observables.

```typescript
import { merge, of } from 'rxjs';

merge(of('A', 'B'), of(1, 2)).subscribe(console.log);
```

- **concat:** Execute observables in sequence.

```typescript
import { concat } from 'rxjs';

concat(of('First'), of('Second')).subscribe(console.log);
```

#### 2.3 Subjects in RxJS
Subjects act as both an Observable and an Observer, meaning they can emit values and be subscribed to.

- **BehaviorSubject:** Emits the last value upon subscription.
- **ReplaySubject:** Replays past values to new subscribers.
- **AsyncSubject:** Emits the last value once the observable completes.

Example of a BehaviorSubject:
```typescript
import { BehaviorSubject } from 'rxjs';

const subject = new BehaviorSubject('Initial Value');
subject.subscribe(console.log);
subject.next('New Value');
```

---

## 3. Error Handling with Observables
Observables provide robust error-handling mechanisms using various RxJS operators.

### Handling Errors with `catchError`
The `catchError` operator helps in catching errors and providing fallback values.

```typescript
import { throwError, of } from 'rxjs';
import { catchError } from 'rxjs/operators';

const observableWithError = throwError('Error occurred!');

observableWithError.pipe(
  catchError(err => {
    console.error(err);
    return of('Fallback value');
  })
).subscribe(console.log);
```

### Retrying Failed Requests
`retry` and `retryWhen` operators allow retrying on errors.

```typescript
import { retry } from 'rxjs/operators';

observableWithError.pipe(
  retry(3)
).subscribe(
  data => console.log(data),
  err => console.error('Error after retries:', err)
);
```

### Finalizing Observables
Using the `finalize` operator to perform cleanup actions.

```typescript
import { finalize } from 'rxjs/operators';

of(1, 2, 3).pipe(
  finalize(() => console.log('Cleanup complete'))
).subscribe(console.log);
```

---

# Angular Performance Optimization

## Change Detection Strategies (OnPush)
- Overview of Angular's change detection mechanism
- Default vs OnPush change detection strategy
- When to use OnPush strategy
- Implementing OnPush change detection in components
- Optimizing component updates with immutability
- Performance benchmarking with different strategies
- Common pitfalls and debugging OnPush issues

## Lazy Loading, Tree Shaking, and Differential Loading

### Lazy Loading
- Introduction to lazy loading
- Benefits of lazy loading for performance
- Configuring lazy loading with Angular routing
- Strategies for optimizing lazy-loaded modules
- Preloading strategies and their impact on performance
- Analyzing bundle sizes after implementing lazy loading

### Tree Shaking
- Understanding tree shaking in Angular
- How Angular CLI leverages tree shaking
- Reducing bundle size with dead code elimination
- Best practices for writing tree-shakable code
- Verifying tree shaking effectiveness

### Differential Loading
- What is differential loading and why it matters
- Serving modern vs legacy browser bundles
- Configuring differential loading in Angular CLI
- Analyzing performance improvements with differential loading
- Compatibility considerations and fallbacks

# Advanced Concepts in Angular 19

## New Features in Angular 19
- Overview of Angular 19 release
- Key improvements and new functionalities
- Changes in Angular CLI and tooling
- Breaking changes and migration strategies

## Module Federation (Micro Frontends)
- Introduction to micro frontends in Angular
- Understanding Webpack Module Federation
- Setting up module federation in Angular
- Sharing state and dependencies across micro frontends
- Pros and cons of micro frontend architecture
- Performance considerations and optimization strategies

## Enhancements in Ivy Rendering Engine
- Overview of Ivy rendering engine improvements
- Compilation and runtime optimizations
- Faster change detection and improved performance
- Memory optimizations and bundle size reduction
- Debugging and profiling with Ivy enhancements

# Best Practices for Angular Performance Optimization
- Efficient use of Angular pipes and directives
- Avoiding unnecessary component re-renders
- Managing state effectively with RxJS and NgRx
- Utilizing Angular's built-in performance tools
- Code splitting and optimizing third-party dependencies
- Continuous monitoring and optimization strategies

# Angular Reactive Form Validation and Nexus Integration

## Angular Reactive Form Validation

### 1. Introduction to Reactive Forms
- **Definition and Overview:** Understanding what reactive forms are and how they work in Angular.
- **Difference between Template-Driven and Reactive Forms:** Key differences, advantages, and use cases.
- **When to Use Reactive Forms:** Scenarios where reactive forms are beneficial.
- **Setting Up Reactive Forms in Angular:** Steps to import required modules and configure them in an Angular project.

#### Sample Code:
```typescript
import { ReactiveFormsModule } from '@angular/forms';
@NgModule({
  imports: [ReactiveFormsModule]
})
export class AppModule {}
```

### 2. Using FormControl, FormGroup, and FormBuilder

#### FormControl
- **Creating Individual Form Controls:**

  ```typescript
  import { FormControl } from '@angular/forms';
  const name = new FormControl('');
  console.log(name.value); // Output: ''
  name.setValue('John');
  console.log(name.value); // Output: 'John'
  ```

- **Tracking Value and State Changes:**

  ```typescript
  name.valueChanges.subscribe(value => console.log(value));
  name.statusChanges.subscribe(status => console.log(status));
  ```

#### FormGroup
- **Grouping Multiple Form Controls:**

  ```typescript
  import { FormGroup, FormControl } from '@angular/forms';
  const profileForm = new FormGroup({
    firstName: new FormControl(''),
    lastName: new FormControl('')
  });
  console.log(profileForm.value);
  ```

#### FormBuilder
- **Simplifying Form Creation:**

  ```typescript
  import { FormBuilder } from '@angular/forms';
  const fb = new FormBuilder();
  const form = fb.group({
    username: [''],
    password: ['']
  });
  console.log(form.value);
  ```

### 3. Form Validation

#### Built-in Validators
- **Example of Required Validator:**

  ```typescript
  import { Validators } from '@angular/forms';
  const emailControl = new FormControl('', [Validators.required, Validators.email]);
  console.log(emailControl.valid); // false
  ```

#### Custom Validations
- **Creating Custom Validator Function:**

  ```typescript
  function ageValidator(control: FormControl) {
    return control.value >= 18 ? null : { ageInvalid: true };
  }
  ```

### 4. Handling Form Submission

```typescript
onSubmit() {
  if (profileForm.valid) {
    console.log(profileForm.value);
  }
}
```

### 5. Reactive Form State Management

```typescript
profileForm.controls['firstName'].disable();
profileForm.controls['lastName'].enable();
```

### 6. Working with Form Arrays

```typescript
const items = new FormArray([
  new FormControl('Item 1'),
  new FormControl('Item 2')
]);
```

## Angular Nexus Integration

### 1. Publishing Components to Nexus

```shell
npm login --registry=http://your-nexus-repo.com/repository/npm-private/
npm publish
```

### 2. Installing Dependencies from Nexus

```shell
npm install @your-scope/component-name --registry=http://your-nexus-repo.com/repository/npm-private/
```

### 3. Automating Deployments with CI/CD

```yaml
steps:
  - name: Install dependencies
    run: npm install
  - name: Publish to Nexus
    run: npm publish
```

By following this detailed student manual, you will gain a comprehensive understanding of Angular Reactive Forms and Nexus integration, enabling you to build robust applications with efficient form handling and scalable component management.

# Angular Student Manual

## Module 1: Angular DevTools for Debugging

### 1.1 Introduction to Angular DevTools
- Overview of Angular DevTools
- Importance of debugging in Angular applications
- Installation and setup of Angular DevTools

**Concept Explanation:**
Angular DevTools provides insights into the internal working of Angular applications by offering features like component tree inspection and performance profiling.

**Sample Code:**
```typescript
console.log('Debugging with Angular DevTools');
```

### 1.2 Exploring the Component Tree
- Inspecting component hierarchy
- Viewing component properties and bindings
- Understanding component change detection

**Concept Explanation:**
Component trees allow developers to visualize component dependencies and inspect properties and bindings easily.

**Sample Code:**
```html
<app-child-component [inputProp]="value"></app-child-component>
```

### 1.3 Performance Profiling
- Tracking component rendering times
- Detecting performance bottlenecks
- Analyzing re-renders and state changes

**Concept Explanation:**
Performance profiling helps identify bottlenecks and optimize rendering times for a smoother user experience.

**Sample Code:**
```typescript
ngOnChanges() { console.time('render'); /* perform logic */ console.timeEnd('render'); }
```

### 1.4 State Inspection and Analysis
- Monitoring application state
- Examining reactive data flows
- Debugging issues with dependency injection

**Concept Explanation:**
State inspection allows tracking of component and service data to identify potential issues in state management.

**Sample Code:**
```typescript
constructor(private service: MyService) { console.log(service.getData()); }
```

### 1.5 Practical Debugging Scenarios
- Common debugging challenges and solutions
- Using breakpoints and console logs
- Best practices for efficient debugging

**Best Practices and Tips:**
- Use `console.log` strategically to avoid clutter.
- Debug change detection issues with DevTools timeline.

## Module 2: Unit Testing with Jasmine/Karma

### 2.1 Introduction to Unit Testing
- What is unit testing?
- Importance of unit testing in Angular applications
- Overview of Jasmine and Karma

### 2.2 Setting Up Jasmine and Karma
- Configuring Karma test runner
- Writing the first test case
- Running tests and analyzing results

### 2.3 Writing Unit Tests
- Testing components, services, and directives
- Using spies and mocks
- Handling asynchronous operations

**Sample Test Cases:**
```typescript
describe('AppComponent', () => {
  let fixture: ComponentFixture<AppComponent>;
  let component: AppComponent;

  beforeEach(() => {
    TestBed.configureTestingModule({
      declarations: [AppComponent]
    }).compileComponents();
    fixture = TestBed.createComponent(AppComponent);
    component = fixture.componentInstance;
  });

  it('should create the app', () => {
    expect(component).toBeTruthy();
  });

  it('should render title in a h1 tag', () => {
    component.title = 'Test App';
    fixture.detectChanges();
    const compiled = fixture.nativeElement;
    expect(compiled.querySelector('h1').textContent).toContain('Test App');
  });
});
```

### 2.4 Best Practices
- Structuring test cases
- Avoiding anti-patterns
- Achieving high code coverage

## Module 3: Test Automation with Cypress

### 3.1 Introduction to Cypress
- Overview and benefits of Cypress
- Setting up Cypress in an Angular project

### 3.2 Writing E2E Test Cases
- Interacting with UI elements
- Performing assertions
- Handling asynchronous operations

**Sample Test Cases:**
```javascript
describe('Login Page', () => {
  it('should successfully login with valid credentials', () => {
    cy.visit('/login');
    cy.get('#username').type('user1');
    cy.get('#password').type('password123');
    cy.get('button[type="submit"]').click();
    cy.url().should('include', '/dashboard');
  });
});
```

### 3.3 Debugging and Reporting
- Using Cypress Dashboard
- Generating test reports
- Integration with CI/CD

## Module 4: End-to-End CRUD Implementation

### 4.1 Setting Up the Angular Project
- Creating a new Angular application
- Installing required dependencies

### 4.2 Implementing CRUD Operations
- Creating services for API interactions
- Handling form inputs and validation
- CRUD UI components

**Sample Test Cases:**
```typescript
describe('Employee Service', () => {
  let service: EmployeeService;
  let httpMock: HttpTestingController;

  beforeEach(() => {
    TestBed.configureTestingModule({
      providers: [EmployeeService],
      imports: [HttpClientTestingModule]
    });
    service = TestBed.inject(EmployeeService);
    httpMock = TestBed.inject(HttpTestingController);
  });

  it('should fetch employee list', () => {
    service.getEmployees().subscribe(employees => {
      expect(employees.length).toBe(3);
    });

    const req = httpMock.expectOne('/api/employees');
    expect(req.request.method).toBe('GET');
    req.flush([{ id: 1 }, { id: 2 }, { id: 3 }]);
  });
});
```

### 4.3 Routing and Navigation
- Setting up Angular routes
- Implementing route guards

### 4.4 State Management
- Using NgRx for state management
- Caching API responses

### 4.5 Testing CRUD Operations
- Unit and integration tests for CRUD
- E2E testing with Cypress

## Example Projects
Mini-projects demonstrating CRUD operations, testing, and debugging.

**Project:** Employee Management CRUD
**Features:** Create, Read, Update, Delete operations with Angular Forms.

**Code Repository:** [GitHub Repo](https://github.com/example/angular-crud)

## Quizzes and Assessments
- Multiple-choice questions and coding exercises.
- Practical assignments.

## Appendix

### A.1 Glossary of Terms
### A.2 Additional Resources and Further Reading
### A.3 Common Errors and Troubleshooting







