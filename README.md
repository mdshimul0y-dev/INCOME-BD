income-bd/
│
├── bot.js
├── web/
│   ├── index.html
│   └── style.css
├── package.json
└── .env{
  "name": "income-bd",
  "version": "1.0.0",
  "main": "bot.js",
  "type": "module",
  "dependencies": {
    "express": "^4.18.2",
    "node-telegram-bot-api": "^0.61.0",
    "dotenv": "^16.3.1"
  }
}import TelegramBot from "node-telegram-bot-api";
import express from "express";
import dotenv from "dotenv";
dotenv.config();

const app = express();
const bot = new TelegramBot(process.env.BOT_TOKEN, { polling: true });

app.use(express.static("web"));

bot.onText(/\/start/, (msg) => {
  const chatId = msg.chat.id;
  const opts = {
    reply_markup: {
      inline_keyboard: [
        [
          {
            text: "🌱 Start Income",
            web_app: { url: "https://your-domain.vercel.app" } // এখানে তোমার ওয়েবসাইট লিংক বসাও
          }
        ]
      ]
    }
  };
  bot.sendMessage(chatId, "Welcome to Income BD! 💸", opts);
});

app.listen(process.env.PORT, () => {
  console.log("Web app running on port " + process.env.PORT);
});<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Income BD</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <div class="container">
    <h1>💸 Welcome to Income BD</h1>
    <p>Start earning your daily points!</p>
    <button id="earnBtn">Start Earning</button>
    <p id="msg"></p>
  </div>

  <script>
    const btn = document.getElementById("earnBtn");
    const msg = document.getElementById("msg");
    btn.onclick = () => {
      msg.textContent = "🎉 You earned 10 points!";
    };
  </script>
</body>
</html>body {
  background: linear-gradient(to right, #00b09b, #96c93d);
  font-family: sans-serif;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}
.container {
  text-align: center;
  background: rgba(0,0,0,0.3);
  padding: 30px;
  border-radius: 15px;
}
button {
  background: #fff;
  color: #333;
  border: none;
  padding: 10px 20px;
  border-radius: 10px;
  font-size: 16px;
  cursor: pointer;
}
button:hover {
  background: #ddd;
}
