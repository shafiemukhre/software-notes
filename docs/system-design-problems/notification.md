---
sidebar_position: 90
---

# Design a notification system

## Skeleton Summary

Step 1

- Ask questions on types of notifications, whether it's real-time, supported devices, notifications triggered by what, user opt-out feature, and how many notifications a day.

Step 2: High-level design

- **Different types of notifications**: iOS uses APNS (Apple Push Notification Service), Android uses FCM (Firebase Cloud Messaging), SMS uses SMS services like Twilio/Nexmo, and email uses commercial email services like Sendgrid/Mailchimp.
- Flow 1: **Contact info gathering flow**: store phone numbers and email addresses in the _user_ table and mobile device token in the _device_token_ table in the database.
- Flow 2: **Notification sending/receiving flow**. (High-level design diagram). Identify problems and propose solutions:
  - Problem: SPOF (single point of failure) if there's only one notification server. -> Solution: Have multiple notification servers and set up automatic horizontal scaling.
  - Message Queue
  - Cache between DB and Notification services

Step 3: Design deep dive

- **Reliability**:
  - Persist notification data in a database and implement a retry mechanism to prevent the notification system from losing any data.
  - Introduce a dedupe mechanism to handle duplicate notifications in a distributed environment.
- **Additional components and considerations**: notification template, notification settings, rate limiting, retry mechanism, security in push notifications, monitor queued notifications, and event tracking.
