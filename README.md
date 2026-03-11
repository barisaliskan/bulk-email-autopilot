# 📬 bulk-email-autopilot

> Send bulk personalized emails with attachments automatically — powered by [n8n](https://n8n.io).

[![n8n](https://img.shields.io/badge/n8n-workflow-orange?logo=n8n)](https://n8n.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Made by Barış Alışkan](https://img.shields.io/badge/made%20by-Bar%C4%B1%C5%9F%20Al%C4%B1%C5%9Fkan-blueviolet)](https://linkedin.com/in/barisaliskan)

---

🎬 Demo

https://github.com/user-attachments/assets/9f03d12e-77c7-417e-abd1-d879dfa63aab.mp4

---
## 📌 What Does It Do?

This n8n workflow lets you send personalized bulk emails with a PDF attachment (e.g. your CV) to an entire list of addresses — fully automated.

1. 📄 Prepares your PDF as a base64 attachment
2. ⏱️ Waits **3 seconds** between sends to avoid spam filters
3. 📧 Sends a personalized email via **Gmail**
4. 🔁 Loops until every address in the list is processed

---

## 🏗️ Flow Diagram

```
Manual Trigger
      │
      ▼
Email List  ──►  Loop Over Items
                       │
                       ▼  (for each email)
                  Prepare Attachment
                       │
                       ▼
                    Wait (3s)
                       │
                       ▼
                  Send via Gmail
                       │
                       └──► Loop Over Items (next)
```

---

## 🚀 Setup

### 1. Requirements
- [n8n](https://docs.n8n.io/getting-started/installation/) (self-hosted or cloud)
- Gmail account with OAuth2 credentials configured in n8n

### 2. Import the Workflow

1. Download `workflow.json`
2. Open your n8n dashboard
3. Click **"Import from file"** and select the file

### 3. Configuration

**`Email Listesi` node** — add your target addresses:
```js
const rawList = `
company1@example.com
company2@example.com
hr@techfirm.com
`;
```

**`CV Hazirla` node** — replace the placeholder with your PDF in base64:
```js
const base64CV = 'YOUR_BASE64_PDF_HERE';
```

To convert your PDF to base64 on the command line:
```bash
base64 -i YourFile.pdf | tr -d '\n'
```
Or use an online tool: [base64.guru/converter/encode/pdf](https://base64.guru/converter/encode/pdf)

**`Gmail Gonder` node:**
- Connect your Gmail OAuth2 credentials
- Customize the `subject` and `message` body to fit your use case

### 4. Run 🎉

Hit the **Manual Trigger** button to start the workflow!

---

## ⚠️ Important Notes

| Topic | Detail |
|-------|--------|
| **Spam risk** | Sending too many emails too quickly may get your Gmail flagged. Increase the wait time if needed. |
| **Attachment** | Update the base64 string every time your PDF changes. |
| **Personalization** | Add extra fields (e.g. `companyName`) to the email list and make the template dynamic for per-company customization. |

---

## 🛠️ Customization Tips

- **Change wait time:** Edit the `amount` value in the `Bekleme` node (in seconds)
- **Batch control:** Add a `batchSize` parameter to the `splitInBatches` node to control concurrency
- **Dynamic list:** Replace the hardcoded email list with a Google Sheets node to pull addresses from a spreadsheet

---

## 📁 File Structure

```
📦 bulk-email-autopilot
 ┣ 📜 workflow.json    # n8n workflow export
 ┣ 📜 README.md        # This file
 ┗ 📜 LICENSE          # MIT License
```

---

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you'd like to change.

---

## 📬 Contact

**Barış Alışkan**
- 🔗 [linkedin.com/in/barisaliskan](https://linkedin.com/in/barisaliskan)
- 💻 [github.com/barisaliskan](https://github.com/barisaliskan)

---

## 📄 License

[MIT](LICENSE) © Barış Alışkan
