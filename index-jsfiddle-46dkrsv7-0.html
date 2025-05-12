<!DOCTYPE html>
<html>

<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>JSFiddle 46dkrsv7</title>

  <style>
    body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: #222;
    color: #eee;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    margin: 0;
    transition: box-shadow 0.3s ease-in-out; /* 警告表示用トランジション */
}

/* 速度超過警告時のスタイル */
body.speed-warning {
    box-shadow: 0 0 30px 15px rgba(255, 0, 0, 0.7); /* 赤いぼかし効果 */
}

.meter-container {
    background-color: #333;
    padding: 30px;
    border-radius: 15px;
    text-align: center;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    width: 90%;
    max-width: 400px;
}

.speed-display {
    margin-bottom: 30px;
}

#speed {
    font-size: 6em; /* 大きな文字で速度を表示 */
    font-weight: bold;
    color: #00ffcc; /* 見やすい色 */
    line-height: 1;
    display: inline-block; /* 後続の単位と同じ行に */
    vertical-align: baseline;
}

.unit {
    font-size: 1.5em;
    color: #aaa;
    margin-left: 10px;
    vertical-align: baseline;
}

.info-grid {
    display: grid;
    grid-template-columns: 1fr 1fr; /* 2列グリッド */
    gap: 15px; /* グリッド間の隙間 */
    font-size: 1.1em;
}

.info-grid div {
    background-color: #444;
    padding: 10px;
    border-radius: 8px;
}

.label {
    display: block;
    font-size: 0.8em;
    color: #bbb;
    margin-bottom: 5px;
}

#altitude, #max-speed, #distance, #time {
    font-weight: bold;
    color: #fff;
}

.status-message {
    margin-top: 20px;
    font-size: 0.9em;
    color: #ffcc00; /* 注意を促す色 */
}
  </style>

  
</head>
<body>
  <!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>自転車スピードメーター</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="meter-container">
        <div class="speed-display">
            <span id="speed">0.0</span>
            <span class="unit">km/h</span>
        </div>

        <div class="info-grid">
            <div>
                <span class="label">標高</span>
                <span id="altitude">---</span> m
            </div>
            <div>
                <span class="label">最高速度</span>
                <span id="max-speed">0.0</span> km/h
            </div>
            <div>
                <span class="label">走行距離</span>
                <span id="distance">0.00</span> km
            </div>
            <div>
                <span class="label">走行時間</span>
                <span id="time">00:00:00</span>
            </div>
        </div>
         <div id="status" class="status-message">GPS信号を取得中...</div>
    </div>

    <script src="script.js"></script>
