# Console Repair Bench

A website for keeping track of the consoles on the repair bench: tag (SP-001), photos, problem, and which parts each one still needs.

- **The website** lives on GitHub Pages (free).
- **The list and photos** live in Supabase (free).
- Only the emails you put in `setup.sql` can sign in and see anything.

Setup takes about 15 minutes. You only do it once.

---

## Part 1: Supabase (the database and photos)

1. Go to **supabase.com**, sign up (free), and press **New project**.
   - Name: `repair-bench`
   - Database password: pick one and save it somewhere (you won't need it day to day).
   - Region: pick one in Europe close to you.
   - Wait a minute or two while it gets ready.

2. In the left menu open **SQL Editor** and start a new query.
   - Open `setup.sql` from this folder and copy everything into the editor.
   - Near the top, replace the two example emails with **your email** and the **dkretro owner's email**.
   - Press **Run**. It should say "Success".

3. In the left menu open **Authentication → Users** and press **Add user → Create new user**.
   - Enter your email and a password. Tick **Auto Confirm User**.
   - Do the same for the dkretro owner's email.
   - These are the logins you'll use on the website.

4. Still in **Authentication**, find the setting **Allow new users to sign up** and turn it **off**.
   (Strangers already can't see anything because of the email list, but this keeps it tidy.)

5. Open **Project Settings → API** (may be called **API Keys**). Copy two things:
   - **Project URL** (looks like `https://abcdefghijkl.supabase.co`)
   - The **anon public** key, or the **publishable** key (starts with `sb_publishable_`).

   Open `config.js` in a text editor (Notepad is fine) and paste them between the quotes. Save.

## Part 2: GitHub (the website)

1. Go to **github.com**, press **+ → New repository**.
   - Name: `repair-bench`
   - Public
   - Press **Create repository**.

2. On the new repository page click **uploading an existing file**.
   Drag in **index.html**, **config.js** and **README.md**, then press **Commit changes**.
   (Leave `setup.sql` out. It has your emails in it.)

3. Open the repository's **Settings → Pages**.
   - Source: **Deploy from a branch**
   - Branch: **main**, folder **/ (root)** → **Save**

4. Wait a minute, then open:
   **https://YOUR-GITHUB-NAME.github.io/repair-bench/**

Send that link to the dkretro owner with the password you made for him. It works on phones too.

---

## Good to know

- **Free plan limits:** about 1 GB of photos (photos are shrunk on upload, so that's a few thousand), and the free project **goes to sleep after a week with nobody using it**. If the site suddenly can't load the list, log in to supabase.com and press **Restore** on the project.
- **Add another person later:** in SQL Editor run
  `insert into public.allowed_users (email) values ('their@email.com');`
  then create a user for them in Authentication → Users.
- **iPhone photos won't upload?** Settings › Camera › Formats › **Most Compatible**.
- The key in `config.js` is meant to be public. Your data is protected by the email list, not by hiding the key.
