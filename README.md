<div align="center">
  <picture>
    <source
      width=125
      media="(prefers-color-scheme: light), (prefers-color-scheme: no-preference)"
      srcset="images/logos/ion_logo_dark.jpg"
    />
    <source
      width=125
      media="(prefers-color-scheme: dark)"
      srcset="images/logos/ion_logo_light.jpg"
    />
    <img alt="Logo">
  </picture>
  <h1>
      Winter Break 2023 Project ☃️
  </h1>
  <p>
    This repository contains the source code for The Ion's automatic facial detection + recognition bot named Spud! We created a real-time, automatic facial detection and recognition system. This fusion of web development, AI, and physical computing delivers an innovative solution for seamless member tracking. As soon as someone walks into the room, our bot will log that into our database, and we're able to see that through a user-friendly interface on our website!
  </p>
</div>

# 📋 Todo

- Thomas's todo list:
  - Add loading skeleton on first loadup.
  - Add "no results" if table is empty.
  - Logs page:
    - Delete a log by clicking trash icon.
      - Are you sure confirmation alert before deleting log.
    - Pagination / records per page.
  - `/dashboard` allowing you to see both members and logs with a toggle.
  - Create models with getter.
  - Use JQuery.
  - Reponsive CSS:
    - Controls section.
    - Dark/light mode.
    - Reponsiveness w/ (r)ems.
  - Merging Khanh's branch:
    - Consolidate views and partials.
    - Mark inputs as reqiured in registration.
  - Include **SSH keys** + `creds.json` in `.gitignore` and remove from commit history.
  - Reset commits + branches after merging.
    - Reset about and tags.
    - Add social preview.
  - Compress all images.
  - Finalize `README.md`:
    - Add screenshots.
    - Add a video demo.
    - Delete this todo section once all other todos have been completed.

# 📸 Screenshots

[Add images of the actual, finalized website here]

# 🎬 Video Demo

[Add a quick video showing how our project works]

# 🌀 About

### Who We Are

We are a group of undergraduates studying at University of Houston (Go Coogs!) that want to apply our various skills to create an awesome project! Our goal was to combine web development, embedded systems, robotics, and AI into one large project and expand our working knowledge.

| <img width=150 src="images/people/thomas.jpg"> | <img width=150 src="images/people/khanh.jpg"> | <img width=150 src="images/people/diana.jpg"> |
| :--------------------------------------------: | :-------------------------------------------: | :-------------------------------------------: |
|                   **Thomas**                   |                   **Khanh**                   |                   **Diana**                   |
|                   (Back End)                   |                  (Front End)                  |             (Facial Recognition)              |

| <img width=150 src="images/people/matthew.jpg"> | <img width=150 src="images/people/sebastian.jpg"> | <img width=150 src="images/people/placeholder.jpg"> |
| :---------------------------------------------: | :-----------------------------------------------: | :-------------------------------------------------: |
|                   **Matthew**                   |                   **Sebastian**                   |                     **Someone**                     |
|               (Facial Detection)                |                 (Docker/Database)                 |                       (Role)                        |

# 🛠️ Tools & Technologies

- **Web**: Node.JS, Express.JS, Socket.io, Google Cloud Platform.
- **Database**: MySQL.
- **AI**: Python, OpenCV.
- **Physical**: Jetson Nano, ESP32.

# 💻 Running Website Locally

> [!IMPORTANT]
> Make sure you're inside the root directory of the project first.

```bash
cd website      # Move into the `website` directory
npm install -y  # Install all dependencies locally
npm run start   # Run the website
```

# 📡 API Documentation

### Conventions

> [!NOTE]
>
> - Colon means variable.
> - Question mark means optional.

### Members Endpoints

| Method | Endpoint              | Description                                                                                                | Required Payload Data                                   |
| :----- | :-------------------- | :--------------------------------------------------------------------------------------------------------- | :------------------------------------------------------ |
| `GET`  | `/api/testmembers`    | Retrieve all registered members' details and supplement with additional fake members for testing purposes. |                                                         |
| `GET`  | `/api/members/:psid?` | Retrieve all registered members' details. Optionally include a PSID to get details of a specific member.   |                                                         |
| `POST` | `/api/members`        | Register a new member into database.                                                                       | `psid`, `email`, `password`, `first`, `last`, `discord` |

### Logs Endpoints

