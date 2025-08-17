An ORM is a tool that helps you work with a database using a regular code instead of writing SQL manually.

## Why An Orm
***

1. Easier to write and read: You use the same language you're coding in (eg JS)
2. Safer. It helps prevent mistakes like SQL injection.
3. Faster development: You don't have to write repetitive SQL for common actions (like creating, reading, updating data)
4. Clear models: You define your data as code, so it's easy to see the structure of your database.
## Why Prisma 
***
1. Typesafety
2. Perfomance
3. Community

```
POSTGRES_USER: ndanyikevin
POSTGRES_DB: prisma_tutorial
POSTGRES_PASSWORD: Kevin123
```
 
## pnpm dlx prisma init
***
this is *Prisma setup command* but run without installing Prisma globally

prisma init creates initial Prisma project setup in your app
1. prisma/schema.prisma

`pnpm dlx prisma init` is basically the **Prisma setup command**, but run without installing Prisma globally.

Here’s what happens step by step:

---

### 1️⃣ `pnpm dlx`

- `pnpm dlx` is like `npx` but for PNPM.
    
- It downloads and runs a package **temporarily** without adding it to your `package.json`.
    
- In this case, it’s downloading the Prisma CLI (`prisma`) just for this command.
    

---

### 2️⃣ `prisma init`

- This creates the **initial Prisma project setup** in your app:
    
    1. **`prisma/schema.prisma`** → the main file where you define your database models and datasource (connection).
        
    2. **`.env`** → environment variables file containing your `DATABASE_URL`.
        
    3. Updates `.gitignore` to ignore the `.env` file.
        
- It’s the “first step” to start working with Prisma.
    

---

### 3️⃣ After Running

You’ll have a folder structure like:

```
.
├── prisma/
│   └── schema.prisma
└── .env
```

---

💡 In short:  
`pnpm dlx prisma init` → **Temporarily installs Prisma CLI, then scaffolds Prisma's starter files in your project.**

---

If you want, I can show you **how your connection string for Docker Postgres would be inserted automatically** when you run this. That way, Prisma will be ready to talk to your database right after `init`.


## pnpm dlx prisma migrate dev --name init
***
`pnpm dlx prisma migrate dev --name init` is the **command that actually creates your database tables** from your Prisma schema during development.

Here’s what it does step-by-step:

---

### 1️⃣ `pnpm dlx`

Again, runs Prisma CLI temporarily (without needing a global install).

---

### 2️⃣ `prisma migrate dev`

This is the **development migration command**.  
It:

1. **Reads** your `prisma/schema.prisma` file.
    
2. **Generates a SQL migration file** inside `prisma/migrations/`.
    
3. **Applies** that migration to your database.
    
4. **Regenerates the Prisma Client** so your app can query the DB with updated types.
    

---

### 3️⃣ `--name init`

- This is just the **name** you give to the migration folder.
    
- `"init"` is usually used for the very first migration — it might contain all your initial tables.
    
- You could also name it something descriptive like `"add_users_table"`.
    

---

### 4️⃣ Example result

If your schema looks like:

```prisma
model User {
  id    Int     @id @default(autoincrement())
  name  String
  email String  @unique
}
```

Running:

```sh
pnpm dlx prisma migrate dev --name init
```

Will create:

```
prisma/migrations/
└── 20250808123456_init/
    └── migration.sql   # SQL that creates the User table
```

And it will apply that SQL to your **actual database**.

---

💡 In short:  
`pnpm dlx prisma migrate dev --name init` → **Creates and applies a database migration based on your schema, and regenerates Prisma Client for type-safe queries.**

--- 


## How to view tables in docker postgres
---
Since your Postgres is running inside Docker, you can see the tables in a few ways — either **inside the container** or **from your host machine**.

---

## **Option 1 – Exec into the Postgres container**

1. Find your container name (you said it’s `postgres`, but you can confirm):
    
    ```sh
    docker ps
    ```
    
2. Open an interactive shell inside it:
    
    ```sh
    docker exec -it postgres psql -U ndanyikevin -d prisma_tutorial
    ```
    
    _(replace `ndanyikevin` and `prisma_tutorial` with your actual `POSTGRES_USER` and `POSTGRES_DB`)_
    
3. Once inside `psql`, run:
    
    ```sql
    \dt
    ```
    
    This lists all tables.
    
4. To exit:
    
    ```sql
    \q
    ```
    

---

## **Option 2 – Connect directly from your host**

If `psql` is installed locally, you can connect without going into Docker:

```sh
psql -h localhost -p 5434 -U ndanyikevin -d prisma_tutorial
```

Then run:

```sql
\dt
```

---

## **Option 3 – Use Prisma Studio (Visual)**

If you want a GUI:

```sh
pnpm dlx prisma studio
```

This will open a browser-based interface showing all tables and data.

---

If you want, I can also give you **a single Docker command** that will instantly list all tables in your DB without going into `psql` manually. That’s the fastest method for checking.