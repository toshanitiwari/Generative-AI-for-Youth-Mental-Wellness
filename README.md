<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Youth Mental Wellness App</title>
  <style>
    body {
      font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
      background: url("WhatsApp Image 2025-09-15 at 6.42.40 PM.jpeg") no-repeat center center fixed;
      background-size: cover;
      position: relative;
    }
    /* Light overlay for readability */
    body::before {
      content: "";
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(255, 255, 255, 0.6);
      backdrop-filter: blur(2px);
      z-index: 0;
    }
    h1, p, #chat, #inputBox, #controls, #emotion, #affirmationBox, #journalBox, #panicBtn {
      position: relative;
      z-index: 1;
    }
    h1 {
      margin: 20px 10px 5px;
      color: #1e3a8a;
      text-align: center;
    }
    p.tagline {
      margin: 0 0 20px;
      color: #374151;
      font-style: italic;
    }
    /* Affirmation Box */
    #affirmationBox {
      background: white;
      padding: 15px;
      margin: 10px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      text-align: center;
      max-width: 500px;
    }
    #affirmationText {
      font-size: 16px;
      color: #111827;
      margin-bottom: 10px;
    }
    #chat {
      width: 90%;
      max-width: 600px;
      background: white;
      border-radius: 16px;
      padding: 15px;
      box-shadow: 0 6px 20px rgba(0,0,0,0.2);
      margin-bottom: 20px;
      display: flex;
      flex-direction: column;
      max-height: 400px;
      overflow-y: auto;
    }
    .message {
      margin: 8px 0;
      padding: 10px 14px;
      border-radius: 12px;
      max-width: 80%;
    }
    .user { background: #dbeafe; align-self: flex-end; }
    .bot { background: #f3f4f6; align-self: flex-start; }
    #controls {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
      flex-wrap: wrap;
      justify-content: center;
    }
    button {
      padding: 8px 16px;
      border: none;
      border-radius: 8px;
      background: #2563eb;
      color: white;
      cursor: pointer;
      transition: 0.2s;
    }
    button:hover { background: #1d4ed8; }
    #inputBox {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
      width: 90%;
      max-width: 600px;
    }
    #userInput {
      flex: 1;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 14px;
    }
    #journalBox {
      width: 90%;
      max-width: 600px;
      background: white;
      border-radius: 16px;
      padding: 15px;
      margin-bottom: 20px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }
    #journalEntries {
      margin-top: 10px;
      max-height: 200px;
      overflow-y: auto;
    }
    .entry {
      background: #f9fafb;
      padding: 8px;
      border-radius: 6px;
      margin-bottom: 6px;
      font-size: 14px;
    }
    #emotion {
      font-weight: bold;
      color: #1f2937;
      margin: 10px 0 30px;
    }
    /* Panic Popup */
    #panicPopup {
      display: none;
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(0,0,0,0.6);
      z-index: 10;
      justify-content: center;
      align-items: center;
    }
    #panicContent {
      background: #fff;
      padding: 20px;
      border-radius: 12px;
      max-width: 400px;
      text-align: center;
      box-shadow: 0 4px 12px rgba(0,0,0,0.3);
    }
    #panicContent h2 {
      margin-bottom: 15px;
      color: #dc2626;
    }
    #panicContent ul {
      text-align: left;
      padding-left: 20px;
    }
    #closePanic {
      margin-top: 15px;
      background: #2563eb;
    }
  </style>
