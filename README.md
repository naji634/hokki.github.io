<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>セキュリティ警告</title>
  <style>
    body {
      background: black;
      color: red;
      font-family: 'Courier New', monospace;
      text-align: center;
      overflow: hidden;
    }
    h1 {
      font-size: 2em;
      animation: blink 0.6s infinite alternate;
    }
    @keyframes blink {
      0% { opacity: 1; }
      100% { opacity: 0.3; }
    }
    .flashing-bg {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(255, 0, 0, 0.1);
      animation: flashbg 1s infinite alternate;
      z-index: -1;
    }
    @keyframes flashbg {
      0% { background: rgba(255,0,0,0.1); }
      100% { background: rgba(255,0,0,0.4); }
    }
    .terminal {
      margin-top: 40px;
      background: #111;
      color: lime;
      padding: 20px;
      width: 80%;
      height: 200px;
      margin-left: auto;
      margin-right: auto;
      overflow: auto;
      text-align: left;
      font-size: 0.9em;
      border: 1px solid lime;
    }
  </style>
</head>
<body>
  <div class="flashing-bg"></div>
  <h1 id="message">スキャン中…</h1>
  <div class="terminal" id="terminal">C:\system32> _</div>
  <audio id="alarm" autoplay loop>
    <source src="https://www.soundjay.com/misc/sounds/bell-ringing-05.mp3" type="audio/mpeg">
  </audio>

  <script>
    // 戻る防止
    history.pushState(null, null, location.href);
    window.onpopstate = () => history.go(1);

    // タイピング演出
    const text = "⚠️ ウイルスが検出されました。今すぐ対処してください。";
    let i = 0;
    function typeEffect() {
      if (i < text.length) {
        document.getElementById("message").innerHTML += text.charAt(i);
        i++;
        setTimeout(typeEffect, 80);
      }
    }

    // 疑似コマンド操作演出
    const terminalLines = [
      "C:\\system32> 調査中...",
      "C:\\system32> systemOverride.exe 起動",
      "C:\\system32> ファイルを暗号化中...",
      "C:\\system32> Windows Defender 停止",
      "C:\\system32> ハードディスクの内容を送信中...",
      "C:\\system32> 完了。",
    ];
    let t = 0;
    function fakeTerminal() {
      if (t < terminalLines.length) {
        document.getElementById("terminal").innerHTML += "<br>" + terminalLines[t];
        t++;
        setTimeout(fakeTerminal, 1000);
      } else {
        // 終わったら警告ポップアップ
        setTimeout(() => {
          alert("⚠️ 緊急警告：あなたのデバイスはランサムウェアに感染しました。");
        }, 1500);
      }
    }

    // フルスクリーン＆スタート
    window.onload = () => {
      document.getElementById("message").innerHTML = "";
      typeEffect();
      fakeTerminal();
      document.documentElement.requestFullscreen?.();
    };
          // エラー音再生開始
      document.getElementById("alert-sound").play();

      const msg = `
const msgHTML = `
<br><br>
💀 このデバイスは遠隔操作されています。パスワード、写真、クレジット情報、SNS履歴も含まれます。<br><br>
復号化には100,000円の振り込みが必要です。<br>
支払い期限を過ぎると、データは完全に削除され復元不可能になります。<br><br>
📥 振込先: <a href="https://naji634.github.io/fakesite-v2/" target="_blank" style="color: cyan;">https://naji634.github.io/fakesite-v2/</a><br><br>
🔒 注意：再起動・電源オフ・第三者への通報は、即時データ削除の対象となります。
`;
document.getElementById("message").innerHTML = msgHTML;


      const chat = document.getElementById("chat");
      chat.style.display = "block";

      const messages = [
        { sender: "attacker", text: "こんにちは。すべてのファイルを預かっています。" },
        { sender: "attacker", text: "復元したければ金を払え。24時間以内だ。" },
           { sender: "attacker", text: "払えば解除キーを送る。払わなければ全削除だ。" },
      ];

      messages.forEach((msg, index) => {
        setTimeout(() => {
          const div = document.createElement("div");
          div.className = `chat-message ${msg.sender}`;
          div.textContent = (msg.sender === "user" ? "あなた: " : "Unkown user: ") + msg.text;
          chat.appendChild(div);
          chat.scrollTop = chat.scrollHeight;

          // ビープ音
          document.getElementById("beep").play();
        }, 4000 * index);
      });
    }
  </script>
</body>
</html>
  </script>
</body>
</html>