</body>
</html>

  <script>
    document.addEventListener('DOMContentLoaded', () => {
    const speedElement = document.getElementById('speed');
    const altitudeElement = document.getElementById('altitude');
    const maxSpeedElement = document.getElementById('max-speed');
    const distanceElement = document.getElementById('distance');
    const timeElement = document.getElementById('time');
    const statusElement = document.getElementById('status');
    const bodyElement = document.body;

    let currentSpeed = 0;
    let maxSpeed = 0;
    let totalDistance = 0;
    let startTime = null;
    let lastPosition = null;
    let watchId = null;
    let simulationIntervalId = null;
    let timeUpdateIntervalId = null;
    let isSimulating = false;

    const GPS_OPTIONS = {
        enableHighAccuracy: true, // 高精度を要求
        timeout: 10000,          // 10秒でタイムアウト
        maximumAge: 0            // キャッシュを使用しない
    };

    // --- 表示更新関数 ---
    function updateDisplay() {
        speedElement.textContent = currentSpeed.toFixed(1); // 速度 (小数点第一位まで)
        maxSpeedElement.textContent = maxSpeed.toFixed(1); // 最高速度
        distanceElement.textContent = totalDistance.toFixed(2); // 距離 (小数点第二位まで)

        // 速度警告
        if (currentSpeed > 40) {
            bodyElement.classList.add('speed-warning');
        } else {
            bodyElement.classList.remove('speed-warning');
        }
    }

    // --- 時間フォーマット関数 ---
    function formatTime(seconds) {
        const h = Math.floor(seconds / 3600).toString().padStart(2, '0');
        const m = Math.floor((seconds % 3600) / 60).toString().padStart(2, '0');
        const s = Math.floor(seconds % 60).toString().padStart(2, '0');
        return `${h}:${m}:${s}`;
    }

    // --- 走行時間更新関数 ---
    function updateElapsedTime() {
        if (!startTime) return;
        const now = Date.now();
        const elapsedSeconds = Math.floor((now - startTime) / 1000);
        timeElement.textContent = formatTime(elapsedSeconds);
    }

    // --- 距離計算関数 (Haversine formula) ---
    function calculateDistance(lat1, lon1, lat2, lon2) {
        const R = 6371; // 地球の半径 (km)
        const dLat = deg2rad(lat2 - lat1);
        const dLon = deg2rad(lon2 - lon1);
        const a =
            Math.sin(dLat / 2) * Math.sin(dLat / 2) +
            Math.cos(deg2rad(lat1)) * Math.cos(deg2rad(lat2)) *
            Math.sin(dLon / 2) * Math.sin(dLon / 2);
        const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
        return R * c; // 距離 (km)
    }

    function deg2rad(deg) {
        return deg * (Math.PI / 180);
    }

    // --- GPS成功時のコールバック ---
    function successCallback(position) {
        statusElement.textContent = 'GPS信号良好'; // ステータス更新
        const { latitude, longitude, speed, altitude, accuracy } = position.coords;
        const timestamp = position.timestamp;

        // 速度 (m/sからkm/hへ変換、nullの場合や精度が低い場合は0扱い)
        // speedがnullになる場合があるので注意
        currentSpeed = speed !== null ? speed * 3.6 : 0;

        // 標高 (nullの場合や精度が低い場合は'---'表示)
        // altitudeAccuracyのサポートは限定的なので、altitudeがあれば表示
        altitudeElement.textContent = altitude !== null ? altitude.toFixed(1) : '---';

        // 最高速度更新
        if (currentSpeed > maxSpeed) {
            maxSpeed = currentSpeed;
        }

        // 走行距離計算
        if (lastPosition && latitude !== null && longitude !== null) {
            const distanceIncrement = calculateDistance(
                lastPosition.latitude, lastPosition.longitude,
                latitude, longitude
            );
            // 極端に大きな移動距離は無視 (GPSの飛び対策)
            if (distanceIncrement > 0 && distanceIncrement < 1) { // 1回の更新で1km以上移動することは稀
                 totalDistance += distanceIncrement;
            }
        }

         // 走行開始時間と時間更新インターバルの設定
         if (startTime === null && currentSpeed > 0) {
            startTime = Date.now() - (lastPosition ? timestamp - lastPosition.timestamp : 0); // 最初の有効な位置からの時間を考慮
            if (!timeUpdateIntervalId) {
                timeUpdateIntervalId = setInterval(updateElapsedTime, 1000); // 1秒ごとに時間更新
            }
         } else if (startTime !== null && currentSpeed <= 0 && lastPosition && lastPosition.speed <= 0) {
             // 停止したら時間計測も一時停止する場合 (オプション)
             // clearInterval(timeUpdateIntervalId);
             // timeUpdateIntervalId = null;
         }


        // 最後の位置情報を更新
        lastPosition = { latitude, longitude, timestamp, speed: currentSpeed };

        // シミュレーション中なら停止
        stopSimulation();
    }

    // --- GPSエラー時のコールバック ---
    function errorCallback(error) {
        let message = 'GPSエラー: ';
        switch (error.code) {
            case error.PERMISSION_DENIED:
                message += '位置情報の利用が許可されていません。';
                break;
            case error.POSITION_UNAVAILABLE:
                message += '位置情報を取得できません。';
                break;
            case error.TIMEOUT:
                message += '位置情報の取得がタイムアウトしました。';
                break;
            default:
                message += '不明なエラーが発生しました。';
                break;
        }
        statusElement.textContent = message;
        console.error(message, error);

        // シミュレーションを開始するか確認
        if (!isSimulating && confirm('GPS信号が取得できません。シミュレーションを開始しますか？')) {
            startSimulation();
        } else if (!isSimulating) {
             statusElement.textContent += ' シミュレーションは開始しません。';
             // GPSが使えない場合、初期表示のままか、固定値を表示
             currentSpeed = 0;
             altitudeElement.textContent = '---';
             updateDisplay(); // 表示をリセット
        }
    }

    // --- シミュレーション開始 ---
    function startSimulation() {
        if (isSimulating) return; // 既に実行中なら何もしない
        isSimulating = true;
        statusElement.textContent = 'シミュレーションモード実行中';
        console.log("シミュレーション開始");

        // GPS監視を停止 (もし動いていたら)
        if (watchId) {
            navigator.geolocation.clearWatch(watchId);
            watchId = null;
        }
        // 実際のGPSデータで更新されていた可能性のある値をリセット
        lastPosition = null;

        // ダミーデータで定期的に更新
        simulationIntervalId = setInterval(() => {
            // ランダムな速度変化 (例: 15km/hを中心に変動)
            currentSpeed += (Math.random() - 0.5) * 4;
            if (currentSpeed < 0) currentSpeed = 0;
            if (currentSpeed > 60) currentSpeed = 60; // 上限

            // 最高速度更新
            if (currentSpeed > maxSpeed) {
                maxSpeed = currentSpeed;
            }

             // 距離を加算 (現在の速度に基づいて適当に)
             // 0.5秒ごとの更新なので、速度(km/h) / 3600 * 0.5 = km
            totalDistance += currentSpeed / 7200;

            // 標高もダミーで変動させる (オプション)
            let currentAlt = parseFloat(altitudeElement.textContent);
            if (isNaN(currentAlt) || currentAlt < 1) currentAlt = 500; // 初期値
            currentAlt += (Math.random() - 0.5) * 5;
            altitudeElement.textContent = currentAlt.toFixed(1);

            // 走行時間計測開始/更新
            if (startTime === null && currentSpeed > 0) {
                 startTime = Date.now();
                 if (!timeUpdateIntervalId) {
                    timeUpdateIntervalId = setInterval(updateElapsedTime, 1000);
                 }
            }
             // 停止したら時間計測も一時停止する場合 (オプション)
             // else if (startTime !== null && currentSpeed === 0) {
             //    clearInterval(timeUpdateIntervalId);
             //    timeUpdateIntervalId = null;
             //}

            // updateDisplay(); // 0.5秒ごとの更新は別途設定するためここでは呼ばない
        }, 500); // シミュレーションデータ生成間隔 (速度更新自体は別)
         // 時間更新も開始
         if (!timeUpdateIntervalId) {
             startTime = startTime || Date.now(); // まだ開始してなければ現在時刻
             timeUpdateIntervalId = setInterval(updateElapsedTime, 1000);
         }
    }

    // --- シミュレーション停止 ---
    function stopSimulation() {
        if (!isSimulating) return;
        isSimulating = false;
        clearInterval(simulationIntervalId);
        simulationIntervalId = null;
        // statusElement.textContent = 'GPS信号良好'; // GPS成功時に呼ばれるのでそちらで設定
        console.log("シミュレーション停止");
    }

    // --- メイン処理 ---
    function startTracking() {
        if (navigator.geolocation) {
            // 0.5秒ごとに表示を更新するタイマー
            setInterval(updateDisplay, 500);

            // GPSの監視を開始
            watchId = navigator.geolocation.watchPosition(
                successCallback,
                errorCallback,
                GPS_OPTIONS
            );
            statusElement.textContent = 'GPS信号を取得中...';

        } else {
            statusElement.textContent = 'お使いのブラウザはGeolocation APIをサポートしていません。';
            // サポートしていない場合もシミュレーション確認
             if (confirm('Geolocationがサポートされていません。シミュレーションを開始しますか？')) {
                startSimulation();
                // シミュレーション時も0.5秒更新と時間表示は必要
                setInterval(updateDisplay, 500);
            }
        }
    }

    // --- 初期化実行 ---
    startTracking();

});
  </script>
</body>
</html>
