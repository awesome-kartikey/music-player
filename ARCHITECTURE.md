# Awesome Kartikey Music Player Architecture

## 1. Introduction

This document outlines the architecture of the Awesome Kartikey Music Player. It is a client-side web application designed to play a predefined list of audio tracks within a web browser. Its simplicity is a key characteristic, relying solely on standard web technologies (HTML, CSS, JavaScript) without external frameworks or backend infrastructure.

## 2. System Architecture

The music player follows a very simple **client-side architecture**. All components (structure, styling, logic, assets) reside within the user's browser after loading the `index.html` page.

- **Presentation Layer:** Managed by HTML (`index.html`) for structure and CSS (`style.css`) for visual presentation and layout.
- **Logic Layer:** Handled entirely by Vanilla JavaScript (`script.js`), responsible for user interactions, audio playback control, and dynamic UI updates.
- **Data Layer:** Consists of static assets - audio files (`music/`) and images (`img/`), along with a hardcoded JavaScript array (`songs` in `script.js`) that acts as the playlist metadata source.

There is **no server-side component** involved in the core functionality.

## 3. Folder Structure

The project uses a flat and straightforward directory structure:

```
music-player/
│
├── index.html          # Main HTML file defining the player structure
├── script.js           # JavaScript file containing all player logic
├── style.css           # CSS file for styling the player
│
├── img/                # Directory containing album art images
│   ├── jacinto-1.jpg
│   ├── jacinto-2.jpg
│   └── ... (other images, filenames match music files)
│
└── music/              # Directory containing audio tracks
    ├── jacinto-1.mp3
    ├── jacinto-2.mp3
    └── ... (other audio files, filenames match image files)

```

- **`index.html`**: The entry point of the application. Defines the necessary HTML elements for the player interface (image container, title, artist, audio element, progress bar, controls). Links to `style.css`, `script.js`, and Font Awesome CSS.
- **`style.css`**: Contains all CSS rules to style the elements defined in `index.html`, including layout, colors, fonts, and basic responsiveness.
- **`script.js`**: The core of the player's functionality. It handles:
  - DOM element selection.
  - Playlist data (`songs` array).
  - Playback state management (`isPlaying` variable, `songIndex`).
  - Event handling for user interactions (button clicks, progress bar clicks).
  - Event handling for the `<audio>` element (`timeupdate`, `ended`).
  - Functions to control audio (`playSong`, `pauseSong`).
  - Functions to navigate tracks (`prevSong`, `nextSong`).
  - Functions to update the UI (`loadSong`, `updateProgressBar`).
- **`img/`**: Stores album art images. Conventionally, filenames match the corresponding music files (e.g., `song-name.jpg`).
- **`music/`**: Stores the audio files (e.g., `song-name.mp3`). Conventionally, filenames match the corresponding image files.

## 4. Major Components

- **HTML Structure (`index.html`)**: Defines semantic elements for the player, including:
  - `<div class="player-container">`: Main wrapper.
  - `<div class="img-container">`: Holds the album art `<img>`.
  - `<h2>` (id: `title`), `<h3>` (id: `artist`): Display song metadata.
  - `<audio>`: The core HTML5 element for audio playback (hidden by default, controlled via JS).
  - `<div class="progress-container">`: Wrapper for the progress bar, listens for clicks.
  - `<div class="progress">`: The visual representation of progress, width is manipulated by JS.
  - `<span>` (ids: `current-time`, `duration`): Display time information.
  - `<div class="player-controls">`: Container for playback control buttons (`<i>` elements with Font Awesome classes).
- **CSS Styling (`style.css`)**: Provides the visual appearance, layout (using Flexbox), and responsiveness (using media queries). Styles elements for visual feedback (e.g., `:hover` states).
- **JavaScript Logic (`script.js`)**:
  - **DOM References:** Variables holding references to key HTML elements.
  - **State Management:** `isPlaying` (boolean) and `songIndex` (number) track the current state.
  - **Core Functions:** `playSong`, `pauseSong`, `loadSong`, `prevSong`, `nextSong`, `updateProgressBar`, `setProgressBar`.
  - **Event Listeners:** Attach functions to specific events on buttons, the progress bar, and the `<audio>` element.
- **Assets (`img/`, `music/`)**: Static media files loaded by the application when a song is selected via `loadSong`.

## 5. Data Flow

The typical data flow for user interaction is as follows:

1.  **Page Load:**
    - `index.html` is loaded and parsed by the browser.
    - `style.css` is loaded and applied.
    - `script.js` is loaded and executed.
    - `script.js` selects DOM elements.
    - `loadSong(songs[0])` is called, loading the first song's metadata, image, and audio source into the respective HTML elements.
2.  **User Clicks Play:**
    - The click event listener on the Play button (`playBtn`) triggers.
    - The handler checks the `isPlaying` state. If false, it calls `playSong()`.
    - `playSong()` sets `isPlaying` to true, updates the button icon and title, and calls `music.play()`.
    - The browser starts playing the audio.
3.  **Audio Plays:**
    - The `<audio>` element continuously fires the `timeupdate` event.
    - The `timeupdate` event listener calls `updateProgressBar()`.
    - `updateProgressBar()` gets `currentTime` and `duration` from the `<audio>` element.
    - It calculates the progress percentage and updates the width of the `progress` div.
    - It formats and updates the `currentTimeEl` and `durationEl` spans.
4.  **User Clicks Progress Bar:**
    - The click event listener on the `progressContainer` triggers `setProgressBar()`.
    - `setProgressBar()` calculates the horizontal click position (`e.offsetX`) relative to the container's width (`this.clientWidth`).
    - It calculates the desired playback time: `(clickX / width) * duration`.
    - It sets the `music.currentTime` property, causing the audio playback to jump to that position.
5.  **Song Ends:**
    - The `<audio>` element fires the `ended` event.
    - The `ended` event listener calls `nextSong()`.
    - `nextSong()` increments `songIndex` (handling wrap-around).
    - It calls `loadSong()` with the new song data.
    - `loadSong()` updates the title, artist, image source, and audio source.
    - `nextSong()` calls `playSong()` to immediately start playing the new track.

## 6. Design Decisions

- **Vanilla JavaScript:** Chosen for its simplicity and lack of external dependencies, suitable for a small project like this. It avoids the overhead of larger frameworks for basic DOM manipulation and event handling.
- **Hardcoded Playlist:** The `songs` array is directly embedded in `script.js`. This is the simplest approach for a fixed playlist demo but is not scalable. A more complex application might fetch this data from an API or read it from a file.
- **File Naming Convention:** Relying on matching base filenames for audio and images (`song-1.mp3`, `song-1.jpg`) simplifies the `loadSong` function, avoiding the need to store separate image paths in the `songs` array. This assumes consistent naming.
- **Global State Variables:** Simple state (`isPlaying`, `songIndex`) is managed using global variables within the script's scope. For larger applications, more robust state management patterns (like modules or closures) would be preferable.
- **Direct DOM Manipulation:** JavaScript directly selects and manipulates DOM element properties and styles. This is standard for Vanilla JS but differs from the declarative approaches used in frameworks like React or Vue.
