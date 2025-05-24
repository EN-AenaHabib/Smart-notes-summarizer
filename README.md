# Notes Summarizer Agent

## Overview

The **Notes Summarizer Agent** is an automated tool designed to help users capture and organize notes directly from any website. Using simple JavaScript bookmarklets, users can select text on a webpage and click **“Add Note”** to save it to a Google Docs draft. When ready, clicking **“Finalize Notes”** triggers an AI summarization that compiles all added notes into a concise summary and saves it into a finalized Google Docs document.

This workflow simplifies gathering research, lecture notes, or any web content, transforming it into well-organized, summarized documents for easy review.

---

## Features

* **Bookmarklets for Easy Note Taking**

  * *Add Note*: Select text on a webpage and add it to a Google Docs draft.
  * *Finalize Notes*: Summarizes all collected notes and saves the summary to a finalized Google Docs file.

* **AI-Powered Summarization**
  Uses Groq’s language model to generate concise, clear summaries from collected notes.

* **Seamless Google Docs Integration**
  Notes and summaries are saved directly into Google Docs for easy access and sharing.

* **Automated Workflow**
  Orchestrated through n8n for smooth, no-code automation.

---

## How It Works

1. **Add Notes**
   While browsing, users select important text and click the **Add Note** bookmarklet. The selected text is sent to the workflow and appended to a Google Docs draft document.

2. **Finalize Notes**
   When the user finishes collecting notes, clicking the **Finalize Notes** bookmarklet triggers the summarization process. The AI processes all notes, generates a summary, and writes the final summarized document to a separate Google Docs file.

3. **JavaScript Bookmarklets**
   Both bookmarklets are small JavaScript snippets saved as browser bookmarks. When clicked, they execute code that sends the selected text or command to the n8n workflow via HTTP requests.

---

## Technologies Used

* **n8n**: Automation platform that orchestrates the workflow.
* **Groq AI Model**: Generates natural language summaries.
* **Google Docs API**: Stores and updates notes and summaries.
* **JavaScript Bookmarklets**: User interface to add/finalize notes directly from the browser.

---

## Setup Instructions

1. **Install and configure n8n** on your server or local machine.
2. **Create Google Docs credentials** and link your Google account with n8n.
3. **Add Groq API credentials** for summarization.
4. **Import or build the workflow** in n8n to handle:

   * Receiving notes from bookmarklets
   * Appending notes to Google Docs draft
   * Summarizing notes and saving final doc
5. **Create the JavaScript bookmarklets** in your browser bookmarks bar using the provided scripts below.
6. **Test** by selecting text on any webpage and clicking the **Add Note** bookmarklet, then finalize with **Finalize Notes**.

---

## JavaScript Bookmarklets

Create new bookmarks in your browser and paste the following code as the bookmark URL.

### Add Note Bookmarklet

Select text on any webpage and click this bookmarklet to send the note to your Google Docs draft.

```javascript
javascript:(function(){   
  const selectedText = window.getSelection().toString().trim();   
  if (!selectedText) {     
    alert("Please select some text first.");     
    return;   
  }   
  fetch("https://YOUR N8N WORKFLOW LINK", {     
    method: "POST",     
    headers: {       
      "Content-Type": "application/json"     
    },     
    body: JSON.stringify({ note: selectedText })   
  })   
  .then(() => alert("Note sent to your Google Doc!"))   
  .catch(err => alert("Error: " + err)); 
})();
```

---

### Finalize Notes Bookmarklet

Click this bookmarklet to trigger the summarization process and save the final summary to a Google Docs document. After completion, it opens the finalized document in a new tab.

```javascript
javascript:(function() {   
  alert("⏳ Loading finalized notes, please wait...");    
  fetch("ADD LINK TO YOUR FINALIZE NOTE N8N WORKFLOW", { method: "POST" })     
    .then(() => {       
      alert("✅ Summary added to finalized note docx.\n\nClick OK to open the document.");       
      window.open("https://docs.google.com/YOUR DOCUMENT LINK", "_blank");     
    })     
    .catch(err => {       
      alert("❌ Error: " + err);       
      console.error(err);     
    }); 
})();
```

---

## Future Enhancements

* User authentication and multi-user support.
* Customizable summary length and style.
* Support for additional note sources like PDFs and emails.
* Integration with popular note-taking apps like Notion or Evernote.

---

## License

This project is licensed under the MIT License.

---
