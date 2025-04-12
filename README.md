<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>セキュリティ警告</title>
</head>
<body style="background:black; color:red; font-family:sans-serif; text-align:center;">
  <h1 id="message">スキャン中…</h1>
  <button onclick="document.documentElement.requestFullscreen();">スキャンを続行</button>

  <script>
    // 無限戻り防止
    history.pushState(null, null, location.href);
    window.onpopstate = () => history.go(1);

    // タイピング効果
    let text = "⚠️ ウイルスが検出されました。今すぐ対処してください。";
    let i = 0;
    function typeEffect() {
      if (i < text.length) {
        document.getElementById("message").innerHTML += text.charAt(i);
        i++;
        setTimeout(typeEffect, 100);
      }
    }
    window.onload = typeEffect;
  </script>
</body>
</html>
