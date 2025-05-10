# GM-TEA
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GM Check-In</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      margin-top: 100px;
    }
    button {
      font-size: 24px;
      padding: 15px 30px;
      border-radius: 10px;
      background-color: #4CAF50;
      color: white;
      border: none;
      cursor: pointer;
    }
    p {
      font-size: 18px;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <h1>GM Check-In</h1>
  <button onclick="checkIn()">GM</button>
  <p id="lastCheck"></p>
  <p id="streakDisplay"></p>

  <script>
    const lastCheckKey = "lastCheckIn";
    const streakKey = "gmStreak";

    function formatDate(d) {
      return d.toISOString().split('T')[0];
    }

    function checkIn() {
      const today = new Date();
      const todayStr = formatDate(today);
      const last = localStorage.getItem(lastCheckKey);
      let streak = parseInt(localStorage.getItem(streakKey)) || 0;

      if (last !== todayStr) {
        // Check if yesterday
        if (last === formatDate(new Date(today.setDate(today.getDate() - 1)))) {
          streak += 1;
        } else {
          streak = 1;
        }
        localStorage.setItem(lastCheckKey, todayStr);
        localStorage.setItem(streakKey, streak);
      }

      updateDisplay();
    }

    function updateDisplay() {
      const last = localStorage.getItem(lastCheckKey);
      const streak = localStorage.getItem(streakKey) || 0;

      document.getElementById("lastCheck").innerText = last
        ? "Last check-in: " + last
        : "No check-in yet.";
      document.getElementById("streakDisplay").innerText = "Streak: " + streak + " day(s)";
  

    updateDisplay();
  </script>
</body>
</html>
