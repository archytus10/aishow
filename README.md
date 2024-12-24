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

## Instructions

- Open Unity Project
- Reimport All Assets after library builds to fix VRMs
- create and add show runner endpoint urls to `.env`
- Play app
- Start Polling
- Launch Preprose in show runner directory
- Launch ShowRunner Simulation web-app 

## References

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

### Node.js Example

```
/* Required environment variables are:
ELEVENLABS_API_KEY
ANTHROPIC_API_KEY
*/

// Claude API endpoint
fastify.post("/api/claude", async function (request, reply) {
  try {
    const response = await fetch("https://api.anthropic.com/v1/messages", {
      method: "POST",
      headers: {
        "x-api-key": process.env.ANTHROPIC_API_KEY,
        "anthropic-version": "2023-06-01",
        "content-type": "application/json",
      },
      body: JSON.stringify(request.body),
    });
    const data = await response.json();
    return reply.send(data);
  } catch (error) {
    fastify.log.error(error);
    return reply.code(500).send({ error: error.message });
  }
});

// ElevenLabs Endpoint to fetch available voices
fastify.get("/api/elevenlabs/voices", async (request, reply) => {
  try {
    const response = await fetch("https://api.elevenlabs.io/v1/voices", {
      method: "GET",
      headers: {
        "xi-api-key": process.env.ELEVENLABS_API_KEY,
      },
    });

    if (!response.ok) {
      const errorData = await response.json();
      return reply.code(response.status).send(errorData);
    }

    const data = await response.json();
    return reply.send(data);
  } catch (error) {
    fastify.log.error(error);
    return reply.code(500).send({ error: error.message });
  }
});

// ElevenLabs Endpoint to speak text using a specified voice
fastify.post("/api/elevenlabs/speak", async (request, reply) => {
  const { text, voice_id } = request.body;

  if (!text || !voice_id) {
    return reply.code(400).send({ error: "Missing 'text' or 'voice_id' in request body." });
  }

  try {
    const response = await fetch(`https://api.elevenlabs.io/v1/text-to-speech/${voice_id}`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "xi-api-key": process.env.ELEVENLABS_API_KEY,
      },
      body: JSON.stringify({
        text: text,
        voice_settings: { stability: 0.5, similarity_boost: 0.5 }, // Optional voice settings
      }),
    });

    if (!response.ok) {
      const errorData = await response.json();
      return reply.code(response.status).send(errorData);
    }

    const audioData = await response.buffer();
    reply.type("audio/mpeg").send(audioData); // Send the audio data as an MP3 file
  } catch (error) {
    fastify.log.error(error);
    return reply.code(500).send({ error: error.message });
  }
});

fastify.post("/api/cast-voices", async function (request, reply) {
  try {
    const { voices, actors, castingPrompt } = request.body;

    const prompt = `${castingPrompt}

Available Voices:
${JSON.stringify(voices, null, 2)}

Characters Needing Voices:
${JSON.stringify(actors, null, 2)}

Please provide a JSON mapping of actor IDs to voice IDs.`;

    const response = await fetch("https://api.anthropic.com/v1/messages", {
      method: "POST",
      headers: {
        "x-api-key": process.env.ANTHROPIC_API_KEY,
        "anthropic-version": "2023-06-01",
        "content-type": "application/json",
      },
      body: JSON.stringify({
        model: "claude-3-5-sonnet-20241022",
        messages: [{ role: "user", content: prompt }],
        max_tokens: 2048
      }),
    });
    
    const data = await response.json();
    return reply.send(data);
    
  } catch (error) {
    return reply.code(500).send({ error: error.message });
  }
});
```


---

![Unity_7LaaHYpQmd](https://github.com/user-attachments/assets/ef8af61d-d923-4beb-b3b1-6d484350aa96)



### Integration with Eliza Goal
- Hook Eliza agents to the system for interactive conversational capabilities.


#### Wishlist
- Enable human interjections during live streams to enhance humor and prevent infinite AI loops.
- Develop a "Director Mode" where humans can influence live scenes.
- Dynamic Voting System - Replace chatbot-like real-time interactivity with a voting system for scene choices. This scales better and simplifies viewer engagement.
- Allow toggling between AI-driven and human-driven interactions.

