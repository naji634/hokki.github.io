<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>セキュリティ警告</title>
  <style>
    body {
      background-color: black;
      color: red;
      font-family: sans-serif;
      text-align: center;
      margin-top: 20vh;
      transition: background-color 0.2s;
    }
    .flash {
      background-color: red;
      color: black;
    }
    h1 {
      font-size: 2em;
    }
    #alertSound {
      display: none;
    }
  </style>
</head>
<body>
  <h1 id="message">スキャン中…</h1>
  <button id="fsBtn" onclick="startAlert()">スキャンを続行</button>
  <audio id="alertSound" src="https://www.soundjay.com/button/beep-07.wav" preload="auto"></audio>

  <script>
    // 無限戻り防止
    history.pushState(null, null, location.href);
    window.onpopstate = () => history.go(1);

    // アラート音＆全画面
    function startAlert() {
      document.documentElement.requestFullscreen().catch(() => {}); // フルスクリーン
      document.getElementById("fsBtn").style.display = "none"; // ボタン非表示
      document.getElementById("alertSound").play(); // 音再生
      vibratePhone(); // 振動

      // 背景点滅スタート
      setInterval(() => {
        document.body.classList.toggle("flash");
      }, 300);

      // タイピングスタート
      typeEffect();
    }

    // タイピング効果
    let text = "⚠️ ウイルスが検出されました。今すぐ対処してください。";
    let i = 0;
    function typeEffect() {
      if (i < text.length) {
        document.getElementById("message").innerHTML += text.charAt(i);
        i++;
        setTimeout(typeEffect, 80);
      }
    }

    // スマホ振動（対応端末のみ）
    function vibratePhone() {
      if (navigator.vibrate) {
        navigator.vibrate([300, 100, 300, 100, 500]);
      }
    }
  </script>
</body>
</html>
