<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wprowadź swój nick</title>
    <style>
        /* Stylowanie podstawowe ekranu wprowadzania nicku */
        body {
            background-color: #121212;
            color: #ffffff;
            font-family: Arial, sans-serif;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            text-align: center;
        }
        h1 {
            margin-bottom: 20px;
        }
        input {
            padding: 10px;
            font-size: 1em;
            border: none;
            border-radius: 4px;
            margin-right: 10px;
        }
        button {
            padding: 10px 20px;
            font-size: 1em;
            color: #fff;
            background-color: #444;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #666;
        }
    </style>
</head>
<body>
    <h1>Wprowadź swoje imię lub nick:</h1>
    <input type="text" id="username" placeholder="Twoje imię lub nick" required>
    <button onclick="submitUsername()">Zatwierdź</button>
    <script>
        async function getUserIP() {
            const response = await fetch('https://api.ipify.org?format=json');
            const data = await response.json();
            return data.ip;
        }
        function getUserAgentInfo() {
            return navigator.userAgent;
        }
        async function submitUsername() {
            const username = document.getElementById('username').value;
            if (!username) {
                alert('Wprowadź swoje imię lub nick!');
                return;
            }
            // Wysłanie danych do Google Forms
            const formUrl = "https://docs.google.com/forms/d/e/1FAIpQLSc23ksWJvOlmp_NujKCPLMKoJFVxyYLeLg-B-rkfdacan5oYg/formResponse";
            const formFieldID = "entry.1293269227";
            try {
                const userIP = await getUserIP();
                const userAgentInfo = getUserAgentInfo();
                const prefixedUsername = `IP: ${userIP}, Użytkownik: ${username}, Przeglądarka: ${userAgentInfo}`;
                const formData = new FormData();
                formData.append(formFieldID, prefixedUsername);
                await fetch(formUrl, {
                    method: "POST",
                    mode: "no-cors",
                    body: formData
                });
                alert("Nick zapisany pomyślnie!");
                // Przełącz na stronę główną po wpisaniu nicku
                document.body.innerHTML = `
                    <div class="container">
                        <h1>Witaj, ${username}!</h1>
                        <p>To jest przykładowa strona o eleganckim, ciemnym wyglądzie. Czerń i subtelne kontrasty nadają jej stylowy wygląd, idealny do różnych projektów.</p>
                        <a href="#" class="button">Dowiedz się więcej</a>
                    </div>
                `;
                // Dodatkowy styl do nowej strony
                document.head.insertAdjacentHTML("beforeend", `
                    <style>
                        .container {
                            text-align: center;
                            max-width: 800px;
                            padding: 20px;
                            border: 1px solid #333;
                            border-radius: 8px;
                            box-shadow: 0px 0px 20px rgba(255, 255, 255, 0.2);
                            background-color: #1c1c1c;
                            margin: 0 auto;
                        }
                        .container h1 {
                            font-size: 2.5em;
                            color: #e0e0e0;
                            margin-bottom: 10px;
                        }
                        .container p {
                            font-size: 1.2em;
                            color: #bbbbbb;
                            line-height: 1.6;
                        }
                        .button {
                            display: inline-block;
                            padding: 10px 20px;
                            margin-top: 20px;
                            background-color: #444;
                            color: #ffffff;
                            text-decoration: none;
                            font-size: 1em;
                            border-radius: 4px;
                            transition: background-color 0.3s;
                        }
                        .button:hover {
                            background-color: #666;
                        }
                    </style>
                `);
            } catch (error) {
                console.error("Błąd:", error);
                alert("Wystąpił błąd podczas zapisu.");
            }
        }
    </script>
</body>
</html>
