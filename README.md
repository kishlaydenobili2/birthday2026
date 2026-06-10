# birthday2026
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Happy Birthday! 🎂</title>
<style>
  body { font-family: sans-serif; text-align: center; background: #fff0f5; padding: 40px 20px; }
  h1 { font-size: 2.5em; color: #e0457b; }
  p  { color: #555; font-size: 1.1em; }
  textarea { width: 90%; max-width: 400px; height: 100px; font-size: 1em;
             border: 2px solid #e0457b; border-radius: 10px; padding: 10px; margin: 16px 0; }
  button { background: #e0457b; color: white; border: none; padding: 12px 32px;
           border-radius: 10px; font-size: 1.1em; cursor: pointer; }
  button:hover { background: #c0356b; }
  #status { margin-top: 16px; font-size: 1em; color: #333; }
</style>
</head>
<body>
  <h1>🎂 Happy Birthday! 🎉</h1>
  <p>Leave a birthday message — it'll appear on a special display just for you!</p>
  <br>
  <textarea id="msg" placeholder="Type your birthday wish here..."></textarea>
  <br>
  <button onclick="sendMsg()">Send Wish 💌</button>
  <div id="status"></div>

<script>
  // Replace this with your ngrok URL each time you start the tunnel
  const ESP_URL = "https://XXXX-XX-XX-XX-XX.ngrok-free.app";

  async function sendMsg() {
    const msg = document.getElementById("msg").value.trim();
    if (!msg) { document.getElementById("status").innerText = "Please write something first!"; return; }
    document.getElementById("status").innerText = "Sending... ✉️";
    try {
      const res = await fetch(ESP_URL + "/message", {
        method: "POST",
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
        body: "msg=" + encodeURIComponent(msg) 
      });
      if (res.ok) document.getElementById("status").innerText = "🎉 Message delivered!";
      else        document.getElementById("status").innerText = "Something went wrong. Try again!";
    } catch (e) {
      document.getElementById("status").innerText = "Could not reach the display. Is the tunnel running?";
    }
  }
</script>
</body>
</html>