# Frontlines — play on your phone with GitHub Pages

This package is the ready-to-host game. No installation, Node.js, API key, or build is needed on GitHub or on your phone.

## Upload and publish

1. Extract **frontlines-github-pages.zip** on your computer. Upload the **extracted contents**, not the ZIP itself.
2. Create an empty **public** GitHub repository, for example `frontlines`.
3. Choose **Add file → Upload files**. Drag all extracted files and the `assets` and `data` folders into the upload area, then commit the upload. Include `.nojekyll` if your file picker hides it. The repository's top level must contain `index.html`, `assets/`, and `data/`; do not place them inside another folder.
4. Open **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**, select **main** and **/(root)**, then **Save**.
5. Wait for GitHub to show the published website link. Open that **HTTPS website link** on your phone. A typical project address is `https://YOUR-USERNAME.github.io/frontlines/`.

The computer does not need to stay on after publication. Internet is needed to load the website. Use a recent phone browser with WebGL support. Physical phone hardware has not been certified; desktop Chromium and Pixel 7 touch emulation are checked locally at a repository-style path.

This ZIP is a compiled website, not an APK. Opening `index.html` directly from your phone's file manager will not run the game correctly; use the GitHub Pages link.

## Quick play

- Open **اختيار دولتي والمضائق**, choose a country, and confirm.
- Use **القوات والمعارك** for armies, fortified bases, swarms and occupation; **الدبلوماسية** for visits and agreements.
- Confirm orders, then press ▶ to advance the simulation.
- Saves stay in that browser's local storage. To move progress from your computer to your phone, export a save from **Archive** and import it on the phone. Hosting does not synchronize saves across devices.

## بالعربي

فك ضغط الملف أولاً وارفع محتوياته إلى مستودع GitHub عام. يجب أن تكون `index.html` ومجلدات `assets` و`data` في المستوى الأول، لا داخل مجلد إضافي. بعدها افتح **Settings → Pages** واختر **Deploy from a branch → main → /(root) → Save**. افتح رابط الموقع الذي يظهر على هاتفك. رفع ملف ZIP وحده لا ينشر اللعبة، وفتح ملف HTML من مدير الملفات لا يكفي. الحفظ محلي لكل متصفح؛ استخدم التصدير والاستيراد لنقل تقدمك.

## About this game

All forces, deployments, military capabilities, strengths, campaigns and combat outcomes are fictional game rules. Geographic references use the pinned Natural Earth source pack. Data attribution and license are included in `data/LICENSE.txt`, `data/manifest.json`, and the provenance files. Public base references retain their source links inside the game.

The package contains browser-ready JavaScript, styles, two workers, map data and its licenses. It excludes local saves, dependencies, caches, test artifacts and private files. Editable source remains in the original development project.

Official GitHub instructions:

- [Upload files](https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository)
- [Configure GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
