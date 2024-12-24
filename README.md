# AISHOW - Unity Showrunner

![Unity_YI04NenMuV](https://github.com/user-attachments/assets/52529291-aa7c-4643-adf4-e49808b29160)

## Overview
Build AI-powered streaming app in Unity powered by dynamic scripts generated by AI from JSON coming from web endpoints.  

- Hackathon Submission: https://github.com/gm3/aishow/wiki/Hackathon-Submission
- DEMO: https://vimeo.com/1041883041?share=copy

![image](https://hackmd.io/_uploads/By0Ounc71x.png)

`Unity 2022.3.53f1`

## Project Overview

This repo is in active development and updated regularly!

## References

- **Video Inspiration**: [YouTube Video](https://www.youtube.com/watch?v=zD9wofGof80)
- **Software Dependencies**:
  - Unity - `Unity 2022.3.53f1` https://unity.com/download
  - uniVRM VRM 1.0 - https://github.com/vrm-c/UniVRM/releases/tag/v0.128.0
  - Sithlords Showrunner Framework for generating JSON / AI scriptwriting https://hackmd.io/@smsithlord/Hk7NOUrmke
 
![Adobe_Premiere_Pro_oQKnCU7Lj5](https://github.com/user-attachments/assets/dcdb9a8d-32d3-4145-95bd-176e30957b09)

## Screenshots

![image](https://hackmd.io/_uploads/Byj-Aoqm1e.png)

![gcCofMWuAy](https://github.com/user-attachments/assets/16907503-666d-4286-8fb3-1a3c729f230c)

## Framework 
- The 3D visualization framework uses **Unity** for rendering.
- Sithlords AI showrunner framework runs on **client-side JavaScript** in a web browser. https://hackmd.io/@smsithlord/Hk7NOUrmke
  - It sends **async calls** to handle:
    - **Scene loading:** Includes location, list of actors, and named spawn points.
      - Actors can spawn randomly if no spawn location is specified.
      - The stage responds with a `loadSceneComplete` event once finished.
    - **Dialogue lines:** Specifies the actor speaking and their line.
      - A TTS system speaks the line and fires a `speakComplete` event after finishing.

### TTS (Text-to-Speech) Integration
- **ElevenLabs**

### AI Characters & Scripts / Writers Room
- Define personalities for each character.
- Use JSON to organize scripts, scene setups, and character interactions.
- Single AI for all scripts or multiple AIs for each character.
- Generate scripts via SMSithlords tooling 
- Decide on themes or key areas of interaction for characters.
- Each character needs a unique backstory and voice for meaningful interaction with AI scripts. Embedding this locally seems optimal.
- Scripts and episodes can be pre-generated for smoother pipelines. Live episodes remain a stretch goal.

### ShowRunnerUX

![image](https://github.com/user-attachments/assets/b3681ea1-d9f1-4549-8241-d8fb7da2a77c)


---

![Unity_7LaaHYpQmd](https://github.com/user-attachments/assets/ef8af61d-d923-4beb-b3b1-6d484350aa96)



### Integration with Eliza Goal
- Hook Eliza agents to the system for interactive conversational capabilities.


#### Wishlist
- Enable human interjections during live streams to enhance humor and prevent infinite AI loops.
- Develop a "Director Mode" where humans can influence live scenes.
- Dynamic Voting System - Replace chatbot-like real-time interactivity with a voting system for scene choices. This scales better and simplifies viewer engagement.
- Allow toggling between AI-driven and human-driven interactions.

