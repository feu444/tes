<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Chat Box Persistante</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #1e1e1e;
      color: #f0f0f0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .chat-container {
      width: 400px;
      background-color: #2c2c2c;
      border-radius: 8px;
      box-shadow: 0 0 10px #000;
      display: flex;
      flex-direction: column;
    }

    .chat-messages {
      height: 300px;
      padding: 10px;
      overflow-y: auto;
      border-bottom: 1px solid #444;
    }

    .chat-messages p {
      margin: 5px 0;
      padding: 8px;
      background-color: #3d3d3d;
      border-radius: 5px;
    }

    .chat-input {
      display: flex;
    }

    .chat-input input {
      flex: 1;
      padding: 10px;
      border: none;
      outline: none;
      background-color: #1e1e1e;
      color: #fff;
    }

    .chat-input button {
      background-color: #4caf50;
      border: none;
      padding: 10px 20px;
      color: white;
      cursor: pointer;
    }

    .chat-input button:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body>
  <div class="chat-container">
    <div class="chat-messages" id="chatMessages"></div>
    <div class="chat-input">
      <input type="text" id="chatInput" placeholder="Écris un message...">
      <button onclick="sendMessage()">Envoyer</button>
    </div>
  </div>

  <script>
    const messages = JSON.parse(localStorage.getItem('chatMessages')) || [];

    function renderMessages() {
      const chatMessages = document.getElementById('chatMessages');
      chatMessages.innerHTML = '';
      messages.forEach(msg => {
        const p = document.createElement('p');
        p.textContent = msg;
        chatMessages.appendChild(p);
      });
      chatMessages.scrollTop = chatMessages.scrollHeight;
    }

    function sendMessage() {
      const input = document.getElementById('chatInput');
      const text = input.value.trim();
      if (text !== '') {
        messages.push(text);
        localStorage.setItem('chatMessages', JSON.stringify(messages));
        renderMessages();
        input.value = '';
      }
    }

    // Envoi avec la touche Entrée
    document.getElementById('chatInput').addEventListener('keydown', function(event) {
      if (event.key === 'Enter') {
        sendMessage();
      }
    });

    // Affiche les messages au chargement
    renderMessages();
  </script>
</body>
</html>
