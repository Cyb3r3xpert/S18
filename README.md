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
            bottom: 70px; /* moved up to create space */
            right: 30px;
            background: rgba(0, 0, 0, 0.6);
            padding: 8px 12px;
            font-size: 14px;
            border-radius: 4px;
            color: #ffffff;
        }

        .quality-selector {
            margin-top: 40px; /* extra space below the video */
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
    </style>
</head>
<body>
    <div class="container">
        <h1>Live Stream by Cyb3r 3xpert</h1>
        <div id="loading">Loading stream...</div>
        <video id="videoPlayer" controls style="display: none;">
            Your browser does not support HTML5 video.
        </video>
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

            const videoSrc = "https://v18tataplaysyndication.akamaized.net/bpk-tv/StarSports_2_Hin_HD_voot_MOB/output03/index.m3u8?hdnea=exp=1745076813~acl=/*~hmac=36f4f27c8ecc68c2018b63629b68c70ec32b77e195bffb94054e205bd2fb5428";

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
        });
    </script>
</body>
</html>