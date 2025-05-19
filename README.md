# Alumni Directory Website

A simple alumni directory where users can:

- Submit their info via a form
- View a public list of alumni entries
- All data is stored in Google Sheets via Google Apps Script

## 🛠 Setup

1. **Create Google Sheet**
   - Add headers: `Name | Batch | Email | Phone | Profession`

2. **Apps Script**
   - Go to **Extensions > Apps Script**
   - Paste the code below:
     ```js
     function doPost(e) {
       var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
       var data = JSON.parse(e.postData.contents);
       sheet.appendRow([data.name, data.batch, data.email, data.phone, data.profession]);
       return ContentService.createTextOutput("Success").setMimeType(ContentService.MimeType.TEXT);
     }

     function doGet() {
       var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
       var data = sheet.getDataRange().getValues();
       var headers = data.shift();
       var result = data.map(row => {
         return {
           name: row[0],
           batch: row[1],
           email: row[2],
           phone: row[3],
           profession: row[4]
         };
       });
       return ContentService.createTextOutput(JSON.stringify(result))
         .setMimeType(ContentService.MimeType.JSON);
     }
     ```
   - Deploy as Web App:
     - Access: Anyone
     - Copy the deployment URL

3. **Frontend**
   - Replace `YOUR_SCRIPT_URL_HERE` in `index.html` with the Web App URL
   - Open `index.html` in your browser or deploy via GitHub Pages, Netlify, etc.

