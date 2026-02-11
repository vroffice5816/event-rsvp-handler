# 📧 Event RSVP System - Complete Setup Guide

## 🎯 System Overview

This RSVP system allows you to:
- Create reusable RSVP pages for multiple events
- Track responses automatically in Google Sheets
- Send personalized links to parents linked to student numbers
- Collect attendance, dietary restrictions, and other information
- View summaries and statistics for each event

---

## 📦 What's Included

1. **event-rsvp.html** - The main RSVP webpage (mobile-responsive)
2. **google-apps-script.gs** - Backend code for Google Sheets integration
3. **README.md** - This setup guide

---

## 🔄 Your Workflow

### **One-Time Setup (Do this once)**
1. Create a Google Sheet for "Event RSVP Responses"
2. Add the Apps Script and deploy as web app
3. Host the event-rsvp.html file online
4. Note down both URLs (you'll reuse them!)

### **For Each New Event**
1. Open your Google Sheet for that specific event (or create a new one)
2. Ensure the script is deployed (only needed once per sheet)
3. Update the event details in your event-rsvp.html CONFIG section
4. In your student records spreadsheet/database:
   - Add a column for RSVP links
   - Use a formula like: `="https://yoursite.com/event-rsvp.html?student="&A2`
   - Where A2 contains the student number
5. Send emails to parents with their personalized links
6. Responses automatically flow into your Google Sheet!

---

## 🚀 Quick Start Setup (20 minutes)

### STEP 1: Set Up Google Sheets (10 min)

1. **Create a New Google Sheet**
   - Go to https://sheets.google.com
   - Click "Blank" to create a new spreadsheet
   - Name it "Event RSVP Responses" or similar

2. **Add the Google Apps Script**
   - In your Google Sheet, click **Extensions > Apps Script**
   - Delete any existing code in the editor
   - Open the file **google-apps-script.gs** from this package
   - Copy ALL the code and paste it into the Apps Script editor
   - Click the **Save** icon (💾)
   - Name your project "RSVP Handler"

3. **Deploy the Script as a Web App**
   - Click **Deploy > New deployment**
   - Click the gear icon ⚙️ next to "Select type"
   - Choose **Web app**
   - Configure the deployment:
     - **Description:** "RSVP Form Handler"
     - **Execute as:** Me (your-email@gmail.com)
     - **Who has access:** Anyone
   - Click **Deploy**
   - Click **Authorize access**
   - Choose your Google account
   - Click **Advanced** if you see a warning
   - Click **Go to RSVP Handler (unsafe)** - don't worry, this is your own script
   - Click **Allow**
   - **IMPORTANT:** Copy the "Web app URL" - it will look like:
     ```
     https://script.google.com/macros/s/AKfycby.../exec
     ```
   - Save this URL - you'll need it in Step 2!

### STEP 2: Configure the RSVP Webpage (5 min)

1. **Open event-rsvp.html** in a text editor (Notepad, TextEdit, VS Code, etc.)

2. **Find the CONFIG section** (around line 267)

3. **Update these values:**

```javascript
const CONFIG = {
    // Paste your Google Apps Script Web App URL here
    GOOGLE_SCRIPT_URL: 'https://script.google.com/macros/s/YOUR_URL_HERE/exec',
    
    // Customize your event details
    eventName: 'Annual School Fair',
    eventDate: 'Saturday, March 15, 2025 at 2:00 PM',
    eventDescription: 'Join us for our Annual School Fair! Enjoy games, food, performances, and community fun.',
    
    // Optional: Add image URLs
    eventImageUrl: '', // URL to event flyer/image
    schoolLogoUrl: '', // URL to school logo
};
```

4. **Save the file**

### STEP 3: Host Your RSVP Page (10 min)

You need to put the HTML file online so parents can access it. Here are the easiest options:

#### **Option A: GitHub Pages (FREE - Recommended)**

1. Create a GitHub account at https://github.com
2. Create a new repository (click the + icon > New repository)
3. Name it something like "school-rsvp"
4. Make it **Public**
5. Upload your **event-rsvp.html** file
6. Go to Settings > Pages
7. Under "Source", select "Deploy from a branch" and choose "main"
8. Click Save
9. Your page will be live at: `https://yourusername.github.io/school-rsvp/event-rsvp.html`

#### **Option B: Google Sites (Simple)**

1. Go to https://sites.google.com
2. Create a new site
3. Insert an "Embed" element
4. Paste your entire HTML code
5. Publish the site
6. Copy the site URL

#### **Option C: School Website**

If your school has a website, ask your IT department to host the HTML file.

### STEP 4: Generate Personalized Links in Your Student Records (5 min)

Now you'll create the personalized links directly in your student records spreadsheet/database.

#### **Method A: Excel/Google Sheets Formula**

If your student records are in Excel or Google Sheets:

1. Open your student records spreadsheet
2. Create a new column called "RSVP Link"
3. In the first row (assuming student numbers are in column A, starting at A2):

**Excel Formula:**
```excel
="https://yourusername.github.io/school-rsvp/event-rsvp.html?student="&A2
```

**Google Sheets Formula:**
```
="https://yourusername.github.io/school-rsvp/event-rsvp.html?student="&A2
```

4. Drag the formula down for all students
5. You now have personalized links for every student!

**Example Result:**
- Student 12345: `https://yoursite.com/event-rsvp.html?student=12345`
- Student 12346: `https://yoursite.com/event-rsvp.html?student=12346`

#### **Method B: Mail Merge Variable**

If using mail merge software (Mailchimp, SendGrid, etc.):

1. Set your base URL as: `https://yoursite.com/event-rsvp.html?student=`
2. Add your student number field variable: `{{student_number}}`
3. Final merge field: `https://yoursite.com/event-rsvp.html?student={{student_number}}`

#### **Method C: Manual (Small Groups)**

For small groups, just manually add the student number:
- Base: `https://yoursite.com/event-rsvp.html?student=`
- Add student number: `12345`
- Final: `https://yoursite.com/event-rsvp.html?student=12345`

---

## 💼 Working with Your Student Records Spreadsheet

### Excel Example

If your student records look like this:

| A (Student ID) | B (Student Name) | C (Parent Email) | D (RSVP Link) |
|----------------|------------------|------------------|---------------|
| 12345          | John Smith       | parent1@mail.com | *Formula here* |
| 12346          | Jane Doe         | parent2@mail.com | *Formula here* |

**In cell D2, enter:**
```excel
="https://yoursite.com/event-rsvp.html?student="&A2
```

Then drag down to auto-fill for all students.

### Google Sheets Example

Same structure, but you can also use ARRAYFORMULA for instant generation:

**In cell D2:**
```
=ARRAYFORMULA(IF(A2:A="","","https://yoursite.com/event-rsvp.html?student="&A2:A))
```

This automatically creates links for all students at once!

### Mail Merge Integration

Popular email tools and how to use them:

**Gmail + Mail Merge (Google Sheets Add-on):**
1. Install "Yet Another Mail Merge" add-on
2. Use `{{RSVP Link}}` in your email template
3. The add-on will replace it with column D values

**Mailchimp:**
1. Import your spreadsheet
2. In your email template use: `*|RSVP Link|*`
3. Mailchimp replaces with the actual links

**Microsoft Outlook Mail Merge:**
1. Use the RSVP Link column as a merge field
2. Insert as hyperlink in email body

---

## 📧 Sending Links to Parents

### Email Template Example:

```
Subject: RSVP for [Event Name] - [Student Name]

Dear Parent/Guardian,

We're excited to invite you to our upcoming [Event Name] on [Date].

Please click the link below to RSVP:
[PASTE PERSONALIZED LINK HERE]

This link is unique to your family and will help us track attendance.

Looking forward to seeing you there!

Best regards,
[Your Name]
[School Name]
```

### Using Mail Merge

Create your email template with the merge field:

```
Dear {{Parent Name}},

We're excited to invite {{Student Name}} and your family to our [Event Name].

Please RSVP by clicking here: {{RSVP Link}}

Thank you!
```

---

## 📊 Viewing Responses

1. **Open your Google Sheet**
2. You'll see a new sheet called **"RSVP Responses"**
3. Each submission appears as a new row with:
   - Timestamp
   - Event details
   - Student number
   - Parent information
   - Attendance status
   - Number of attendees
   - Dietary restrictions
   - Comments

### Generate Summary Statistics

1. In Apps Script, click **Run > Select function > createSummarySheet**
2. Click Run
3. A new "Summary" sheet will be created with:
   - Total responses per event
   - Yes/No/Maybe counts
   - Total expected attendees

---

## 🔄 Using the System for Multiple Events

### Method 1: Update CONFIG in HTML (Quick)

For each new event, just change these lines in event-rsvp.html:

```javascript
eventName: 'Spring Concert',
eventDate: 'Friday, April 12, 2025 at 7:00 PM',
eventDescription: 'Join us for our annual spring concert...',
```

Then re-upload the file (or use the same file if you want to track all events in one sheet).

### Method 2: Create Separate Pages (Better Organization)

1. Make a copy of event-rsvp.html
2. Rename it (e.g., spring-concert-rsvp.html)
3. Update the CONFIG for the new event
4. Upload to your hosting
5. Generate new links with the new URL

All responses still go to the same Google Sheet, organized by event name!

---

## 🎨 Customization Options

### Change Colors

In event-rsvp.html, find the CONFIG section:

```javascript
primaryColor: '#667eea',    // Change to your school color
secondaryColor: '#764ba2'   // Change to complementary color
```

### Add School Logo

1. Upload your logo image to a hosting service (imgur.com, Google Drive, etc.)
2. Get the direct image URL
3. Update CONFIG:

```javascript
schoolLogoUrl: 'https://yoursite.com/logo.png',
```

### Add Event Image

```javascript
eventImageUrl: 'https://yoursite.com/event-flyer.jpg',
```

### Modify Form Fields

To add/remove fields, edit the HTML in event-rsvp.html:
- Find the `<form id="rsvpForm">` section
- Add/remove form groups as needed
- Update the Google Apps Script to match your new fields

---

## 🔒 Security Features

- Each student number gets a unique link
- Parents can't see other families' responses
- Responses are stored securely in your Google Sheet
- Only you (the Google Sheet owner) can access the data
- No login required for parents (frictionless RSVP)

---

## 🐛 Troubleshooting

### "Submissions aren't appearing in Google Sheets"

1. Check that you pasted the correct Google Apps Script URL in CONFIG
2. Make sure the URL starts with `https://script.google.com/macros/s/`
3. Re-deploy the Apps Script and get a fresh URL
4. Clear your browser cache and try again

### "Parents can't access the page"

1. Make sure the HTML file is publicly accessible
2. Test the link in an incognito/private browser window
3. Check that GitHub Pages is enabled (if using GitHub)

### "The page looks broken"

1. Make sure you uploaded the COMPLETE HTML file
2. Don't edit the file in Google Docs or Word (use a text editor)
3. Check for any missing closing tags

### "Student number not showing"

1. Make sure the link includes `?student=12345` at the end
2. Check that you're using the link generator correctly
3. Test a link yourself to verify it works

---

## 📞 Email Notifications (Optional)

To receive an email every time someone RSVPs:

1. Open **google-apps-script.gs**
2. Find the commented section (around line 65)
3. Uncomment the code and add your email:

```javascript
const adminEmail = 'your-email@school.com';
```

4. Save and re-deploy the script

---

## 💡 Pro Tips

1. **Test First:** Before sending to all parents, test with 2-3 dummy student numbers
2. **Backup Data:** Regularly download your Google Sheet as a backup
3. **Track Completion:** Use the student numbers to see who hasn't responded
4. **Follow-up:** Send reminder emails to families who haven't RSVP'd
5. **Mobile-Friendly:** The page works great on phones - parents can RSVP anywhere!

---

## 📋 Checklist

- [ ] Created Google Sheet for responses
- [ ] Added Apps Script code
- [ ] Deployed as web app and copied URL
- [ ] Updated CONFIG in event-rsvp.html with script URL
- [ ] Hosted HTML file online and noted the URL
- [ ] Updated event details in CONFIG for your event
- [ ] Added RSVP link column in student records spreadsheet
- [ ] Created formula to generate personalized links
- [ ] Tested a submission with a sample student number
- [ ] Verified data appears in Google Sheet
- [ ] Sent emails to parents with their unique links

---

## 🎓 Advanced Features

### Export Responses to Excel

1. In Google Sheets, click **File > Download > Microsoft Excel**
2. You now have all responses in Excel format

### Create QR Codes

1. Use a QR code generator (e.g., qr-code-generator.com)
2. Paste each personalized link
3. Download the QR codes
4. Print on invitations or flyers

### Integration with Email Marketing

Export the CSV from the link generator and import into:
- Mailchimp
- Constant Contact
- SendGrid
- Your school's email system

Each email can include the personalized RSVP link.

---

## ❓ Frequently Asked Questions

**Q: Can parents change their RSVP after submitting?**
A: Yes! They can click their link again and resubmit. You'll see multiple entries in the sheet (use the latest one).

**Q: What if two students have the same parent?**
A: Generate separate links for each student. Parents can submit multiple RSVPs.

**Q: Can I see who hasn't responded?**
A: Yes! Compare your student list with the "Student Number" column in Google Sheets.

**Q: Is this GDPR/privacy compliant?**
A: You're collecting standard contact information with parental consent. Check your school's privacy policy.

**Q: Can I use this for other types of events?**
A: Absolutely! Works for: field trips, parent-teacher conferences, workshops, fundraisers, etc.

---

## 🤝 Support

If you need help:
1. Re-read this guide carefully
2. Check the troubleshooting section
3. Test each step individually
4. Ask your school's IT department for hosting assistance

---

## 📄 License & Usage

Feel free to use and modify this system for your school's needs. No attribution required.

---

**You're all set! Happy event planning! 🎉**
