// Gmail to CRM Automation Script
// Extracts leads (name, email, phone) from emails and sends them to a CRM via webhook

const CONFIG = {
  GHL_WEBHOOK_URL: 'YOUR_WEBHOOK_URL', // hidden for security
  LABEL_PROCESSED: 'GHL_Processed',
  MAX_THREADS: 200
};

function runOnce() {
  processLeads_();
}

function processLeads_() {
  Logger.log("Starting processLeads...");

  const labelProcessed = getOrCreateLabel_(CONFIG.LABEL_PROCESSED);

  const threads = GmailApp.search("-label:" + CONFIG.LABEL_PROCESSED, 0, CONFIG.MAX_THREADS);
  Logger.log("Threads found: " + threads.length);

  threads.forEach(thread => {

    const messages = thread.getMessages();

    messages.forEach(message => {

      const from = message.getFrom();
      const body = message.getPlainBody();
      const subject = message.getSubject();

      Logger.log("Processing email from: " + from);

      // Extract phone number
      const phoneMatch = body.match(/(\+?\d{10,})/);
      const phone = phoneMatch ? phoneMatch[0] : "";

      // Extract email
      const emailMatch = body.match(/[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}/i);
      const email = emailMatch ? emailMatch[0] : "";

      // Extract name (basic pattern)
      let firstName = "";
      let lastName = "";

      const nameMatch = body.match(/Name[:\-]\s*([A-Za-z]+)\s*([A-Za-z]*)/i);
      if (nameMatch) {
        firstName = nameMatch[1] || "";
        lastName = nameMatch[2] || "";
      }

      const lead = {
        firstName: firstName,
        lastName: lastName,
        email: email,
        phone: phone
      };

      Logger.log("Extracted lead: " + JSON.stringify(lead));

      // Always label email as processed
      thread.addLabel(labelProcessed);

      // Only send leads from specific source (example: homes.com)
      if (from.toLowerCase().includes("homes.com")) {

        // Only send if valid contact info exists
        if (phone || email) {

          const response = UrlFetchApp.fetch(CONFIG.GHL_WEBHOOK_URL, {
            method: "post",
            contentType: "application/json",
            payload: JSON.stringify(lead)
          });

          Logger.log("Webhook response: " + response.getResponseCode());
          Logger.log("Lead sent successfully.");

        } else {
          Logger.log("Skipped lead — no phone or email.");
        }

      } else {
        Logger.log("Not target source — no contact created.");
      }

    });

  });

  Logger.log("Process finished.");
}

function getOrCreateLabel_(name) {
  let label = GmailApp.getUserLabelByName(name);
  if (!label) {
    label = GmailApp.createLabel(name);
  }
  return label;
}
