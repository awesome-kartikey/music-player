# Frequently Asked Questions (FAQ)

Here are some common questions about the Awesome Kartikey Music Player:

**Q1: How do I add my own songs to the player?**

**A:** To add your own music:

1.  Place your audio files (e.g., `.mp3`) into the `music/` folder.
2.  Place the corresponding album cover images (e.g., `.jpg`) into the `img/` folder. Ensure the image filename (without extension) matches the audio filename (without extension). For example, if you have `my-song.mp3`, you should have `my-song.jpg`.
3.  Open the `script.js` file.
4.  Locate the `songs` array.
5.  Add a new object to the array for each song you want to add, following this format:
    ```javascript
    {
        name: 'your-filename-base', // The base name of your files (e.g., 'my-song')
        displayName: 'Song Title to Display',
        artist: 'Artist Name to Display',
    }
    ```
    **Example:**
    ```javascript
    const songs = [
      // ... other songs ...
      {
        name: "my-new-track",
        displayName: "My Awesome New Track",
        artist: "Me",
      },
    ];
    ```
6.  Save `script.js` and refresh `index.html` in your browser.

**Q2: What audio formats are supported?**

**A:** The player uses the standard HTML5 `<audio>` element. Supported formats depend on the browser, but common formats like MP3, WAV, and Ogg Vorbis are generally well-supported. This specific implementation is geared towards MP3 files as indicated in the setup.

**Q3: The player isn't working or showing my songs. What should I check?**

**A:**

1.  **File Paths:** Double-check that the filenames in the `songs` array in `script.js` _exactly_ match the names of your files in the `music/` and `img/` folders (excluding the extension). Remember, case sensitivity matters on some systems.
2.  **Folder Structure:** Ensure the `music/` and `img/` folders are in the same directory as `index.html`.
3.  **Browser Console:** Open your browser's developer tools (usually by pressing F12) and check the "Console" tab for any error messages. These messages often indicate what went wrong (e.g., file not found, JavaScript error).
4.  **File Existence:** Make sure the music and image files actually exist in the specified folders.

**Q4: Can I change the appearance of the player?**

**A:** Yes! The player's appearance is controlled by the `style.css` file. You can modify this file to change colors, fonts, layout, sizes, and more. Basic knowledge of CSS is required.

**Q5: Does the player remember the last played song or position?**

**A:** No, this simple version of the player does not have persistence. It will always start with the first song in the playlist (`songs[0]`) when the page is loaded or refreshed. Adding persistence would require using browser storage mechanisms like `localStorage`.

**Q6: Can I add features like shuffle or repeat?**

**A:** These features are not currently implemented. You would need to modify the `script.js` file to add the logic for shuffle (randomizing the song order or next selection) and repeat (replaying the current song or the entire playlist).

**Q7: Is an internet connection required to use the player?**

**A:** An internet connection is needed initially to load the Font Awesome icons (if you are using the CDN link in `index.html`). However, once the page and assets (HTML, CSS, JS, music, images) are loaded, the player itself works offline as all playback logic runs in the browser. If you download Font Awesome and reference it locally, no internet connection would be needed after the initial setup.
