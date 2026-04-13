<div align="center">

🌐 DevBrowse

The Blazingly Fast, Ultra-Lightweight Developer Browser

Report Bug · Request Feature

</div>

⚡ Why DevBrowse?

Frontend developers shouldn't have to sacrifice gigabytes of RAM just to test responsiveness.

While traditional developer browsers (like Sizzy or Polypane) rely on heavy Electron instances, or web-based tools rely on buggy <iframe> hacks that get blocked by CORS and X-Frame-Options, DevBrowse takes a radically different approach.

Built on top of Tauri v2, DevBrowse uses your operating system's Native Webviews (Edge WebView2, WebKit, or WebKitGTK). The result? A true 1-to-1 rendering experience, zero CORS issues, and a memory footprint that is a fraction of what Electron requires.

✨ Key Features (MVP)

📱 Multi-Device Testing: Render mobile (iPhone) and tablet (iPad) views simultaneously in a single window.

🚀 Native Performance: Written in Rust and Svelte for near-instant startup times and minimal resource usage.

🛡️ Zero CORS / Iframe Restrictions: By using OS-level WebviewWindows, DevBrowse bypasses all web security headers that typically block UI testing tools.

🎨 Distraction-Free UI: A minimalist, developer-focused interface powered by TailwindCSS.

🛠️ Tech Stack

Frontend: SvelteKit + TailwindCSS

Backend / Window Manager: Tauri v2 + Rust

Rendering Engine: OS Native Webview API

🚀 Getting Started

Prerequisites

Before you begin, ensure you have the following installed:

Node.js (v18 or higher)

Rust & Cargo

Linux Users only: You will need to install webkit2gtk and other Tauri dependencies. See Tauri Docs.

Installation

Clone the repository

git clone [https://github.com/your-username/dev-browser.git](https://github.com/your-username/dev-browser.git)
cd dev-browser


Install frontend dependencies

npm install


Run in development mode

npm run tauri dev


Note: The first compilation might take a few minutes as Rust downloads and builds the core dependencies.

🗺️ Roadmap

DevBrowse is actively under development. Here's what is coming next:

[ ] Synchronized Interactions: Sync scroll, click, and hover events across all device webviews simultaneously.

[ ] Custom Devices: Allow users to add/edit custom screen dimensions and user-agents.

[ ] One-Click Screenshots: Capture full-page screenshots of all active webviews.

[ ] DevTools Integration: Dedicated inspector/console for each viewport.

🤝 Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are greatly appreciated.

Fork the Project

Create your Feature Branch (git checkout -b feature/AmazingFeature)

Commit your Changes (git commit -m 'Add some AmazingFeature')

Push to the Branch (git push origin feature/AmazingFeature)

Open a Pull Request

💖 Support the Project

If DevBrowse saves you hours of responsive debugging, consider buying me a coffee to help keep the project alive and actively maintained!

<a href="https://www.google.com/search?q=https://www.buymeacoffee.com/your-username" target="_blank"><img src="https://www.google.com/search?q=https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 50px !important;width: 200px !important;" ></a>

📄 License

Distributed under the MIT License. See LICENSE for more information.