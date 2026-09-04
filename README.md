# Notion Quick Add Shortcut (To Notion)

An Apple Shortcut called "To Notion" for iOS and macOS that prompts you for custom task text, logs today's date, and creates a new page in a Notion database. Trigger it from your home screen, menu bar, or any app via the Share Sheet (built for the Calendar layout, but compatible with others). It also captures optional shared URLs from your browser or other apps into a designated text property.

## Install

You can install the shortcut using either option below:

* **Option 1 (iCloud Link):** Tap the [iOS & macOS Notion Quick Add Shortcut link](https://www.icloud.com/shortcuts/82191b3b26b6458cbd084023a44536dd) and tap **Add Shortcut** when prompted.
* **Option 2 (Direct File):** Download the [To.Notion.GitHub.shortcut](https://github.com/Aifilesss/ios-macos-notion-quick-add-shortcut/releases/download/v1.0.0/To.Notion.GitHub.shortcut) file directly from this release and double-click it to import it into your Shortcuts app.

Follow the Setup steps below before running it for the first time.

## What it does

- Prompts you to type a custom task name or title
- Grabs the current date, formatted as `yyyy-MM-dd`
- Captures shared URLs or page links if triggered via the Share Sheet in any browser or app
- Sends a `POST` request to the Notion API to create a new page in your database
- Shows a confirmation notification when done

## Notion database requirements

Your target database needs these three properties, named and typed exactly as below (Notion property names are case-sensitive):

| Property Name | Type       |
|----------------|-----------|
| `Name`         | Title     |
| `Date`         | Date      |
| `Text`         | Text      |

## Setup

### 1. Create a Notion integration

1. Go to [notion.so/my-integrations](https://www.notion.so/my-integrations)
2. Click **New integration**, give it a name, and select the workspace containing your database
3. Copy the **Internal Integration Token**. This is your `NOTION_TOKEN`

### 2. Share your database with the integration

1. Open your target database in Notion
2. Click the **•••** menu (top right) → **Connections**
3. Search for and add the integration you just created

### 3. Get your database ID

1. Open your database as a full page (not a linked view)
2. Copy the ID from the URL. It's the string of characters right after your workspace name and before any `?v=` parameter
3. Format it with dashes in the standard UUID pattern (`8-4-4-4-12`), making it 36 characters total, e.g.:
   `29668d3a-3879-80f1-b6f9-e940b3d96795`

### 4. Add your token and database ID to the shortcut

1. Open the shortcut in the Shortcuts app → tap the three dots (`...`) to edit
2. Locate the **Get Contents of URL** action
3. Tap **Show More** (or tap directly on the headers/body fields to expand them)
4. Under **Headers**, find the `Authorization` key. Replace `YOUR_NOTION_TOKEN_HERE` with your actual Notion Internal Integration Token, making sure to keep the word `Bearer ` and a single space in front of it (e.g., `Bearer secret_abc123...`)
5. Under **Request Body**, locate `parent` → `database_id` and replace `YOUR_DATABASE_ID_HERE` with your real database ID (the 36-character dashed ID)
6. Tap **Done** in the top right to save your changes

### 5. Enable Share Sheet (optional, for capturing shared links)

1. Tap the **info/settings icon** on the shortcut
2. Toggle on **Show in Share Sheet**
3. Under **Accepts**, make sure URLs/web pages are included

### Notes

- Keep your integration token private — anyone with it can write to any database you've shared with that integration.
- **Troubleshooting:** If nothing appears in Notion after running the shortcut, make sure you have fully shared your database with your integration (see Step 2) and that your database ID is copied correctly with dashes.
