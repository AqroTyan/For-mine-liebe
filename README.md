
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Couple Sync Widget</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-slate-900 text-slate-100 min-h-screen flex items-center justify-center p-4">

    <div class="w-full max-w-sm bg-slate-800/90 backdrop-blur border border-slate-700 p-6 rounded-3xl shadow-2xl space-y-6">
        <div class="text-center">
            <h1 class="text-2xl font-bold tracking-tight text-white">Couple Sync 🤍</h1>
            <p class="text-xs text-slate-400 mt-1">Выберите роль и введите код пары</p>
        </div>

        <!-- Форма входа -->
        <div id="loginBox" class="space-y-4">
            <input id="roomInput" type="text" placeholder="Код пары (например: love123)" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-center font-mono focus:outline-none focus:border-indigo-500 text-white">
            
            <div class="grid grid-cols-2 gap-2">
                <button onclick="connectAs('user1')" class="bg-indigo-600 hover:bg-indigo-500 py-2.5 rounded-xl text-sm font-semibold transition text-white">Я (Парень)</button>
                <button onclick="connectAs('user2')" class="bg-pink-600 hover:bg-pink-500 py-2.5 rounded-xl text-sm font-semibold transition text-white">Девушка</button>
            </div>
        </div>

        <div id="appBody" class="space-y-6 hidden">
            <!-- Мой статус -->
            <div class="bg-slate-900/60 p-4 rounded-2xl border border-slate-700/50 space-y-4">
                <h2 id="myRoleTitle" class="text-xs font-bold text-indigo-400 uppercase tracking-wider">Моё состояние</h2>
                
                <div>
                    <div class="flex justify-between text-sm mb-1">
                        <span>Подавленность</span>
                        <span id="myDepressionVal" class="font-bold text-rose-400">0%</span>
                    </div>
                    <input type="range" id="myDepression" min="0" max="100" value="0" oninput="updateMyStatus()" class="w-full accent-rose-500 cursor-pointer">
                </div>

                <div>
                    <div class="flex justify-between text-sm mb-1">
                        <span>Желание пообщаться</span>
                        <span id="myChatVal" class="font-bold text-emerald-400">0%</span>
                    </div>
                    <input type="range" id="myChat" min="0" max="100" value="0" oninput="updateMyStatus()" class="w-full accent-emerald-500 cursor-pointer">
                </div>
            </div>

            <!-- Статус партнера -->
            <div class="bg-slate-900/60 p-4 rounded-2xl border border-slate-700/50 space-y-3">
                <h2 id="partnerRoleTitle" class="text-xs font-bold text-pink-400 uppercase tracking-wider">Состояние второй половинки</h2>
                
                <div class="flex justify-between items-center bg-slate-800/80 p-3 rounded-xl border border-slate-700/40">
                    <span class="text-sm">Подавленность:</span>
                    <span id="partnerDepression" class="font-bold text-sm bg-slate-900 px-3 py-1 rounded-lg text-slate-300">--</span>
                </div>

                <div class="flex justify-between items-center bg-slate-800/80 p-3 rounded-xl border border-slate-700/40">
                    <span class="text-sm">Желание пообщаться:</span>
                    <span id="partnerChat" class="font-bold text-sm bg-slate-900 px-3 py-1 rounded-lg text-slate-300">--</span>
                </div>
            </div>

            <button onclick="logout()" class="w-full bg-slate-700 hover:bg-slate-600 py-2 rounded-xl text-xs font-medium text-slate-300 transition">Сменить код / роль</button>
        </div>
    </div>

    <!-- Подключаем современный Firebase через модули -->
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

        if ("Notification" in window) {
            Notification.requestPermission();
        }

        // Автоматический вход, если данные сохранились в памяти телефона
        if (roomId && myRole) {
            startApp();
        }

        window.connectAs = function(role) {
            const input = document.getElementById("roomInput").value.trim();
            if (!input) return alert("Введите код пары!");
            
            roomId = input;
            myRole = role;

            // Сохраняем в память телефона, чтобы при перезагрузке не сбивалось
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
            
            onValue(partnerRef, (snap) => {
                const data = snap.val();
                if (data) {
                    renderPartnerData(data);
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

        let alertSentDepression = false;
        let alertSentChat = false;

        function renderPartnerData(data) {
            const depEl = document.getElementById("partnerDepression");
            const chatEl = document.getElementById("partnerChat");

            depEl.innerText = (data.depression ?? 0) + "%";
            chatEl.innerText = (data.chat ?? 0) + "%";

            depEl.className = `font-bold text-sm px-3 py-1 rounded-lg ${data.depression >= 85 ? 'bg-rose-500/20 text-rose-400 animate-pulse border border-rose-500/50' : 'bg-slate-900 text-slate-200'}`;
            chatEl.className = `font-bold text-sm px-3 py-1 rounded-lg ${data.chat >= 85 ? 'bg-emerald-500/20 text-emerald-400 animate-pulse border border-emerald-500/50' : 'bg-slate-900 text-slate-200'}`;

            if (data.depression >= 85 && !alertSentDepression) {
                sendNotification("⚠️ Внимание!", "У вашей второй половинки критический уровень подавленности.");
                alertSentDepression = true;
            } else if (data.depression < 85) {
                alertSentDepression = false;
            }

            if (data.chat >= 85 && !alertSentChat) {
                sendNotification("💬 Высокое желание пообщаться!", "Ваша вторая половинка очень хочет с вами поговорить.");
                alertSentChat = true;
            } else if (data.chat < 85) {
                alertSentChat = false;
            }
        }

        function sendNotification(title, body) {
            if (Notification.permission === "granted") {
                new Notification(title, { body: body });
            }
        }
    </script>
</body>
</html>
