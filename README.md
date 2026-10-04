# Arknights: Endfield Daily Sign-in Script (Google Apps Script)

This is a **Google Apps Script** that automates the daily sign-in process for **Arknights: Endfield** (SKPORT/Gryphline). It runs automatically on Google's servers, so you don't need to keep your computer on.

---

## Features

- ✅ **Auto Check-in:** Runs automatically every day (set to 3:00 AM UTC+7 / Asia/Jakarta).
- 🔒 **Secure:** Runs within your private Google Account. Use of script properties to store secrets, allows safe sharing of script with google share functionality.
- 🤖 **Auto Role Detection:** Automatically fetches your in-game profile ID (`sk-game-role`). No complex headers to copy!
- 💬 **Discord Notifications (Optional):** Sends a message to your server with check-in status, server profiles, and claimed rewards.

---

## 🚀 Setup Instructions

### Step 1: Get Your ACCOUNT_TOKEN

The website uses `httpOnly` cookies that cannot be copied via standard browser console commands. You need to extract this token manually using Developer Tools.

1. Open the [Endfield Sign-in Page](https://game.skport.com/endfield/sign-in).
2. Log in with your **Hypergryph/SKPORT** account.
3. Open browser **DevTools** by pressing **F12** (or right-click anywhere > Inspect).
4. Navigate to the **Application** tab in the DevTools window (you may need to click `>>` to see it).
5. In the left sidebar, expand **Cookies** → select **`https://game.skport.com`** (or `.skport.com`).
6. Find the cookie named **`ACCOUNT_TOKEN`** in the list.
7. **Copy the Value** of that cookie.

> ⚠️ **IMPORTANT:** Keep this token secret. Do not share it with anyone. It represents your direct access to your account.

---

### Step 2: Install the Script

1. Go to [script.google.com](https://script.google.com/).
2. Click **+ New Project**.
3. Delete any code currently in the editor (e.g., `function myFunction...`).
4. **Paste** the provided script code into the editor.
5. At the right of the script, find the menu and settings button.
6. Open Settings, scroll to bottom and add script properties: "ACCOUNT_TOKEN", "DISCORD_WEBHOOK_URL", "DISCORD_PING_USER_ID".
7. Paste value of ACCOUNT_TOKEN you copied into value of property you added.

---

### Step 3: Setup Discord Notification (Optional)

If you want to receive a notification on Discord when the script runs:

1. Open **Discord** and go to your server.
2. Right-click the text channel where you want notifications.
3. Select **Edit Channel** → **Integrations** → **Webhooks**.
4. Click **New Webhook**.
5. (Optional) Rename it and give it an avatar.
6. Click **Copy Webhook URL**.
7. Go back to your Google Script settings, script properties and fill value of DISCORD_WEBHOOK_URL
8. Also "Copy user ID" from right mouse click on user name/avatar menu to copy and fill DISCORD_PING_USER_ID script property to also get discord pings

---

### Step 4: Activate the Daily Schedule

1. Save the script (Floppy disk icon or Ctrl+S). Give the project a name (e.g., "Endfield Daily").
2. In the toolbar dropdown menu (next to "Debug"), select **`setupDailyTrigger`**.
3. Click **Run**.
4. **Authorization:**
   - Google will ask for permission to run. Click **Review Permissions**.
   - Select your Google Account.
   - You will likely see a screen saying "Google hasn’t verified this app" (because it's a custom script you just made).
   - Click **Advanced** (bottom left) -> **Go to [Project Name] (unsafe)**.
   - Click **Allow**.
5. Check the **Execution Log** at the bottom. It should say:
   > _Trigger set! The 'main' function will run daily between 3 AM and 4 AM (UTC+7)._

---

## ❓ FAQ & Troubleshooting

**Q: The script failed with "Failed to auto-detect game role".**  
A: If the automated role finder cannot find your account, you can still configure it manually. Switch your DevTools to the **Network** tab, reload the sign-in page, search for `attendance`, and locate `sk-game-role` in the Request Headers. Copy its value and paste it into the `SK_GAME_ROLE` variable in the script.

**Q: The script failed with "Token Expired".**  
A: The `ACCOUNT_TOKEN` may expire after a few weeks or months, or if you log out of the website manually. Simply repeat **Step 1** to get a new token and update the script variable.

**Q: How do I test if it works right now?**  
A: In the script editor, select the function **`main`** from the dropdown and click **Run**. Check the logs or your Discord channel for the result.

**Q: How do I stop the script?**  
A: To stop it from running, go to the **Triggers** icon (alarm clock) on the left sidebar of the script editor and delete the trigger listed there.
