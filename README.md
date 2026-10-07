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
 Node.js / Express Backend
          |
          | Real-time Event
          v
       Socket.IO
          |
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
5. The backend processes the received lead information.
6. The backend sends the new lead to the React Native application using Socket.IO.
7. The React Native application receives the event and updates its leads list.
8. The new lead appears automatically without manually refreshing or interacting with the device.

## Technologies Used

* React Native
* Node.js
* Express.js
* Meta Webhooks
* Meta Graph API
* Socket.IO
* ngrok for local webhook testing

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

> Update the folder names above according to the actual repository structure.

## Prerequisites

* Node.js
* npm
* React Native development environment
* Android emulator or physical Android device
* Meta Developer account
* Meta App configured for Lead Ads/Webhooks
* Meta access token and required permissions
* ngrok

## Environment Variables

Create a `.env` file in the backend if your implementation uses environment variables.

Example:

```env
PORT=5000
META_VERIFY_TOKEN=your_webhook_verify_token
META_ACCESS_TOKEN=your_meta_access_token
META_APP_SECRET=your_meta_app_secret
```

**Do not commit real credentials or access tokens to GitHub.**

Add `.env` to `.gitignore`.

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

The backend should run on the configured port.

For example:

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

Configure the webhook URL in the Meta Developer Dashboard.

For example:

```text
https://your-ngrok-url.ngrok-free.app/webhook
```

Use the exact webhook path implemented in the backend.

## Running the React Native App

Navigate to your React Native project:

```bash
cd mobile
```

Install dependencies:

```bash
npm install
```

Run the application using the command appropriate for your project.

For example:

```bash
npx react-native run-android
```

Keep the **Leads List** screen open.

## Meta Lead Testing

The project uses Meta's Lead Testing Tool to simulate lead submissions.

### Testing Flow

```text
1. Start the backend
          ↓
2. Start ngrok
          ↓
3. Start React Native app
          ↓
4. Open the Leads List screen
          ↓
5. Open Meta Lead Testing Tool
          ↓
6. Submit a test lead
          ↓
7. Meta sends webhook notification
          ↓
8. Backend receives the notification
          ↓
9. Backend retrieves lead details
          ↓
10. Socket.IO sends the lead to React Native
          ↓
11. Lead appears automatically
```

No manual refresh or interaction is required on the React Native device.

## Webhook Verification

Meta requires webhook verification when configuring the webhook.

The backend implements the verification endpoint using the configured verification token.

The basic flow is:

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

After successful verification, Meta can send webhook events to the backend.

## Real-Time Updates

Socket.IO is used to send the newly received lead from the backend to the React Native application.

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
   | Update application state
   v
Leads List
```

This allows the React Native screen to update automatically without requiring a manual refresh.

## Demo

The Loom demonstration shows:

1. React Native application already open on the Leads List screen.
2. Meta Lead Testing Tool opened separately.
3. A test lead submitted through Meta.
4. Meta sending the webhook notification.
5. Backend processing the lead.
6. Lead appearing automatically in the React Native application.
7. No manual action performed on the device.

## Assumptions

* Meta Developer App and required Lead Ads configuration are already set up.
* Required Meta permissions and access token are available.
* Meta's Lead Testing Tool is used instead of a real advertising campaign.
* ngrok is used to expose the local webhook endpoint during development.
* The backend and React Native application are running before submitting the test lead.
* Test data is used for demonstration purposes.

## Security

Do not commit the following to GitHub:

* Meta access tokens
* Meta App Secret
* Webhook verification tokens
* `.env` files containing sensitive values

Use environment variables for sensitive configuration.

## Official Documentation

* [Meta Webhooks](https://developers.facebook.com/docs/graph-api/webhooks/)
* [Meta Lead Ads Webhooks](https://developers.facebook.com/docs/marketing-api/guides/lead-ads/webhooks/)
* [Meta Lead Testing](https://developers.facebook.com/docs/marketing-api/guides/lead-ads/testing/)
* [Meta Graph API](https://developers.facebook.com/docs/graph-api/)

## Author

**Polireddy Dondapati**

This project was developed as a Proof of Concept for the Meta Lead Ads + React Native assignment.
