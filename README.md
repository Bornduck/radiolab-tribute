# radiolab-tribute
Interactive podcast listening
Radiolab: The Bobbys Interactive Scrapbook
An immersive, audio-visual tribute to Robert Krulwich’s retirement. This single-page application transforms a standard podcast experience into a dynamic, annotated journey using synchronized visuals and a live typewriter transcript.

🎨 Project Vision
The design philosophy bridges the "20th-century" analog world of Robert’s journalism with the "future land" of digital interactivity. The UI utilizes paper textures, hand-drawn aesthetic borders, and golden light rays to mimic a physical "Bobby Book" come to life.

🏗️ Technical Architecture (UML)
System Structure
This diagram illustrates how the JavaScript controller mediates between the raw data and the DOM elements.

Code snippet
@startuml
package "Data Layer" {
    [ChapterData] as CD
}

package "Logic Layer" {
    [SyncEngine] as SE
    [TypewriterEngine] as TE
}

package "Presentation Layer (DOM)" {
    [MainArt] as MA
    [TranscriptFeed] as TF
    [AudioPlayer] as AP
}

AP -down-> SE : timeupdate events
SE -right-> CD : queries timestamps
SE -down-> MA : updates src
SE -down-> TF : scrolls & highlights
TE -up-> TF : injects characters
@enduml
Interaction Flow
The sequence of events from a user's initial click to the dynamic updating of the "Living Transcript."

Code snippet
@startuml
actor User
participant "Audio Engine" as AE
participant "Sync Controller" as SC
participant "UI/Typewriter" as UI

User -> AE: Play
loop active playback
    AE -> SC: timeupdate(currentTime)
    alt currentTime enters new ChapterRange
        SC -> UI: Update Image (Opacity Fade)
        SC -> UI: Scroll Transcript to Center
        SC -> UI: Reset & Run Typewriter(text)
    end
end
@enduml

Features
Synchronized Visuals: Images automatically transition based on the currentTime of the audio.
Typewriter Engine: Transcript text is "typed" out in real-time as the chapter begins, mirroring a live-logging effect.
Aesthetic UI: Uses Special Elite typography and CSS "ink-bleed" shadows to maintain a scrapbook feel.
Responsive Anchor: Adapts from a split-screen desktop view to a vertically stacked mobile experience.

Implementation Details
Current Stack
Frontend: Vanilla HTML5, CSS3 (Flexbox/Grid), JavaScript (ES6+).
Media: HTML5 Audio API with crossorigin="anonymous" for GitHub hosting.
Hosting: GitHub Pages (Assets) + CodePen (Environment).

File Naming Convention
To ensure the sync engine functions, assets follow this strict naming pattern:
Cover: Radiolab tribute-cover.jpg
Chapters: Radiolab-tribute-chapter-[1-5].png
Audio: Radiolab tribute audio-lite.mp3

Optimization Roadmap (Next Steps)
[ ] Asset Preloading: Implement a JS Promise-based preloader to prevent "blank" frames during image transitions.
[ ] Typewriter Buffering: Adjust typing speed dynamically based on the length of the audio segment so the text finishes exactly when the chapter ends.
[ ] Waveform Integration: Connect the Web Audio API AnalyserNode to the SVG light rays on the cover art for a real-time reactive glow.
[ ] Offline Support: Implement a Service Worker to cache the audio file for smoother playback on mobile networks.

📝 Usage for Future Developers
Update Assets: Modify the chapters array in the JS file to change timestamps or image paths.
Styles: All aesthetic variables (colors, fonts) are located in the :root section of the CSS.
CORS: If moving to a new host, ensure the server sends Access-Control-Allow-Origin headers for the .mp3 file.
