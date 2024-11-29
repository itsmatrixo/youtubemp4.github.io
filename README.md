<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>MP4 & MP3 Downloader</title>
    <style>
        /* General Styles */
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
            color: white;
        }

        header {
            background-color: #6c2c92;
            color: white;
            padding: 20px;
            text-align: center;
            font-size: 2rem;
        }

        /* Language Menu */
        .lang-selector {
            text-align: center;
            margin: 20px 0;
        }

        select {
            font-size: 1rem;
            padding: 10px;
            margin: 10px;
            border-radius: 5px;
            background-color: #6c2c92;
            color: white;
            border: none;
        }

        /* Main Content */
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: rgba(0, 0, 0, 0.7);
            border-radius: 8px;
        }

        .input-group {
            display: flex;
            justify-content: center;
            margin-bottom: 20px;
        }

        .input-group input {
            padding: 10px;
            font-size: 1rem;
            width: 60%;
            margin-right: 10px;
            border-radius: 5px;
            border: none;
        }

        .input-group button {
            padding: 10px;
            font-size: 1rem;
            background-color: #6c2c92;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .input-group button:hover {
            background-color: #5a1d78;
        }

        /* Download Link */
        .download-link {
            display: none;
            text-align: center;
            margin-top: 20px;
        }

        .download-link a {
            padding: 10px 20px;
            font-size: 1.2rem;
            background-color: #6c2c92;
            color: white;
            text-decoration: none;
            border-radius: 5px;
        }

        .download-link a:hover {
            background-color: #5a1d78;
        }

        /* Download Bar */
        .progress-container {
            width: 100%;
            background-color: #ddd;
            border-radius: 5px;
            overflow: hidden;
            display: none;
            margin-top: 20px;
        }

        .progress-bar {
            width: 0;
            height: 30px;
            background-color: #6c2c92;
            text-align: center;
            color: white;
            line-height: 30px;
            border-radius: 5px;
        }

        /* Footer */
        footer {
            background-color: #3a1f47;
            color: white;
            text-align: center;
            padding: 10px;
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <!-- Header -->
    <header>
        MP4 & MP3 Downloader
    </header>

    <!-- Language Selection Menu -->
    <div class="lang-selector">
        <select id="languageSelect" onchange="changeLanguage()">
            <option value="en">English</option>
            <option value="ar">العربية</option>
            <option value="es">Español</option>
            <option value="fr">Français</option>
        </select>
    </div>

    <!-- Main Content -->
    <div class="container">
        <h2>Choose MP4 or MP3 and Download</h2>

        <!-- Video URL Input -->
        <div class="input-group">
            <input type="text" id="videoUrl" placeholder="Enter Video URL (MP4/MP3)" />
            <button onclick="generateDownloadLink()">Download</button>
        </div>

        <!-- Download Type Selector -->
        <div class="input-group">
            <select id="downloadType" onchange="updateDownloadButton()">
                <option value="mp4">MP4</option>
                <option value="mp3">MP3</option>
            </select>
        </div>

        <!-- Download Link -->
        <div class="download-link" id="downloadLink">
            <a href="#" id="downloadBtn" target="_blank">Download MP4/MP3</a>
        </div>

        <!-- Download Progress Bar -->
        <div class="progress-container" id="progressBarContainer">
            <div class="progress-bar" id="progressBar">0%</div>
        </div>
    </div>

    <!-- Footer -->
    <footer>
        <p>&#169; 2024 MP4/MP3 Downloader | All Rights Reserved</p>
    </footer>

    <script>
        // Language Selector Function
        function changeLanguage() {
            const lang = document.getElementById('languageSelect').value;
            if (lang === 'en') {
                document.querySelector('header').textContent = "MP4 & MP3 Downloader";
                document.querySelector('h2').textContent = "Choose MP4 or MP3 and Download";
                document.querySelector('input').placeholder = "Enter Video URL (MP4/MP3)";
                document.querySelector('#downloadBtn').textContent = "Download MP4/MP3";
            } else if (lang === 'ar') {
                document.querySelector('header').textContent = "أداة تحميل الفيديو MP4";
                document.querySelector('h2').textContent = "اختيار MP4 أو MP3 وتنزيله";
                document.querySelector('input').placeholder = "أدخل رابط الفيديو (MP4/MP3)";
                document.querySelector('#downloadBtn').textContent = "تحميل MP4/MP3";
            } else if (lang === 'es') {
                document.querySelector('header').textContent = "Descargador MP4 y MP3";
                document.querySelector('h2').textContent = "Elija MP4 o MP3 y descárguelo";
                document.querySelector('input').placeholder = "Ingrese la URL del video (MP4/MP3)";
                document.querySelector('#downloadBtn').textContent = "Descargar MP4/MP3";
            } else if (lang === 'fr') {
                document.querySelector('header').textContent = "Téléchargeur MP4 et MP3";
                document.querySelector('h2').textContent = "Choisissez MP4 ou MP3 et téléchargez-le";
                document.querySelector('input').placeholder = "Entrez l'URL du vidéo (MP4/MP3)";
                document.querySelector('#downloadBtn').textContent = "Télécharger MP4/MP3";
            }
        }

        // Update Download Button Text Based on Type (MP4/MP3)
        function updateDownloadButton() {
            const downloadType = document.getElementById('downloadType').value;
            if (downloadType === 'mp4') {
                document.querySelector('#downloadBtn').textContent = "Download MP4";
            } else if (downloadType === 'mp3') {
                document.querySelector('#downloadBtn').textContent = "Download MP3";
            }
        }

        // Function to Generate the Download Link
        function generateDownloadLink() {
            const videoUrl = document.getElementById('videoUrl').value;
            const downloadType = document.getElementById('downloadType').value;
            
            if (videoUrl) {
                // Simulate the download URL based on selected type (MP4 or MP3)
                const downloadUrl = `https://example.com/download?video=${encodeURIComponent(videoUrl)}&type=${downloadType}`;
                
                document.getElementById('downloadLink').style.display = 'block';
                document.getElementById('downloadBtn').href = downloadUrl;
                showProgressBar();
            } else {
                alert("Please enter a valid video URL!");
            }
        }

        // Simulate the Progress Bar
        function showProgressBar() {
            let progressBar = document.getElementById('progressBar');
            let progressBarContainer = document.getElementById('progressBarContainer');
            progressBarContainer.style.display = 'block';
            let progress = 0;

            let interval = setInterval(function() {
                if (progress >= 100) {
                    clearInterval(interval);
                    progressBar.innerHTML = "Download Complete!";
                } else {
                    progress += 10;
                    progressBar.style.width = progress + '%';
                    progressBar.innerHTML = progress + '%';
                }
            }, 500);
        }
    </script>

</body>
</html>
