<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=0,viewport-fit=cover" />
  <title>Share Flex Message</title>
  <style>
    body{font-family:system-ui,Segoe UI,Roboto,Arial;margin:0;background:#111;color:#fff}
    .wrap{max-width:520px;margin:40px auto;padding:20px}
    button{padding:14px 20px;font-weight:700;border:0;border-radius:14px;cursor:pointer;font-size:18px}
    #btnShare{background:#00b900;color:#fff;width:100%}
    .note{margin-top:10px;opacity:.75;font-size:14px}
    .card{background:#1c1c1e;border-radius:16px;overflow:hidden;box-shadow:0 10px 30px rgba(0,0,0,.4);padding:20px;text-align:center}
    .preview-img{width:100%;border-radius:12px;margin-bottom:16px}
    .title{font-size:20px;font-weight:bold;margin-bottom:10px}
  </style>
  <script src="https://static.line-scdn.net/liff/edge/2/sdk.js"></script>
</head>
<body>
  <div class="wrap">
    <div class="card">
      <img class="preview-img" src="https://img5.pic.in.th/file/secure-sv1/H-100-10d5f3823b3c6e431.jpg" alt="Preview"/>
      <button id="btnShare" disabled>แชร์ต่อให้เพื่อน</button>
    </div>
  </div>

  <script>
    const LIFF_ID = "2008148869-PR8wpdDb";

    function buildFlex() {
      return {
        "type": "flex",
        "altText": "Flex Message",
        "contents": {
          "type": "bubble",
          "hero": {
            "type": "image",
            "size": "full",
            "aspectRatio": "20:20",
            "url": "https://img5.pic.in.th/file/secure-sv1/H-100-10d5f3823b3c6e431.jpg",
            "aspectMode": "cover",
            "action": { "type": "uri", "label": "Line", "uri": "https://tinyurl.com/h1691h" }
          },
          "footer": {
            "type": "box",
            "layout": "vertical",
            "spacing": "sm",
            "backgroundColor": "#ffffff",
            "contents": [
              {
                "type": "button",
                "style": "primary",
                "height": "sm",
                "color": "#ec008c",
                "action": { "type": "uri", "label": "รับฟรี 100", "uri": "https://tinyurl.com/1683hoeY" }
              },
              {
                "type": "button",
                "style": "primary",
                "height": "sm",
                "color": "#ec008c",
                "action": { "type": "uri", "label": "สมัครสมาชิก", "uri": "https://tinyurl.com/Free168holiday" }
              },
              {
                "type": "button",
                "style": "primary",
                "color": "#2cc958",
                "action": { "type": "uri", "label": "แชร์ 10 คน รับทุนฟรี", "uri": `https://liff.line.me/${LIFF_ID}` }
              },
              { "type": "spacer", "size": "sm" }
            ]
          }
        }
      };
    }

    async function sendShare() {
      try {
        if (!liff.isInClient()) {
          liff.openWindow({ url: `https://liff.line.me/${LIFF_ID}`, external: false });
          return;
        }
        if (!liff.isApiAvailable('shareTargetPicker')) {
          alert('อุปกรณ์นี้ยังไม่รองรับการแชร์');
          return;
        }
        const result = await liff.shareTargetPicker([buildFlex()]);
        alert(result ? 'ส่งเรียบร้อย!' : 'ผู้ใช้ยกเลิกการแชร์');
      } catch (e) {
        console.error(e);
        alert('เกิดข้อผิดพลาดระหว่างการแชร์');
      }
    }

    async function main() {
      try {
        await liff.init({ liffId: LIFF_ID });
        if (liff.isInClient() && !liff.isLoggedIn()) liff.login();
        document.getElementById('btnShare').disabled = false;
        document.getElementById('btnShare').addEventListener('click', sendShare);
      } catch (e) {
        console.error('LIFF initialization failed', e);
        alert('LIFF init ล้มเหลว: ตรวจ LIFF ID / สิทธิ์ใน LINE Developers');
      }
    }
    main();
  </script>
</body>
</html>
