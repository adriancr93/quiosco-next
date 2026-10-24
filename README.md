# Quiosco Next.js

**Quiosco** is a self-service food-ordering kiosk app built with Next.js 14 (App Router), TypeScript, Prisma, and PostgreSQL. Customers browse products by category and place orders; an admin panel manages products and tracks/completes orders.

## Tech stack

- **Next.js 14** (App Router) + React 18 + TypeScript
- **Prisma 5** ORM with **PostgreSQL**
- **Tailwind CSS** for styling
- **Zustand** for client-side cart state ([src/store.ts](src/store.ts))
- **SWR** for client-side data fetching
- **Zod** for schema/form validation ([src/schema](src/schema))
- **next-cloudinary** for product image uploads (Cloudinary)
- **react-toastify** for toast notifications

## Project structure

- [app/](app) — routes (App Router): `/` (categories home), `/order/[category]` (customer ordering flow), `/orders` (public order-status board + API), `/admin` (products & orders management + API)
- [actions/](actions) — Next.js Server Actions (`create-order-action`, `complete-order-action`, `create-product-action`, `update-product-action`)
- [components/](components) — UI split into `admin/`, `order/`, `products/`, `ui/`
- [prisma/schema.prisma](prisma/schema.prisma) — data model: `Category`, `Product`, `Order`, `OrderProducts`
- [prisma/seed.ts](prisma/seed.ts) — seeds categories/products from [prisma/data](prisma/data)
- [src/](src) — `lib/` (Prisma client singleton), `schema/` (Zod schemas), `types/`, `utils/`

## Getting started

1. Install dependencies:

   ```bash
   npm install
   ```

2. Copy the environment template and set your PostgreSQL connection string:

   ```bash
   cp .env.example .env
   ```

   Set `DATABASE_URL` in `.env` (PostgreSQL >= 15 required).

3. Apply migrations and generate the Prisma Client:

   ```bash
   npx prisma migrate dev
   ```

4. (Optional) Seed the database with sample categories and products:

   ```bash
   npx prisma db seed
   ```

5. Run the development server:

   ```bash
   npm run dev
   ```

   Open [http://localhost:3000](http://localhost:3000) for the customer view, and `/admin` for the admin panel.

## npm scripts

```bash
npm run dev     # start the dev server (next dev)
npm run build   # build for production (next build)
npm run start   # start the production server (next start)
npm run lint    # run ESLint (next lint)
```

## Environment variables

| Variable       | Description                                          |
| -------------- | ----------------------------------------------------- |
| `DATABASE_URL` | PostgreSQL connection string used by Prisma.          |

Product images are uploaded via a Cloudinary upload widget (`next-cloudinary`) using a hardcoded upload preset in [components/products/ImageUpload.tsx](components/products/ImageUpload.tsx), and `next.config.mjs` allows images from `res.cloudinary.com`. No Cloudinary API keys are required client-side for the current unsigned upload preset.

---

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

This project uses Prisma 7 with PostgreSQL. Set `DATABASE_URL` in a local `.env` file; `prisma.config.ts` loads it and points the CLI to `prisma/schema.prisma`. The Prisma schema is in `prisma/schema.prisma`, and migrations are stored in `prisma/migrations/`.

### Prisma commands

Run these commands from the project root. They use the Prisma CLI installed in this project:

```bash
npx prisma generate
npx prisma validate
npx prisma format
npx prisma migrate dev --name <migration_name>
npx prisma migrate status
npx prisma migrate deploy
npx prisma studio
```

Use `migrate dev` while developing to create and apply a migration, replacing `<migration_name>` with a descriptive name (for example, `add_product_description`). Use `migrate deploy` to apply committed migrations in production or CI; it does not create migrations. `migrate status` checks whether the database is up to date. `generate` regenerates the Prisma Client after schema changes, and `studio` opens the local database browser.

The following commands are available for specific workflows:

```bash
npx prisma db push
npx prisma db pull
npx prisma migrate reset
```

`db push` synchronizes the schema directly without creating a migration, so prefer `migrate dev` for changes that should be tracked in Git. `db pull` introspects the database and updates the Prisma schema. `migrate reset` drops and recreates the development database, reapplies migrations, and deletes its data; do not run it against a database whose data you need to keep.

For PostgreSQL, Prisma ORM 7 also uses the project's PostgreSQL driver adapter when the application connects to the database. For more details, see the [official Prisma documentation](https://www.prisma.io/docs/orm).

### Supported databases

- MariaDB
- Microsoft SQL Server (2017, 2019, and 2022)
- MongoDB
- MySQL
- PostgreSQL
- SQLite

Data Fetching

Data fetching in Next.js can be done in four different ways:

- On the server with `fetch()`.
- On the server with an ORM or SQL queries.
- On the client with a Route Handler and a GET request.
- On the client with React Query, Axios, SWR, or other options.

