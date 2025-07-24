# Android Messages Desktop

**Android Messages Desktop** is an Electron wrapper for [Google Messages for Web](https://messages.google.com/web/), allowing you to use Android Messages as a standalone desktop app on Linux.

## Features

- Native desktop window
- Tray icon with menu
- Minimize to tray
- System notifications
- Opens links in your default browser
- Single instance lock
- Application icon and launcher integration

## Installation

### Build and run locally

1. Clone this repository:
    ```sh
    git clone https://github.com/yourname/android-messages-desktop.git
    cd android-messages-desktop
    ```

2. Install dependencies:
    ```sh
    npm install
    ```

3. Start the app:
    ```sh
    npm start
    ```

### Build native package

To build a distributable AppImage or native package:

```sh
npm run dist
