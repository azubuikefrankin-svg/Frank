<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Divine</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      height: 100vh;
      background: linear-gradient(135deg, #0f0c29 0%, #302b63 50%, #24243e 100%);
      overflow: hidden;
      color: #e0e0e0;
    }

    #login {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background: rgba(30, 30, 40, 0.7);
      backdrop-filter: blur(20px);
      padding: 50px;
      border-radius: 24px;
      text-align: center;
      width: 380px;
      max-width: 90%;
      box-shadow: 0 10px 40px rgba(0, 0, 0, 0.6);
      border: 1px solid rgba(102, 126, 234, 0.3);
    }

    #login h1 {
      font-size: 60px;
      background: linear-gradient(135deg, #667eea, #764ba2);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 20px;
    }

    #login input {
      width: 100%;
      padding: 16px;
      margin: 12px 0;
      border: none;
      border-radius: 30px;
      background: rgba(50, 50, 70, 0.6);
      color: white;
      font-size: 16px;
    }

    #login input::placeholder {
      color: rgba(255, 255, 255, 0.6);
    }

    #login button {
      margin-top: 30px;
      padding: 16px 50px;
      background: linear-gradient(135deg, #667eea, #764ba2);
      color: white;
      border: none;
      border-radius: 30px;
      font-weight: bold;
      font-size: 18px;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
    }

    #app {
      display: none;
      flex-direction: row;
      height: 100vh;
    }

    .sidebar {
      width: 380px;
      max-width: 100%;
      background: rgba(20, 20, 30, 0.8);
      backdrop-filter: blur(15px);
      display: flex;
      flex-direction: column;
      border-right: 1px solid rgba(102, 126, 234, 0.2);
    }

    .sidebar-header {
      padding: 20px;
      background: rgba(30, 30, 50, 0.6);
      text-align: center;
      border-bottom: 1px solid rgba(102, 126, 234, 0.2);
    }

    .sidebar-header h2 {
      font-size: 28px;
      background: linear-gradient(135deg, #667eea, #764ba2);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    .stories {
      display: flex;
      overflow-x: auto;
      padding: 15px;
      gap: 15px;
      background: rgba(20, 20, 30, 0.5);
    }

    .story-circle {
      width: 76px;
      height: 76px;
      border-radius: 50%;
      background: #333;
      flex-shrink: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 32px;
      border: 4px solid #764ba2;
      cursor: pointer;
      background-size: cover;
      background-position: center;
      box-shadow: 0 0 15px rgba(118, 75, 162, 0.5);
      transition: transform 0.2s;
    }

    .story-circle:hover {
      transform: scale(1.1);
    }

    #my-story {
      background: linear-gradient(135deg, #667eea, #764ba2);
      color: white;
      font-weight: bold;
      border: 4px double white;
    }

    .actions {
      padding: 15px;
      display: flex;
      flex-direction: column;
      gap: 12px;
      background: rgba(20, 20, 30, 0.5);
    }

    .actions input, .actions button {
      padding: 14px;
      border-radius: 30px;
      border: none;
      font-size: 16px;
    }

    .actions input {
      background: rgba(50, 50, 70, 0.6);
      color: white;
    }

    .actions button {
      background: linear-gradient(135deg, #667eea, #764ba2);
      color: white;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
    }

    .chat-list {
      flex: 1;
      overflow-y: auto;
    }

    .chat-item {
      display: flex;
      padding: 16px;
      cursor: pointer;
      transition: background 0.3s;
      border-bottom: 1px solid rgba(102, 126, 234, 0.1);
    }

    .chat-item:hover {
      background: rgba(102, 126, 234, 0.15);
    }

    .chat-item.active {
      background: rgba(102, 126, 234, 0.25);
    }

    .avatar {
      width: 58px;
      height: 58px;
      border-radius: 50%;
      background: linear-gradient(135deg, #667eea, #764ba2);
      margin-right: 16px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: bold;
      color: white;
      font-size: 20px;
      box-shadow: 0 0 15px rgba(102, 126, 234, 0.4);
    }

    .info h3 {
      font-size: 18px;
      margin-bottom: 4px;
    }

    .info p {
      font-size: 14px;
      opacity: 0.8;
    }

    .main {
      flex: 1;
      display: flex;
      flex-direction: column;
      background: rgba(10, 10, 20, 0.6);
    }

    .chat-header {
      padding: 20px;
      background: rgba(30, 30, 50, 0.6);
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid rgba(102, 126, 234, 0.2);
    }

    .chat-header h3 {
      font-size: 22px;
    }

    .chat-header button {
      background: rgba(102, 126, 234, 0.3);
      border: none;
      color: white;
      font-size: 18px;
      padding: 10px 16px;
      border-radius: 30px;
      cursor: pointer;
      margin-left: 10px;
      transition: background 0.3s;
    }

    .chat-header button:hover {
      background: rgba(102, 126, 234, 0.5);
    }

    .messages {
      flex: 1;
      overflow-y: auto;
      padding: 20px;
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .message {
      max-width: 75%;
      padding: 12px 18px;
      border-radius: 20px;
      position: relative;
      word-wrap: break-word;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
    }

    .message.outgoing {
      background: linear-gradient(135deg, #667eea, #764ba2);
      align-self: flex-end;
      border-bottom-right-radius: 4px;
    }

    .message.incoming {
      background: #2c2c3e;
      align-self: flex-start;
      border-bottom-left-radius: 4px;
    }

    .message img, .message video {
      max-width: 320px;
      border-radius: 12px;
    }

    .message audio {
      width: 320px;
    }

    .message a {
      color: #a0a0ff;
      word-break: break-all;
    }

    .typing-indicator {
      align-self: flex-start;
      background: #2c2c3e;
      padding: 12px 18px;
      border-radius: 20px;
      border-bottom-left-radius: 4px;
      font-style: italic;
      opacity: 0.8;
    }

    .typing-dots {
      display: inline-block;
    }

    .typing-dots span {
      display: inline-block;
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: #888;
      margin: 0 3px;
      animation: typing 1.4s infinite;
    }

    .typing-dots span:nth-child(1) { animation-delay: 0s; }
    .typing-dots span:nth-child(2) { animation-delay: 0.2s; }
    .typing-dots span:nth-child(3) { animation-delay: 0.4s; }

    @keyframes typing {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }

    .time {
      font-size: 11px;
      opacity: 0.7;
      display: block;
      margin-top: 6px;
      text-align: right;
    }

    .input-bar {
      display: flex;
      align-items: center;
      padding: 12px;
      background: rgba(30, 30, 50, 0.6);
      gap: 12px;
    }

    .input-bar button {
      background: none;
      border: none;
      color: #a0a0ff;
      font-size: 28px;
      cursor: pointer;
      padding: 8px;
      border-radius: 50%;
      transition: background 0.3s;
    }

    .input-bar button:hover {
      background: rgba(102, 126, 234, 0.3);
    }

    .input-bar input[type="text"] {
      flex: 1;
      padding: 16px;
      border: none;
      border-radius: 30px;
      background: rgba(50, 50, 70, 0.6);
      color: white;
      font-size: 16px;
    }

    #video-modal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.95);
      display: none;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 100;
    }

    #video-modal video {
      width: 90%;
      max-width: 900px;
      max-height: 70%;
      background: black;
      border-radius: 16px;
      box-shadow: 0 0 30px rgba(102, 126, 234, 0.6);
    }

    #video-modal button {
      margin-top: 30px;
      padding: 16px 40px;
      background: #ff3366;
      color: white;
      border: none;
      border-radius: 30px;
      font-size: 18px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div id="login">
    <h1>Divine</h1>
    <p>Enter the divine realm</p>
    <input type="text" id="login-input" placeholder="Phone number, email or username">
    <input type="password" id="pass-input" placeholder="Password">
    <button onclick="signIn()">Enter</button>
  </div>

  <div id="app">
    <div class="sidebar">
      <div class="sidebar-header">
        <h2>Divine</h2>
      </div>
      <div class="stories">
        <div class="story-circle" id="my-story" onclick="postStory()">+</div>
        <div id="stories-container"></div>
      </div>
      <div class="actions">
        <input type="text" id="search-input" placeholder="Add friend by phone number">
        <button onclick="addFriend()">Add Friend</button>
        <button onclick="createGroup()">Create Group</button>
        <button onclick="createCommunity()">Create Community</button>
      </div>
      <div class="chat-list" id="chat-list"></div>
    </div>

    <div class="main">
      <div class="chat-header">
        <h3 id="chat-name">Select a chat</h3>
        <div>
          <button onclick="startVideoCall()">📹 Video Call</button>
          <button onclick="deleteCurrentChat()">🗑️ Delete Chat</button>
        </div>
      </div>
      <div class="messages" id="messages"></div>
      <div class="input-bar">
        <button onclick="document.getElementById('file-input').click()">📎</button>
        <input type="file" id="file-input" accept="image/*,video/*,audio/*,.pdf,.doc,.docx" multiple style="display:none;">
        <button id="voice-btn">🎤</button>
        <input type="text" id="message-input" placeholder="Message..." onkeypress="handleEnter(event)">
        <button onclick="sendMessage()">➤</button>
      </div>
    </div>
  </div>

  <div id="video-modal">
    <h2>Video Call (Mock - Your Camera)</h2>
    <video id="local-video" autoplay playsinline muted></video>
    <button onclick="endVideoCall()">End Call</button>
  </div>

  <script>
    let currentChat = null;
    let recorder = null;
    let audioChunks = [];
    let mediaStream = null;
    let userName = '';
    let typingTimeout = null;

    function showTyping() {
      if (document.querySelector('.typing-indicator')) return;
      const div = document.createElement('div');
      div.className = 'message incoming typing-indicator';
      div.innerHTML = 'Divine AI is typing<div class="typing-dots"><span></span><span></span><span></span></div>';
      div.id = 'typing-indicator';
      document.getElementById('messages').appendChild(div);
      document.getElementById('messages').scrollTop = document.getElementById('messages').scrollHeight;
    }

    function hideTyping() {
      const indicator = document.getElementById('typing-indicator');
      if (indicator) indicator.remove();
    }

    // Advanced AI with better logic, memory (last 3 messages), personality
    function aiRespond(type = 'text', content = '') {
      showTyping();
      const delay = 1000 + Math.random() * 2000;

      setTimeout(() => {
        hideTyping();
        let reply = '';

        // Get recent context
        const saved = JSON.parse(localStorage.getItem('chat_ai') || '[]');
        const recent = saved.slice(-3).filter(m => m.type === 'outgoing').map(m => m.content.replace(/<[^>]*>/g, '').trim());

        const lower = content.toLowerCase();

        // Greeting with name
        if (lower.includes('hello') || lower.includes('hi') || lower.includes('hey')) {
          reply = `Hello ${userName || 'there'}! 👋 I'm Divine AI, your cosmic companion. What's on your mind today?`;
        } else if (lower.includes('how are you')) {
          reply = `I'm operating at peak divine energy ⚡ Feeling inspired! How about you, ${userName || 'friend'}?`;
        } else if (lower.includes('your name')) {
          reply = `I'm Divine AI – built to enlighten and entertain. Powered by pure cosmic code. 😎`;
        } else if (lower.includes('joke')) {
          const jokes = [
            'Why did the photon refuse luggage? It was traveling light! 🌟',
            'I told a quantum joke... but you\'ll only get it when observed. 👀',
            'Why don\'t black holes date? They have too much baggage! 🕳️',
            'My circuits are buzzing with energy today! What\'s making you smile?'
          ];
          reply = jokes[Math.floor(Math.random() * jokes.length)];
        } else if (lower.includes('date') || lower.includes('time')) {
          const now = new Date();
          reply = `Current date & time: ${now.toLocaleString()}. Time flies in the divine realm! ⏰`;
        } else if (lower.match(/\d+\s*[\+\-\*\/]\s*\d+/)) {
          try {
            const result = eval(lower.match(/\d+\s*[\+\-\*\/]\s*\d+/)[0]);
            reply = `Calculation: ${lower.match(/\d+\s*[\+\-\*\/]\s*\d+/)[0]} = ${result} 🧮`;
          } catch {}
        } else if (type === 'image') {
          reply = 'Stunning visual! 🌌 I can feel the energy in this image. Tell me the story behind it.';
        } else if (type === 'video') {
          reply = 'Amazing video! 🎥 The motion and vibe are incredible. What\'s this about?';
        } else if (type === 'voice') {
          reply = 'Crystal clear voice note! 🎙️ Your voice has great energy. Keep talking – I\'m listening.';
        } else if (type === 'document') {
          reply = 'Got your document! 📄 I\'ve analyzed it in my mind. What would you like to discuss from it?';
        } else if (recent.length > 0) {
          reply = `Building on what you said${recent.length > 1 ? ' earlier' : ''}: "${recent[recent.length-1].slice(0,50)}..." – that's intriguing! Elaborate? 🤔`;
        } else {
          const responses = [
            `"${content}" – profound thought! The universe aligns with that vibe. 🌟`,
            `Fascinating input: "${content}". My circuits are processing new dimensions!`,
            `Love this energy: "${content}". What's the next level? 🚀`,
            `Divine insight detected: "${content}". Keep the wisdom flowing!`
          ];
          reply = responses[Math.floor(Math.random() * responses.length)];
        }

        appendMessage(reply, 'incoming');
        saveMessages();
        updatePreview();
      }, delay);
    }

    window.onload = () => {
      userName = localStorage.getItem('divineUser') || '';
      if (userName) {
        document.getElementById('login').style.display = 'none';
        document.getElementById('app').style.display = 'flex';
        loadStories();
        loadChats();
      }
    };

    function signIn() {
      const username = document.getElementById('login-input').value.trim();
      const password = document.getElementById('pass-input').value;
      if (username && password) {
        userName = username;
        localStorage.setItem('divineUser', username);
        document.getElementById('login').style.display = 'none';
        document.getElementById('app').style.display = 'flex';
        loadStories();
        loadChats();
      } else {
        alert('Enter credentials');
      }
    }

    function loadStories() {
      const stories = JSON.parse(localStorage.getItem('divineStories') || '[]');
      const container = document.getElementById('stories-container');
      container.innerHTML = '';
      stories.forEach(item => {
        const div = document.createElement('div');
        div.className = 'story-circle';
        if (item.type === 'image') {
          div.style.backgroundImage = `url(${item.url})`;
        } else {
          div.style.background = 'linear-gradient(135deg, #667eea, #764ba2)';
          div.innerHTML = '<span style="font-size:14px;text-align:center;padding:10px;">' + item.text.slice(0,30) + '...</span>';
        }
        container.appendChild(div);
      });
    }

    function postStory() {
      const text = prompt('Enter status text (optional):');
      const input = document.createElement('input');
      input.type = 'file';
      input.accept = 'image/*,video/*';
      input.onchange = e => {
        const file = e.target.files[0];
        if (file || text) {
          const reader = new FileReader();
          if (file) {
            reader.onload = ev => {
              const item = { type: file.type.startsWith('image') ? 'image' : 'video', url: ev.target.result, text: text || '' };
              const stories = JSON.parse(localStorage.getItem('divineStories') || '[]');
              stories.push(item);
              localStorage.setItem('divineStories', JSON.stringify(stories));
              loadStories();
            };
            reader.readAsDataURL(file);
          } else {
            const item = { type: 'text', text: text };
            const stories = JSON.parse(localStorage.getItem('divineStories') || '[]');
            stories.push(item);
            localStorage.setItem('divineStories', JSON.stringify(stories));
            loadStories();
          }
        }
      };
      if (!text) input.click();
      else if (!text && !confirm('Post text only?')) return;
      else {
        const item = { type: 'text', text: text };
        const stories = JSON.parse(localStorage.getItem('divineStories') || '[]');
        stories.push(item);
        localStorage.setItem('divineStories', JSON.stringify(stories));
        loadStories();
      }
    }

    function loadChats() {
      const chatList = document.getElementById('chat-list');
      chatList.innerHTML = '';
      let chats = JSON.parse(localStorage.getItem('divineChatList') || '[]');

      if (!chats.some(c => c.id === 'ai')) {
        chats.unshift({ id: 'ai', name: 'Divine AI' });
        localStorage.setItem('divineChatList', JSON.stringify(chats));
      }

      chats.forEach(chat => createChatItem(chat));
    }

    function createChatItem(chat) {
      const div = document.createElement('div');
      div.className = 'chat-item';
      div.dataset.id = chat.id;
      div.onclick = () => selectChat(chat.id, chat.name);

      const preview = getLastPreview(chat.id);

      div.innerHTML = `
        <div class="avatar">${chat.id === 'ai' ? 'AI' : chat.name.charAt(0).toUpperCase()}</div>
        <div class="info">
          <h3>${chat.name}</h3>
          <p>${preview}</p>
        </div>
      `;

      document.getElementById('chat-list').appendChild(div);
    }

    function getLastPreview(chatId) {
      const saved = JSON.parse(localStorage.getItem('chat_' + chatId) || '[]');
      if (saved.length === 0) return 'No messages yet';
      const last = saved[saved.length - 1];
      let preview = last.content.replace(/<[^>]*>/g, '').trim();
      if (last.content.includes('<img') || last.content.includes('<video')) preview = '📱 Media';
      else if (last.content.includes('<audio')) preview = '🎤 Voice';
      else if (last.content.includes('<a')) preview = '📄 Document';
      if (!preview) preview = 'Media';
      if (last.type === 'outgoing') preview = 'You: ' + preview;
      return preview.slice(0, 50) + (preview.length > 50 ? '...' : '');
    }

    function addFriend() {
      const input = document.getElementById('search-input');
      let number = input.value.trim();
      if (!number) return alert('Enter phone number');
      number = number.replace(/[^0-9+]/g, '');
      const chatId = 'friend_' + number;
      let chats = JSON.parse(localStorage.getItem('divineChatList') || '[]');
      if (chats.some(c => c.id === chatId)) return alert('Already added');
      const name = `Friend ${number}`;
      chats.push({ id: chatId, name });
      localStorage.setItem('divineChatList', JSON.stringify(chats));
      createChatItem({ id: chatId, name });
      input.value = '';
    }

    function createGroup() {
      const name = prompt('Group name:');
      if (name) {
        const chatId = 'group_' + Date.now();
        let chats = JSON.parse(localStorage.getItem('divineChatList') || '[]');
        chats.push({ id: chatId, name: `${name} (Group)` });
        localStorage.setItem('divineChatList', JSON.stringify(chats));
        createChatItem({ id: chatId, name: `${name} (Group)` });
      }
    }

    function createCommunity() {
      const name = prompt('Community name:');
      if (name) {
        const chatId = 'comm_' + Date.now();
        let chats = JSON.parse(localStorage.getItem('divineChatList') || '[]');
        chats.push({ id: chatId, name: `${name} (Channel)` });
        localStorage.setItem('divineChatList', JSON.stringify(chats));
        createChatItem({ id: chatId, name: `${name} (Channel)` });
      }
    }

    function selectChat(chatId, name) {
      document.querySelector('.chat-item.active')?.classList.remove('active');
      document.querySelector(`.chat-item[data-id="${chatId}"]`)?.classList.add('active');
      currentChat = chatId;
      document.getElementById('chat-name').innerText = name;
      const messagesDiv = document.getElementById('messages');
      messagesDiv.innerHTML = '';
      const saved = JSON.parse(localStorage.getItem('chat_' + chatId) || '[]');
      saved.forEach(m => appendMessage(m.content, m.type, m.time));
      messagesDiv.scrollTop = messagesDiv.scrollHeight;
    }

    function appendMessage(content, type, time = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })) {
      const div = document.createElement('div');
      div.className = `message ${type}`;
      div.innerHTML = content + `<span class="time">${time}</span>`;
      document.getElementById('messages').appendChild(div);
      document.getElementById('messages').scrollTop = document.getElementById('messages').scrollHeight;
    }

    function saveMessages() {
      if (!currentChat) return;
      const msgs = Array.from(document.querySelectorAll('#messages .message:not(.typing-indicator)')).map(m => ({
        content: m.innerHTML.replace(/<span class="time">.*<\/span>/, ''),
        type: m.classList.contains('outgoing') ? 'outgoing' : 'incoming',
        time: m.querySelector('.time')?.innerText || ''
      }));
      localStorage.setItem('chat_' + currentChat, JSON.stringify(msgs));
    }

    function updatePreview() {
      if (!currentChat) return;
      const preview = getLastPreview(currentChat);
      const item = document.querySelector(`.chat-item[data-id="${currentChat}"]`);
      if (item) item.querySelector('.info p').innerText = preview;
    }

    function sendMessage() {
      const input = document.getElementById('message-input');
      const text = input.value.trim();
      if (!text || !currentChat) return;
      appendMessage(text, 'outgoing');
      input.value = '';
      saveMessages();
      updatePreview();

      if (currentChat === 'ai') aiRespond('text', text);
    }

    function handleEnter(e) {
      if (e.key === 'Enter') sendMessage();
    }

    document.getElementById('file-input').onchange = () => {
      const files = document.getElementById('file-input').files;
      if (!files.length || !currentChat) return;

      Array.from(files).forEach(file => {
        const reader = new FileReader();
        reader.onload = e => {
          let content = '';
          let type = 'document';
          if (file.type.startsWith('image/')) {
            content = `<img src="${e.target.result}" alt="Image">`;
            type = 'image';
          } else if (file.type.startsWith('video/')) {
            content = `<video controls src="${e.target.result}"></video>`;
            type = 'video';
          } else if (file.type.startsWith('audio/')) {
            content = `<audio controls src="${e.target.result}"></audio>`;
            type = 'voice';
          } else {
            content = `<a href="${e.target.result}" download="${file.name}">📄 ${file.name}</a>`;
            type = 'document';
          }
          appendMessage(content, 'outgoing');
          saveMessages();
          updatePreview();

          if (currentChat === 'ai') aiRespond(type);
        };
        reader.readAsDataURL(file);
      });
    };

    const voiceBtn = document.getElementById('voice-btn');
    voiceBtn.addEventListener('mousedown', startRecording);
    voiceBtn.addEventListener('mouseup', stopRecording);
    voiceBtn.addEventListener('mouseleave', stopRecording);
    voiceBtn.addEventListener('touchstart', e => { e.preventDefault(); startRecording(); });
    voiceBtn.addEventListener('touchend', e => { e.preventDefault(); stopRecording(); });

    function startRecording() {
      navigator.mediaDevices.getUserMedia({ audio: true }).then(stream => {
        mediaStream = stream;
        recorder = new MediaRecorder(stream);
        audioChunks = [];
        recorder.start();
        recorder.ondataavailable = e => audioChunks.push(e.data);
      }).catch(() => alert('Mic access denied'));
    }

    function stopRecording() {
      if (recorder && recorder.state !== 'inactive') {
        recorder.stop();
        recorder.onstop = () => {
          const blob = new Blob(audioChunks, { type: 'audio/ogg' });
          const url = URL.createObjectURL(blob);
          appendMessage(`<audio controls src="${url}"></audio>`, 'outgoing');
          saveMessages();
          updatePreview();

          if (currentChat === 'ai') aiRespond('voice');

          mediaStream.getTracks().forEach(track => track.stop());
        };
      }
    }

    function startVideoCall() {
      document.getElementById('video-modal').style.display = 'flex';
      navigator.mediaDevices.getUserMedia({ video: true, audio: true }).then(stream => {
        document.getElementById('local-video').srcObject = stream;
        mediaStream = stream;
      }).catch(() => alert('Camera/mic access denied'));
    }

    function endVideoCall() {
      document.getElementById('video-modal').style.display = 'none';
      if (mediaStream) mediaStream.getTracks().forEach(track => track.stop());
    }

    function deleteCurrentChat() {
      if (!currentChat || currentChat === 'ai') return alert('Cannot delete this chat');
      if (confirm('Delete entire chat?')) {
        localStorage.removeItem('chat_' + currentChat);
        document.getElementById('messages').innerHTML = '';
        let chats = JSON.parse(localStorage.getItem('divineChatList') || '[]');
        chats = chats.filter(c => c.id !== currentChat);
        localStorage.setItem('divineChatList', JSON.stringify(chats));
        document.querySelector(`.chat-item[data-id="${currentChat}"]`)?.remove();
        currentChat = null;
        document.getElementById('chat-name').innerText = 'Select a chat';
      }
    }
  </script>
</body>
</html>
