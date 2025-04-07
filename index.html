<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>내 주변 공중화장실 찾기</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <!-- Leaflet 스타일시트 -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    #map { height: 400px; margin-top: 20px; }
    #toilet-list { margin-top: 20px; }
    .toilet-item { border: 1px solid #ccc; padding: 10px; margin-bottom: 10px; }
  </style>
</head>
<body>
  <h1>내 주변 공중화장실 찾기</h1>
  <button onclick="getLocation()">내 위치로 검색 / 리로딩</button>
  <div id="status"></div>
  <div id="map"></div>
  <div id="toilet-list"></div>

  <!-- Leaflet 스크립트 -->
  <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
  <script>
    let map;
    let userMarker = null;
    let toiletMarkers = [];

    function initMap(lat, lon) {
      if (!map) {
        map = L.map('map').setView([lat, lon], 15);
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
          attribution: '© OpenStreetMap'
        }).addTo(map);
      } else {
        map.setView([lat, lon], 15);
      }

      // 기존 사용자 마커 제거
      if (userMarker) {
        map.removeLayer(userMarker);
      }

      // 새로운 사용자 마커 생성
      userMarker = L.marker([lat, lon]).addTo(map)
        .bindPopup('내 위치')
        .openPopup();
    }

    async function getLocation() {
      const status = document.getElementById('status');
      const list = document.getElementById('toilet-list');
      list.innerHTML = '';
      status.textContent = '위치를 찾는 중...';

      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(async (position) => {
          const lat = position.coords.latitude;
          const lon = position.coords.longitude;
          status.textContent = `내 위치: (${lat.toFixed(4)}, ${lon.toFixed(4)})`;

          initMap(lat, lon);

          // 기존 화장실 마커 제거
          toiletMarkers.forEach(marker => map.removeLayer(marker));
          toiletMarkers = [];

          const toiletData = await fetch('toilets.json').then(res => res.json());

          function getDistance(lat1, lon1, lat2, lon2) {
            const R = 6371;
            const dLat = (lat2 - lat1) * Math.PI / 180;
            const dLon = (lon2 - lon1) * Math.PI / 180;
            const a = Math.sin(dLat/2) * Math.sin(dLat/2) +
                      Math.cos(lat1 * Math.PI / 180) * Math.cos(lat2 * Math.PI / 180) *
                      Math.sin(dLon/2) * Math.sin(dLon/2);
            const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
            return R * c;
          }

          const nearby = toiletData
            .map(toilet => ({
              ...toilet,
              distance: getDistance(lat, lon, toilet.latitude, toilet.longitude)
            }))
            .sort((a, b) => a.distance - b.distance)
            .slice(0, 10);

          nearby.forEach(t => {
            const marker = L.marker([t.latitude, t.longitude])
              .addTo(map)
              .bindPopup(`<strong>${t.name}</strong><br>${t.address}<br>${t.distance.toFixed(2)} km`);
            toiletMarkers.push(marker);
          });

          list.innerHTML = nearby.map(t =>
            `<div class="toilet-item">
              <strong>${t.name}</strong><br>
              주소: ${t.address}<br>
              거리: ${t.distance.toFixed(2)} km
            </div>`
          ).join('');
        }, () => {
          status.textContent = '위치 정보를 가져올 수 없습니다.';
        });
      } else {
        status.textContent = '브라우저가 위치 정보를 지원하지 않습니다.';
      }
    }
  </script>
</body>
</html>
