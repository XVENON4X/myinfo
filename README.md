<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wprowadź swój nick</title>
    <style>
        /* Stylowanie podstawowe ekranu wprowadzania nicku */
        body {
            background-color: #121212; /* Ciemne tło */
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
                    <div class="content">
                        <h1>Witaj, ${username}!</h1>
                        <p>Cześć! Witaj na mojej stronie. Nazywam się Maks, pochodzę z Podkarpacia, w Polsce. Od zawsze interesowałem się elektroniką i tym, co można z nią zrobić. Moje pasje są różnorodne, ale łączy je technologia – fascynuje mnie programowanie, tworzenie gier, praca z mikrokontrolerami, a także nagrywanie filmów na YouTube i drony FPV.
                        </p>
<p>
Jestem introwertykiem, a ludzie, którzy mnie znają, wiedzą, że potrzebuję czasu, aby otworzyć się na innych. Życie nauczyło mnie pewnej ostrożności, dlatego wolę mniejsze grupy i towarzystwo osób, które dobrze znam. Myślę, że zaledwie 1% osób, które mnie znają, naprawdę rozumie, kim jestem. W rozmowach bardziej słucham niż mówię – interesuje mnie, co inni mają do powiedzenia. Staram się unikać sytuacji, w których ludzie przerywają sobie nawzajem albo niepotrzebnie podnoszą głos. Cenię spokój i szacunek w komunikacji.
</p>
<p>
jak ja myślę o sobie: Kiedy myślę o sobie, widzę kogoś, kto zawsze jest zajęty, ale mimo to stara się robić jak najwięcej. Mam wrażenie, że na nic nie mam czasu, a jednocześnie próbuję zajmować się wszystkim, co mnie interesuje. Szkoła jest dla mnie sporym wyzwaniem – potrafię spędzić trzy godziny ucząc się czegoś, a potem dostać ocenę niedostateczną. Nie jestem typem osoby, która dobrze radzi sobie z bezmyślnym „wkuwaniem” wiedzy. To podejście do nauki, w którym liczy się tylko zapamiętywanie, nie przemawia do mnie i uważam je za mało sensowne. Wolę zrozumieć, jak coś działa, zamiast po prostu zapamiętać fakty.
</p>
<p>
Z drugiej strony, rzeczy, które naprawdę lubię, przychodzą mi naturalnie i nie wymagają wielkiego wysiłku. Jednak niewiele osób tak naprawdę mnie rozumie. Nie jestem osobą, która łatwo się otwiera – jeśli nie muszę rozmawiać, to zazwyczaj tego unikam. Być może dlatego trudno jest mnie dobrze poznać.
</p>
<p>
jak myśle że inni myślą o mnie: Jak myślę, że inni mnie postrzegają? Wydaje mi się, że wiele osób widzi mnie jako osobę leniwą, która unika obowiązków i po prostu spędza czas na graniu w gry. Często czuję, że ludzie myślą, że nie interesuję się niczym poważnym, że nie chce mi się uczyć ani rozwijać, a jedyne, co umiem, to ubierać się na czarno i siedzieć w swoim świecie.
</p>
<p>
Wiem, że taki obraz może wydawać się prosty, ale nie oddaje tego, kim naprawdę jestem. Jestem introwertykiem, który sporo analizuje i ma własne podejście do życia. Może nie zawsze robię to, czego inni oczekują, i nie zawsze podążam za tym, co wydaje się być „normą.” Ale mam swoje zainteresowania i cele, nawet jeśli nie są one widoczne na pierwszy rzut oka.</p>
                    </div>
                `;
                // Dodatkowy styl do nowej strony
                document.head.insertAdjacentHTML("beforeend", `
                    <style>
                        body {
                            background-color: #121212; /* Ciemne tło dla całej strony */
                            color: #ffffff; /* Kolor tekstu */
                            margin: 0;
                            padding: 20px;
                            font-family: Arial, sans-serif;
                        }
                        .content {
                            color: #ffffff; /* Kolor tekstu */
                            line-height: 1.6; /* Lepsza czytelność tekstu */
                        }
                        h1 {
                            font-size: 2.5em;
                            margin-bottom: 10px;
                        }
                        p {
                            font-size: 1.2em; /* Zmniejsz rozmiar czcionki */
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
