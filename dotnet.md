# C# Fundamentals: Task, ValueTask, IQueryable

These three types are used everywhere in ASP.NET Core and Entity Framework. Understanding them will make reading backend code much easier.

---

# Task<T>

## What is it?

`Task<T>` represents an **asynchronous operation** that will return a value of type `T` in the future.

Example:

```csharp
Task<ApplicationUser> GetMeAsync();
```

This means:

> This method cannot return an `ApplicationUser` immediately (for example, because it needs to query the database). Instead, it returns a `Task` that will eventually contain the result.

Usage:

```csharp
ApplicationUser user = await identityBroker.GetMeAsync();
```

The `await` keyword tells the program:

> "Wait here until the asynchronous operation completes."

---

## When is it used?

Use `Task<T>` for operations that take time, such as:

- Database queries
- HTTP requests
- File operations
- Calling external services

These operations should not block the current thread.

---

## Why not return the object directly?

Because retrieving the data takes time.

```
Application
      │
      ▼
Database Request
      │
      ▼
Waiting...
      │
      ▼
ApplicationUser
```

Instead of blocking the thread, the method returns a `Task`.

---

## How to remember

> **Task = A promise to return a value later.**

---

# ValueTask<T>

## What is it?

`ValueTask<T>` is similar to `Task<T>`, but it is optimized for scenarios where the result may already be available.

Example:

```csharp
ValueTask<IdentityResult> InsertUserAsync(...);
```

---

## Why does it exist?

Creating a `Task` allocates memory.

If a method frequently completes immediately, creating a new `Task` every time is unnecessary.

`ValueTask` allows the method to return the result directly without creating a new `Task`.

```
Is the result already available?
        │
 Yes ───┴──► Return immediately
        │
 No
        ▼
Create a Task
```

---

## When should you use it?

In most applications, simply use `Task`.

Use `ValueTask` only when performance optimization is necessary.

If you're unsure, choose `Task`.

---

## How to remember

> **ValueTask = Task with an optimization for already available results.**

---

# IQueryable<T>

## What is it?

`IQueryable<T>` represents a **database query**, not the actual data.

Example:

```csharp
IQueryable<ApplicationUser> GetAll();
```

This does **NOT** mean:

> Return all users.

It means:

> Return a query that can be modified before execution.

---

## How does it work?

Create the query:

```csharp
var users = broker.GetAll();
```

No SQL is executed yet.

Add filtering:

```csharp
users = users.Where(u => u.Age > 18);
```

Still no database call.

Add sorting:

```csharp
users = users.OrderBy(u => u.Name);
```

Still no database call.

Finally execute:

```csharp
var result = await users.ToListAsync();
```

Only now does Entity Framework generate and execute SQL:

```sql
SELECT *
FROM Users
WHERE Age > 18
ORDER BY Name;
```

---

## Why is this useful?

If the method returned:

```csharp
List<ApplicationUser>
```

the application would first load every user into memory.

```
Database
      │
100,000 users
      │
      ▼
Application Memory
      │
Filtering
```

This wastes memory and is inefficient.

With `IQueryable`, filtering happens inside the database.

```
Database
      │
WHERE Age > 18
ORDER BY Name
      │
      ▼
10 matching users
```

This is much faster.

---

## How to remember

> **IQueryable = A SQL query that hasn't been executed yet.**

The query is executed only when methods like these are called:

- `ToListAsync()`
- `FirstOrDefaultAsync()`
- `SingleAsync()`
- `CountAsync()`
- `AnyAsync()`

These are called **terminal operations** because they trigger query execution.

---

# Understanding the IIdentityBroker Interface

```csharp
public interface IIdentityBroker
{
    Task<ApplicationUser> GetMeAsync();

    IQueryable<ApplicationUser> GetAll();

    ValueTask<IdentityResult> InsertUserAsync(
        ApplicationUser applicationUser,
        string password);
}
```

## Method Breakdown

### `Task<ApplicationUser> GetMeAsync();`

Retrieves the currently authenticated user.

Since the user must be loaded from the database, the operation is asynchronous.

Returns:

```csharp
Task<ApplicationUser>
```

---

### `IQueryable<ApplicationUser> GetAll();`

Returns a query for all users.

The database is **not queried immediately**.

You can continue building the query:

```csharp
.Where(...)
.OrderBy(...)
.Skip(...)
.Take(...)
```

The SQL query is executed only when calling methods like `ToListAsync()`.

---

### `ValueTask<IdentityResult> InsertUserAsync(...)`

Creates a new user.

Returns an `IdentityResult` describing whether the operation succeeded or failed.

`ValueTask` is used as a performance optimization.

---

# Quick Cheat Sheet

| Type | Meaning | Easy Way to Remember |
|------|---------|----------------------|
| `Task<T>` | Asynchronous operation | Promise to return a value later |
| `ValueTask<T>` | Optimized asynchronous operation | Returns immediately if possible |
| `IQueryable<T>` | Deferred database query | SQL query that hasn't executed yet |

---

# Mental Model

Whenever you see:

```csharp
Task<T>
```

Ask yourself:

> **"What operation takes time?"**

Usually:
- Database
- Network
- File system

---

Whenever you see:

```csharp
ValueTask<T>
```

Ask yourself:

> **"Can this result already be available?"**

If yes, `ValueTask` avoids creating a new `Task`.

---

Whenever you see:

```csharp
IQueryable<T>
```

Ask yourself:

> **"Has the database been queried yet?"**

Most of the time, the answer is:

> **No. The query is still being built.**
