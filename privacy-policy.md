# Privacy Policy for Hero Defense: Shattered Crown

**Last updated: 2026-07-16**

This privacy policy describes how **Prince Forge** ("we", "us", or "our") handles
information when you use the Hero Defense: Shattered Crown mobile application ("the App").

By downloading and using the App, you agree to the practices described in this policy.

---

## 1. Information We Collect

### 1.1 Information You Provide Directly
We do **not** require you to create an account, provide an email address, or submit
any personal information to use the App. The App can be used entirely without
providing any personal data.

### 1.2 Information Collected Automatically
The App stores the following data **locally on your device** using Godot's
ConfigFile system (in the app's private storage area):

- **Game progress**: completed levels, star ratings, currency amounts (crystals,
  essence, gold), hero unlock status, hero experience points, upgrade tiers
- **Game settings**: difficulty preference, colorblind mode, high-contrast mode,
  text size, audio volume, reduced motion preference, bloom toggle
- **Age gate response**: a one-time confirmation that the player is old enough
  to play (stored as a boolean flag — no birth date or age is collected)
- **Consecutive failure tracking**: per-level failure count used to provide
  comeback bonus rewards and stuck-player hints (reset on victory)
- **Ad cooldown timestamps**: used to enforce cooldown periods between rewarded ads
- **In-app purchase state**: which non-consumable purchases you've made (Remove Ads,
  Crystal Blessing) - stored locally so the App knows your entitlements offline

This local data is **never transmitted to our servers**. It remains on your device
and can be cleared at any time by uninstalling the App or using the in-game
"Clear Save" option.

### 1.3 Information Collected by Third-Party Services
The App integrates with the following third-party services, which may collect
information as described in their respective privacy policies:

#### Google AdMob (Ads)
- **Purpose**: Serves rewarded video advertisements within the App
- **Data collected**: Device identifier (advertising ID), IP address, coarse
  location (country-level), device type, operating system version, app usage
  data related to ad interactions
