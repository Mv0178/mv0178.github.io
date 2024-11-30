<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Compteur de Clics</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600&display=swap" rel="stylesheet">
    <link rel="icon" href="https://cdn-icons-png.flaticon.com/512/5893/5893051.png" type="image/png" />
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            text-align: center;
            margin: 0;
            padding: 20px;
            background-image: url('https://cdn-icons-png.flaticon.com/512/7346/7346836.png');
            background-size: cover;
            background-position: center;
            color: #333;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        .views-container {
            position: absolute;
            top: 20px;
            left: 20px;
            background-color: rgba(30, 30, 30, 0.8);
            color: #00ff00;
            border: 2px solid #00ff00;
            border-radius: 15px;
            padding: 10px;
            width: 150px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.5);
            text-align: center;
        }

        .credits {
            position: absolute;
            bottom: 20px;
            right: 20px;
            text-align: left;
            font-size: 16px;
            color: #666;
            font-weight: bold;
        }

        .credits img {
            width: 60px;
            vertical-align: middle;
            margin-right: 5px;
        }

        .main-content {
            flex: 1;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            padding: 40px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            max-width: 500px;
            margin: 60px auto;
            position: relative;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .central-logo {
            position: absolute;
            top: -100px;
            left: 50%;
            transform: translateX(-50%);
            width: 200px;
        }

        h1 {
            color: #ff6347;
            margin-bottom: 20px;
            font-size: 60px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        }

        input {
            padding: 10px;
            font-size: 16px;
            border: 2px solid #ccc;
            border-radius: 5px;
            width: 80%;
            margin-bottom: 20px;
            transition: border-color 0.3s;
        }

        input:focus {
            border-color: #ff6347;
        }

        button {
            padding: 15px 30px;
            font-size: 24px;
            background-color: #ffeb3b;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px;
            display: flex;
            align-items: center;
        }

        #clickIcon {
            width: 40px;
            margin-right: 10px;
        }

        #totalClicks, #userClicks {
            font-size: 24px;
            margin: 20px 0;
        }

        #leaderboard {
            text-align: left;
            margin: 0 auto;
            background-color: #fff;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
            width: 300px;
        }

        .leaderboard-entry {
            margin: 5px 0;
            font-size: 18px;
        }

        .credit {
            margin-top: 20px;
            font-size: 20px;
            color: #666;
        }

        .copyright {
            font-size: 12px;
            color: #999;
        }
    </style>
</head>
<body>

    <div class="views-container">
        <h3>Nombre de vues :</h3>
        <div id="viewCount">0</div>
    </div>

    <img src="https://cdn-icons-png.flaticon.com/512/5893/5893051.png" alt="Logo" class="central-logo"/>

    <div class="main-content" id="mainContent">
        <h1>Compteur de Clics</h1>
        <input type="text" id="username" placeholder="Entrez votre nom d'utilisateur" aria-label="Nom d'utilisateur" />
        <button id="clickButton" aria-label="Cliquez ici pour compter un clic">
            <img src="https://cdn-icons-png.flaticon.com/512/5226/5226574.png" id="clickIcon" alt="Cliquez ici !" /> 
            Cliquez ici !
        </button>

        <div id="totalClicks">Total des clics : 0</div>
        <div id="userClicks"></div>

        <div id="leaderboard"></div>
        <p><strong>Tapez</strong> sur l'écran pour cliquer sur mobile !</p>
    </div>

    <div class="credits">
        <img src="https://cdn.pixabay.com/photo/2020/09/17/22/52/website-5580513_1280.png" alt="Logo Crédit" />
        <p>Développé par<br>Sar et Maël V</p>
        <p class="copyright">Tout droit réservé</p>
    </div>

    <script>
        // Chargement des données du stockage local
        let totalClicks = localStorage.getItem('totalClicks') ? parseInt(localStorage.getItem('totalClicks')) : 0;
        let viewCount = localStorage.getItem('viewCount') ? parseInt(localStorage.getItem('viewCount')) : 0;
        const userClicks = JSON.parse(localStorage.getItem('userClicks')) || {};
        let lastClickTime = 0;
        const clickDelay = 10; // 10 millisecondes entre les clics

        // Incrémente le nombre de vues uniquement lors du premier chargement
        if (viewCount === 0) {
            viewCount++;
            localStorage.setItem('viewCount', viewCount);
        }

        // Mise à jour de l'affichage initial
        document.getElementById('totalClicks').innerText = `Total des clics : ${totalClicks}`;
        document.getElementById('viewCount').innerText = viewCount;

        // Écouteur d'événement pour le clic du bouton
        document.getElementById('clickButton').addEventListener('click', registerClick);

        function registerClick() {
            const currentTime = Date.now();

            // Vérifie si suffisamment de temps s'est écoulé depuis le dernier clic
            if (currentTime - lastClickTime >= clickDelay) {
                lastClickTime = currentTime;

                const username = document.getElementById('username').value.trim() || 'Utilisateur';

                // Incrémente le nombre total de clics
                totalClicks++;
                userClicks[username] = (userClicks[username] || 0) + 1;

                // Sauvegarde dans le stockage local
                localStorage.setItem('totalClicks', totalClicks);
                localStorage.setItem('userClicks', JSON.stringify(userClicks));

                // Met à jour l'affichage
                document.getElementById('totalClicks').innerText = `Total des clics : ${totalClicks}`;
                document.getElementById('userClicks').innerText = `${username} a cliqué ! 🎉`;

                updateLeaderboard();
            } else {
                alert("Attendez un moment avant de cliquer à nouveau !");
            }
        }

        function updateLeaderboard() {
            let leaderboardHtml = "<h3>Classement :</h3>";
            const sortedUsers = Object.keys(userClicks).sort((a, b) => userClicks[b] - userClicks[a]);
            sortedUsers.forEach(user => {
                leaderboardHtml += `<div class="leaderboard-entry">${user} : ${userClicks[user]} clic(s) 🌟</div>`;
            });
            document.getElementById('leaderboard').innerHTML = leaderboardHtml;
        }
    </script>

</body>
</html>
