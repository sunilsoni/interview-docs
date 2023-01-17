---
layout: default
title: CLI
parent: Angular
resource: true
desc: "Angular CLI (Command Line Interface) interview questions and answers."
categories: [Angular Pipes]
---

# Angular CLI (Command Line Interface)
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

Angular is a JavaScript framework for building web applications and Angular CLI (Command Line Interface) is a tool that helps to create, manage, and test Angular projects. Here are some commonly used Angular CLI commands:

###   `ng new [project-name]` 

Creates a new Angular project with the given name.

```typescript
ng new my-project
```

###    `ng serve`

Runs the project locally in development mode and starts a development server. It also watches for file changes and automatically rebuilds the application.

```typescript
ng serve

```

###   `ng generate [schematic] [name]`

Generates new files and updates existing files based on a schematic. The schematic can be a component, service, module, etc.

```typescript

ng generate component my-component

```

###   `ng build`

Builds the project for production and creates a distribution version in the dist folder. It also minifies and optimizes the code for better performance.

```typescript
ng build --prod


```

###    `ng test`

Runs unit tests for the project using the Karma test runner.


```typescript
ng test


```

###    `ng lint`

Lints the project's code using the configured linter. It checks for code style and potential errors.



```typescript
ng lint


```

###    `ng e2e`

Runs end-to-end (E2E) tests for the project using the Protractor test framework.


```typescript

ng e2e

```

###    `ng update`

Updates the project's dependencies and configuration to the latest version of Angular.


```typescript
ng update @angular/cli


```

###   ` ng xi18n`

Extracts i18n messages from the project's code for localization.


```typescript
ng xi18n --output-path src/locale


```

###    `ng add [package]`

Add new capabilities to your project with additional libraries or packages.


```typescript
ng add @ng-bootstrap/schematics


```

###    `ng deploy`

Deploys the application to a specified platform.


```typescript
ng deploy --project my-project


```

###    `ng doc [keyword]`

Opens the official Angular documentation in the browser and searches for the specified keyword.

```typescript
ng doc component


```
###    `ng eject`

Ejects the project from the Angular CLI and gives you full control over the build and configuration.

```typescript

ng eject

```

###   ` ng help`

Displays a list of available commands and their descriptions.
```typescript

ng help

```
###    `ng version`

Shows the version of the installed Angular CLI and the version of the locally installed packages.

```typescript

ng version

```

 
