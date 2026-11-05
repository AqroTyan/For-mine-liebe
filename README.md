<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Couple Sync Widgets</title>
    <script src="https://cdn.jsdelivr.net/npm/react@18/umd/react.production.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background: #0f172a; color: #f8fafc; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center p-4">
    <div id="root" class="w-full max-w-md"></div>

    <script type="text/babel">
        function App() {
            const [pairCode, setPairCode] = React.useState("777888");
            const [inputCode, setInputCode] = React.useState("");
            const [depression, setDepression] = React.useState(15);
            const [chatDesire, setChatDesire] = React.useState(70);
            
            // Партнер (симуляция или данные из базы)
            const [partnerDepression, setPartnerDepression] = React.useState(40);
            const [partnerChatDesire, setPartnerChatDesire] = React.useState(85);

            // Проверка критических триггеров уведомлений
            React.useEffect(() => {
                if (partnerDepression >= 85) {
                    alert("⚠️ ВНИМАНИЕ: У партнера критический уровень подавленности!");
                }
                if (partnerChatDesire >= 85) {
                    alert("💬 ПАРТНЕР ХОЧЕТ ОБЩАТЬСЯ: Уровень желания пообщаться на максимуме!");
                }
            }, [partnerDepression, partnerChatDesire]);

            return (
                <div className="space-y-6">
                    <header className="text-center">
                        <h1 className="text-2xl font-bold tracking-tight">Couple Sync 🤍</h1>
                        <p className="text-xs text-slate-400 mt-1">Код вашої пари: <span className="text-indigo-400 font-mono font-bold text-sm">{pairCode}</span></p>
                    </header>

                    {/* Мої віджети */}
                    <div className="bg-slate-800/80 backdrop-blur border border-slate-700/60 rounded-2xl p-5 shadow-xl space-y-4">
                        <h2 className="text-sm font-semibold text-slate-300 uppercase tracking-wider">Мій стан</h2>
                        
                        <div>
                            <div className="flex justify-between text-sm mb-1">
                                <span>Подавленість</span>
                                <span className="font-bold text-rose-400">{depression}%</span>
                            </div>
                            <input 
                                type="range" min="0" max="100" value={depression} 
                                onChange={(e) => setDepression(Number(e.target.value))}
                                className="w-full accent-rose-500 cursor-pointer"
                            />
                        </div>

                        <div>
                            <div className="flex justify-between text-sm mb-1">
                                <span>Бажання пообщаться</span>
                                <span className="font-bold text-emerald-400">{chatDesire}%</span>
                            </div>
                            <input 
                                type="range" min="0" max="100" value={chatDesire} 
                                onChange={(e) => setChatDesire(Number(e.target.value))}
                                className="w-full accent-emerald-500 cursor-pointer"
                            />
                        </div>
                    </div>

                    {/* Віджети партнера */}
                    <div className="bg-slate-800/80 backdrop-blur border border-slate-700/60 rounded-2xl p-5 shadow-xl space-y-4">
                        <h2 className="text-sm font-semibold text-slate-300 uppercase tracking-wider">Стан партнера</h2>
                        
                        <div className="space-y-3">
                            <div className="bg-slate-900/60 p-3 rounded-xl flex justify-between items-center">
                                <span className="text-sm text-slate-300">Подавленість партнера</span>
                                <span className={`font-bold px-2.5 py-1 rounded-lg text-xs ${partnerDepression >= 85 ? 'bg-rose-500/20 text-rose-400 animate-pulse' : 'bg-slate-800 text-slate-200'}`}>
                                    {partnerDepression}% {partnerDepression >= 85 && '⚠️'}
                                </span>
                            </div>

                            <div className="bg-slate-900/60 p-3 rounded-xl flex justify-between items-center">
                                <span className="text-sm text-slate-300">Бажання пообщаться</span>
                                <span className={`font-bold px-2.5 py-1 rounded-lg text-xs ${partnerChatDesire >= 85 ? 'bg-emerald-500/20 text-emerald-400 animate-pulse' : 'bg-slate-800 text-slate-200'}`}>
                                    {partnerChatDesire}% {partnerChatDesire >= 85 && '🔥'}
                                </span>
                            </div>
                        </div>
                    </div>
                </div>
            );
        }

        ReactDOM.createRoot(document.getElementById('root')).render(<App />);
    </script>
</body>
</html>
