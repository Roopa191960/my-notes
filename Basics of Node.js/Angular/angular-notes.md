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