---
layout: page
title: Chat Buddy — Real-Time Communication App
description: Cross-platform group chat, voice, and video calling app built with Flutter and Firebase.
img: assets/img/chatbuddy.png   # optional preview image for project grid
importance: 6
category: Flutter and Firebase Mobile Applications
links:
  - name: code
    url: https://github.com/Chava-Sai/Chat-Buddy
---

## Overview
**Chat Buddy** is a real-time chat and collaboration app built using **Flutter**, **Firebase**, and **Zego Cloud**.  
It enables seamless communication through **group chats**, **voice**, and **video calls** — designed with role differentiation for admins and students, ensuring privacy, simplicity, and a great user experience.

<div class="text-center my-3">
  <img src="{{ 'assets/img/chatbuddy.png' | relative_url }}" alt="Chat Buddy App" class="img-fluid rounded z-depth-1" width="600" loading="lazy">
</div>

---

## Features
- 💬 **Instant Messaging** — Dynamic group chat with live message updates via Firestore.  
- 🎥 **Video & Voice Calls** — High-quality calls using **Zego Cloud SDK**.  
- 👥 **Role Differentiation** — Admins manage groups; students communicate within assigned spaces.  
- 🔐 **Secure Authentication** — Firebase-based login, sign-up, and password recovery.  
- ⚙️ **Group Management** — View members, create or exit groups, and moderate activity.  
- 🌐 **Cross-Platform** — Runs smoothly on Android and iOS.

---

## Screenshots
<table>
  <tr>
    <td align="center"><strong>Login Screen</strong><br><img src="https://github.com/Chava-Sai/Chat-Buddy/assets/129037829/3626916d-c15e-4387-b58f-92816cb675f3" width="380"></td>
    <td align="center"><strong>Signup</strong><br><img src="https://github.com/Chava-Sai/Chat-Buddy/assets/129037829/1b6fb915-2729-4892-9277-b4e8fea64cd9" width="380"></td>
  </tr>
  <tr>
    <td align="center"><strong>Home Screen</strong><br><img src="https://github.com/Chava-Sai/Chat-Buddy/assets/129037829/0e459464-7683-49ff-988b-9dc3743cc14d" width="380"></td>
    <td align="center"><strong>Group Chat</strong><br><img src="https://github.com/Chava-Sai/Chat-Buddy/assets/129037829/de44c93e-77d9-4c17-97f8-726ec3ec1be5" width="380"></td>
  </tr>
  <tr>
    <td align="center"><strong>Audio Call</strong><br><img src="https://github.com/Chava-Sai/Chat-Buddy/assets/129037829/21e88f05-93e4-43cd-ad00-ffd1241a131a" width="380"></td>
    <td align="center"><strong>Video Call</strong><br><img src="https://github.com/Chava-Sai/Chat-Buddy/assets/129037829/466e9b56-c25c-4e5e-baab-bd52becdef01" width="380"></td>
  </tr>
</table>

---

## Technology Stack
| Layer | Technologies Used |
|:------|:------------------|
| **Frontend** | Flutter |
| **Backend** | Firebase (Authentication, Firestore) |
| **Realtime Calls** | Zego Cloud SDK |
| **Storage & State** | Shared Preferences, Firestore Streams |
| **HTTP Requests** | Flutter `http` package |

---

## Installation

```bash
# Clone the repository
git clone https://github.com/Chava-Sai/Chat-Buddy.git
cd Chat-Buddy
```

## Install dependencies

```bash
flutter pub get
```

## Run the app

```bash
flutter run
```

> 💡 **Before running:** add your Firebase configuration for both **Android** and **iOS** (Google Services files).

---

## Authentication

Chat Buddy uses **Firebase Authentication** for secure, role-based access.

| Role            | Access                                      |
|-----------------|---------------------------------------------|
| **Admin**       | Create & manage groups, moderate users      |
| **Student**     | Join groups, chat, and make calls           |
| **Forgot Password** | Reset via Firebase email recovery          |

---

## Integration

### Firebase Firestore
- **Users** collection: stores user info, groups, and IDs.  
- **Groups** collection: manages messages and membership data.

### Zego Cloud
Integrated via **Zego Cloud SDK** for voice and video calls, using Flutter plugins for API communication and session control.

---

## Widgets & UI Components
- Custom chat bubbles with dynamic alignment  
- `StreamBuilder` widgets for live Firestore updates  
- Integrated media buttons for call/chat toggles  
- Profile, settings, and group-info screens with persistent state management

---

## Future Enhancements
- 🧩 Push notifications via **Firebase Cloud Messaging (FCM)**
- 💾 Offline chat caching with **Hive**
- 📱 Typing indicators & message delivery status
- 🌙 Dark mode and adaptive theming for accessibility

---

## Contributors
- **Developer:** Srinivasa Sai Chava  
- **Repo:** [Chat-Buddy on GitHub](https://github.com/Chava-Sai/Chat-Buddy)

---

> “Let’s chat, connect, and build communities with privacy and purpose.”