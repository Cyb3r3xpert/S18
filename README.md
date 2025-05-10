<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>BTEUP Card Portal</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #74ebd5, #acb6e5);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .container {
      background: white;
      padding: 40px 30px;
      border-radius: 16px;
      box-shadow: 0 12px 24px rgba(0, 0, 0, 0.2);
      text-align: center;
      width: 100%;
      max-width: 400px;
      animation: fadeIn 0.8s ease-in-out;
    }

    h1 {
      margin-bottom: 20px;
      font-size: 24px;
      color: #333;
    }

    input[type="text"] {
      padding: 12px;
      width: 100%;
      margin-bottom: 20px;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 16px;
      transition: border 0.3s, box-shadow 0.3s;
    }

    input:focus {
      outline: none;
      border-color: #0078d7;
      box-shadow: 0 0 5px rgba(0, 120, 215, 0.5);
    }

    .options {
      display: flex;
      justify-content: center;
      gap: 20px;
      margin-bottom: 20px;
    }

    label {
      font-size: 16px;
      color: #333;
    }

    button {
      padding: 12px 24px;
      background-color: #0078d7;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 16px;
      transition: background-color 0.3s ease;
    }

    button:hover {
      background-color: #005fa3;
    }

    .credit {
      margin-top: 30px;
      font-size: 14px;
      color: #444;
    }

    .credit a {
      color: #0078d7;
      text-decoration: none;
      font-weight: bold;
    }

    .credit a:hover {
      text-decoration: underline;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>BTEUP Card Generator</h1>
    <input type="text" id="enrollInput" placeholder="Enter your Enrollment Number">
    
    <div class="options">
      <label><input type="radio" name="cardType" value="admit" checked> Admit Card</label>
      <label><input type="radio" name="cardType" value="verify"> Verification Card</label>
    </div>

    <button onclick="redirectToCard()">Submit</button>

    <p class="credit">Website made by <strong>cyb3e 3xp3rt</strong> | Contact: <a href="https://t.me/slayer9646" target="_blank">@slayer9646</a></p>
  </div>

  <script>
    function redirectToCard() {
      const enrollNumber = document.getElementById("enrollInput").value.trim();
      const cardType = document.querySelector('input[name="cardType"]:checked').value;

      if (!enrollNumber) {
        alert("Please enter a valid enrollment number.");
        return;
      }

      let baseUrl = "";
      if (cardType === "admit") {
        baseUrl = "https://bteup.ac.in/ESeva/Student/AdmitCard.aspx?EnrollNumber=";
      } else if (cardType === "verify") {
        baseUrl = "https://bteup.ac.in/ESeva/Student/VerificationCard.aspx?EnrollNumber=";
      }

      const fullUrl = baseUrl + encodeURIComponent(enrollNumber);
      window.location.href = fullUrl; // Redirects in same tab (no link shown)
    }
  </script>
</body>
</html>