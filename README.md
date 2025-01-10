# niwon

1. HTML - Bot Interface
 The HTML file will serve as the main structure for your hydration guru bot. 
 It will include a chat interface with a text input and a display area for messages.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hydration Guru Bot</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="chat-container">
    <div class="chat-box" id="chatBox">
      <!-- Chat messages will appear here -->
    </div>
    <input type="text" id="userInput" class="user-input" placeholder="Ask me about hydration...">
    <button id="sendBtn" class="send-btn">Send</button>
  </div>

  <script src="app.js"></script>
</body>
</html>




2. CSS - Styling
You'll need some basic CSS to style the chat interface and make it user-friendly.

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background-color: #f0f8ff;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.chat-container {
  background-color: #fff;
  border-radius: 10px;
  width: 400px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  display: flex;
  flex-direction: column;
  height: 500px;
}

.chat-box {
  flex-grow: 1;
  padding: 15px;
  overflow-y: auto;
  border-bottom: 1px solid #ddd;
  height: 400px;
}

.user-input {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  margin: 10px;
  width: calc(100% - 20px);
}

.send-btn {
  background-color: #4CAF50;
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 5px;
  margin: 10px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.send-btn:hover {
  background-color: #45a049;
}

.message {
  padding: 8px;
  margin: 5px 0;
  border-radius: 5px;
}

.user-message {
  background-color: #d1f7c4;
  text-align: right;
}

.bot-message {
  background-color: #f0f0f0;
}





4. JavaScript - Bot Logic
The JavaScript will handle the user input and the bot's responses.

document.getElementById('sendBtn').addEventListener('click', function() {
  const userInput = document.getElementById('userInput').value;
  if (userInput.trim() !== "") {
    addMessage(userInput, 'user');
    generateBotResponse(userInput);
    document.getElementById('userInput').value = ''; // Clear input
  }
});

document.getElementById('userInput').addEventListener('keypress', function(event) {
  if (event.key === 'Enter') {
    document.getElementById('sendBtn').click();
  }
});

function addMessage(message, sender) {
  const messageContainer = document.createElement('div');
  messageContainer.classList.add('message');
  messageContainer.classList.add(sender === 'user' ? 'user-message' : 'bot-message');
  messageContainer.textContent = message;
  document.getElementById('chatBox').appendChild(messageContainer);
  document.getElementById('chatBox').scrollTop = document.getElementById('chatBox').scrollHeight; // Scroll to the bottom
}

function generateBotResponse(input) {
  let response = "";
  
  // Simple keyword-based responses
  if (input.toLowerCase().includes("water")) {
    response = "Water is essential for maintaining your body's hydration! Aim to drink at least 8 glasses a day.";
  } else if (input.toLowerCase().includes("dehydration")) {
    response = "Dehydration can cause headaches, fatigue, and dizziness. Drink water and electrolytes to stay hydrated!";
  } else if (input.toLowerCase().includes("how much")) {
    response = "It’s generally recommended to drink around 2 liters of water per day, but it varies based on activity and climate.";
  } else if (input.toLowerCase().includes("tips")) {
    response = "Try carrying a water bottle with you, set reminders to drink water, and eat water-rich foods like fruits and vegetables!";
  } else if (input.toLowerCase().includes("thank")) {
    response = "You're welcome! Stay hydrated and healthy!";
  } else {
    response = "I'm your hydration guru! Ask me anything about staying hydrated.";
  }
  
  addMessage(response, 'bot');
}
