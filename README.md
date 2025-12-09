# 🚀 Summer 2026 Internship Alert System

**Automated email notifications for new Software Engineering and AI/ML/Data Science internship postings every 30 minutes.**

Never miss an internship opportunity again! This GitHub Actions-powered system monitors the [SimplifyJobs Summer 2026 Internships](https://github.com/SimplifyJobs/Summer2026-Internships) repository and sends you instant email alerts when new roles are posted.

---

## ✨ Features

- 🔔 **Instant Notifications** - Get emails within 30 minutes of new postings
- 💻 **SWE Focused** - Tracks Software Engineering roles only
- 🤖 **AI/ML/DS Coverage** - Also monitors Data Science, AI & Machine Learning positions
- 📧 **Beautiful HTML Emails** - Clean, formatted emails with direct application links
- ⚡ **Zero Maintenance** - Runs automatically in the cloud via GitHub Actions
- 🆓 **Completely Free** - No servers, no costs, just GitHub's free tier

---

## 📋 What You'll Receive

When new internships are posted, you'll get an email like this:

```
🎉 New Internship Opportunities!

📅 Last Updated: 2025-12-03T23:38:36Z
💬 Latest Commit: Added 5 new SWE roles
🔗 Commit SHA: c2f8bbe

💻 NEW SOFTWARE ENGINEERING ROLES (3)

1. Google
   Software Engineer Intern
   📍 Mountain View, CA
   [Apply Now]

2. Meta
   Software Engineer Intern - Infrastructure
   📍 Menlo Park, CA
   [Apply Now]

3. Microsoft
   Software Engineer Intern
   📍 Redmond, WA
   [Apply Now]

📊 Total SWE Roles: 328 | Total AI/ML/DS Roles: 521
```

---

## ⚠️ Important Disclaimer

**This system ONLY tracks:**
- 💻 Software Engineering internships
- 🤖 AI/ML/Data Science internships

**Other categories (PM, Quant, Hardware) are NOT monitored.**

Checks run **every 30 minutes** - you'll be notified within half an hour of new postings.

---

## 🚀 Quick Start (5 Minutes)

### Step 1: Fork This Repository

1. Click the **"Fork"** button at the top right of this page
2. This creates your own copy of the monitoring system

### Step 2: Set Up Email Sending (Gmail)

You need a Gmail account to send notifications from:

1. **Use any Gmail account** (or create a new one)
2. **Enable 2-Factor Authentication:**
   - Go to [Google Account Security](https://myaccount.google.com/security)
   - Turn on 2-Step Verification
3. **Generate App Password:**
   - Go to [App Passwords](https://myaccount.google.com/apppasswords)
   - Select "Mail" and "Other (Custom name)"
   - Name it "Internship Monitor"
   - **Copy the 16-character password** (e.g., `abcd efgh ijkl mnop`)

### Step 3: Configure GitHub Secrets

1. In your forked repo, go to **Settings → Secrets and variables → Actions**
2. Click **"New repository secret"** and add these three secrets:

| Secret Name | Value | Example |
|-------------|-------|---------|
| `EMAIL_USERNAME` | Your Gmail address | `yourname@gmail.com` |
| `EMAIL_PASSWORD` | Gmail App Password (no spaces) | `abcdefghijklmnop` |
| `RECIPIENT_EMAIL` | Email(s) where you want alerts | `your.email@school.edu` or `email1@school.edu, email2@gmail.com` |

> 💡 **Tip:** You can add multiple recipient emails directly in the `RECIPIENT_EMAIL` secret by separating them with commas.

### Step 4: Enable GitHub Actions

1. Go to the **Actions** tab in your repo
2. Click **"I understand my workflows, go ahead and enable them"**
3. That's it! The system will start monitoring automatically

### Step 5: Test It (Optional)

1. Go to **Actions → Internship Monitor**
2. Click **"Run workflow"** → **"Run workflow"**
3. Wait ~1 minute for it to complete
4. Check your email! (First run initializes the system, may not send email)

---

## 📖 How It Works

```
┌─────────────────────────────────────────────────────────┐
│  SimplifyJobs Repo Updates                              │
│  (New internship posted)                                │
└────────────────┬────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────┐
│  GitHub Actions (Every 30 minutes)                      │
│  • Fetches latest README                                │
│  • Parses SWE and AI/ML sections                        │
│  • Compares with previous version                       │
└────────────────┬────────────────────────────────────────┘
                 │
                 ▼
         New roles detected?
                 │
        ┌────────┴────────┐
        │                 │
       YES               NO
        │                 │
        ▼                 ▼
  Send Email        Do Nothing
   Alert!
```

---

## 🎛️ Customization

### Change Notification Frequency

Edit `.github/workflows/internship-monitor.yml`:

```yaml
schedule:
  - cron: '*/30 * * * *'  # Every 30 minutes (default)
```

**Other options:**
- Every 15 minutes: `*/15 * * * *`
- Every hour: `0 * * * *`
- Every 2 hours: `0 */2 * * *`

### Monitor Different Branches

The system monitors the `dev` branch by default (gets updates first). To change:

Edit line ~25 in the workflow file:
```yaml
https://raw.githubusercontent.com/SimplifyJobs/Summer2026-Internships/dev/README.md
```

Change `dev` to `main` if you prefer the stable branch.

### Add More Recipients

**Option 1: Via Secret (Recommended)**

Update your `RECIPIENT_EMAIL` secret to include multiple emails:
```
email1@example.com, email2@example.com, email3@example.com
```

**Option 2: Directly in Workflow**

Edit the workflow file and change:
```yaml
to: ${{ secrets.RECIPIENT_EMAIL }}
```

To:
```yaml
to: email1@example.com, email2@example.com
```

---

## 🔧 Troubleshooting

### Not Receiving Emails?

1. **Check spam folder** - First time emails often go to spam
2. **Verify secrets** - Settings → Secrets → Actions
   - Make sure `EMAIL_USERNAME`, `EMAIL_PASSWORD`, and `RECIPIENT_EMAIL` are set
   - Gmail App Password should be 16 characters, no spaces
3. **Check Actions logs** - Actions tab → Latest workflow run → Look for errors
4. **Test Gmail login** - Try using the app password in an email client to verify it works

### Workflow Not Running?

1. **Enable Actions** - Go to Actions tab and enable workflows
2. **Check permissions** - Settings → Actions → General
   - Set Workflow permissions to "Read and write permissions"
3. **Repository activity** - GitHub may pause workflows on inactive repos
   - Just run the workflow manually once to reactivate

### Getting Duplicate Notifications?

This is normal if:
- You just set up the system (baseline is being established)
- You modified `previous_readme.md` manually
- The SimplifyJobs repo reformatted their README

**Solution:** Let it run once without changes. It will sync up automatically.

### Not Getting Notifications for New Roles?

1. Check the SimplifyJobs repo - are there actually new SWE or AI/ML roles?
2. Verify your `previous_readme.md` is up to date (should auto-update after each check)
3. Check Actions logs to see what's being detected

---

## 🤝 Contributing

Found a bug? Have a feature idea? Contributions are welcome!

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Commit your changes: `git commit -am 'Add feature'`
4. Push to the branch: `git push origin feature-name`
5. Open a Pull Request

---

## 📝 Technical Details

- **Language:** Python 3.11
- **Automation:** GitHub Actions
- **Email Service:** Gmail SMTP
- **Monitoring Frequency:** Every 30 minutes (configurable)
- **Parsing Method:** Regex-based HTML table parsing
- **Storage:** GitHub repository (previous_readme.md)

---

## ⚖️ License

This project is licensed under the MIT License - feel free to use, modify, and distribute.

---

## 🙏 Acknowledgments

- **SimplifyJobs** - For maintaining the incredible [Summer 2026 Internships](https://github.com/SimplifyJobs/Summer2026-Internships) repository
- **Pitt CSC** - For their partnership in curating internship opportunities
- **GitHub Actions** - For free automation infrastructure

---

## 📬 Questions?

Open an issue in this repository or check the [Discussions](../../discussions) tab!

---

<div align="center">

**⭐ If this helped you land an internship, give it a star! ⭐**

Made with ❤️ for students hunting internships

*Good luck with your applications! 🚀*

</div>
