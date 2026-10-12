# How To Publish This Website (And Put It On Your Own Domain)

This guide takes the site from "a folder of files" to "a public website at your own address". It is a one-time setup. Plan on about 20 minutes, plus waiting time for the domain (from a few minutes up to 24 hours).

Once it's set up, every change pushed to the repository rebuilds and republishes the site automatically. See `EDITING.md` for day-to-day updates.

How it works: GitHub stores the files, and a GitHub Action (`.github/workflows/deploy.yml`) builds the site and puts the result on a branch called `gh-pages`. GitHub Pages then serves that branch to the world for free.

---

## Part 1: Decide The Web Address

Pick **one** of these three options before uploading anything. Then set the two lines near the top of `_config.yml` to match.

| Option                                 | Repository name                             | Site address                       | `url:` in `_config.yml`           | `baseurl:` |
| -------------------------------------- | ------------------------------------------- | ---------------------------------- | --------------------------------- | ---------- |
| **A. Your own domain** (recommended)   | anything, e.g. `website`                    | `https://www.example.com`          | `https://www.example.com`         | _(empty)_  |
| **B. Free GitHub address**             | exactly `USERNAME.github.io`                | `https://USERNAME.github.io`       | `https://USERNAME.github.io`      | _(empty)_  |
| **C. Free GitHub address, any name**   | anything, e.g. `website`                    | `https://USERNAME.github.io/website` | `https://USERNAME.github.io`    | `/website` |

`USERNAME` is the GitHub account name. Option B is the easiest way to start: you can add a custom domain later (Part 4) without moving anything.

For option A, also do step 4.3 below (the `CNAME` file) **before** uploading.

> This site is set up with option B: account `nbellomo`, repository `nbellomo.github.io`, address `https://nbellomo.github.io`. `_config.yml` already matches.

---

## Part 2: Put The Files On GitHub

1. Sign in to the GitHub account that will own the site.
2. Click **+** (top right) → **New repository**.
   - Name: as chosen in Part 1.
   - Visibility: **Public**. Free GitHub Pages requires a public repository.
   - Do **not** tick "Add a README", ".gitignore" or "license". The repository must start empty.
   - Click **Create repository**.
3. Upload the files. Use one of these two methods.

### Method 1: Command line (recommended)

This folder is already a git repository with one commit. From inside the folder, run:

```bash
git remote add origin https://github.com/USERNAME/REPOSITORY.git
git push -u origin main
```

Pushing requires being logged in as the new account, or as a collaborator on it. If someone else is doing the upload, the account owner first adds them under **Settings → Collaborators → Add people**, and they accept the email invitation.

If `git push` answers `403` / "Permission denied", git is using a different saved GitHub login. The simplest fix is **GitHub Desktop**: sign in as the right account, then **File → Add local repository** (pick this folder), **Publish / Push**.

### Method 2: Web upload (no git needed)

On the empty repository page, click **"uploading an existing file"** and drag in the contents of this folder.

- **Hidden folders matter.** The `.github` folder holds the publishing robot and **must** be uploaded. On a Mac, press **Cmd + Shift + .** in Finder to show hidden files before dragging.
- **Skip the `.git` folder.** Don't upload it.
- **Big uploads may fail.** The web uploader handles about 100 files at a time, so upload folder by folder if needed.

After uploading, check that `.github/workflows/deploy.yml` appears in the repository.

---

## Part 3: Turn The Website On

1. Open the repository's **Actions** tab.
   - If GitHub asks to enable workflows, click the green button.
   - A run called **"Deploy site"** starts automatically after each upload. Wait until it shows a green ✓ (about 2–3 minutes).
   - If nothing is running, click **Deploy site** in the left list → **Run workflow** → **Run workflow**.
2. When it's green, a new branch called `gh-pages` exists. This is the built website.
3. Go to **Settings → Pages**. Under **Build and deployment**:
   - **Source:** _Deploy from a branch_
   - **Branch:** `gh-pages`, folder `/ (root)` → **Save**
4. Wait a minute and refresh. The top of the page shows **"Your site is live at …"**. Click it.

The site is now public. With option B or C you're done; Part 4 is only for a custom domain.

---

## Part 4: Use Your Own Domain (e.g. `www.nicolabellomo.com`)

### 4.1 Buy the domain

Buy the domain from any registrar (Cloudflare, Porkbun, Namecheap, Gandi, Aruba, OVH, …). Expect about 10–20 €/year for `.com`, `.it`, `.eu` and similar. You don't need hosting, email or website-builder add-ons. GitHub hosts the site for free.

