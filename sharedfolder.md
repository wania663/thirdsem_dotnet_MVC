# 💡 Shared Folder — Simple Explanation

---

## 📁 Location

```

Views/
├── Home/
├── User/
└── Shared/   👈 ye folder sab pages ke liye common hota hai

````

Agar tumhare paas 10 pages hain aur har page pe same **navbar**, **footer**, aur **CSS links** lagani ho,  
to kya tum har file me likhogi?  
❌ Nahi — bohot time waste hoga.

👉 Isi problem ko solve karta hai **Shared folder** ✅

---

## 🔹 1. `_Layout.cshtml` → “Master Template Page”

Soch lo ye **main design frame** hota hai — jaise ek template jisme **navbar**, **footer**, aur **main CSS/scripts** hoti hain.  
Har page isi layout ke andar render hota hai.

### 📘 Example:
```html
<!DOCTYPE html>
<html>
<head>
    <title>@ViewData["Title"] - MyApp</title>
    <link rel="stylesheet" href="~/css/site.css" />
</head>
<body>
    <header>
        <h1>🚀 My Website Navbar</h1>
        <nav>
            <a href="/Home/Index">Home</a> |
            <a href="/User/Index">Users</a>
        </nav>
    </header>

    <!-- Yahan page ka content load hota -->
    <main>
        @RenderBody()
    </main>

    <footer>
        <p>© 2025 My Website</p>
    </footer>
</body>
</html>
````

### 📌 `@RenderBody()`

👉 Ye jagah hai jahan tumhara page ka actual content inject hota hai
(e.g. `Home/Index.cshtml` ka content)

So har new page automatically isi layout me appear karega ✅

---

## 🔹 2. `_ViewStart.cshtml` → “Default Layout Set Karne Wali File”

Ye file har page ke liye **default layout** set karti hai.
Taki tumhe har `cshtml` file me manually layout likhne ki zarurat na pade.

### 📘 Example:

```csharp
@{
    Layout = "_Layout.cshtml";
}
```

### 💬 Matlab:

> Har view yehi layout use karega — jab tak manually kuch aur layout na diya jaye.

✅ **Benefit:** Har page automatically master layout use karega.

---

## 🔹 3. `_ViewImports.cshtml` → “Common Imports Wali File”

Ye file ek tarah se **shortcut** hai —
isme tum **common namespaces** aur **Razor TagHelpers** likh sakti ho jo sab views me automatically apply honge.

### 📘 Example:

```csharp
@using MyApp.Models
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```

### 💬 Matlab:

> Ab tumhe har page me `@using MyApp.Models` likhne ki zarurat nahi — sab me auto apply ho jayega.

✅ **Benefit:** Less repetition, cleaner code.

---

## 🔹 4. `_ValidationScriptsPartial.cshtml` → “Form Validation JS Include Wali File”

Ye chhoti file hoti hai jisme **client-side validation scripts (JavaScript/jQuery)** hoti hain —
form validation ke liye (like required fields, email format check, etc.)

### 📘 Example:

```html
<script src="~/lib/jquery-validation/dist/jquery.validate.min.js"></script>
<script src="~/lib/jquery-validation-unobtrusive/jquery.validate.unobtrusive.min.js"></script>
```

Aur jab tum form ke neeche ye likhti ho:

```html
<partial name="_ValidationScriptsPartial" />
```

To ye file validation JS automatically add kar deti hai 💥

---

## ⚙️ Simple Real-Life Analogy

| File Name                          | Role                     | Real Life Example                                                 |
| ---------------------------------- | ------------------------ | ----------------------------------------------------------------- |
| `_Layout.cshtml`                   | Master design            | Jaise ek template jisme navbar/footer fix ho                      |
| `_ViewStart.cshtml`                | Layout auto attach karta | Jaise ek setting file jo sab pages pe same theme apply kare       |
| `_ViewImports.cshtml`              | Common imports rakhta    | Jaise ek “global shortcut” jahan se sab files ko access milti hai |
| `_ValidationScriptsPartial.cshtml` | Validation JS rakhta     | Jaise form filling ke time red error show karne wale scripts      |

---

✅ **Summary:**
Shared folder ek “common resources” folder hai jahan tum repeat hone wale design aur code ko ek hi jagah likh sakti ho —
aur har view file automatically usko use kar leti hai.

```
```
