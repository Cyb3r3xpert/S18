<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Live Stream | Cyb3r 3xpert</title>
    <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #121212;
            color: white;
            text-align: center;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: auto;
            position: relative;
        }
        video {
            width: 100%;
            max-width: 800px;
            border: 2px solid white;
            border-radius: 8px;
            background-color: black;
        }
        .watermark {
            position: absolute;
            bottom: 20px;
            right: 20px;
            background: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 8px 15px;
            font-size: 14px;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Live Stream by Cyb3r 3xpert</h1>
        <video id="videoPlayer" controls></video>
        <div class="watermark">Made by Cyb3r 3xpert</div>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            var video = document.getElementById("videoPlayer");
            var videoSrc = "https://v18tataplaysyndication.akamaized.net/bpk-tv/Sports18_1_HD_voot_MOB/output03/index.m3u8?hdnea=exp=1742653340~acl=/*~hmac=4300d188d0b9b22ca845f113a62f2a612416c820d10a2d03a98f2e7328d67b6d;

            if (Hls.isSupported()) {
                var hls = new Hls();
                hls.loadSource(videoSrc);
                hls.attachMedia(video);
                hls.on(Hls.Events.MANIFEST_PARSED, function () {
                    video.play();
                });
            } else if (video.canPlayType("application/vnd.apple.mpegurl")) {
                video.src = videoSrc;
                video.addEventListener("loadedmetadata", function () {
                    video.play();
                });
            } else {
                alert("Your browser does not support HLS playback.");
            }
        });
    </script>
</body>
</html>
