# Orbit icons

Cobalt `#2C47D4` tile, white orbit ring tilted -24 degrees, a planet in the middle and one satellite.

## Web (`web/`)

| File | Use |
| --- | --- |
| `favicon.ico` | 16, 32 and 48 px in one file, for old browsers and `/favicon.ico` requests |
| `favicon.svg` | Modern browsers; scales to any size |
| `favicon-small.svg`, `favicon-16/32/48.png` | Thicker ring and bigger dots so the mark survives at tab size |
| `apple-touch-icon.png` | 180 px, square and opaque (iOS rounds the corners) |
| `icon-192.png`, `icon-512.png` | PWA / Android Chrome |
| `icon-maskable-512.png` | PWA maskable icon (mark inside the safe zone) |
| `site.webmanifest` | References the three PWA icons |

```html
<link rel="icon" href="/favicon.ico" sizes="48x48">
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
<link rel="manifest" href="/site.webmanifest">
<meta name="theme-color" content="#2C47D4">
```

**Next.js (the Orbit web app):** put `favicon.ico` in `app/`, keep `app/icon.svg`, and copy `apple-touch-icon.png` to `app/apple-icon.png`. Next adds the tags for you.
**Download page:** copy everything in `web/` to the site root and paste the tags above into `<head>`.

## Android (`android/`)

Copy `android/res/` over `app/src/main/res/` in your Android project (it merges by folder).

- `mipmap-anydpi-v26/ic_launcher.xml` and `ic_launcher_round.xml`: adaptive icon for Android 8+ with a cobalt background, the white mark as foreground and a `monochrome` layer for Android 13+ themed icons.
- `drawable/ic_launcher_foreground.xml`, `ic_launcher_monochrome.xml`: vector layers on the 108 dp canvas. The mark stays inside the 66 dp safe zone, so circle, squircle and rounded-square masks never clip it.
- `values/ic_launcher_background.xml`: the background colour.
- `mipmap-mdpi` … `mipmap-xxxhdpi`: 48 / 72 / 96 / 144 / 192 px PNGs for Android 7 and older.
- `play-store-icon-512.png`: upload in Play Console → Main store listing → App icon. It's full-bleed on purpose; Google Play applies the rounded mask.
- `source/`: SVG and 432 px PNG layers, if you'd rather import through Android Studio's Image Asset tool.

In `AndroidManifest.xml`:

```xml
<application
    android:icon="@mipmap/ic_launcher"
    android:roundIcon="@mipmap/ic_launcher_round" ... >
```

If you build with Expo or React Native, use `android/source/adaptive-foreground-432.png` as `adaptiveIcon.foregroundImage`, `adaptive-monochrome-432.png` as `monochromeImage`, and `#2C47D4` as `backgroundColor`.