</head>
<body>
  <h1>Youth Mental Wellness App 🌱</h1>
  <p class="tagline">“Your safe space to express, reflect, and grow.”</p>

  <!-- Daily Affirmation Box -->
  <div id="affirmationBox">
    <div id="affirmationText">Loading your daily affirmation...</div>
    <button id="newAffirmationBtn">✨ New Affirmation</button>
  </div>
  
  <div id="chat"></div>

  <div id="inputBox">
    <input type="text" id="userInput" placeholder="Type how you feel..." />
    <button id="sendBtn">Send</button>
  </div>

  <div id="controls">
    <button id="speakBtn">🎤 Speak</button>
    <button id="respondBtn">💬 Get Response</button>
    <button id="panicBtn">🚨 Panic Button</button>
  </div>

  <!-- Journaling -->
  <div id="journalBox">
    <h3>📝 Daily Journal</h3>
    <textarea id="journalInput" rows="3" placeholder="Write your thoughts here..."></textarea><br/>
    <button id="saveJournalBtn">Save Entry</button>
    <div id="journalEntries"></div>
  </div>

  <p id="emotion">Detected Emotion: Neutral</p>

  <!-- Panic Popup -->
  <div id="panicPopup">
    <div id="panicContent">
      <h2>Take a Deep Breath 🌸</h2>
      <p>Here are some calming tips:</p>
      <ul>
        <li>🌬️ Breathe in for 4 sec, hold for 4 sec, exhale for 6 sec.</li>
        <li>🎶 Listen to soothing music.</li>
        <li>🧘 Try grounding: name 5 things you see, 4 touch, 3 hear, 2 smell, 1 taste.</li>
        <li>📞 Talk to someone you trust.</li>
      </ul>
      <p><b>Helpline Numbers (India):</b><br/>
        ☎️ Vandrevala Foundation Helpline: 1860 266 2345 / 1800 233 3330<br/>
        ☎️ AASRA Helpline: +91-9820466726<br/>
        ☎️ Snehi Helpline: +91-9582208181
      </p>
      <button id="closePanic">Close</button>
    </div>
  </div>

  <script>
    const chat = document.getElementById("chat");
    const speakBtn = document.getElementById("speakBtn");
    const respondBtn = document.getElementById("respondBtn");
    const sendBtn = document.getElementById("sendBtn");
    const userInput = document.getElementById("userInput");

    // Daily Affirmations
    const affirmationText = document.getElementById("affirmationText");
    const newAffirmationBtn = document.getElementById("newAffirmationBtn");

    const affirmations = [
      "🌸 I am worthy of love and kindness.",
      "☀️ I choose peace over worry.",
      "💪 I am stronger than my challenges.",
      "🌈 My mind is calm, my heart is light.",
      "✨ I deserve rest, healing, and happiness.",
      "🌿 Every day is a new beginning."
    ];

    function showAffirmation() {
      const random = affirmations[Math.floor(Math.random() * affirmations.length)];
      affirmationText.textContent = random;
    }
    newAffirmationBtn.addEventListener("click", showAffirmation);
    window.onload = showAffirmation;

    function addMessage(text, sender) {
      const msg = document.createElement("div");
      msg.className = "message " + sender;
      msg.textContent = text;
      chat.appendChild(msg);
      chat.scrollTop = chat.scrollHeight;
    }

    // Handle text input
    sendBtn.addEventListener("click", () => {
      if (userInput.value.trim() !== "") {
        userMessage = userInput.value.trim();
        addMessage("You: " + userMessage, "user");
        userInput.value = "";
      }
    });

    // Speech recognition
    const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    const recognition = new SpeechRecognition();
    recognition.continuous = false;
    recognition.lang = "en-US";

    recognition.onresult = (event) => {
      userMessage = event.results[0][0].transcript;
      addMessage("You: " + userMessage, "user");
    };

    speakBtn.addEventListener("click", () => {
      recognition.start();
    });

    // Simple generative AI placeholder
    respondBtn.addEventListener("click", () => {
      const responses = [
        "I hear you. It’s okay to feel this way 💙",
        "Take a deep breath — you’re doing great 🌸",
        "Remember, tough times don’t last, but tough people do 💪",
        "Try writing down your thoughts, it might help 📖",
        "Talking to a friend can lighten your mind 🌈"
      ];
      const reply = responses[Math.floor(Math.random() * responses.length)];
      addMessage("Bot: " + reply, "bot");
    });

    // Journaling
    const saveJournalBtn = document.getElementById("saveJournalBtn");
    const journalInput = document.getElementById("journalInput");
    const journalEntries = document.getElementById("journalEntries");

    saveJournalBtn.addEventListener("click", () => {
      const text = journalInput.value.trim();
      if (text) {
        const entry = document.createElement("div");
        entry.className = "entry";
        entry.textContent = new Date().toLocaleDateString() + ": " + text;
        journalEntries.appendChild(entry);
        journalInput.value = "";
      }
    });

    // Panic Button
    const panicBtn = document.getElementById("panicBtn");
    const panicPopup = document.getElementById("panicPopup");
    const closePanic = document.getElementById("closePanic");

    panicBtn.addEventListener("click", () => {
      panicPopup.style.display = "flex";
    });
    closePanic.addEventListener("click", () => {
      panicPopup.style.display = "none";
    });
  </script>
</body>
</html>
# Generative-AI-for-Youth-Mental-Wellness
Our prototype leverages Generative AI to provide personalized, accessible, and scalable mental health support. 