### 4.2 Point the domain at GitHub (DNS records)

In the registrar's control panel, find **DNS settings** / **DNS records** and add these records. First delete any existing "parking" `A`, `AAAA` or `CNAME` records for `@` and `www`.

| Type    | Host / Name | Value                   |
| ------- | ----------- | ----------------------- |
| `A`     | `@`         | `185.199.108.153`       |
| `A`     | `@`         | `185.199.109.153`       |
| `A`     | `@`         | `185.199.110.153`       |
| `A`     | `@`         | `185.199.111.153`       |
| `AAAA`  | `@`         | `2606:50c0:8000::153`   |
| `AAAA`  | `@`         | `2606:50c0:8001::153`   |
| `AAAA`  | `@`         | `2606:50c0:8002::153`   |
| `AAAA`  | `@`         | `2606:50c0:8003::153`   |
| `CNAME` | `www`       | `USERNAME.github.io`    |

(`@` means "the bare domain", e.g. `nicolabellomo.com`. Some registrars want it left blank instead.)

With these records, both `nicolabellomo.com` and `www.nicolabellomo.com` work; GitHub redirects one to the other.

### 4.3 Tell the website its new address

In the repository (pencil icon to edit on GitHub, or locally):

1. **Create a file named exactly `CNAME`** (capital letters, no extension) in the top folder. It holds a single line with the domain:

   ```
   www.nicolabellomo.com
   ```

2. **Edit `_config.yml`:** set `url: https://www.nicolabellomo.com` and leave `baseurl:` empty.
3. Commit / save. The "Deploy site" action runs again.

> **Why the `CNAME` file is required:** the publishing robot rebuilds the `gh-pages` branch from scratch on every update. If the domain is only typed into Settings (step 4.4), GitHub stores it on that branch, and the next update erases it. The site then quietly falls back to the `github.io` address. A `CNAME` file in the repository survives every rebuild.

### 4.4 Connect the domain in GitHub

1. **Settings → Pages → Custom domain:** type `www.nicolabellomo.com` → **Save**.
2. GitHub runs a "DNS check". It may say _unsuccessful_ for a while; new DNS records can take from minutes to 24 hours to spread.
3. When the check passes, tick **Enforce HTTPS**. If the box is greyed out, GitHub is still issuing the free security certificate; come back in an hour.

### 4.5 (Recommended) Verify the domain

This stops anyone else from claiming the domain on GitHub if the site is ever switched off.

1. Click the profile picture → **Settings → Pages** (the _account_ settings, not the repository's) → **Add a domain**.
2. Enter `nicolabellomo.com`. GitHub shows a `TXT` record to add at the registrar.
3. Add it, wait a few minutes, click **Verify**.

---

## Part 5: Before Telling Anyone About It

The site still contains a few placeholders, all marked **PROXY** in the files: the email address, CV details, office address and research card images. The list is at the bottom of `EDITING.md`. To find every one, use GitHub's search box inside the repository and search for `PROXY`.

---

## Troubleshooting

| Symptom | Fix |
| --- | --- |
| **"Deploy site" has a red ✗** | Click it → click the failed step to read the error. If it says `Permission denied` / `403` while pushing to `gh-pages`: **Settings → Actions → General → Workflow permissions** → _Read and write permissions_ → Save, then re-run. |
| **Site shows a 404 page** | Wait 2 minutes and hard-refresh. Check that **Settings → Pages** points to branch `gh-pages`, `/ (root)`. |
| **Site appears but has no styling, or links are broken** | `url` / `baseurl` in `_config.yml` don't match the real address. Recheck the table in Part 1. |
| **Custom domain stopped working after an update** | The `CNAME` file is missing from the repository (see 4.3). |
| **"DNS check unsuccessful" for more than a day** | Re-check the records in 4.2 for typos and leftover parking records. Online checkers such as dnschecker.org show what the world currently sees. |
| **Publications list is empty** | That list is loaded live from INSPIRE-HEP when someone opens the page. If INSPIRE is down, it fills in again once INSPIRE is back. Nothing needs fixing on the site. |

## Previewing Locally (Optional)

To see changes before publishing, on a computer with Ruby 3.3+ installed:

```bash
bundle install
bundle exec jekyll serve
```

Then open <http://localhost:4000>. Responsive image variants need ImageMagick (`brew install imagemagick`). Without it, a few pictures may not show in the local preview, but they work on the published site.
