<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>Live Stream | Cyb3r 3xpert</title>
    <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #0f0f0f;
            color: #f5f5f5;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .container {
            width: 100%;
            max-width: 900px;
            padding: 20px;
            position: relative;
            box-sizing: border-box;
        }
        h1 {
            margin-bottom: 20px;
            color: #00ffff;
            text-align: center;
        }
        video {
            width: 100%;
            border: 2px solid #00ffff;
            border-radius: 10px;
            background-color: black;
        }
        .watermark {
            position: absolute;
            bottom: 70px;
            right: 30px;
            background: rgba(0, 0, 0, 0.6);
            padding: 8px 12px;
            font-size: 14px;
            border-radius: 4px;
            color: #ffffff;
        }
        .quality-selector {
            margin-top: 40px;
            text-align: center;
        }
        select {
            padding: 8px 12px;
            background-color: #222;
            color: #fff;
            border: 1px solid #00ffff;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
        }
        select:focus {
            outline: none;
            box-shadow: 0 0 5px #00ffff;
        }
        #loading {
            color: gray;
            margin-top: 10px;
        }
        #viewerCount {
            margin-top: 15px;
            font-size: 18px;
            color: #00ff00;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Live Stream by Cyb3r 3xpert</h1>
        <div id="loading">Loading stream...</div>
        <video id="videoPlayer" controls style="display: none;">
            Your browser does not support HTML5 video.
        </video>
        <div id="viewerCount">Loading viewers...</div>
        <div class="watermark">Made by Cyb3r 3xpert</div>
        <div class="quality-selector">
            <label for="quality" style="margin-right: 8px;">Quality:</label>
            <select id="quality"></select>
        </div>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            const video = document.getElementById("videoPlayer");
            const qualitySelect = document.getElementById("quality");
            const loading = document.getElementById("loading");
            const viewerCount = document.getElementById("viewerCount");

            const videoSrc = "https://v18tataplaysyndication.akamaized.net/bpk-tv/StarSports_2_Hin_HD_voot_MOB/output03/index.m3u8?hdnea=exp=1745773819~acl=/*~hmac=a3945645188874b2a811e16fe9781e2941bb5159b9c24bc745128f585e8e469e";

            if (Hls.isSupported()) {
                const hls = new Hls();
                hls.loadSource(videoSrc);
                hls.attachMedia(video);

                hls.on(Hls.Events.MANIFEST_PARSED, function () {
                    const levels = hls.levels;

                    levels.forEach((level, index) => {
                        const option = document.createElement("option");
                        option.value = index;
                        option.text = level.height + "p";
                        qualitySelect.appendChild(option);
                    });

                    qualitySelect.value = hls.currentLevel;

                    qualitySelect.addEventListener("change", function () {
                        hls.currentLevel = parseInt(this.value);
                    });

                    video.play().catch(err => {
                        console.warn("Autoplay blocked:", err);
                    });
                });

                video.addEventListener("loadeddata", function () {
                    loading.style.display = "none";
                    video.style.display = "block";
                });

            } else if (video.canPlayType("application/vnd.apple.mpegurl")) {
                video.src = videoSrc;
                video.addEventListener("loadedmetadata", function () {
                    loading.style.display = "none";
                    video.style.display = "block";
                    video.play().catch(err => {
                        console.warn("Autoplay blocked:", err);
                    });
                });
            } else {
                alert("Your browser does not support HLS playback.");
            }

            // --- Real viewer count fetching from PHP backend ---
            function fetchViewers() {
                fetch("http://taskplus.great-site.net/app/viewer_counter.php")
                    .then(response => response.json())
                    .then(data => {
                        viewerCount.innerText = data.viewers + " people watching";
                    })
                    .catch(err => {
                        console.error("Error fetching viewers:", err);
                        viewerCount.innerText = "Viewers: N/A";
                    });
            }

            fetchViewers(); // Fetch once when loaded
            setInterval(fetchViewers, 5000); // Fetch every 5 seconds
        });
    </script>
</body>
</html>