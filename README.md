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
            var videoSrc = "https://jcevents.akamaized.net/bpk-tv/JC_Sports18_1HD/JCHLS/hdntl=exp=1741585633~acl=%2F*~id=97ff5c734c6f4a3ea96b01cfd44846cc~data=hdntl~hmac=db0dbae6b8d53b386b4bc9848af7139235c4f2c36e1bc9ee44971a36249f2c20/JC_Sports18_1HD-audio_108038_eng=108000-video=2297600.m3u8";

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
