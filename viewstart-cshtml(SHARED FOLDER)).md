# 💡 `_ViewStart.cshtml` — Automatic Layout System Explained (Beginner Story Style)

---

## 🌍 Pehle Recap:

| File | Role |
|------|------|
| `_Layout.cshtml` | Master design (Navbar + Footer) |
| `@RenderBody()` | Jahan har page ka content show hota hai |

Lekin… har page me likhna padta tha:

```cshtml
@{
    Layout = "_Layout.cshtml";
}
````

😅 Bar-bar likhna boring aur time-waste hai!

---

## 💡 Solution: `_ViewStart.cshtml`

ASP.NET ne kaha 👇

> “Tum ek aisi **common file** bana lo jo sab pages ke liye **automatic layout set** kar de.”

Wo file hai 👉 **`_ViewStart.cshtml`**

---

## 📁 Location:

```
Views/
 ├── _ViewStart.cshtml
 ├── Shared/
 │     └── _Layout.cshtml
 ├── Home/
 │     └── Index.cshtml
 └── About/
       └── Index.cshtml
```

---

## 🧩 Example of `_ViewStart.cshtml`

```cshtml
@{
    Layout = "_Layout.cshtml";
}
```

💬 **Meaning:**

> “Mere project ke sab views (Home, About, Contact)
> automatically `_Layout.cshtml` layout use karenge.”

---

## ⚙️ Kaise Kaam Karta Hai (Step-by-Step):

1️⃣ Jab ASP.NET koi page (view) run karta hai —
wo sabse pehle `_ViewStart.cshtml` file check karta hai.

2️⃣ Usme likha hota hai `Layout = "_Layout.cshtml";`
→ to wo automatically layout set kar deta hai.

3️⃣ Ab har page me manually likhne ki zarurat **nahi** 🎉

---

## 💻 Example Without `_ViewStart.cshtml`

```cshtml
// Home/Index.cshtml
@{
   Layout = "_Layout.cshtml";
}
<h2>Home</h2>

// About/Index.cshtml
@{
   Layout = "_Layout.cshtml";
}
<h2>About</h2>
```

😩 Har page pe likhna padta hai…

---

## 💻 Example With `_ViewStart.cshtml`

```cshtml
// _ViewStart.cshtml
@{
   Layout = "_Layout.cshtml";
}

// Home/Index.cshtml
<h2>Home</h2>

// About/Index.cshtml
<h2>About</h2>
```

✅ Ab dono pages automatically `_Layout` use karenge — bina likhe!

---

## 🧠 Simple Words Me:

| File                | Kaam                                      | Example                   |
| ------------------- | ----------------------------------------- | ------------------------- |
| `_Layout.cshtml`    | Master template (Navbar + Footer)         | Common design             |
| `_ViewStart.cshtml` | Har page ke liye default layout set karna | Layout auto apply         |
| `@RenderBody()`     | Page ka content show karna                | “Yahan content dikhayein” |

---

## 🎯 Ek Line Me Yaad Rakhna:

> `_ViewStart.cshtml` bolta hai:
> “Mere project ke sab pages ek hi layout use karein, jab tak koi page kuch aur na bole.” 💬

---

✨ Ab tumhara **automatic layout system** concept 100% clear hai —
bas `_ViewStart.cshtml` ko ek “auto layout setting file” samjho 💎

```
```
