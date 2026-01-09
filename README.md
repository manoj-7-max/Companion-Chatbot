# Companion-Chatbot
Source Code

index.html

<!DOCTYPE html>
<html>
<head>
  <title>Companion Chatbot</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="chat-container">
  <div class="header">
    <h2>🤖 Companion Bot</h2>
    <button onclick="toggleDark()">🌙</button>
  </div>

  <div id="chat-box"></div>

  <div class="quick-buttons">
    <button onclick="quickMsg('I feel sad')">😔 Sad</button>
    <button onclick="quickMsg('I am stressed')">😰 Stress</button>
    <button onclick="quickMsg('Motivate me')">💪 Motivate</button>
    <button onclick="quickMsg('Tell me a quote')">🌈 Quote</button>
  </div>

  <div class="typing" id="typing">Bot is typing...</div>

  <div class="input-area">
    <input type="text" id="user-input" placeholder="Share your thoughts here...">
    <button onclick="sendMessage()">Send</button>
  </div>
</div>

<script src="script.js"></script>
</body>
</html>



style.css

body {
  font-family: Arial;
  background: linear-gradient(to right, #e3f2fd, #fff);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.chat-container {
  width: 380px;
  background: white;
  border-radius: 15px;
  padding: 10px;
  box-shadow: 0 0 15px #aaa;
}

.dark {
  background: #121212;
  color: white;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

#chat-box {
  height: 320px;
  overflow-y: auto;
  border: 1px solid #ddd;
  padding: 10px;
  margin: 10px 0;
}

.user {
  text-align: right;
  margin: 6px;
  color: #1565c0;
}

.bot {
  text-align: left;
  margin: 6px;
  color: #2e7d32;
}

.time {
  font-size: 10px;
  color: gray;
}

.input-area {
  display: flex;
}

input {
  flex: 1;
  padding: 8px;
}

button {
  padding: 8px;
  background: #1565c0;
  color: white;
  border: none;
  margin-left: 5px;
  border-radius: 5px;
}

.quick-buttons button {
  margin: 3px;
  background: #eee;
  color: black;
}

.typing {
  font-size: 12px;
  color: gray;
  display: none;
}



script.js

let moodMemory = "";
let dark = false;

function sendMessage() {
  const input = document.getElementById("user-input");
  const message = input.value.trim();
  if (message === "") return;

  addMessage("You", message, "user");
  input.value = "";

  document.getElementById("typing").style.display = "block";

  setTimeout(() => {
    const reply = getBotReply(message.toLowerCase());
    document.getElementById("typing").style.display = "none";
    addMessage("Bot", reply, "bot");
  }, 1000);
}

function quickMsg(text) {
  document.getElementById("user-input").value = text;
  sendMessage();
}

function addMessage(sender, text, className) {
  const chatBox = document.getElementById("chat-box");
  const div = document.createElement("div");
  const time = new Date().toLocaleTimeString();

  div.className = className;
  div.innerHTML = `<b>${sender}:</b> ${text}<div class="time">${time}</div>`;
  chatBox.appendChild(div);
  chatBox.scrollTop = chatBox.scrollHeight;
}

function getBotReply(msg) {

  if (msg.includes("sad") || msg.includes("lonely")) {
    moodMemory = "sad";
    return "I'm really sorry you're feeling low 🤍 You're safe here. Want to talk about what happened?";
  }

  if (msg.includes("stress") || msg.includes("tired")) {
    moodMemory = "stress";
    return "That sounds heavy 😔 Try taking one slow deep breath with me. You're stronger than you think 💪";
  }

  if (msg.includes("happy")) {
    moodMemory = "happy";
    return "Yayyy 😄 I love hearing happy moments! Tell me what made your day special ✨";
  }

  if (msg.includes("motivate")) {
    return "🌟 You are capable of more than you imagine. Small steps every day create big success.";
  }

  if (msg.includes("quote")) {
    return "🌈 'Believe in yourself even when no one else does.'";
  }

  if (msg.includes("hello") || msg.includes("hi")) {
    return "Hello 😊 I'm always here to listen and support you.";
  }

  if (moodMemory === "sad") {
    return "I'm still here with you 🤍 Would sharing a little more help you feel lighter?";
  }

  return "I may not fully understand, but I'm listening 🤗 Tell me more.";
}

function toggleDark() {
  dark = !dark;
  document.querySelector(".chat-container").classList.toggle("dark");
}


