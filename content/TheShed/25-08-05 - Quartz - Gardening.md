---
date: 2025-08-06
aliases:
  - Quartz - Gardening
tags:
  - digitalgarden
summary: Guide to creating a digital garden using quartz, github with Cloudflare
type: note
status: published
---
# Complete Quartz Digital Garden Setup Guide

There is a very brilliant documentation site for [Quartz](https://quartz.jzhao.xyz/). You should run through this.

---

**My particular use case:** Despite having Obsidian Publish for two years, I wasn't really using it. I like to tinker, and I love the process of learning. Keen to stand up my own garden and tweak it as I go.

I have a large vault where I manage daily and weekly thoughts. Not everything needs to go out to the web - I only want to publish certain things.

My ecosystem: Windows PC, Windows laptop, and iPad. I use OneDrive to sync between the Windows devices, and FreeSync to copy selected content to iCloud when I use Obsidian on the iPad.

The approach outlined below was the steps I took to get the embryonic digital garden up to Cloudflare Pages via GitHub.

---

A comprehensive guide to setting up a Quartz-powered digital garden with Cloudflare Pages deployment:

## Prerequisites

- **Node.js v22** or higher with **npm v10.9.2+**
- **Git** installed and configured
- **GitHub account**
- **Cloudflare account** with domain management
- **Obsidian** (or any Markdown editor)

Check your versions:

```bash
node --version    # Should show v22+
npm --version     # Should show v10.9.2+
```

## Part 1: Quartz Installation & Setup

### Choose Your Location

**Recommended approach:** Use OneDrive (or similar cloud sync) so you can work from multiple devices:

```
C:\Users\[username]\OneDrive\Documents\your-garden-name\
```

### Clone Quartz First

1. **Create and navigate to your folder:**
    
    ```bash
    mkdir "C:\Users\[username]\OneDrive\Documents\your-garden-name"
    cd "C:\Users\[username]\OneDrive\Documents\your-garden-name"
    ```
    
2. **Clone Quartz directly into your folder:**
    
    ```bash
    git clone https://github.com/jackyzha0/quartz.git .
    ```
    
    **Note:** The `.` at the end clones into the current directory.
    
3. **Install dependencies:**
    
    ```bash
    npm install
    ```
    

### Quartz Creates This Structure For You:

```
your-garden/
├── content/              # ← Your posts go here
│   └── .gitkeep         # placeholder file
├── quartz.config.ts     # Configuration
├── package.json         # Dependencies list
├── node_modules/        # Tools (excluded from Git)
└── ... other Quartz files
```

## Part 2: Add Your Content

### Option A: Copy from Existing Vault

**If you have a large Obsidian vault** (like I do), you can selectively copy content:

1. **Delete the placeholder:**
    
    ```bash
    del content\.gitkeep
    ```
    
2. **Copy content manually** or use **FreeFileSync** to copy specific folders:
    
    ```
    Source: C:\Your\Large\Vault\PublicContent\
    Target: C:\Your\Garden\content\
    ```
    

### Option B: Create Content Fresh

**If starting from scratch**, you might want to create an Obsidian vault in the same folder to take advantage of Obsidian's linking and editing features while writing directly in the `content/` folder.

**Hybrid approach:** You can also do both - copy some existing content from your main vault and create fresh content directly in the garden.

Create these essential pieces in the `content/` folder:

- **About page** (`content/about/index.md`)
- **First blog post** (`content/blog/2025-08-05-your-first-post.md`)
- **Home page** (`content/index.md`)

### Content Structure Within the content/ Folder:

```
content/
├── about/
│   └── index.md
├── blog/
│   └── 2025-08-05-your-first-post.md
├── kitchen/    # or your own categories
├── study/
└── assets/
```

**Using FreeFileSync tip:** Set up a sync relationship between your main vault's public content and the Quartz `content/` folder. This lets you write in your main vault and automatically sync to your digital garden.

### Frontmatter Format

**Suggested basic frontmatter for a post** (suspect I'll revisit this later):

```yaml
---
aliases:
  - Short Name
  - Alternative Name
date: 2025-08-05
status: published
---
# Your Post Title

Your content here...
```

### Test Local Build

```bash
# Build and serve locally
npx quartz build --serve
```

Visit `http://localhost:8080` to preview your site.

## Part 3: Git Repository Setup

> [!info] Git is a source code repository system that tracks changes to your files. We'll use GitHub to store our digital garden files, and Cloudflare Pages has a built-in process to automatically pick up files from there - it acts as a bridge between your content and your live website.

### Create a GitHub Repository

1. **Go to GitHub.com** → **New repository**
2. **Settings:**
    - Name: `your-garden-name`
    - Visibility: **Public** (required for free Cloudflare Pages)
    - **Don't initialize** with README/gitignore

### Initialise the Git Repository

1. **Using a notebook, or text editor....verify .gitignore excludes the right files:**
    
    The `.gitignore` file tells Git which files to ignore and never include in the repository. Quartz comes with a good default, but we've added a couple of extras:
    
    ```
    node_modules/        # JavaScript dependencies (recreated by npm install)
    sync.ffs_db          # FreeFileSync database files (personal sync settings)
    .obsidian/           # Obsidian settings (personal workspace configuration)
    .DS_Store            # macOS system files
    Thumbs.db            # Windows thumbnail cache
    *.tmp                # Temporary files
    public/              # Build output (recreated by Quartz build)
    .quartz-cache/       # Quartz cache files
    ```
    
2. **Check your Git remote connection - I found my folder was still connected to the Quartz branch v4 and needed to point to my newly created repository.**
    
    ```bash
    git remote -v
    ```
    
    **If it shows `jackyzha0/quartz.git`, change it to your repository:**
    
    ```bash
    git remote set-url origin https://github.com/[username]/your-garden-name.git
    ```
    
3. **Check and rename your branch (Quartz uses v4, we want main):**
    
    ```bash
    git branch
    git branch -m main  # if currently on v4
    ```
    
4. **Add and commit your changes:**
    
    ```bash
    git add .
    git commit -m "Initial commit - Quartz digital garden"
    ```
    
5. **Connect and push:**
    
    ```bash
    git remote add origin https://github.com/[username]/your-garden-name.git
    git push -u origin main
    ```
    

**Important:** The push may take 10-15 minutes due to the number of files.

> [!info] **My experience:** First attempt without the Quartz files was near instant, but with the proper Quartz files, my first attempt failed, 2nd attempt got stuck at 94% for some time. I'd allow 20 minutes for the first push.

## Part 4: Cloudflare Pages Deployment

> [!info] Cloudflare Pages is a hosting service that automatically builds and serves your website. When you push changes to GitHub, Cloudflare detects them, runs the Quartz build process (`npx quartz build`), and publishes the resulting website to their global network. This means your digital garden is fast-loading worldwide and updates automatically whenever you commit new content.

### Find Cloudflare Pages

**Create Cloudflare account** if you don't have one already. For my use case, I already had a domain managed in Cloudflare, but didn't know how to use Pages or how to find them in the dashboard.

**Locating Pages in Cloudflare:**

- **Cloudflare Dashboard** → **Workers & Pages** (under "Compute (Workers)")
- **Click Pages tab** → **"Import an existing Git repository"**

### Configure Build Settings

**Project settings:**

- **Project name:** Your preference
- **Production branch:** `main`
- **Framework preset:** "None" or "Other"
- **Build command:** `npx quartz build`
- **Build output directory:** `public`
- **Root directory:** Leave blank

### Deploy

1. **Click "Save and Deploy"**
    
2. **Wait for build** (advised 2-5 minutes)
    
3. **Initial SSL might fail** - this is normal
    

> [!info] **Note:** My first attempt without the Quartz files was near instant, and it bombed...so had to go through the above lifecycle. I've tried to write the above lifecycle in a way you wouldn't experience this. 2nd attempt it was in a fankle looking for my original repository, which I'd deleted and started again. Hopefully it works on first attempt if my notes are good. In this case the build was pretty quick...but the output link failed due to not having a certificate. I gave up waiting and just assigned a domain that did have a certificate and it worked straight away.

## Part 5: Domain Configuration

### Option A: Use .pages.dev Domain

- **Wait 15-30 minutes** for SSL certificate provisioning
- **Your site:** `https://your-project-name.pages.dev`

### Option B: Custom Domain (Recommended)

1. **Cloudflare Pages project** → **Custom domains**
2. **Add your domain:** `yourdomain.com`
3. **Follow DNS instructions** (usually automatic if domain is already in Cloudflare)
4. **SSL works immediately** with existing Cloudflare domain

---

At time of writing, I'd purely got 3 markdown files up and running which is the above I hope to cover:
- [[Writing and Refresh Process]] 
- [[Customisation]]
- [[25-08-04 - Inner Struggle of a public repository]]

# Troubleshooting

### Common Issues

**"npm error could not determine executable to run":**

- Missing `node_modules` - run `npm install`
- Repository only has content, missing Quartz build files

**If you mess up the Git setup (like I did initially):**

- First iteration I hadn't included the Quartz files (my personal assistant said I didn't need them, gave me the impression Cloudflare would have this covered), only content
- Had to start over a couple of times to get it right, even going nuclear - and pulling a Kenny Loggins by going to the danger zone and deleting the repository
- The repository needs to be PUBLIC for free cloudfare pages (see [[25-08-04 - Inner Struggle of a public repository]])

**To reset and start fresh as an option not to delete:**

```bash
Remove-Item -Recurse -Force .git
git init
git add .
git commit -m "Initial commit - Quartz digital garden"
git branch -M main
```

- Cancel and retry deployment
- Check GitHub permissions: "The repository cannot be accessed. Configure installation."
- Delete and recreate GitHub repository if permissions broken

**Build stuck in queue for hours:**

- Wait 15-30 minutes for provisioning
- Try custom domain if available (often faster)
- Browser auto-redirects to HTTPS even when certificate isn't ready

**Large push taking forever (11,590+ files):**

- Ensure `node_modules/` is in `.gitignore`
- Force push with `-f` flag if repository content needs complete replacement

**Git remote errors:**

- `error: remote origin already exists` - use `git remote set-url origin [URL]`
- `error: src refspec main does not match any` - make a commit first, or push to correct branch (`v4` vs `main`)
- Check current branch with `git branch` - might be on `v4` instead of `main`

**Repository pointing to wrong location:**

- `git remote -v` shows `jackyzha0/quartz.git` instead of your repo
- Use `git remote set-url origin https://github.com/[username]/[repo].git`

**Connection failures during push:**

- `RPC failed; curl 55 Recv failure: Connection was reset`
- Often happens with large pushes, but may succeed despite error message
- Check GitHub repository to verify if push actually completed

**Cloudflare Pages can't find "Pages" option:**

- Look under "Compute (Workers)" → "Pages" tab
- Not in individual domain settings, must be at account level
- Direct URL: `https://dash.cloudflare.com/pages` (may 404 if not available on account)

# Benefits of This Setup

- ✅ **Write anywhere** (if using OneDrive sync) - Not Post Anywhere
- ✅ **Automatic deployment** (commit triggers rebuild)
- ✅ **Version control** (full Git history)
- ✅ **Fast global CDN** (Cloudflare network)
- ✅ **Digital garden features** (backlinks, graph view, search)
- ✅ **Custom domain support**
- ✅ **Free hosting** (GitHub + Cloudflare free tiers)

## Alternative: GitHub Pages

For simpler setup, GitHub Pages works too:

1. **GitHub repository** → **Settings** → **Pages**
2. **Source:** Deploy from branch `main`
3. **Configure custom domain** in settings
4. **Same workflow**, slightly slower performance

## Final Notes

- **First setup is complex** - adding content afterwards is simple
- **Content is just Markdown** - easily portable to other systems
- **Quartz updates:** Occasionally merge upstream changes
- **Backup strategy:** Content lives in Git + local files

> [!note] My hope is that the initial setup investment will pay off with a powerful, fast, and flexible digital garden that grows with my needs.