# 💎 ASP.NET Core MVC – Views (Scratch → Pro)

---

## 🌱 A. Basic Understanding (Foundation Level)

### 🔹 What is a View?
View ek file hoti hai jo **user ko output (HTML page)** dikhati hai.  
Simple words me → Controller data laya, View us data ko dikhata hai.

💡 Example:  
Agar controller ne user list bheji → view us list ko ek HTML table me show karega.

> So, **View = UI (User Interface)** part of MVC.

---

## 🧩 B. View Folder Structure (Project Level)

Default MVC structure:
```

📂 Views/
├── 📁 Home/
│     ├── Index.cshtml
│     ├── About.cshtml
│     └── Contact.cshtml
├── 📁 User/
│     ├── Index.cshtml
│     ├── Create.cshtml
│     ├── Edit.cshtml
│     ├── Delete.cshtml
├── 📁 Shared/
│     ├── _Layout.cshtml
│     ├── _ViewStart.cshtml
│     ├── _ViewImports.cshtml
│     ├── _ValidationScriptsPartial.cshtml

```

### 🔹 Home folder:
`HomeController` ke liye views yahan rakhe jate hain.  
Example: `return View("Index")` → open karega `Views/Home/Index.cshtml`.

### 🔹 User folder:
`UserController` ke liye sab views (Create/Edit/Delete etc.) yahan honge.

### 🔹 Shared folder:
Yahan **common views** hoti hain jo sab pages me reuse hoti hain.  
Jaise:
- `_Layout.cshtml` → master layout (navbar, footer)
- `_ViewStart.cshtml` → default layout set krta
- `_ViewImports.cshtml` → common namespaces import
- `_ValidationScriptsPartial.cshtml` → validation js include

---

## ⚙️ C. View Connection Rule

Controller jab `return View()` likhta hai,
ASP.NET auto search krta hai:
```

Views/<ControllerName>/<ActionName>.cshtml

````

💡 Example:
```csharp
public class UserController : Controller
{
    public IActionResult Index()
    {
        return View();
    }
}
````

→ ASP.NET search karega: `Views/User/Index.cshtml`

---

## 🎨 D. Razor (.cshtml) Basics

### 🔹 Razor kya hai?

Razor ek **templating engine** hai jo HTML aur C# code ko mix krne deta hai.

### 🔹 Syntax:

```html
<h2>Hello @Model.Name</h2>
<p>Today: @DateTime.Now</p>
```

### 🔹 Razor Comments:

```csharp
@* ye comment browser me show nahi hoga *@
```

---

## 💻 E. Types of Views

| Type                | Use                  | Example            |
| ------------------- | -------------------- | ------------------ |
| Normal View         | Simple HTML Page     | Index.cshtml       |
| Strongly Typed View | Model data display   | `@model User`      |
| Partial View        | Reusable component   | `_UserCard.cshtml` |
| Layout View         | Common master design | `_Layout.cshtml`   |

---

## ⚡ F. Strongly Typed Views

### 🔹 Purpose:

Model data directly view me pass krne ke liye.

### 🔹 Example:

**Controller:**

```csharp
public IActionResult Details()
{
    var user = new User { Name = "Wania", Age = 17 };
    return View(user);
}
```

**View (Details.cshtml):**

```html
@model User
<h2>@Model.Name - @Model.Age</h2>
```

Output:
`Wania - 17`

✅ Benefits:

* Compile-time error check
* IntelliSense support

---

## 🎨 G. Layout Views (Master Page Design)

### 🔹 _Layout.cshtml

Is file me header, footer, navbar hota hai.
Har page ka base structure yehi hota hai.

Example:

```html
<!DOCTYPE html>
<html>
<head>
    <title>@ViewData["Title"] - MyApp</title>
</head>
<body>
    <header>My Navbar</header>
    <div class="content">
        @RenderBody()
    </div>
    <footer>© 2025 MyApp</footer>
</body>
</html>
```

### 🔹 _ViewStart.cshtml

Yahan likha jata hai konsa layout use hoga:

```csharp
@{
    Layout = "_Layout.cshtml";
}
```

---

## ⚙️ H. _ViewImports.cshtml

Yahan global settings hoti hain:

```csharp
@using MyApp.Models
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```

Matlab ab har view me `@using` likhne ki zarurat nahi.

---

## 🧩 I. Partial Views (Reusable Components)

Partial view = chhoti view jo doosri view me include hoti hai.

**Example:**
`_UserCard.cshtml`

```html
<div class="card">
  <h3>@Model.Name</h3>
</div>
```

**Use:**

```html
@Html.Partial("_UserCard", user)
```

---

## 💬 J. Data Passing Methods

| Method   | Description           | Example                   |
| -------- | --------------------- | ------------------------- |
| Model    | Strongly typed object | `return View(user);`      |
| ViewBag  | Dynamic property      | `ViewBag.Name = "Wania";` |
| ViewData | Key-value dictionary  | `ViewData["Age"] = 17;`   |

**View Example:**

```html
<h3>@Model.Name</h3>
<h4>@ViewBag.Name</h4>
<h5>@ViewData["Age"]</h5>
```

---

## 🧠 K. Tag Helpers

Tag Helpers HTML tags ko C# se connect krte hain.

Example:

```html
<form asp-controller="User" asp-action="Create">
    <input asp-for="Name" />
    <button type="submit">Save</button>
</form>
```

Ye HTML form ko direct `UserController` ke Create action se bind krta hai.

---

