# Next.js

The React Framework for the Web.

## What is Next.js?

Next.js is a React framework for building full-stack websites and applications. You can use React components to build the UI, and take advantage of Next.js's additional features and optimizations.

Next.js automatically configures and compiles your application, so you can focus on building it instead of setting everything up from scratch. Among other things, it allows you to render pages on the server.

## Key Features

- Rendering
- Optimizations
- TypeScript
- Routing
- Data Fetching

## Creating a Project

You can create a React application using a build tool such as Vite, or create it with Next.js, which already includes features like routing.

### React with Vite

To create a React project with JavaScript:

```bash
npm create vite@latest my-react-project -- --template react
cd my-react-project
npm install
npm run dev
```

To use TypeScript, replace the `react` template with `react-ts`:

```bash
npm create vite@latest my-react-project -- --template react-ts
```

### Next.js

To create a Next.js project:

```bash
npx create-next-app@latest my-next-project
cd my-next-project
npm run dev
```

The setup wizard lets you choose options such as TypeScript, ESLint, and the App Router. After starting the server, open the address shown in the terminal (usually `http://localhost:3000`).

## Next.js Routers: App Router and Pages Router

Since version 13, Next.js has two routers: the **App Router** and the **Pages Router**. For new projects, the App Router is recommended. The Pages Router is still available, but all new Next.js features are added to the App Router.

The code between the App Router and the Pages Router can be quite different, especially when it comes to file naming conventions and data fetching.

## App Router File Conventions

The App Router includes file conventions that organize your application and define the behavior of its routes. Folders represent route segments; for a route to be accessible, it typically needs to include a `page` or `route` file.

Files can use the `.js`, `.jsx`, or `.tsx` extensions.

- `layout`: shared UI for a route and its child routes.
- `page`: the UI for a route.
- `loading`: UI shown while a route is loading, using Suspense.
- `not-found`: UI shown when a resource is not found (404).
- `error`: UI shown for unexpected errors.
- `route`: an API endpoint, for example for a REST API.

## Rendering in Next.js

### Client and Server Components

#### Server Components

Server Components are a new type of component that is rendered ahead of the application, before building the bundle, in an environment separate from your application.

One of the main features Next.js has had since it was launched is the ability to run React code on the server (SSR).

In earlier versions, the same code would run first on the server and then on the client.

Since Next.js 13 with the app directory, all components run on the server by default.

When needed, you can mark a component to run on the client using the `"use client"` directive.

When you have applications with both Server and Client Components, it's important to note that the data flow is unidirectional.

### Considerations

#### When to Use Server Components

- Fetch data from an ORM and display it.
- Run server-side functions and access resources that are only available on the backend.
- Handle authentication, API keys, or tokens.

#### When to Use Client Components

- Add interactivity to your application using events such as `onClick`, `onSubmit`, and `onChange`.
- Use React hooks such as `useState`, `useEffect`, and `useReducer`.
- Use libraries that do not run on the server, such as Toast, Zustand, or other client-only libraries.
- Use browser APIs such as Local Storage, the Notifications API, and the Geolocation API.
- Consume JSON data from an external API.


## Prisma ORM (Object-Relational Mapping)

Prisma is an open-source ORM for JavaScript and TypeScript. Its main tools are Prisma Client, Prisma Migrate, and Prisma Studio.

### Prisma tools

- **Prisma Client** is a type-safe query builder for accessing your database. It supports Node.js and works with Next.js.
- **Prisma Migrate** lets you define your database tables and relationships in a Prisma schema, then create and manage database migrations.
- **Prisma Studio** is a visual interface for viewing and editing data in your database locally.

### Installing Prisma

From your project directory, install the Prisma CLI and client, then initialize Prisma. Choose the provider that matches your database:

```bash
npm install prisma --save-dev
npm install @prisma/client @prisma/adapter-pg pg
npx prisma init --datasource-provider postgresql
```

For a SQL database such as PostgreSQL, set your `DATABASE_URL` in `.env`, define your models in `prisma/schema.prisma`, and create the database tables with:

```bash
npx prisma migrate dev --name init
npx prisma generate
npx prisma studio
```

The migration command above is for SQL databases; MongoDB uses a different workflow. The adapter packages above are for PostgreSQL, and Prisma ORM 7 requires a driver adapter to connect to your database. Installation and setup details vary by database and Prisma version, so follow the relevant guide in the [official Prisma documentation](https://www.prisma.io/docs/orm).

### Supported databases

- MariaDB
- Microsoft SQL Server (2017, 2019, and 2022)
- MongoDB
- MySQL
- PostgreSQL
- SQLite
