const express = require("express");
const app = express();

app.use(express.json());

const PORT = process.env.PORT || 3000;

app.get("/", (req, res) => {
  res.send("Bot Tài Xỉu đang hoạt động!");
});

app.post("/webhook", (req, res) => {
  res.sendStatus(200);

  const data = req.body;

  const message = (
    data.message?.text ||
    data.text ||
    ""
  ).trim().toLowerCase();

  // Chỉ xử lý lệnh .taixiu
  if (!message.includes(".taixiu")) return;

  // Chấp nhận tài hoặc xiu
  const match = message.match(
    /@bot\s+\.taixiu\s+(tài|tai|xỉu|xiu)\b/i
  );

  if (!match) return;

  // Random 50/50
  const ketQua = Math.random() < 0.5
    ? "Tài"
    : "Xỉu";

  const traLoi = `🎲 Kết Quả : ${ketQua}`;

  console.log("Lệnh:", message);
  console.log("Bot trả lời:", traLoi);

  // TODO:
