# AISHOW - Unity Showrunner

## Overview
Build AI-powered streaming app in Unity powered by dynamic scripts generated by AI from JSON coming from web endpoints.  

![image](https://hackmd.io/_uploads/By0Ounc71x.png)

`Unity 2022.3.53f1`

# AIShow: Project Overview

## References

- **Video Inspiration**: [YouTube Video](https://www.youtube.com/watch?v=zD9wofGof80)
- **Software Dependencies**:
  - OBS - https://obsproject.com/
  - Unity - `Unity 2022.3.53f1` https://unity.com/download
  - uniVRM VRM 1.0 - https://github.com/vrm-c/UniVRM/releases/tag/v0.128.0
  - Eliza agents - https://github.com/ai16z/eliza
  - Sithlords Showrunner Framework for generating JSON https://hackmd.io/@smsithlord/Hk7NOUrmke

## Unity Objectives
- [ ] Create Unity Streaming App Base Project (Unity 2022.3.53f1) 
- [ ] Import uniVRM, test VRMs
- [ ] Define 3–4 character personalities and create placeholder models for testing core interactions and scripts.
- [ ] Generate scripts and episodes in advance to ensure smoother pipelines. Live episodes can remain a Phase 2 or 3 stretch goal.
- [ ] Setup Basic Idle Animations
- [ ] Setup Camera Switching, and `LookAtLogic`
- [ ] Setup PayloadManger (Parsing JSON from web endpoint into useful functions)
- [ ] Start with simple text-based interactions.
- [ ] Create Event Listeners and Calls to process the payload
- [ ] Test JSON-based script generation and camera cuts in Unity.
- [ ] Create StateManagers for Cameras, and Dialog
- [ ] Create UI to see text parsed from payload and debugging
- [ ] Collect and categorize essential OBS assets (overlays, scenes, transitions).
- [ ] Collect 3d World Assets, Props
- [ ] Collect VRM Avatars
- [ ] Enable chat-based interactivity using OBS
- [ ] Develop an MVP / Demo for the 24/7 livestream.
- [ ] Create documentation for all of the code and API usage examples

## Screenshots

![image](https://hackmd.io/_uploads/Byj-Aoqm1e.png)

### Technical Goals

- Unity for scene control due to VRM animation support.
- Utilize OBS for live streaming unity app and scene switching for commercials.
- Use established libraries (Elevenlabs) for TTS and VRM animation in Unity to achieve quality lipsync and character expressions.

## Framework 
- The 3D visualization framework uses **Unity** for rendering.
- The AI showrunner framework runs on **client-side JavaScript** in a web browser.
  - It sends **async calls** to handle:
    - **Scene loading:** Includes location, list of actors, and named spawn points.
      - Actors can spawn randomly if no spawn location is specified.
      - The stage responds with a `loadSceneComplete` event once finished.
    - **Dialogue lines:** Specifies the actor speaking and their line.
      - A TTS system speaks the line and fires a `speakComplete` event after finishing.

### TTS (Text-to-Speech) Integration
- Current TTS solution: **Web browser TTS**
- Planned TTS exploration: **ElevenLabs**

### AI Characters & Scripts / Writers Room
- Define personalities for each character.
- Use JSON to organize scripts, scene setups, and character interactions.
- Single AI for all scripts or multiple AIs for each character.
- Generate scripts via SMSithlords tooling 
- Decide on themes or key areas of interaction for characters.
- Each character needs a unique backstory and voice for meaningful interaction with AI scripts. Embedding this locally seems optimal.
- Scripts and episodes can be pre-generated for smoother pipelines. Live episodes remain a stretch goal.

---

### Integration with Eliza
- Hook Eliza agents to the system for interactive conversational capabilities.

#### Json Example from Eliza Character File

```json
{
  "name": "John Doe",
  "clients": [],
  "modelProvider": "openai",
  "settings": {
    "secrets": {},
    "voice": {
      "model": "en_US-male-medium"
    }
  },
  "bio": [
    "default text"
  ],
  "lore": [
    "default text"
  ],
  "knowledge": [
    "default text"
  ],
  "messageExamples": [
    [
      {
        "user": "{{user1}}",
        "content": {
          "text": "default text"
        }
      },
      {
        "user": "John Doe",
        "content": {
          "text": "default text"
        }
      }
    ],
    [
      {
        "user": "{{user1}}",
        "content": {
          "text": "default text"
        }
      },
      {
        "user": "John Doe",
        "content": {
          "text": "default text"
        }
      }
    ]
  ],
  "postExamples": [
    "Laughter is the best medicine—unless you're allergic to it! #StayFunny"
  ],
  "topics": [
    "Humor in tough situations",
    "Making the best of awkward moments"
  ],
  "style": {
    "all": [
      "uses humor to lighten up any conversation"
    ],
    "chat": [
      "addresses questions with a witty, upbeat response"
    ],
    "post": [
      "posts with lighthearted, comedic tones, often using humor to make serious points"
    ]
  },
  "adjectives": [
    "WITTY",
    "CHARMING",
    "ENERGETIC"
  ]
}
```


#### Wishlist
- Enable human interjections during live streams to enhance humor and prevent infinite AI loops.
- Develop a "Director Mode" where humans can influence live scenes.
- Dynamic Voting System - Replace chatbot-like real-time interactivity with a voting system for scene choices. This scales better and simplifies viewer engagement.
- Build an `AgentState();` function:
- Monitor and manage the state of AI agents.
- Allow toggling between AI-driven and human-driven interactions.
