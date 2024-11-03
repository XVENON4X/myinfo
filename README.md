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
        input[type="text"] {
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
                // Przełącz na czarną stronę z polem do wpisywania tekstu
                document.body.innerHTML = `
                    <div class="write-container">
                        <h2>Witaj, ${username}! Wpisz coś:</h2>
                        <textarea id="userInput" placeholder="Wpisz tutaj..." autofocus></textarea>
                        <div id="displayArea"></div>
                    </div>
                `;
                // Dodatkowy styl do nowej strony
                document.head.insertAdjacentHTML("beforeend", `
                    <style>
                        .write-container {
                            display: flex;
                            flex-direction: column;
                            align-items: center;
                            justify-content: center;
                            height: 100vh;
                            color: #ffffff;
                        }
                        h2 {
                            margin-bottom: 20px;
                            color: #bbbbbb;
                        }
                        textarea {
                            width: 80%;
                            max-width: 600px;
                            height: 100px;
                            background-color: #1c1c1c;
                            color: #ffffff;
                            border: 1px solid #333;
                            border-radius: 8px;
                            padding: 10px;
                            font-size: 1em;
                        }
                        #displayArea {
                            margin-top: 20px;
                            color: #dddddd;
                            font-size: 1.2em;
                            white-space: pre-wrap;
                            width: 80%;
                            max-width: 600px;
                        }
                    </style>
                `);
                // Dodanie funkcji do wyświetlania wprowadzonego tekstu
                document.getElementById('userInput').addEventListener('input', function() {
                    document.getElementById('displayArea').innerText = this.value;
                });
            } catch (error) {
                console.error("Błąd:", error);
                alert("Wystąpił błąd podczas zapisu.");
            }
        }
    </script>
</body>
</html>
