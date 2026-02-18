

# Smart Bookmark App

A simple bookmark manager where users can **save, view, and delete bookmarks**. Bookmarks are **private for each user** and updates happen **instantly across multiple tabs** using Supabase Realtime.

---

## 🔹 Live Demo

[Book Mark Task Live](https://book-mark-task.vercel.app)

---

## 🔹 Features

* **Google OAuth Login** – Login using Google account only
* **Add bookmarks** – Store URL + title
* **Delete bookmarks** – Remove bookmarks anytime
* **Private bookmarks** – Users can only see their own bookmarks
* **Realtime updates** – Changes are instantly reflected in all open tabs
* **Responsive UI** – Works on desktop, tablet, and mobile

---

## 🔹 Tech Stack

* **Frontend:** Next.js 16 (App Router) + React + Tailwind CSS
* **Backend / Database:** Supabase (Auth, Database, Realtime)
* **Hosting / Deployment:** Vercel

---

## 🔹 Installation

1. Clone the repo:

```bash
git clone https://github.com/<your-username>/smart-bookmark-app.git
cd smart-bookmark-app
```

2. Install dependencies:

```bash
npm install
```

3. Create `.env.local` in the root folder and add your Supabase keys:

```env
NEXT_PUBLIC_SUPABASE_URL=https://<your-project-id>.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=<your-anon-key>
```

4. Run the project locally:

```bash
npm run dev
```

* Open `http://localhost:3000` to see the app

---

## 🔹 Database Setup

Run the following SQL in Supabase SQL editor to create the table and policies:

```sql
create table bookmarks (
  id uuid default uuid_generate_v4() primary key,
  user_id uuid references auth.users not null,
  title text not null,
  url text not null,
  created_at timestamp default now()
);

alter table bookmarks enable row level security;

create policy "Users can view own bookmarks"
on bookmarks
for select
using (auth.uid() = user_id);

create policy "Users can insert own bookmarks"
on bookmarks
for insert
with check (auth.uid() = user_id);

create policy "Users can delete own bookmarks"
on bookmarks
for delete
using (auth.uid() = user_id);

ALTER TABLE bookmarks REPLICA IDENTITY FULL;
```

---

## 🔹 How Realtime Works

* Supabase Realtime tracks **insert, update, delete** events in the `bookmarks` table.
* Each tab subscribes to changes **for the logged-in user only**.
* When a bookmark is added or deleted, all open tabs **update instantly** without refreshing.

---

## 🔹 Deployment

* Deployed on **Vercel**: [Live Demo](https://book-mark-task.vercel.app)
* Make sure **Supabase redirect URL** is set to `https://<your-vercel-domain>/dashboard` for Google OAuth.

---

## 🔹 Notes for Interview

* **RLS (Row Level Security):** Ensures users only access their own bookmarks
* **Realtime:** Provides instant updates across tabs
* **Privacy-first design:** Each bookmark is tied to a user ID
* **Frontend UX:** Responsive, clean design using Tailwind CSS

> You can demo by opening **two tabs**, logging in with the same account, and adding or deleting bookmarks. Changes appear instantly in both tabs.

---

## 🔹 Screenshots

![Dashboard Screenshot](./public/screenshot-dashboard.png)
*Replace with your own screenshot if needed*

---

## 🔹 Author

**Janardhan Naik**

* Email: [naikjanardhan568@gmail.com](mailto:naikjanardhan568@gmail.com)
* GitHub: [janardhan-naik](https://github.com/janardhan-naik)

---

Do you want me to also **make a shorter “one-page version”** of this README that’s perfect for **copy-pasting directly in Google Docs for interview submission**? It will be very clean and concise.
