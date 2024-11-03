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
                // Przełącz na czarną stronę z informacjami i polem do wpisywania tekstu
                document.body.innerHTML = `
                    <div class="info-container">
                        <h2>Witaj, ${username}!</h2>
                        <p>
                        Cześć! Witaj na mojej stronie. Nazywam się Maks, pochodzę z Podkarpacia, w Polsce. Od zawsze interesowałem się elektroniką i tym, co można z nią zrobić. Moje pasje są różnorodne, ale łączy je technologia – fascynuje mnie programowanie, tworzenie gier, praca z mikrokontrolerami, a także nagrywanie filmów na YouTube i drony FPV.

Jestem introwertykiem, a ludzie, którzy mnie znają, wiedzą, że potrzebuję czasu, aby otworzyć się na innych. Życie nauczyło mnie pewnej ostrożności, dlatego wolę mniejsze grupy i towarzystwo osób, które dobrze znam. Myślę, że zaledwie 1% osób, które mnie znają, naprawdę rozumie, kim jestem. W rozmowach bardziej słucham niż mówię – interesuje mnie, co inni mają do powiedzenia. Staram się unikać sytuacji, w których ludzie przerywają sobie nawzajem albo niepotrzebnie podnoszą głos. Cenię spokój i szacunek w komunikacji.

jak ja myślę o sobie: Kiedy myślę o sobie, widzę kogoś, kto zawsze jest zajęty, ale mimo to stara się robić jak najwięcej. Mam wrażenie, że na nic nie mam czasu, a jednocześnie próbuję zajmować się wszystkim, co mnie interesuje. Szkoła jest dla mnie sporym wyzwaniem – potrafię spędzić trzy godziny ucząc się czegoś, a potem dostać ocenę niedostateczną. Nie jestem typem osoby, która dobrze radzi sobie z bezmyślnym „wkuwaniem” wiedzy. To podejście do nauki, w którym liczy się tylko zapamiętywanie, nie przemawia do mnie i uważam je za mało sensowne. Wolę zrozumieć, jak coś działa, zamiast po prostu zapamiętać fakty.

Z drugiej strony, rzeczy, które naprawdę lubię, przychodzą mi naturalnie i nie wymagają wielkiego wysiłku. Jednak niewiele osób tak naprawdę mnie rozumie. Nie jestem osobą, która łatwo się otwiera – jeśli nie muszę rozmawiać, to zazwyczaj tego unikam. Być może dlatego trudno jest mnie dobrze poznać.

jak myśle że inni myślą o mnie: Jak myślę, że inni mnie postrzegają? Wydaje mi się, że wiele osób widzi mnie jako osobę leniwą, która unika obowiązków i po prostu spędza czas na graniu w gry. Często czuję, że ludzie myślą, że nie interesuję się niczym poważnym, że nie chce mi się uczyć ani rozwijać, a jedyne, co umiem, to ubierać się na czarno i siedzieć w swoim świecie.

Wiem, że taki obraz może wydawać się prosty, ale nie oddaje tego, kim naprawdę jestem. Jestem introwertykiem, który sporo analizuje i ma własne podejście do życia. Może nie zawsze robię to, czego inni oczekują, i nie zawsze podążam za tym, co wydaje się być „normą.” Ale mam swoje zainteresowania i cele, nawet jeśli nie są one widoczne na pierwszy rzut oka.
                        </p>
                        <textarea id="userInput" placeholder="Wpisz tutaj..." autofocus></textarea>
                        <div id="displayArea"></div>
                    </div>
                `;
                // Dodatkowy styl do nowej strony
                document.head.insertAdjacentHTML("beforeend", `
                    <style>
                        .info-container {
                            display: flex;
                            flex-direction: column;
                            align-items: center;
                            justify-content: center;
                            height: 100vh;
                            color: #ffffff;
                            padding: 20px;
                            overflow-y: auto;
                        }
                        h2 {
                            margin-bottom: 20px;
                        }
                        p {
                            text-align: justify;
                            margin: 10px 0;
                            line-height: 1.6;
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
                            margin-top: 20px;
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
                alert("Wystąpił błąd podczas zap
