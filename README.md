<!DOCTYPE
html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Compte à Rebours</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      color: #fff;
      margin: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      padding: 20px;
      text-align: center;
    }

    h1 {
      margin-bottom: 10px;
    }

    input[type="date"] {
      padding: 10px;
      font-size: 16px;
      border-radius: 8px;
      border: none;
      margin-bottom: 20px;
    }

    .countdown {
      font-size: 24px;
      margin-top: 20px;
      background: rgba(255,255,255,0.1);
      padding: 20px;
      border-radius: 15px;
    }

    @media (max-width: 480px) {
      .countdown {
        font-size: 18px;
      }
    }
  </style>
</head>
<body>
  <h1>⏳ Compte à Rebours</h1>
  <p>Sélectionne une date importante :</p>
  <input type="date" id="datePicker" />
  <div class="countdown" id="countdown">Aucune date sélectionnée</div>

  <script>
    const dateInput = document.getElementById("datePicker");
    const countdownEl = document.getElementById("countdown");

    let interval = null;

    dateInput.addEventListener("change", () => {
      clearInterval(interval); // reset timer

      const targetDate = new Date(dateInput.value);
      if (isNaN(targetDate)) return;

      interval = setInterval(() => {
        const now = new Date();
        const diff = targetDate - now;

        if (diff <= 0) {
          countdownEl.textContent = "🎉 La date est arrivée !";
          clearInterval(interval);
          return;
        }

        const days = Math.floor(diff / (1000 * 60 * 60 * 24));
        const hours = Math.floor((diff / (1000 * 60 * 60)) % 24);
        const minutes = Math.floor((diff / (1000 * 60)) % 60);
        const seconds = Math.floor((diff / 1000) % 60);

        countdownEl.textContent = `${days}j ${hours}h ${minutes}m ${seconds}s restants`;
      }, 1000);
    });
  </script>
</body>
</html>