| Method   | Endpoint           | Description                                                                                                                                                              | Required Payload Data |
| :------- | :----------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------- |
| `GET`    | `/api/testlogs`    | Retrieve all logs and supplement with fake logs for testing purposes. Timestamps of the fake logs are guarenteed to be older than the oldest timestamp of the real data. |                       |
| `GET`    | `/api/logs/:psid?` | Retrieve all logs. Optionally include a PSID to get logs for a specific member.                                                                                          |                       |
| `POST`   | `/api/logs`        | Insert a log into database by PSID. Member must be registered beforehand.                                                                                                | `psid`                |
| `DELETE` | `/api/logs/:id`    | Delete a log by its log ID (not PSID).                                                                                                                                   |                       |

<details>
  <summary>
    <h3>API Examples (cURL)</h3>
  </summary>

```bash
# Register new member
curl -X POST http://localhost:8000/api/members \
  -d "psid=1234567" \
  -d "email=test@user.com" \
  -d "password=password" \
  -d "first=Test" \
  -d "last=User" \
  -d "discord=test_user"

# Find member with a PSID of 1234567
curl http://localhost:8000/api/members/1234567

# Log a member with a PSID of 1234567
curl -X POST http://localhost:8000/api/logs -d "psid=1234567"

# Retrieve all logs
curl http://localhost:8000/api/logs

# Delete a log with an ID of 20
curl -X DELETE http://localhost:8000/api/logs/20
```

</details>

<details>
  <summary>
    <h3>API Examples (Python)</h3>
  </summary>

```python
from pprint import pprint
import requests

# Register new member
requests.post(
    "http://localhost:8000/api/members",
    data={
        "psid": 1234567,
        "email": "test@user.com",
        "password": "password",
        "first": "Test",
        "last": "User",
        "discord": "test_user",
    },
)

# Find member with a PSID of 1234567
r = requests.get("http://localhost:8000/api/members/1234567")
pprint(r.json())

# Log a member with a PSID of 1234567
requests.post(
    "http://localhost:8000/api/logs",
    data={"psid": 1234567},
)

# Retreive all logs
r = requests.get("http://localhost:8000/api/logs")
pprint(r.json())

# Delete a log with an ID of 20
requests.delete("http://localhost:8000/api/logs/20")
```

</details>

<details>
  <summary>
    <h3>API Examples (JavaScript)</h3>
  </summary>

```js
// Register new member
fetch("http://localhost:8000/api/members", {
  method: "POST",
  headers: {
    "Content-Type": "application/x-www-form-urlencoded",
  },
  body: new URLSearchParams({
    psid: 1234567,
    email: "test@user.com",
    password: "password",
    first: "Test",
    last: "User",
    discord: "test_user",
  }),
});

// Find member with a PSID of 1234567
fetch("http://localhost:8000/api/members/1234567")
  .then((response) => response.json())
  .then((data) => console.log(data));

// Log a member with a PSID of 1234567
fetch("http://localhost:8000/api/logs", {
  method: "POST",
  headers: {
    "Content-Type": "application/x-www-form-urlencoded",
  },
  body: new URLSearchParams({
    psid: 1234567,
  }),
});

// Retrieve all logs
fetch("http://localhost:8000/api/logs")
  .then((response) => response.json())
  .then((data) => console.log(data));

// Delete a log with an ID of 20
fetch("http://localhost:8000/api/logs/20", {
  method: "DELETE",
});
```

</details>

# 🚀 Future Plans

As we look ahead, our team envisions exciting expansions and enhancements for this project! Our commitment to innovation drives us to explore new features and improvements to elevate functionality. Here are some of the future plans on our roadmap:

- **Enhanced User Interface**: We plan to refine and optimize the user interface for a more seamless and modern experience.
- **Real-time Analytics**: Implementing real-time analytics to provide insights into member activity, trends, and overall system performance.
- **Machine Learning Integration**: Exploring the integration of machine learning algorithms to enhance facial recognition accuracy and adaptability.
- **Mobile Application**: Developing a dedicated mobile application for on-the-go access to member logs, notifications, and system controls.
- **Security Enhancements**: Continuously improving security measures to ensure the integrity of member data and our servers.

These plans reflect our ongoing commitment to pushing the boundaries of technology and delivering a robust and cutting-edge solution. Stay tuned for exciting updates as we evolve Spud into an even more powerful and feature-rich robot!
