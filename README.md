# 📱 Semi-Automated LINE Status Check-In (Stage 1)

This iOS Shortcut automation enables users to quickly send a status update via the LINE app and log the same data to a Google Sheet using Make.com (formerly Integromat) through a webhook.

Designed with neurodivergent accessibility in mind, it minimizes decision fatigue and removes barriers to communication.

---

## ⚙️ Features

- Tap-based interaction using iPhone's **Back Tap** (double tap)
- Sends pre-filled messages via the **LINE app** using URL schemes
- Simultaneously logs check-in data (status, battery, location, time) via **Make.com Webhook**
- Two status options: `I'm out` and `I'm back`
- Supports structured logging into **Google Sheets**

---

## 🧠 Why This Helps People with ADHD / Neurodivergent Needs
People with ADHD often struggle with:

- Remembering to update others
- Switching mental gears for minor communication tasks
- Getting overwhelmed by app navigation or typing

This automation:

✅ Removes decision fatigue  
✅ Provides structure through tactile input (Back Tap)  
✅ Reduces the barrier to quick safety updates  

By using minimal input and offering fast, reliable output, it streamlines communication for those who benefit most from automation.

---

## 📲 How It Works (Stage 1 Workflow)

1. **Trigger**: Double-tap the back of your iPhone (via Accessibility > Back Tap)
2. **Menu Prompt**: Choose `I'm out` or `I'm back`
3. **Actions**:
   - Generate variables: current time, date, battery %, location, and maps URL
   - Compose pre-filled text message
   - Encode and open URL with `line://msg/text/`
   - Post data to Make.com Webhook in JSON format

---

## 🧩 Technical Challenges & Solution

### ❌ Problem: Using `If` Caused Logic Errors
- `If Menu Result` logic failed to reliably interpret selection text
- Hard-coded values like `I'm out` wouldn't trigger expected branches
- Internal referencing in Shortcuts caused inconsistent behavior

### ✅ Final Solution: Use `Choose from Menu` as Logic Handler
- Removed all `If` blocks
- Embedded each logic branch directly inside the corresponding menu option
- Global variables (date, location, battery) were initialized at the top of the Shortcut to ensure availability

---

## 🔗 Sample JSON Payload Explanation

The shortcut sends the following payload to Make.com:

```json
{
  "timestamp": "2024-09-22 18:24",
  "sender": "Michael",
  "battery": "86%",
  "location": "https://maps.apple.com/?ll=35.6895,139.6917",
  "message": "Hey, just giving you a quick update of where I am...",
  "status": "I'm out"
}
```

📝 **Note:** The Make.com webhook module should be set to `POST`, with a header:

```
Content-Type: application/json
```

---

## 🧪 Potential Use Cases

👤 Solo travelers checking in with loved ones  
👨‍👩‍👧 Teens keeping parents informed  
👩‍🦰 Women alerting partners of safe arrival/departure  
🏠 Remote workers logging status updates  
👴 Elderly or dependents needing simplified interaction

---

## 🔮 Future Applications (Stage 2 and Beyond)

### ☁️ Webhook-Enhanced Version
- Auto-log check-in data to Google Sheets, Notion, or Airtable
- Notify other platforms like Discord, Telegram, Slack
- Trigger Make.com automation flows

### 🔒 Privacy-Conscious Expansion
- Encrypt or hash location data before sending
- Store logs locally or in secure cloud endpoints

### 📡 NFC or Siri Integration
- Use NFC tag scan or Siri phrase to initiate check-in
- Extend into HomeKit scenes based on check-in status

---

## 🛠 Setup Instructions

1. **Create Webhook in Make.com**
   - Create a new scenario with a Webhook module
   - Copy the generated webhook URL

2. **Create a Google Sheet**
   - Add headers: `timestamp`, `sender`, `battery`, `location`, `message`, `status`

3. **Link Google Sheets module** to the webhook
   - Use incoming webhook data to map into the Google Sheet

4. **Download and Customize Shortcut**
   - Set the webhook URL in the `Get Contents of URL` block
   - Add your personalized text message templates

5. **Enable Back Tap**
   - Settings > Accessibility > Touch > Back Tap > Double Tap > Select the shortcut

---

## 📦 Repository Contents

- `README.md` (this file)
- `sample-payload.json` (optional JSON sample for testing)
- `.shortcut` file (coming soon)

---

## 🙋‍♂️ Maintainer
Chipa Mwenya 
