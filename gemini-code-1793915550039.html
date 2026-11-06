
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Couple Sync 🤍</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="apple-touch-icon" href="https://cdn-icons-png.flaticon.com/512/833/833472.png">
    
    <!-- OneSignal SDK -->
    <script src="https://cdn.onesignal.com/sdks/web/v16/OneSignalSDK.page.js" defer></script>
    <script>
      window.OneSignalDeferred = window.OneSignalDeferred || [];
      window.OneSignalDeferred.push(async function(OneSignal) {
        await OneSignal.init({
          appId: "6e5430aa-22dd-4822-8de4-b8077fe2fd2c",
        });
      });
    </script>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen flex items-center justify-center p-4 selection:bg-indigo-500 selection:text-white">

    <!-- Всплывающий баннер уведомления (Toast) -->
    <div id="toast" class="fixed top-4 left-4 right-4 max-w-sm mx-auto text-white p-4 rounded-2xl shadow-2xl transition-all duration-500 transform -translate-y-32 opacity-0 z-50 flex items-center justify-between border border-white/20">
        <div class="flex items-center gap-3">
            <span id="toastIcon" class="text-2xl">⚠️</span>
            <div>
                <h4 id="toastTitle" class="font-bold text-sm">Внимание!</h4>
                <p id="toastBody" class="text-xs text-slate-100">Критическое состояние партнера!</p>
            </div>
        </div>
        <button onclick="hideToast()" class="bg-black/20 hover:bg-black/40 text-white text-sm font-bold w-8 h-8 rounded-full flex items-center justify-center transition">✕</button>
    </div>

    <div class="w-full max-w-sm bg-slate-900/90 backdrop-blur-xl border border-slate-800 p-6 rounded-3xl shadow-2xl space-y-6">
        <div class="text-center">
            <h1 class="text-2xl font-extrabold tracking-tight text-white flex items-center justify-center gap-2">
                Couple Sync <span class="text-rose-500">🤍</span>
            </h1>
            <p class="text-xs text-slate-400 mt-1">Твой личный мост взаимопонимания</p>
        </div>

        <!-- Кнопка запроса push-уведомлений и проверки -->
        <button id="pushPromptBtn" onclick="requestPushPermission()" class="w-full bg-indigo-600/20 border border-indigo-500/40 hover:bg-indigo-600/30 text-indigo-300 py-2.5 rounded-xl text-xs font-semibold transition flex items-center justify-center gap-2">
            <span>🔔</span> Включить уведомления?
        </button>

        <!-- Форма входа / Выбора роли -->
        <div id="loginBox" class="space-y-4">
            <input id="roomInput" type="text" placeholder="Код пары (например: love123)" class="w-full bg-slate-950 border border-slate-800 rounded-2xl px-4 py-3 text-sm text-center font-mono focus:outline-none focus:border-indigo-500 text-white transition">
            
            <div class="grid grid-cols-2 gap-3">
                <button onclick="connectAs('user1')" class="bg-indigo-600 hover:bg-indigo-500 py-3 rounded-2xl text-sm font-semibold transition text-white shadow-lg shadow-indigo-600/20">Я (Парень)</button>
                <button onclick="connectAs('user2')" class="bg-pink-600 hover:bg-pink-500 py-3 rounded-2xl text-sm font-semibold transition text-white shadow-lg shadow-pink-600/20">Девушка</button>
            </div>
        </div>

        <!-- Основной интерфейс приложения -->
        <div id="appBody" class="space-y-6 hidden">
            <!-- Мой статус -->
            <div class="bg-slate-950/60 p-4 rounded-2xl border border-slate-800/80 space-y-4 shadow-inner">
                <h2 id="myRoleTitle" class="text-xs font-bold text-indigo-400 uppercase tracking-wider">Моё состояние</h2>
                
                <div class="space-y-1">
                    <div class="flex justify-between text-xs font-medium">
                        <span class="text-slate-300">Подавленность</span>
                        <span id="myDepressionVal" class="font-bold text-rose-400">0%</span>
                    </div>
                    <input type="range" id="myDepression" min="0" max="100" value="0" oninput="updateMyStatus()" class="w-full accent-rose-500 cursor-pointer h-2 bg-slate-800 rounded-lg appearance-none">
                </div>

                <div class="space-y-1">
                    <div class="flex justify-between text-xs font-medium">
                        <span class="text-slate-300">Желание пообщаться</span>
                        <span id="myChatVal" class="font-bold text-emerald-400">0%</span>
                    </div>
                    <input type="range" id="myChat" min="0" max="100" value="0" oninput="updateMyStatus()" class="w-full accent-emerald-500 cursor-pointer h-2 bg-slate-800 rounded-lg appearance-none">
                </div>
            </div>

            <!-- Статус партнера -->
            <div class="bg-slate-950/60 p-4 rounded-2xl border border-slate-800/80 space-y-3 shadow-inner">
                <h2 id="partnerRoleTitle" class="text-xs font-bold text-pink-400 uppercase tracking-wider">Состояние второй половинки</h2>
                
                <div class="flex justify-between items-center bg-slate-900/80 p-3 rounded-xl border border-slate-800/50">
                    <span class="text-xs text-slate-300">Подавленность:</span>
                    <span id="partnerDepression" class="font-bold text-sm bg-slate-950 px-3 py-1 rounded-lg text-slate-300 transition-all">--</span>
                </div>

                <div class="flex justify-between items-center bg-slate-900/80 p-3 rounded-xl border border-slate-800/50">
                    <span class="text-xs text-slate-300">Желание пообщаться:</span>
                    <span id="partnerChat" class="font-bold text-sm bg-slate-950 px-3 py-1 rounded-lg text-slate-300 transition-all">--</span>
                </div>
            </div>

            <button onclick="logout()" class="w-full bg-slate-800/50 hover:bg-slate-800 py-2.5 rounded-xl text-xs font-medium text-slate-400 transition border border-slate-700/30">Сменить код / роль</button>
        </div>
    </div>

    <!-- Модули Firebase и JS-логика -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getDatabase, ref, set, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

        const firebaseConfig = {
            apiKey: "AIzaSyAQL-Mk4Ppvuid0oxvaeTg50lTzCK8E1VA",
            authDomain: "for-love-12b31.firebaseapp.com",
            databaseURL: "https://for-love-12b31-default-rtdb.firebaseio.com",
            projectId: "for-love-12b31",
            storageBucket: "for-love-12b31.firebasestorage.app",
            messagingSenderId: "184511953697",
            appId: "1:184511953697:web:1855880ee7b82f94985c60"
        };

        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        let roomId = localStorage.getItem("couple_room") || "";
        let myRole = localStorage.getItem("couple_role") || ""; 

        if (roomId && myRole) {
            document.getElementById("roomInput").value = roomId;
            startApp();
        }

        // Запрос разрешения и тестовый системный пуш
        window.requestPushPermission = function() {
            window.OneSignalDeferred = window.OneSignalDeferred || [];
            window.OneSignalDeferred.push(function(OneSignal) {
                OneSignal.Notifications.requestPermission().then(function(permission) {
                    const btn = document.getElementById("pushPromptBtn");
                    if (permission) {
                        btn.innerHTML = "<span>✅</span> Уведомления включены";
                        btn.className = "w-full bg-emerald-600/20 border border-emerald-500/40 text-emerald-300 py-2.5 rounded-xl text-xs font-semibold cursor-default transition flex items-center justify-center gap-2";
                        sendTestPush();
                    } else {
                        btn.innerHTML = "<span>❌</span> Уведомления заблокированы";
                        btn.className = "w-full bg-rose-600/20 border border-rose-500/40 text-rose-300 py-2.5 rounded-xl text-xs font-semibold transition flex items-center justify-center gap-2";
                    }
                });
            });
        };

        function sendTestPush() {
            fetch("https://onesignal.com/api/v1/notifications", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json; charset=utf-8",
                    "Authorization": "Basic os_v2_app_nbyuew323u2uydj2736483y2dhwuihduy3i2764382764832u"
                },
                body: JSON.stringify({
                    app_id: "6e5430aa-22dd-4822-8de4-b8077fe2fd2c",
                    included_segments: ["Subscribed Users"],
                    headings: {"ru": "Включить уведомления?", "en": "Enable notifications?"},
                    contents: {"ru": "Уведомления успешно работают! 🤍", "en": "Notifications enabled!"}
                })
            }).catch(err => console.error("Ошибка отправки:", err));
        }

        window.connectAs = function(role) {
            const input = document.getElementById("roomInput").value.trim();
            if (!input) return alert("Введите код пары!");
            
            roomId = input;
            myRole = role;

            localStorage.setItem("couple_room", roomId);
            localStorage.setItem("couple_role", myRole);

            startApp();
        };

        function startApp() {
            document.getElementById("loginBox").classList.add("hidden");
            document.getElementById("appBody").classList.remove("hidden");

            document.getElementById("myRoleTitle").innerText = myRole === "user1" ? "Моё состояние (Парень)" : "Моё состояние (Девушка)";
            document.getElementById("partnerRoleTitle").innerText = myRole === "user1" ? "Состояние девушки" : "Состояние парня";

            const partnerRole = myRole === "user1" ? "user2" : "user1";
            const partnerRef = ref(db, `rooms/${roomId}/${partnerRole}`);
            
            let isFirstLoad = true;

            onValue(partnerRef, (snap) => {
                const data = snap.val();
                if (data) {
                    renderPartnerData(data, isFirstLoad);
                    isFirstLoad = false;
                }
            });
        }

        window.updateMyStatus = function() {
            if (!roomId || !myRole) return;

            const depression = parseInt(document.getElementById("myDepression").value);
            const chat = parseInt(document.getElementById("myChat").value);

            document.getElementById("myDepressionVal").innerText = depression + "%";
            document.getElementById("myChatVal").innerText = chat + "%";

            set(ref(db, `rooms/${roomId}/${myRole}`), {
                depression: depression,
                chat: chat,
                updatedAt: Date.now()
            });
        };

        window.logout = function() {
            localStorage.removeItem("couple_room");
            localStorage.removeItem("couple_role");
            location.reload();
        };

        let lastDep = 0;
        let lastChat = 0;

        function renderPartnerData(data, isFirstLoad) {
            const depEl = document.getElementById("partnerDepression");
            const chatEl = document.getElementById("partnerChat");

            const depVal = data.depression ?? 0;
            const chatVal = data.chat ?? 0;

            depEl.innerText = depVal + "%";
            chatEl.innerText = chatVal + "%";

            depEl.className = `font-bold text-sm px-3 py-1 rounded-lg transition-all ${depVal >= 85 ? 'bg-rose-500/20 text-rose-400 animate-pulse border border-rose-500/50' : 'bg-slate-950 text-slate-300'}`;
            chatEl.className = `font-bold text-sm px-3 py-1 rounded-lg transition-all ${chatVal >= 85 ? 'bg-emerald-500/20 text-emerald-400 animate-pulse border border-emerald-500/50' : 'bg-slate-950 text-slate-300'}`;

            if (!isFirstLoad) {
                if (depVal >= 85 && lastDep < 85) {
                    showToast("⚠️", "Критическая подавленность!", "Партнеру очень тяжело, поддержи его!", "bg-rose-600");
                }
                if (chatVal >= 85 && lastChat < 85) {
                    showToast("💬", "Сильное желание пообщаться!", "Партнёр очень хочет поговорить с тобой!", "bg-emerald-600");
                }
            }

            lastDep = depVal;
            lastChat = chatVal;
        }

        window.showToast = function(icon, title, body, bgClass) {
            const toast = document.getElementById("toast");
            
            toast.className = `fixed top-4 left-4 right-4 max-w-sm mx-auto ${bgClass} text-white p-4 rounded-2xl shadow-2xl transition-all duration-500 transform translate-y-0 opacity-100 z-50 flex items-center justify-between border border-white/20`;

            document.getElementById("toastIcon").innerText = icon;
            document.getElementById("toastTitle").innerText = title;
            document.getElementById("toastBody").innerText = body;

            if (navigator.vibrate) {
                navigator.vibrate([200, 100, 200]);
            }

            window.toastTimer = setTimeout(hideToast, 6000);
        };

        window.hideToast = function() {
            const toast = document.getElementById("toast");
            toast.classList.add("-translate-y-32", "opacity-0");
            if (window.toastTimer) clearTimeout(window.toastTimer);
        };
    </script>
</body>
</html>
