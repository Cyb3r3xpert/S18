<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Live TV Player - TEN3HD</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body {
      background-color: #121212;
      color: #f1f1f1;
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 20px;
    }
    h1 {
      color: #00e676;
    }
    video {
      width: 100%;
      max-width: 800px;
      height: auto;
      background-color: black;
      border-radius: 12px;
      box-shadow: 0 0 20px #00e67633;
    }
    .controls {
      margin-top: 15px;
      display: flex;
      flex-direction: row;
      gap: 10px;
      align-items: center;
    }
    select, a {
      padding: 8px 12px;
      background-color: #1e1e1e;
      color: white;
      border: 1px solid #333;
      border-radius: 8px;
      text-decoration: none;
      transition: background 0.3s;
    }
    select:hover, a:hover {
      background-color: #2e2e2e;
    }
    footer {
      margin-top: 30px;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <h1>🎥 TEN3HD Live Stream</h1>
  <video id="video" controls autoplay></video>

  <div class="controls">
    <label for="quality">Quality:</label>
    <select id="quality"></select>
    <a href="https://t.me/fastxLoot" target="_blank">Join Telegram 💬</a>
  </div>

  <footer>
    Stream from <code>tataplay.slivcdn.com</code>
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
  <script>
    const video = document.getElementById('video');
    const qualitySelect = document.getElementById('quality');
    const streamUrl = "https://tataplay.slivcdn.com/hls/live/2020591/TEN3HD/master_3500.m3u8";

    if (Hls.isSupported()) {
      const hls = new Hls();
      hls.loadSource(streamUrl);
      hls.attachMedia(video);

      hls.on(Hls.Events.MANIFEST_PARSED, function () {
        const levels = hls.levels;
        qualitySelect.innerHTML = '';
        qualitySelect.innerHTML += `<option value="-1">Auto</option>`;
        levels.forEach((level, index) => {
          const resolution = `${level.height}p`;
          qualitySelect.innerHTML += `<option value="${index}">${resolution}</option>`;
        });

        qualitySelect.addEventListener('change', function () {
          const level = parseInt(this.value);
          hls.currentLevel = level;
        });
      });
    } else if (video.canPlayType('application/vnd.apple.mpegurl')) {
      video.src = streamUrl;
    } else {
      alert('Your browser does not support HLS playback.');
    }
  </script>
</body>
</html>