# AirBallot 🗳️ 

**The Zero-Backend, Offline-Persistent Electronic Voting Machine (EVM).**

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![Vanilla JS](https://img.shields.io/badge/Vanilla_JS-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Zero Server](https://img.shields.io/badge/Backend-NONE-dc3545?style=for-the-badge)
![License: MIT](https://img.shields.io/badge/License-MIT-success?style=for-the-badge)

AirBallot is a fully functional, production-ready Electronic Voting Suite built entirely in standard HTML, CSS, and Vanilla JavaScript. 

It is designed specifically for **secure, single-terminal kiosk environments** (like a school computer lab or a local club election) where data must remain strictly on the local machine without ever touching the internet.

### 🧠 The Engineering Challenge
Traditionally, web browsers are strictly sandboxed. An HTML file cannot automatically write a user's vote to a physical file on a hard drive without prompting the user to "Download" a new file every single time. To build a voting machine that saves data instantly, developers normally have to spin up a background server (Node.js, Python, PHP) to handle the file writing.

**AirBallot bypasses this completely.**

### ⚙️ How AirBallot Works (The "Shared Memory" Bridge)
AirBallot achieves true "Serverless Local Persistence" by bridging two native browser APIs:
1. **The Web File System Access API:** When the Admin initializes the system, they grant the browser a one-time secure read/write lock on the local election folder.
2. **IndexedDB:** AirBallot captures that `FileSystemDirectoryHandle` and tucks it deep into the browser's internal IndexedDB memory.
3. **Multi-Tab Syncing:** When the separate *Voting Booth* or *Live Results* tabs are opened, they don't need to ask the user for folder permission again. They silently reach into IndexedDB, retrieve the active directory handle, and instantly sync with the master `database.txt` file.

The result is a lightning-fast, multi-page web application that live-edits a physical hard drive with zero backend infrastructure.

---

## ✨ Comprehensive Feature List

### 🗳️ The Voting Kiosk (`voting.html`)
* **Continuous Voting Flow:** Designed for high-throughput lines. Once a vote is cast, a success overlay flashes, and the UI instantly resets to the active ballot for the next voter. No navigating back to home menus.
* **Strict Anti-Scroll UI:** Dynamic CSS grid-scaling calculates the number of candidates (from 2 to 10+) and automatically resizes the candidate cards (Huge, Large, Medium, Small) to guarantee the ballot never requires scrolling.
* **Hardware Audio Synthesizer:** Uses the native browser `AudioContext` to generate loud, piercing electronic confirmation "beeps" using mathematical square waves, bypassing the need for external `.mp3` files.
* **1-Tap vs. 2-Tap Security:** Administrators can toggle the booth between "Instant Tap" (maximum speed) or "Requires OK Confirmation" (prevents accidental screen taps).

### 📊 The Projector Screen (`results.html`)
* **Suspense Reveal Mechanics:** Vote counts are hidden behind a `???` blur until the Admin clicks "Reveal," which drops a massive Winner Banner and animates the progress bars.
* **Client-Side Canvas Rendering:** Features a built-in report generator that uses an invisible HTML5 `<canvas>` to instantly draw high-resolution tally sheets and export them as physical `.png` images directly into the local `/results` folder.

### ⚙️ The Admin Suite (`admin.html`)
* **Live Kill-Switches:** The Master PIN allows admins to instantly pause or unlock the active voting booths remotely.
* **Granular Database Controls:** Admins can edit candidate names/photos on the fly, wipe votes to zero for a *specific class* without affecting others, or trigger a total factory reset.
* **Offline Media Handling:** Candidate photos are sourced locally from a `src/` folder, ensuring the UI remains beautiful even on air-gapped, internet-free computers.
* **Data Backups:** 1-click JSON backup downloads to secure data mid-election.
