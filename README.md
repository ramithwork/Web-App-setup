# Web App setup
Make the web app look and feel like a native app.

## Versioning
1.0.3 - Pico CSS Integration.
1.0.2 - A working UI is completed. Not tested on a phone with an actual notch but loos good on my iPhone SE. Some important PWA head tags and CSS might be missing but it won't affect my purpose so far. Pico CSS haven't been added.
1.0.1 - Basics done.
1.0.0 - Initialisation.

## Steps
1. Add picocss.
2. In the root folder (where index.html is) create "site.webmanifest" file and add 
    {
      "display": "standalone"
    }
3. Link to index.html:
    <link rel="manifest" href="site.webmanifest">
4. Add Short Name to manifest:
    "short_name": "Web App"
5. Icon & Splash Screen
    Use PWA Asset Generator (https://github.com/elegantapp/pwa-asset-generator)
    1. $ npm install pwa-asset-generator
    2. Basic One-off exec:
        $ npx pwa-asset-generator [source-file] [output-folder]
    3. Recommended:
        npx pwa-asset-generator src/assets/setting-svgrepo-com.svg src -m src/site.webmanifest --padding "calc(50vh - 25%) calc(50vw - 25%)" -b "linear-gradeint(135deg, #2fb9e4, #FF0098)" -q 100 -i src/index.html --favicon
NOTE: pwa-asset-generator didn't work. So instead created a basic manifest. Continuing rest for now and will revist this later.
NOTE: Look into push notifications on PWA.
6. Check the manifest and index head for minimal code to be able to save to phone Home Screen with icon.
NOTE: Ideally you wanna understand how PWA's should work with Firebase apps.
7. Add viewport-fit=cover to (index.html head):
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
8. CSS to push the header down because it will cover the notch:
    @media screen and (display-mode: standalone) {
        header {
            height: 88px !important;
        }
    }
9. You may have to add a margin-top to the element after the header to compensate for step 8.
10. Add user-scalable=no
        <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, user-scalable=no">
11. Add CSS to disable element highlighting when tapped/clicked:
        body {
            -webkit-tap-highlight-color: transparent;
        }
12. Add CSS to keep the fixed header below notch:
        padding-top: constant(safe-area-inset-top); /* Older iOS (pre-11.2) */
        padding-top: env(safe-area-inset-top, 20px); /* Modern approach with a fallback */
        /* You can combine it with existing padding if needed */
        /* padding-top: calc(10px + env(safe-area-inset-top)); */

## Resources:
- Sam (Main source): https://youtu.be/KzvK809rl3Q
- Truth about PWA: https://youtu.be/3ODP6tTpjqA