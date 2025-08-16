# Awesome Kartikey Music Player

A simple, clean, and functional web-based music player built with HTML, CSS, and Vanilla JavaScript.

![Music Player Screenshot](https://iamkartikey.vercel.app/project-screenshots/joke-teller.png)

## Description

This project is a front-end music player application that allows users to play a predefined list of songs. It features basic controls like play, pause, next, and previous, along with a progress bar to track and seek through the currently playing song.

## Features

- **Playback Controls:** Play, Pause.
- **Track Navigation:** Next and Previous song functionality.
- **Progress Bar:** Displays song progress and allows seeking.
- **Time Display:** Shows current playback time and total song duration.
- **Dynamic UI Updates:** Updates song title, artist, and album art dynamically.
- **Auto-Play Next:** Automatically plays the next song when the current one finishes.
- **Simple & Clean UI:** Minimalist design.

## Tech Stack

- **HTML5:** For structuring the web page.
- **CSS3:** For styling the player interface, including responsive design for smaller screens.
- **Vanilla JavaScript:** For handling player logic, DOM manipulation, and event handling.
- **Font Awesome:** For player control icons.

## Setup Instructions

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/awesome-kartikey/music-player.git
    cd music-player
    ```
2.  **Ensure you have the necessary assets:**
    - Place your music files (MP3 format recommended) inside the `music/` directory.
    - Place the corresponding album art images (JPG format recommended) inside the `img/` directory.
    - **Important:** The JavaScript code (`script.js`) expects the audio file and image file for a song to have the same base name (e.g., `song-1.mp3` and `song-1.jpg`). You'll need to update the `songs` array in `script.js` to match your filenames and desired display names/artists.
    ```javascript
    // Example entry in script.js
    const songs = [
      {
        name: "your-song-filename-base", // e.g., 'my-track-1' for 'my-track-1.mp3' and 'my-track-1.jpg'
        displayName: "Your Song Title",
        artist: "Your Artist Name",
      },
      // ... add more songs
    ];
    ```
3.  **Open the application:**
    - Simply open the `index.html` file in your web browser. No build step or server is required for basic functionality.

## Usage

- Click the **Play** button (<i class="fas fa-play"></i>) to start playing the current song.
- Click the **Pause** button (<i class="fas fa-pause"></i>) to pause the current song.
- Click the **Next** button (<i class="fas fa-forward"></i>) to skip to the next song in the playlist.
- Click the **Previous** button (<i class="fas fa-backward"></i>) to go back to the previous song.
- Click anywhere on the **progress bar** to jump to that specific point in the song.
- The player will automatically proceed to the next song when the current one finishes.