- **Use**: Ad delivery, frequency capping, ad fraud prevention, analytics
- **Link**: [Google AdMob Privacy Policy](https://support.google.com/admob/answer/6128543)
- **Consent**: Before initializing AdMob, the App requests consent via
  Google's User Messaging Platform (UMP). You can change your privacy choices
  at any time via the "Privacy Choices" button in the App's settings menu.
- **Note**: If you purchase "Remove Ads", ad data collection stops as no ads
  will be served to your device.

#### Google User Messaging Platform (UMP / Consent)
- **Purpose**: Collects user consent for ad personalization in compliance
  with GDPR and other privacy regulations
- **Data collected**: Consent status (obtained/not required/required), stored
  on device
- **Use**: Determines whether personalized or non-personalized ads are shown
- **Link**: [Google UMP Privacy](https://policies.google.com/privacy)

#### Google Play Billing (In-App Purchases)
- **Purpose**: Processes in-app purchases (crystal packs, essence packs,
  Remove Ads, Crystal Blessing)
- **Data collected**: Purchase tokens, transaction IDs, your Google account's
  purchase history (managed by Google Play, not by us)
- **Use**: Verifying and fulfilling purchases, restoring previous purchases
- **Server-side validation**: Purchase tokens are sent to our validation
  endpoint (`billing-server-delta.vercel.app`) to verify authenticity against
  the Google Play Developer API before entitlements are granted. This prevents
  fraudulent purchases. Only the product ID, purchase token, and package name
  are transmitted — no personal data.
- **Link**: [Google Play Privacy Policy](https://policies.google.com/privacy)

#### Google Play Games Services (Cloud Save)
- **Purpose**: Backs up your game progress to the cloud so it can be restored
  on a new device or after reinstall
- **Data collected**: Google account ID (for identifying the save snapshot),
  game save data (same as the local save file)
- **Use**: Automatic cloud save sync on level completion and app pause;
  automatic download on app start if a newer cloud save exists
- **Link**: [Google Play Games Services Privacy](https://policies.google.com/privacy)
- **Note**: Cloud save is optional. If you do not sign in to Google Play Games,
  your progress remains only on your device.

#### Google Play Services
- **Purpose**: Required infrastructure for ads, billing, and cloud save on Android
- **Data collected**: As described in Google's privacy policy
- **Link**: [Google Privacy Policy](https://policies.google.com/privacy)

---

## 2. How We Use Information

- To operate, maintain, and improve the App's functionality
- To serve relevant rewarded video ads (via Google AdMob)
- To process and fulfill in-app purchases (via Google Play Billing)
- To restore your previous purchases when you reinstall the App or switch devices
- To enforce ad cooldown periods (stored locally on your device)

We do **not** use your information to:
- Send marketing emails or push notifications
- Build user profiles for sale or sharing with third parties
- Track your location beyond what is required by ad networks (country-level)

---

## 3. How We Share Information

We do **not** sell, rent, or trade your personal information. The only sharing
that occurs is:

- **With Google AdMob**: As needed to serve ads (device ID, ad interaction data)
- **With Google Play**: As needed to process purchases (purchase tokens)
- **As required by law**: If we are compelled to disclose information by a valid
  legal request (subpoena, court order, etc.)

---

## 4. Data Retention

- **Local game data**: Retained on your device until you uninstall the App or
  clear the save file. We have no access to this data and cannot retrieve it.
- **Ad data (Google AdMob)**: Retained per Google's data retention policies
- **Purchase data (Google Play)**: Retained per Google Play's policies and linked
  to your Google account so purchases can be restored

---

## 5. Children's Privacy

The App is intended for a general audience and is rated **Everyone 10+**
per the IARC rating system. The App does **not** knowingly collect personal
information from children under 13.

On first launch, the App displays a neutral age gate asking the player to
confirm they are old enough to play, or to seek a parent's help. This is a
one-time confirmation stored as a boolean flag — no birth date, age, or
personal information is collected. Players who indicate they need parental
help are shown a brief guidance message.

Google AdMob is configured to serve ads appropriate for the App's content rating.
If you believe a child under 13 has provided personal information to us through
the App, please contact us so we can investigate and take appropriate action.

---

## 6. Your Rights

### 6.1 Reset Ad Advertising ID
You can reset your device's advertising ID at any time in your Android settings:
**Settings → Google → Ads → Reset advertising ID**.

### 6.2 Opt Out of Personalized Ads
You can opt out of personalized ads from Google AdMob in your Android settings:
**Settings → Google → Ads → Opt out of Ads Personalization**.

You can also change your ad privacy choices within the App by tapping
**"Privacy Choices"** in the settings menu. This re-opens the Google UMP
consent form, allowing you to update your ad personalization preferences
at any time.

### 6.3 Clear Local Data
You can clear all locally-stored game data by:
- Using the in-game "Clear Save" option (in the settings menu), or
- Uninstalling the App

### 6.4 Restore Purchases
If you reinstall the App or switch devices, use the "Restore Purchases" button
in the App's Store → Remove Ads tab to re-apply your previous purchases.

---

## 7. Security

- Local game data is stored in the App's private storage area, which is sandboxed
  by Android and not accessible to other apps on a non-rooted device.
- In-app purchase verification is handled by Google Play Billing, which uses
  signed purchase tokens to prevent tampering.
- We do not transmit your local game data over the internet.

---

## 8. Third-Party Links

The App contains links to:
- Google Play Store (for rating the App)
- Google AdMob (ad content, which may link to external sites)

We are not responsible for the privacy practices of third-party sites. Please
review the privacy policies of any third-party sites you visit.

---

## 9. Changes to This Privacy Policy

We may update this privacy policy from time to time. When we do, we will:
- Update the "Last updated" date at the top of this policy
- Notify you of significant changes by updating the App's store listing

We encourage you to review this policy periodically.

---

## 10. International Users

The App is available worldwide on the Google Play Store. If you are accessing
the App from outside your home country, be aware that your information may be
transferred to, stored, and processed in the United States or other countries
where Google's servers are located. By using the App, you consent to such
transfers.

---

## 11. Contact Us

If you have questions about this privacy policy or the App's data practices,
please contact us at:

**Prince Forge**
Email: **kollintheprince@gmail.com**
Website: **https://princeforge.github.io**

---

## Summary (TL;DR)

- We collect **no personal information** directly - all game data stays on your device.
- A **neutral age gate** appears on first launch (one-time boolean confirmation, no age or birth date collected).
- **Google UMP** collects your consent choice before ads are shown; you can change it
  anytime via "Privacy Choices" in settings.
- **Google AdMob** may collect device IDs and ad interaction data to serve ads.
- **Google Play Billing** processes your purchases - purchase tokens are sent to our
  validation server to verify authenticity.
- **Google Play Games Services** optionally backs up your progress to the cloud.
- You can reset your ad ID, opt out of personalized ads, change your privacy choices,
  and clear your local data at any time.
- Purchasing "Remove Ads" stops all ad-related data collection from your device.
