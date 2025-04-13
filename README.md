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
            var videoSrc = "https://v18tataplaysyndication.akamaized.net/bpk-tv/StarSports_2_Hin_HD_voot_MOB/output03/hdntl=exp=1744629512~acl=%2f*~data=hdntl~hmac=9cb4e01b761e283d216b7bfa7b9f1d7b147b55e642b41ff7afd51ef8bcd0c60c/StarSports_2_Hin_HD_voot_MOB-audio_108038_hin=108000-video=305200.m3u8";

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
