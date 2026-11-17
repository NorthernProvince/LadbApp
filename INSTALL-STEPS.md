# Lavevars Lodge: make it an app with no URL bar

## 1. Edit index.html

**A. In `<head>`, right after the `<title>` line, add:**

```html
<link rel="manifest" href="manifest.webmanifest">
<meta name="theme-color" content="#0A3032">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="Lavevars">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<link rel="apple-touch-icon" href="icon-192.png">
```

**B. Replace the existing `<meta name="viewport" ...>` line with:**

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
```

**C. At the end of the `<style>` block (just before `</style>`), add:**

```css
body{padding-top:env(safe-area-inset-top);padding-bottom:env(safe-area-inset-bottom)}
.sidebar{padding-top:calc(24px + env(safe-area-inset-top))}
@media (display-mode: standalone){body{-webkit-user-select:none;user-select:none}input,select{-webkit-user-select:text;user-select:text}}
```

**D. In the script, inside the `DOMContentLoaded` handler, add this line at the end:**

```js
if('serviceWorker' in navigator)navigator.serviceWorker.register('sw.js').catch(()=>{});
```

## 2. Make two icons from your logo
From `LadyB logo.jpeg`, export square PNGs named exactly:
- `icon-192.png` (192 x 192)
- `icon-512.png` (512 x 512)

Put them in the same folder as index.html, manifest.webmanifest and sw.js.

## 3. Host the folder over HTTPS
Installable apps require HTTPS. Free options: GitHub Pages, Netlify, Cloudflare Pages, Vercel.
Upload these files together: index.html, manifest.webmanifest, sw.js, icon-192.png, icon-512.png, LadyB logo.jpeg

## 4. Install it
- **Android (Chrome):** open the site, menu (3 dots), **Install app**.
- **iPhone (Safari):** Share button, **Add to Home Screen**.
- **Windows/Mac (Chrome/Edge):** click the install icon at the right of the address bar.

The app now opens from its own icon, full screen, with no URL.
