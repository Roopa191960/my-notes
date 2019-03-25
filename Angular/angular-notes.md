# Angular

# 1. Introdution

**What is Angular?**
Angular is a platform that makes it easy to build applications with the web. Angular combines declarative templates, dependency injection, end to end tooling, and integrated best practices to solve development challenges. Angular empowers developers to build applications that live on the web, mobile, or the desktop.

## 2. Installation

1. Install NodeJS + NPM
2. Check compatible/laterst versions: `npm -v` & `node -v`
3. Install Angular: `npm install -g @angular/cli`
4. Uninstall & install if required: `npm uninstall -g angular-cli @angular/cli `, `npm cache clean` and `npm install -g @angular/cli`
5. Check `ng --version`
6. New project: `ng new <PROJ_DIR>` 
7. Run project: `ng serve --open` -> keep it running! It got browser sync to rebuild and refresh in it :). `--open` opens browser.
8. Open project at: `http://localhost:4200/` 

## 3. Structure

* The `node_modules` directory is where all of the libraries we need to build Angular are stored.
* In the `src` directory, is placed the source code of your application.
* The `app/` folder contains file related to our initial App component:
* The `app.component.html` contains template of the component
* The `app.component.scss` contains the CSS styles for the component
* The `app.component.spec.ts` contains the tests of our component
* The `app.component.ts` contains a TypeScript code (logic) of the component
* The `app.module.ts` contains the configuration of the App module
* In the `assets` directory, you place any static assets like images or icons.
* `index.html` is the main file of our app.
* If we peek inside our `index.html` file, we can see there’s a element `<app-root></app-root>`, which will generate (render) our App component in the following place.
* The `styles.scss` or `styles.css` contains the global styles for our application
* The `angular.json` file contains the configuration of our app.

## 4. Components

Components can be thought of as small pieces of an interface that are independent of each other. Components of a similar nature are well encapsulated, in other words, self-sufficient. Developers can reuse them across different parts of an application.

### 4.1 Components of component

1. Component logic (.ts file)
    
    1. **Imports**: At the begining of the component's .ts file we have to import a Component from the Angular library. 
    2. **Metadata**: The `@Component` decorator which we imported in a first line allows us to specify a matadata for our component.

    ```js
    @Component({
        selector: 'app-root',
        templateUrl: './app.component.html',
        styleUrls: ['./app.component.scss']
    })
    ```
    3. **Class**: The logic holder.
    ```js
    export class AppComponent {
        ...
    }
    ```
2. Component template (.html) file)
3. Component styles (.scss file)
4. Component tests (.spec.ts file)
5. App.module code (.module.ts file) -> only one per project

### 4.1. Adding new componenents (Manually).

* Create component directory under app dir. `server` 
* Create component typescript file. `server.component.ts`
    ```js
        import { Component } from "@angular/core";

        @Component({
            selector: 'app-server',
            templateUrl: './server.component.html',
        })

        export class ServerComponent{
        }
    ```
* Create component html file. `server.component.html`
* Declare new component at `app.module.ts`.
    ```js
    import { ServerComponent } from './components/server/server.component';
    ...
    // In @NgModule({....});
    declarations: [
        AppComponent,
        ServerComponent,
    ],
    ...
    ```
* Use new selector in `app.component.html` as `<app-server></app-server>`

### 4.2. Adding new componenents (using generator).

* `ng generate component <COMP_NAME>`
* Or shorthand: `ng g c <DIR_NAME>/<COMP_NAME>`

* It declares and includes everything required.

### 4.3. Component properties

* typescript file: `template` -> direct HTML input, `templateUrl` -> points to external file.
* use `` instreaad of `''`
* Same can be applied to style as well: use `styleUrls: []` or `styles: [``]`.

### 4.4. Component selector options

1. Component selector: `selector: 'app-root'` ->use `<app-root></app-root>` 
2. Attribute selector: `selector: '[app-root]'` use: `<div app-root></div>`
3. Select by class: `selector: '.app-root'` use: `<div class="app-root"></div>`

## 5. Data binding
Communication between typescript to HTML

* One way or Two way.

1. String interpolation -> `{{ data }}`, `{{ fun_ret_string() }}`
2. Propert binding -> `[property] = "data"`. Properties like disabled, innerText, etc
    ```html
    <button [disabled]="!allowNewServer">Add new</button>
    ```
    ```js
    allowNewServer = false;
    constructor(){
        setTimeout(() => {
        this.allowNewServer = true;
        }, 2000);
    }
    ```
3. Event binding -> `(event) = "expression"`

    Example 1
    ```html
    <button (click)="onCreateServer()">Add new</button>
    ```
    ```js
    onCreateServer(){
        console.log('Clickec');
    }
    ```

    Example 2
    ```html
    <input type="text" name="servername" (input)="onNameUpdate($event)">
    ```
    ```js
    onNameUpdate(event: any){
        this.serverName = event.target.value;
    }
    ```

4. Two way data binding -> `[(ngModel)] = "data"`
    ```html
    <input type="text" name="servername" [(ngModel)]="serverName">
    ```
    ```js
    serverName = 'pre-filled-value';
    ```
    ** Requires `import { FormsModule } from '@angular/forms';` & `imports: [FormsModule],`  in app.module.ts.

## 6. Directives

Directives are instructions in the DOM. An Attribute directive changes the appearance or behavior of a DOM element.

There are three kinds of directives in Angular:
1. **Components** directives with a template.

    `<app-root></app-root>`

2. **Structural directives** change the DOM layout by adding and removing DOM elements.

    ```html
    <!-- If -->
    <p *ngIf="Condition_statement"> text</p>
    <!-- If Else -->
    <p class="alert alert-info" *ngIf="allowNewServer; else noAllow">You are allowed to create</p>
    <ng-template #noAllow>
        <p class="alert alert-danger">You are allowed to create</p>
    </ng-template>
    ```

3. **Attribute directives** change the appearance or behavior of an element, component, or another directive
    ```html
    <!-- Inline -->
    <h2 [ngStyle] = "{'color': 'gray'}" >text</h2>
    <!-- Using function -->
    <h2 class="text-center" [ngStyle] = "{'background-color': getColor()}" >text</h2>
    <!-- Adding classes -->
    <h2 class="text-center" [ngClass] = "{'my-class': serverStatus === 'online'}" >text</h2>
    ```