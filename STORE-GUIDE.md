# Publishing to App Stores

## Prerequisites

- **Android**: Install [Android Studio](https://developer.android.com/studio)
- **iOS**: Install [Xcode](https://apps.apple.com/us/app/xcode/id497799835) (Mac only)
- **Google Play Console**: $25 one-time fee → https://play.google.com/console
- **Apple Developer Program**: $99/year → https://developer.apple.com/programs

## Build Steps

### 1. Sync web files to native projects

Any time you edit `index.html`, copy it to `www/` and sync:

```bash
cp index.html www/
cp manifest.json www/
cp sw.js www/
cp -r icons www/
npx cap sync
```

### 2. Android (Google Play)

```bash
npx cap open android
```

This opens Android Studio. Then:

1. **Set app icon**: In Android Studio, right-click `app/src/main/res` → New → Image Asset. Use `icons/icon-1024.png` as the source.
2. **Build signed APK/AAB**: Build → Generate Signed Bundle/APK → Android App Bundle (.aab)
   - Create a new keystore (save it safely — you need it for every update)
   - Select "release" build variant
3. **Upload to Google Play Console**:
   - Create app → "Poppy's Ultimate Insult Generator"
   - Target audience: select "Ages 6-12" (triggers COPPA compliance)
   - Content rating: fill out the IARC questionnaire
   - Upload the `.aab` file to Production → Create new release
   - Set price to $0.99 (or free)
   - Add screenshots (take them from the running app)
   - Submit for review (~1-3 days)

### 3. iOS (App Store)

```bash
npx cap open ios
```

This opens Xcode. Then:

1. **Set up signing**: In Xcode, select the "App" target → Signing & Capabilities → select your Apple Developer team
2. **Set app icon**: In the Assets.xcassets → AppIcon, drag `icons/icon-1024.png` into the 1024x1024 slot (Xcode generates all other sizes)
3. **Set Bundle ID**: `com.poppys.insultgenerator`
4. **Archive**: Product → Archive → Distribute App → App Store Connect
5. **In App Store Connect** (https://appstoreconnect.apple.com):
   - Create new app → "Poppy's Ultimate Insult Generator"
   - Age rating: fill out the questionnaire (no objectionable content — this is silly humor)
   - Set the "Made for Kids" flag
   - Price: $0.99 (Apple takes 15% for small developers)
   - Upload screenshots for iPhone 6.7", 6.5", 5.5" and iPad
   - Submit for review (~1-7 days)

## Store Listing Copy

**Title**: Poppy's Ultimate Insult Generator

**Subtitle**: 16 Billion Silly Zingers!

**Description**:
Generate hilariously silly insults by tapping five colorful strips! Mix and match over 16 BILLION possible combinations of people, actions, things, twists, and creatures to create the ultimate zinger.

Perfect for kids who love gross-out humor, silly wordplay, and making their friends laugh. Tap each strip to randomize it, or hit Shuffle All for instant chaos!

Features:
• 5 tappable strips that generate random insult parts
• Over 16 billion unique combinations
• Copy your favorite insults to share with friends
• Fun, colorful design with satisfying flip animations
• No ads, no in-app purchases, no internet required
• Works offline — insult anywhere, anytime!

Inspired by Mike Barfield's book "The Ultimate Insult Generator"

**Keywords**: insult generator, kids humor, funny, gross, silly, jokes, word game, random generator

**Category**: Entertainment (primary), Games → Word (secondary)

## COPPA Compliance Notes

Since this targets kids:
- ✅ No data collection (fully offline)
- ✅ No ads
- ✅ No social features or login
- ✅ No links to external websites (in the native app version)
- ✅ No in-app purchases (if sold as paid app)
- Remove the "Inspired by" footer link if it goes external
