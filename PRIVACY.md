# Privacy Policy — ControlX

**Last Updated:** November 18, 2026

## 1. Introduction

Welcome to **ControlX** ("we," "our," or "the project"). ControlX is an open-source, experimental mixed-reality (MR) and AI agent application built for the Meta Global AI Developer Hackathon. It enables users to tag physical objects in passthrough video, generate device connectors via an AI coding agent on a companion computer, and interact with hardware or software using spatial AR/VR controls or hand gestures.

Because ControlX interacts with headset cameras, microphones, hand-tracking sensors, local OS terminals, and external AI models, this Privacy Policy explains what data is accessed, how it is processed, and how you retain control over your information.

---

## 2. Modes of Operation: LIVE vs. FIXTURE

ControlX operates in two distinct modes that govern whether external network calls are made:

* **FIXTURE Mode (Default without an API key):** No data is sent to external AI model APIs. All model responses, object outlines, and agent scripts are replayed locally from recorded fixtures.
* **LIVE Mode (Requires `MODEL_API_KEY`):** Your local Node server communicates with the **Meta Model API** to perform object segmentation, voice transcription, agentic code generation, and image creation.

---

## 3. Information We Access and Process

Depending on the features you use across the Quest headset, web camera mode (`/quest/hands.html`), and Mac companion server, ControlX processes the following categories of data:

### A. Camera and Passthrough Video Frames
* **Object Detection & Verification:** When running in AR/passthrough or webcam mode, ControlX captures camera frames (`getUserMedia`) to identify and outline objects using **SAM 3.1** (`sam-3.1`) and to perform deterministic before/after pixel verification inside object bounding boxes.
* **Muse Buddy Photo Sharing:** In the optional *Buddy* feature, capturing a real-world object displays a local preview first. The image is **only** transmitted to Meta's models (`muse-spark-1.3`) if you explicitly select **Show Buddy**; selecting **Retake** discards the image locally.
* **QR Pairing:** Camera frames are decoded locally in the browser using `jsQR` to pair your headset with your Mac companion.

### B. Hand, Head, and Spatial Pose Data
* **Real-Time Interaction:** ControlX reads skeletal joint poses (WebXR Hand Input API) and head poses to drive UI gestures, screen-touch planes, and generated hand-wiring scripts. On desktop/mobile webcams (`/quest/hands.html`), hand tracking uses classical computer vision locally in a Web Worker without calling external AI models.
* **Physical-AI Recording (Motion Lab):** If you explicitly activate recording (e.g., via `?lab=1` or the emulator panel), ControlX records passthrough video alongside head and 25-joint hand pose data at up to 30 Hz. These recordings are stored locally so you can review them in **Motion lab** (`/companion/tracking/`) and export datasets at your discretion.

### C. Voice and Audio Data
* **Voice Commands:** When you use the hold-to-talk button to issue a wiring request, audio clips are sent to **Muse Voice Transcribe** (`muse-voice-transcribe-1.0`) in LIVE mode to convert your speech into text prompts.
* **Text-to-Speech:** Spoken progress updates and companion replies are generated using local OS/browser speech synthesis (macOS speech, iOS `AVSpeechSynthesizer`, or browser `speechSynthesis`).

### D. Local System, Workspace, and Device Data
* **Muse Agent Execution:** When running on your Mac, the Muse agent (`muse-spark-1.3` or opt-in `muse-code`) has access to a local workspace (`apps/server/.data/muse-agent/`) and a `bash` tool operating with your macOS user account's permissions to write, test, and run device connectors.
* **Connected Peripherals:** ControlX communicates locally with devices reachable by your computer or browser over USB-MIDI, Web Serial, Web Bluetooth / BLE (e.g., DJI Osmo Mobile 4), local network HTTP, or macOS Accessibility APIs (e.g., keyboard events for scrolling browser tabs).
* **API Keys:** Your `MODEL_API_KEY` is stored locally in your `.env` file on the server and is stripped from payloads sent to client interfaces.

---

## 4. Data Storage, Logs, and Retention

ControlX is designed as a self-hosted local-first prototype. We do not operate a central cloud backend to collect your personal data.

* **Local Telemetry & Logs:** During operation, your local server logs model call metadata (model ID, latency, token counts) at `/api/muse/calls` and active agent connectors/logs at `/api/agent/connectors`. These endpoints are restricted to `localhost` or paired devices on your trusted local network.
* **Persistent Agent Workspace:** Generated connectors (`connectors/<device>/index.mjs`) and agent notes (`NOTES.md`) remain on your local disk in `apps/server/.data/muse-agent/` until you delete them.
* **No User Accounts or Tracking:** ControlX does not require user registration and does not use third-party advertising cookies or behavioral analytics trackers.

---

## 5. Third-Party Services

When running in **LIVE** mode with your own API credentials, prompts, object crops/snapshots, and voice recordings are transmitted to **Meta's Model API** (including `sam-3.1`, `muse-spark-1.3`, `muse-wonder-1.0`, `muse-image-1.0`, and `muse-voice-transcribe-1.0`). Data sent to these endpoints is governed by Meta's applicable API Terms of Service and Privacy Policy.

ControlX does not call or bundle any non-Meta AI models at runtime.

---

## 6. Security Considerations

Because ControlX is a developer prototype capable of executing AI-generated code on your host machine:
* **Trusted Networks Only:** Run the server (`:8787` / `:8443`) only on trusted local networks with your own hardware.
* **OS Permissions:** Features such as macOS Accessibility control (for sending keystrokes) and USB-MIDI/Bluetooth access require explicit system-level permission grants from you.
* **Sandboxed Headset Code:** Generated hand-wiring programs run inside a restricted Web Worker on the headset with value clamping, rate limiting, and watchdog timeouts.

---

## 7. Children's Privacy

ControlX is an experimental developer tool and is not intended for use by children under the age of 13 (or the applicable age of digital consent in your jurisdiction). We do not knowingly collect personal data from children.

---

## 8. Changes to This Policy

As ControlX evolves, we may update this Privacy Policy to reflect new features, device adapters, or model integrations. Updates will be committed directly to the project repository.

---

## 9. Contact and Source Code

ControlX is an independent open-source project licensed under the MIT License and is not affiliated with or endorsed by Meta, DJI, Teenage Engineering, or Apple.

For questions, bug reports, or privacy inquiries, please open an issue on the official GitHub repository:
* **Repository:** <https://github.com/puspamadak/control-x>