## 🧩 L. Razor Directives (Viva Ready)

| Directive          | Purpose          | Example                    |
| ------------------ | ---------------- | -------------------------- |
| `@model`           | define model     | `@model User`              |
| `@using`           | import namespace | `@using MyApp.Models`      |
| `@if`              | condition        | `@if(Model.Age > 18)`      |
| `@foreach`         | loop             | `@foreach(var u in Model)` |
| `@RenderBody()`    | layout body      | layout page me             |
| `@RenderSection()` | optional section | footer scripts ke liye     |

---

## 🔄 M. Full Flow (Request → Response)

1️⃣ User ne URL hit kiya `/User/Index`
2️⃣ Routing → `UserController.Index()`
3️⃣ Controller ne model data laya
4️⃣ `return View(model)`
5️⃣ View file: `Views/User/Index.cshtml`
6️⃣ Razor engine → HTML generate
7️⃣ Output browser me show ✅

---

## 🎓 N. Viva + Interview Qs

1️⃣ View kya hoti hai?
2️⃣ Razor kya karta hai?
3️⃣ ViewBag aur ViewData me fark?
4️⃣ @RenderBody aur @RenderSection difference?
5️⃣ _Layout.cshtml ka role kya hai?
6️⃣ Partial view kya hai?
7️⃣ _ViewStart aur _ViewImports kis liye use hote hain?
8️⃣ Tag Helpers kya hote hain?
9️⃣ View lifecycle explain karo.

---

## 💡 O. Pro Tips

✅ Views me logic mat likho — sirf display code rakho.
✅ Common layout use karo har page ke liye.
✅ Partial views se UI repeat avoid karo.
✅ Controller aur view naming same rakho.
✅ CSS & JS → `wwwroot/` folder me rakho.

---

# 🎨 ASP.NET Core MVC — Views (Beginner to Pro)

---

## 🎯 1️⃣ View kya hoti hai?
View wo part hota hai jo **user ko visible UI show karta hai**.  
Ye mainly **HTML + Razor syntax** se banta hai.  
👉 Basically ye **UI layer** hai MVC ka.

---

## 🎯 2️⃣ Razor kya karta hai?
**Razor ek templating engine** hai jo **C# code ko HTML me embed** karne deta hai.  
Syntax start hota hai **@** se.

```cshtml
<h2>Hello @Model.Name!</h2>
````

Ye HTML + C# ko mix karke dynamic page create karta hai.

---

## 🎯 3️⃣ ViewBag aur ViewData me fark?

| Feature  | ViewBag                  | ViewData                     |
| -------- | ------------------------ | ---------------------------- |
| Type     | Dynamic object           | Dictionary (key-value)       |
| Syntax   | `ViewBag.Name = "Wania"` | `ViewData["Name"] = "Wania"` |
| Usage    | Access directly          | Access by key                |
| Lifetime | Same request only        | Same request only            |

✅ Dono temporary data pass karte hain **Controller → View**.

---

## 🎯 4️⃣ @RenderBody aur @RenderSection difference?

| Concept            | Explanation                                                                                         |
| ------------------ | --------------------------------------------------------------------------------------------------- |
| **@RenderBody**    | Layout page ka main content area hota hai jahan individual page ka content inject hota hai.         |
| **@RenderSection** | Optional or named section hoti hai jisme specific content (like scripts ya sidebar) add karte hain. |

Example:

```cshtml
@RenderBody()
@RenderSection("scripts", required: false)
```

---

## 🎯 5️⃣ _Layout.cshtml ka role kya hai?

Ye **Master Page** jaisa hota hai — sab pages ke liye **common structure** define karta hai (header, footer, navbar etc).
Individual pages sirf apna unique content `RenderBody()` me daalte hain.

---

## 🎯 6️⃣ Partial View kya hai?

Partial view ek **reusable view component** hota hai jise hum kisi bhi page me include kar sakte hain (like small widgets, forms).

Example:

```cshtml
@Html.Partial("_LoginPartial")
```

It helps avoid code repetition.

---

## 🎯 7️⃣ _ViewStart aur _ViewImports kis liye use hote hain?

| File                    | Use                                                                                             |
| ----------------------- | ----------------------------------------------------------------------------------------------- |
| **_ViewStart.cshtml**   | Ye define karta hai kaunsa layout file use karni hai sab views ke liye.                         |
| **_ViewImports.cshtml** | Isme common namespaces aur tag helpers import kiye jaate hain (like `@using`, `@addTagHelper`). |

---

## 🎯 8️⃣ Tag Helpers kya hote hain?

Tag Helpers **HTML tags ko C# backend ke saath connect** karte hain.

Example:

```cshtml
<form asp-controller="Home" asp-action="Submit">
```

Ye code C# ke controller action ko directly bind karta hai — cleaner aur strongly typed approach deta hai.

---

## 🎯 9️⃣ View Lifecycle explain karo

Basic flow 👇
1️⃣ Request controller ko jaata hai.
2️⃣ Controller model prepare karta hai.
3️⃣ Controller View return karta hai (`return View(model);`)
4️⃣ Razor engine C# + HTML merge karta hai.
5️⃣ Final HTML browser ko render hota hai.

---

✨ **Summary:**

* View = User Interface
* Razor = Dynamic HTML generator
* ViewBag/ViewData = Temporary data pass
* Layout = Common design
* Partial View = Reusable component
* Tag Helpers = Smart HTML
* _ViewStart/_ViewImports = Global setup

---

```


