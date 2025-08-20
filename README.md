<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>LINE Flex Share Demo</title>
  <script src="https://static.line-scdn.net/liff/edge/2/sdk.js"></script>
</head>
<body>
  <h2>ทดสอบ Flex Share</h2>
  <button id="shareBtn">📤 แชร์ไปยังเพื่อน</button>

  <script>
    async function main() {
      await liff.init({ liffId: "2007959352-mpLy7O5l" });

      console.log("LINE version:", liff.getLineVersion());
      console.log("shareTargetPicker available?", liff.isApiAvailable('shareTargetPicker'));

      if (!liff.isApiAvailable('shareTargetPicker')) {
        alert("LINE App ไม่รองรับ shareTargetPicker ❌");
        return;
      }

      document.getElementById("shareBtn").onclick = async () => {
        const flexMessage = {
          type: "flex",
          altText: "Flex Demo",
          contents: {
            type: "bubble",
            body: {
              type: "box",
              layout: "vertical",
              contents: [
                { type: "text", text: "Hello LINE 👋", weight: "bold", size: "xl", align: "center" },
                { type: "text", text: "นี่คือ Flex Message ตัวอย่าง", size: "md", color: "#666666", align: "center" }
              ]
            }
          }
        };

        try {
          const result = await liff.shareTargetPicker([flexMessage]);
          if (result) alert("✅ แชร์เรียบร้อย");
          else alert("❌ ยกเลิกการแชร์");
        } catch (err) {
          console.error(err);
          alert("⚠️ Error: " + err);
        }
      };
    }

    main();
  </script>
</body>
</html>
