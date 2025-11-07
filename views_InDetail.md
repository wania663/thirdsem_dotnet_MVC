# 🎨 ASP.NET Core MVC — Views (Beginner Friendly Notes)

---

## 🧠 Basic Concept
**View** basically wo part hota hai jo **user ko dikhai deta hai.**  
It shows the output to the user, like pages such as home, about, or user list.

Think like this 👇
- **Model** → Data aur logic ka brain  
- **Controller** → Bridge (traffic police)  
- **View** → Frontend (jo user dekhta hai)

Flow:
1. Controller request receive karta hai  
2. Model se data fetch karta hai  
3. View ko data send karta hai  
4. View HTML ke through data dikhata hai  

---

## 📂 Folder Structure (Inside Views Folder)

```

Views/
├── Home/
│     ├── Index.cshtml
│     ├── About.cshtml
│     └── Contact.cshtml
├── User/
│     ├── Index.cshtml
│     ├── Create.cshtml
│     ├── Edit.cshtml
│     ├── Delete.cshtml
├── Shared/
│     ├── _Layout.cshtml
│     ├── _ViewImports.cshtml
│     ├── _ViewStart.cshtml
│     └── _ValidationScriptsPartial.cshtml

````

---

## 🔹 1️⃣ Views/Home/
This folder belongs to **HomeController.cs**  
Usually contains:
- **Index.cshtml** → Homepage  
- **About.cshtml** → About Page  
- **Contact.cshtml** → Contact Form  

**Example:**
```html
<h1>Welcome to My Website!</h1>
<p>This is the home page.</p>
````

---

## 🔹 2️⃣ Views/User/

This folder belongs to **UserController.cs**

| File          | Purpose        |
| ------------- | -------------- |
| Index.cshtml  | Show all users |
| Create.cshtml | Add new user   |
| Edit.cshtml   | Update user    |
| Delete.cshtml | Confirm delete |

**Example:**

```html
@model IEnumerable<MyApp.Models.User>
<h2>User List</h2>
@foreach(var u in Model)
{
   <p>@u.Name - @u.Email</p>
}
```

**Controller Example:**

```csharp
public IActionResult Index()
{
   var users = _context.Users.ToList();
   return View(users);
}
```

---

## 🔹 3️⃣ Views/Shared/

This folder stores **common files** used in multiple pages.

| File                             | Purpose                      |
| -------------------------------- | ---------------------------- |
| _Layout.cshtml                   | Main layout (header, footer) |
| _ViewImports.cshtml              | Imports namespaces & helpers |
| _ViewStart.cshtml                | Sets default layout          |
| _ValidationScriptsPartial.cshtml | Adds form validation scripts |

---

## 🩵 _Layout.cshtml (Master Page)

Acts like a **template** for all pages.
Each view’s content appears where `@RenderBody()` is placed.

**Example:**

```html
<!DOCTYPE html>
<html>
<head>
   <title>@ViewData["Title"]</title>
</head>
<body>
   <header>
      Navbar - <a href="/">Home</a> | <a href="/User">Users</a>
   </header>

   <main>
      @RenderBody()
   </main>

   <footer>© 2025 MyApp</footer>
</body>
</html>
```

---

## 🩵 _ViewStart.cshtml

Tells every view which layout to use.

```csharp
@{
   Layout = "_Layout";
}
```

So, every page automatically applies `_Layout.cshtml`.

---

## 🩵 _ViewImports.cshtml

Contains namespaces and tag helpers that are shared across views.

```csharp
@using MyApp.Models
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```

---

## 🩵 _ValidationScriptsPartial.cshtml

Adds **client-side validation scripts** for forms.

```html
<script src="~/lib/jquery-validation/dist/jquery.validate.min.js"></script>
<script src="~/lib/jquery-validation-unobtrusive/jquery.validate.unobtrusive.min.js"></script>
```

---

## 💬 Full Example Flow

**Controller:**

```csharp
public IActionResult Index()
{
   var users = _context.Users.ToList();
   return View(users);
}
```

**View:**

```html
@model IEnumerable<MyApp.Models.User>
<h2>Users List</h2>
@foreach(var u in Model)
{
   <p>@u.Name (@u.Email)</p>
}
```

**Output:**

```
Users List
John (john@email.com)
Emma (emma@email.com)
```

---

## 🧩 Quick Summary

| Folder            | Purpose             | Example            |
| ----------------- | ------------------- | ------------------ |
| Home              | Static pages        | Index.cshtml       |
| User              | CRUD pages          | Create/Edit/Delete |
| Shared            | Common design files | _Layout.cshtml     |
| Each .cshtml file | HTML + Razor View   | Used for display   |

---

## 🧠 Key Takeaway

* **View** is the presentation layer.
* It displays data provided by the **Controller**.
* Uses `.cshtml` files (HTML + Razor syntax).
* Common design and logic stay in **Shared folder**.

---




