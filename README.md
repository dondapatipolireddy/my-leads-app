# Meta Lead Ads + React Native PoC

A Proof of Concept that receives test leads from **Meta Lead Ads** through a webhook and displays them automatically in an already-open **React Native** application.

The project uses Meta's **Lead Testing Tool**, so no real advertising campaign is required.

## Problem Statement

When a user submits a Meta Lead Ad form, the submitted lead should appear in a React Native application's leads list without requiring the user to refresh the application or perform any manual action on the device.

## Architecture

```text
Meta Lead Testing Tool
          |
          | Test Lead Submission
          v
     Meta Webhook
          |
          | Webhook Notification
          v
 Node.js / Express Backend
          |
          | Lead ID
          v
     Meta Graph API
          |
          | Lead Details
          v
       Database
          |
          | New Lead Event
          v
      Socket.IO
          |
          | Real-time Event
          v
    React Native App
          |
          v
      Leads List
```

## How It Works

1. A test lead is submitted using Meta's Lead Testing Tool.
2. Meta sends a webhook notification to the backend.
3. The backend receives the webhook event and extracts the lead ID.
4. The backend uses the Meta Graph API to retrieve the lead details.
5. The lead information is stored in the database.
6. The backend sends a real-time event to the React Native application.
7. The React Native application receives the event and updates the leads list.
8. The new lead appears without manually refreshing or interacting with the device.

## Technologies Used

* React Native
* Node.js
* Express.js
* Meta Webhooks
* Meta Graph API
* Socket.IO
* MongoDB
* ngrok for exposing the local webhook endpoint during development

## Project Structure

```text
my-leads-app/
│
├── backend/
│   ├── ...
│   └── ...
│
├── mobile/
│   ├── ...
│   └── ...
│
├── README.md
└── ...
```

> Update the folder names above if your actual repository structure is different.

## Prerequisites

Before running the project, make sure you have:

* Node.js installed
* npm installed
* React Native development environment configured
* Android emulator or physical Android device
* MongoDB running, if MongoDB is used
* A Meta Developer account
* A Meta App configured for Lead Ads/Webhooks
* A Page connected to the Meta application
* Required Meta access tokens and permissions
* ngrok installed for local webhook testing

## Environment Variables

Create the required environment file for the backend.

Example:

```env
PORT=5000
MONGODB_URI=your_mongodb_connection_string

META_VERIFY_TOKEN=your_webhook_verify_token
META_ACCESS_TOKEN=your_meta_access_token
META_APP_SECRET=your_meta_app_secret

FRONTEND_URL=your_react_native_backend_url
```

Do not commit real access tokens, app secrets, passwords, or other credentials to GitHub.

Use `.gitignore` for files containing secrets.

## Running the Backend

Navigate to the backend directory:

```bash
cd backend
```

Install dependencies:

```bash
npm install
```

Start the backend:

```bash
npm start
```

The backend should run on the configured port, for example:

```text
http://localhost:5000
```

## Exposing the Webhook

Meta needs to access the webhook endpoint from the internet.

For local development, ngrok can be used:

```bash
ngrok http 5000
```

Copy the HTTPS forwarding URL provided by ngrok.

For example:

```text
https://xxxx.ngrok-free.app
```

Configure the corresponding webhook URL in the Meta Developer Dashboard.

Example:

```text
https://xxxx.ngrok-free.app/webhook
```

The exact endpoint should match the route implemented in the backend.

## Running the React Native App

Navigate to the React Native project:

```bash
cd mobile
```

Install dependencies:

```bash
npm install
```

Start the application using the command appropriate for the project.

For example:

```bash
npx react-native run-android
```

Keep the **Leads List** screen open.

## Meta Lead Testing

The project uses Meta's Lead Testing Tool to simulate lead submissions.

Testing flow:

```text
1. Start backend
       ↓
2. Start ngrok
       ↓
3. Start React Native app
       ↓
4. Open Leads List screen
       ↓
5. Open Meta Lead Testing Tool
       ↓
6. Submit a test lead
       ↓
7. Meta sends webhook notification
       ↓
8. Backend processes the lead
       ↓
9. React Native receives the real-time event
       ↓
10. Lead appears automatically
```

No manual refresh should be required on the React Native device.

## Webhook Verification

Meta requires webhook verification when configuring the webhook.

The backend implements the verification endpoint using the configured verification token.

The verification flow is:

```text
Meta
  |
  | GET verification request
  v
Backend webhook endpoint
  |
  | Verify token
  v
Verification response
```

After successful verification, Meta can send webhook events to the endpoint.

## Real-Time Updates

The React Native application maintains a connection with the backend for real-time lead updates.

When a new lead is successfully processed:

```text
Backend
   |
   | new-lead event
   v
Socket.IO
   |
   v
React Native
   |
   v
Update leads state
   |
   v
New lead displayed
```

This allows the application to update the screen without requiring the user to manually refresh it.

## Demo

The demonstration shows:

1. React Native application already open on the Leads List screen.
2. Meta Lead Testing Tool opened separately.
3. A test lead submitted through Meta.
4. The lead received by the backend.
5. The lead appearing automatically in the React Native application.
6. No manual action performed on the device after the submission.

## Assumptions

* Meta Developer App and required Lead Ads configuration are already set up.
* The required Meta permissions and access token are available.
* The Meta Lead Testing Tool is used instead of a real advertising campaign.
* The backend is exposed publicly during local testing using ngrok.
* The React Native application and backend are running before the test lead is submitted.
* Test data is used only for demonstration purposes.

## Security Notes

The following should never be committed to the repository:

* Meta access tokens
* Meta App Secret
* Database credentials
* Webhook secrets
* `.env` files containing sensitive values

Use environment variables for sensitive configuration.

## Official Documentation

* Meta Webhooks: https://developers.facebook.com/docs/graph-api/webhooks/
* Meta Lead Ads Webhooks: https://developers.facebook.com/docs/marketing-api/guides/lead-ads/webhooks/
* Meta Lead Testing: https://developers.facebook.com/docs/marketing-api/guides/lead-ads/testing/
* Meta Graph API: https://developers.facebook.com/docs/graph-api/

## Author

**Polireddy Dondapati**

This project was developed as a Proof of Concept for the Meta Lead Ads + React Native assignment.
 Expo users and ask questions.
