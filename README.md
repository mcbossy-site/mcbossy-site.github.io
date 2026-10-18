<!DOCTYPE html>
<html lang="pl" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MCBossy.pl - Oficjalny Serwer Minecraft</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts: Inter & Unbounded -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&family=Unbounded:wght@600;800;900&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        emeraldGlow: '#10b981',
                        accentPurple: '#a855f7',
                        darkBg: '#090d16',
                        cardBg: 'rgba(15, 23, 42, 0.75)',
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        heading: ['Unbounded', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        /* Custom Glowing & Background Effects */
        body {
            background-color: #080c14;
            color: #f3f4f6;
            background-image: 
                radial-gradient(circle at 15% 20%, rgba(16, 185, 129, 0.08) 0%, transparent 40%),
                radial-gradient(circle at 85% 60%, rgba(168, 85, 247, 0.08) 0%, transparent 40%);
            background-attachment: fixed;
        }

        .glow-emerald {
            box-shadow: 0 0 25px rgba(16, 185, 129, 0.35);
        }

        .glow-purple {
            box-shadow: 0 0 25px rgba(168, 85, 247, 0.35);
        }

        .text-glow {
            text-shadow: 0 0 15px rgba(16, 185, 129, 0.5);
        }

        /* Glassmorphism card styles */
        .glass-card {
            background: rgba(15, 23, 42, 0.65);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        .glass-card:hover {
            border-color: rgba(16, 185, 129, 0.3);
        }

        /* Hero Animation */
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }
        .floating {
            animation: float 4s ease-in-out infinite;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #080c14;
        }
        ::-webkit-scrollbar-thumb {
            background: #1e293b;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #10b981;
        }
    </style>
</head>
<body class="font-sans antialiased overflow-x-hidden selection:bg-emerald-500 selection:text-black">

    <!-- Navigation Bar -->
    <nav class="fixed top-0 left-0 w-full z-50 glass-card border-b border-white/10 transition-all duration-300" id="navbar">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <!-- Brand Logo -->
            <a href="#" class="flex items-center gap-3 group">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-emerald-400 to-emerald-600 flex items-center justify-center text-slate-950 font-heading font-extrabold text-xl shadow-lg group-hover:scale-105 transition-transform">
                    M
                </div>
                <span class="font-heading font-extrabold text-xl tracking-tight text-white group-hover:text-emerald-400 transition-colors">
                    MCBOSSY<span class="text-emerald-400">.PL</span>
                </span>
            </a>

            <!-- Desktop Links -->
            <div class="hidden md:flex items-center gap-8 font-medium text-sm text-gray-300">
                <a href="#about" class="hover:text-emerald-400 transition-colors">O Serwerze</a>
                <a href="#features" class="hover:text-emerald-400 transition-colors">Tryby i Zalety</a>
                <a href="#shop" class="hover:text-emerald-400 transition-colors">Sklep / Rangi</a>
                <a href="#community" class="hover:text-emerald-400 transition-colors">Społeczność</a>
            </div>

            <!-- Action Button -->
            <div class="hidden md:flex items-center gap-4">
                <a href="https://discord.gg" target="_blank" class="px-4 py-2.5 rounded-xl bg-indigo-600/20 text-indigo-400 hover:bg-indigo-600/30 border border-indigo-500/30 font-semibold text-sm flex items-center gap-2 transition-all">
                    <i class="fa-brands fa-discord"></i> Discord
                </a>
                <button onclick="copyIP('mc.mcbossy.pl')" class="px-5 py-2.5 rounded-xl bg-gradient-to-r from-emerald-500 to-teal-600 text-slate-950 font-bold text-sm hover:brightness-110 shadow-lg shadow-emerald-500/20 flex items-center gap-2 transition-all active:scale-95">
                    <i class="fa-solid fa-gamepad"></i> Graj Teraz
                </button>
            </div>

            <!-- Mobile Hamburger -->
            <button id="mobileMenuBtn" class="md:hidden text-gray-300 hover:text-white text-2xl focus:outline-none">
                <i class="fa-solid fa-bars"></i>
            </button>
        </div>

        <!-- Mobile Menu Dropdown -->
        <div id="mobileMenu" class="hidden md:hidden glass-card border-t border-white/10 px-6 py-4 flex flex-col gap-4 text-gray-300">
            <a href="#about" class="hover:text-emerald-400 py-1" onclick="toggleMobileMenu()">O Serwerze</a>
            <a href="#features" class="hover:text-emerald-400 py-1" onclick="toggleMobileMenu()">Tryby i Zalety</a>
            <a href="#shop" class="hover:text-emerald-400 py-1" onclick="toggleMobileMenu()">Sklep / Rangi</a>
            <a href="#community" class="hover:text-emerald-400 py-1" onclick="toggleMobileMenu()">Społeczność</a>
            <div class="pt-2 flex flex-col gap-3">
                <a href="https://discord.gg" target="_blank" class="w-full py-2.5 rounded-xl bg-indigo-600/20 text-indigo-400 border border-indigo-500/30 font-semibold text-center text-sm flex items-center justify-center gap-2">
                    <i class="fa-brands fa-discord"></i> Dołącz do Discorda
                </a>
                <button onclick="copyIP('mc.mcbossy.pl')" class="w-full py-2.5 rounded-xl bg-emerald-500 text-slate-950 font-bold text-center text-sm flex items-center justify-center gap-2">
                    <i class="fa-solid fa-copy"></i> Skopiuj IP Serwera
                </button>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section class="relative pt-36 pb-20 md:pt-48 md:pb-32 px-4 max-w-7xl mx-auto flex flex-col items-center text-center">
        
        <!-- Online Status Badge -->
        <div class="inline-flex items-center gap-3 px-4 py-2 rounded-full glass-card border border-emerald-500/30 mb-8 floating">
            <span class="relative flex h-3 w-3">
                <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"></span>
                <span class="relative inline-flex rounded-full h-3 w-3 bg-emerald-500"></span>
            </span>
            <span class="text-xs sm:text-sm font-semibold text-gray-300">
                Serwer Jest Online: <span id="playerCount" class="text-emerald-400 font-bold">128</span> / 500 graczy
            </span>
        </div>

        <!-- Main Title -->
        <h1 class="font-heading text-4xl sm:text-6xl md:text-7xl font-black tracking-tight text-white mb-6 leading-tight">
            NOWY WYMIAR <br class="hidden sm:inline" />
            <span class="bg-gradient-to-r from-emerald-400 via-teal-300 to-cyan-400 bg-clip-text text-transparent text-glow">
                MINECRAFTA
            </span>
        </h1>

        <!-- Subtitle -->
        <p class="max-w-2xl text-gray-400 text-base sm:text-lg mb-10 leading-relaxed">
            Dołącz do najnowocześniejszego serwera Survival + Gildie z autorskimi systemami ekonomii, unikalnymi eventami oraz niesamowitą społecznością!
        </p>

        <!-- Interactive IP Box -->
        <div class="w-full max-w-md glass-card p-2 sm:p-3 rounded-2xl flex items-center justify-between gap-2 border border-emerald-500/30 glow-emerald mb-8">
            <div class="flex items-center gap-3 pl-3 overflow-hidden">
                <i class="fa-solid fa-server text-emerald-400 text-xl"></i>
                <span class="font-heading font-bold text-base sm:text-lg text-white tracking-wider truncate" id="serverIP">mc.mcbossy.pl</span>
            </div>
            <button onclick="copyIP('mc.mcbossy.pl')" class="px-5 py-3 rounded-xl bg-emerald-500 hover:bg-emerald-400 text-slate-950 font-extrabold text-sm flex items-center gap-2 transition-all shrink-0 active:scale-95">
                <i class="fa-regular fa-copy"></i>
                <span class="hidden sm:inline">KOPIUJ IP</span>
            </button>
        </div>

        <!-- Quick Stats -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-4 w-full max-w-4xl mt-6">
            <div class="glass-card p-4 rounded-2xl text-center">
                <div class="text-emerald-400 font-heading font-extrabold text-2xl sm:text-3xl">1.20.x</div>
                <div class="text-gray-400 text-xs sm:text-sm mt-1">Wersja Gry</div>
            </div>
            <div class="glass-card p-4 rounded-2xl text-center">
                <div class="text-purple-400 font-heading font-extrabold text-2xl sm:text-3xl">100%</div>
                <div class="text-gray-400 text-xs sm:text-sm mt-1">Autorskie Plugin-y</div>
            </div>
            <div class="glass-card p-4 rounded-2xl text-center">
                <div class="text-emerald-400 font-heading font-extrabold text-2xl sm:text-3xl">24/7</div>
                <div class="text-gray-400 text-xs sm:text-sm mt-1">Niskie Pingi / Brak Lagów</div>
            </div>
            <div class="glass-card p-4 rounded-2xl text-center">
                <div class="text-cyan-400 font-heading font-extrabold text-2xl sm:text-3xl">2000+</div>
                <div class="text-gray-400 text-xs sm:text-sm mt-1">Zarejestrowanych</div>
            </div>
        </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="py-20 px-4 max-w-7xl mx-auto">
        <div class="text-center mb-16">
            <h2 class="text-emerald-400 font-semibold text-sm uppercase tracking-widest mb-2">Dlaczego Warto Grać?</h2>
            <h3 class="font-heading text-3xl sm:text-4xl font-extrabold text-white">CO ZNAJDZIESZ NA MCBOSSY?</h3>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
            <!-- Feature 1 -->
            <div class="glass-card p-8 rounded-3xl relative overflow-hidden group hover:-translate-y-2 transition-transform duration-300">
                <div class="w-14 h-14 rounded-2xl bg-emerald-500/10 border border-emerald-500/20 text-emerald-400 flex items-center justify-center text-2xl mb-6 group-hover:bg-emerald-500 group-hover:text-slate-950 transition-colors">
                    <i class="fa-solid fa-shield-halved"></i>
                </div>
                <h4 class="font-heading font-bold text-xl text-white mb-3">System Gildii & Działek</h4>
                <p class="text-gray-400 text-sm leading-relaxed">
                    Załóż własny podbój ze znajomymi lub wybuduj bezpieczne królestwo. Unikalny system wojen gildii oraz ochrony terenu!
                </p>
            </div>

            <!-- Feature 2 -->
            <div class="glass-card p-8 rounded-3xl relative overflow-hidden group hover:-translate-y-2 transition-transform duration-300">
                <div class="w-14 h-14 rounded-2xl bg-purple-500/10 border border-purple-500/20 text-purple-400 flex items-center justify-center text-2xl mb-6 group-hover:bg-purple-500 group-hover:text-slate-950 transition-colors">
                    <i class="fa-solid fa-coins"></i>
                </div>
                <h4 class="font-heading font-bold text-xl text-white mb-3">Rozbudowana Ekonomia</h4>
                <p class="text-gray-400 text-sm leading-relaxed">
                    Rynki graczy, domy aukcyjne, prace oraz własne sklepy. Handluj surowcami, zarabiaj wirtualną walutę i zdominuj serwerowy rynek!
                </p>
            </div>

            <!-- Feature 3 -->
            <div class="glass-card p-8 rounded-3xl relative overflow-hidden group hover:-translate-y-2 transition-transform duration-300">
                <div class="w-14 h-14 rounded-2xl bg-cyan-500/10 border border-cyan-500/20 text-cyan-400 flex items-center justify-center text-2xl mb-6 group-hover:bg-cyan-500 group-hover:text-slate-950 transition-colors">
                    <i class="fa-solid fa-dragon"></i>
                </div>
                <h4 class="font-heading font-bold text-xl text-white mb-3">Bossy i Rajdy</h4>
                <p class="text-gray-400 text-sm leading-relaxed">
                    Walcz z potężnymi bossami na specjalnych arenach! Zdobądź epicki ekwipunek, unikalne klucze do skrzyń i legendarne artefakty.
                </p>
            </div>
        </div>
    </section>

    <!-- Shop / Ranks Section -->
    <section id="shop" class="py-20 px-4 max-w-7xl mx-auto">
        <div class="text-center mb-16">
            <h2 class="text-purple-400 font-semibold text-sm uppercase tracking-widest mb-2">Wspieraj Rozwój Serwera</h2>
            <h3 class="font-heading text-3xl sm:text-4xl font-extrabold text-white">SKLEP & RANGI PREMIUM</h3>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 items-stretch">
            <!-- Rank VIP -->
            <div class="glass-card p-8 rounded-3xl flex flex-col justify-between border border-emerald-500/20">
                <div>
                    <div class="flex items-center justify-between mb-4">
                        <h4 class="font-heading font-extrabold text-2xl text-emerald-400">VIP</h4>
                        <span class="text-xs font-semibold px-3 py-1 rounded-full bg-emerald-500/20 text-emerald-300 border border-emerald-500/30">Na 30 Dni</span>
                    </div>
                    <div class="text-3xl font-heading font-black text-white mb-6">14.99 <span class="text-sm font-normal text-gray-400">PLN</span></div>
                    <ul class="text-sm text-gray-300 space-y-3 mb-8">
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-emerald-400"></i> Prefiks [VIP] na czacie</li>
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-emerald-400"></i> Dostęp do komendy /fly na spawnie</li>
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-emerald-400"></i> Zestaw przedmiotów /kit vip</li>
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-emerald-400"></i> Rezerwowy slot przy pełnym serwerze</li>
                    </ul>
                </div>
                <button onclick="openShopModal('VIP')" class="w-full py-3 rounded-xl bg-emerald-500/20 hover:bg-emerald-500 hover:text-slate-950 text-emerald-400 font-bold border border-emerald-500/30 transition-all">
                    Zakup Rangę
                </button>
            </div>

            <!-- Rank SVIP (Featured) -->
            <div class="glass-card p-8 rounded-3xl flex flex-col justify-between border-2 border-purple-500 relative glow-purple scale-105 z-10 my-4 md:my-0">
                <div class="absolute -top-4 left-1/2 -translate-x-1/2 bg-purple-600 text-white font-bold text-xs px-4 py-1 rounded-full uppercase tracking-wider">
                    Najpopularniejsza
                </div>
                <div>
                    <div class="flex items-center justify-between mb-4">
                        <h4 class="font-heading font-extrabold text-2xl text-purple-400">SUPER VIP</h4>
                        <span class="text-xs font-semibold px-3 py-1 rounded-full bg-purple-500/20 text-purple-300 border border-purple-500/30">Na 30 Dni</span>
                    </div>
                    <div class="text-3xl font-heading font-black text-white mb-6">29.99 <span class="text-sm font-normal text-gray-400">PLN</span></div>
                    <ul class="text-sm text-gray-300 space-y-3 mb-8">
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-purple-400"></i> Wszystkie przywileje VIP</li>
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-purple-400"></i> Dostęp do komendy /enderchest wszędzie</li>
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-purple-400"></i> Zwiększona pojemność działki (+50%)</li>
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-purple-400"></i> Unikalny kosmetyczny efekt cząsteczek</li>
                    </ul>
                </div>
                <button onclick="openShopModal('SUPER VIP')" class="w-full py-3 rounded-xl bg-purple-500 hover:bg-purple-400 text-white font-extrabold transition-all shadow-lg shadow-purple-500/30">
                    Zakup Rangę
                </button>
            </div>

            <!-- Rank BOSS -->
            <div class="glass-card p-8 rounded-3xl flex flex-col justify-between border border-cyan-500/20">
                <div>
                    <div class="flex items-center justify-between mb-4">
                        <h4 class="font-heading font-extrabold text-2xl text-cyan-400">BOSSY</h4>
                        <span class="text-xs font-semibold px-3 py-1 rounded-full bg-cyan-500/20 text-cyan-300 border border-cyan-500/30">Na Zawsze</span>
                    </div>
                    <div class="text-3xl font-heading font-black text-white mb-6">59.99 <span class="text-sm font-normal text-gray-400">PLN</span></div>
                    <ul class="text-sm text-gray-300 space-y-3 mb-8">
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-cyan-400"></i> Miano Króla Serwera [BOSSY]</li>
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-cyan-400"></i> Nielimitowane domy (/sethome)</li>
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-cyan-400"></i> Dostęp do prywatnej strefy BOSS Zone</li>
                        <li class="flex items-center gap-2"><i class="fa-solid fa-check text-cyan-400"></i> Najwyższy priorytet wsparcia na Discordzie</li>
                    </ul>
                </div>
                <button onclick="openShopModal('BOSSY')" class="w-full py-3 rounded-xl bg-cyan-500/20 hover:bg-cyan-500 hover:text-slate-950 text-cyan-400 font-bold border border-cyan-500/30 transition-all">
                    Zakup Rangę
                </button>
            </div>
        </div>
    </section>

    <!-- Community & Discord Banner -->
    <section id="community" class="py-16 px-4 max-w-7xl mx-auto">
        <div class="glass-card p-8 sm:p-12 rounded-3xl border border-indigo-500/30 relative overflow-hidden flex flex-col md:flex-row items-center justify-between gap-8">
            <div class="max-w-xl text-center md:text-left">
                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-indigo-500/20 text-indigo-300 text-xs font-semibold mb-4 border border-indigo-500/30">
                    <i class="fa-brands fa-discord"></i> Społeczność Discord
                </div>
                <h3 class="font-heading text-2xl sm:text-3xl font-extrabold text-white mb-4">DOŁĄCZ DO NASZEGO DISCORDA!</h3>
                <p class="text-gray-400 text-sm sm:text-base leading-relaxed">
                    Bądź na bieżąco z nowościami, bierz udział w cotygodniowych konkursach o rangi oraz zgłaszaj swoje propozycje zmian bezpośrednio do administracji.
                </p>
            </div>
            <a href="https://discord.gg" target="_blank" class="px-8 py-4 rounded-2xl bg-indigo-600 hover:bg-indigo-500 text-white font-extrabold text-base shadow-lg shadow-indigo-600/30 flex items-center gap-3 transition-all shrink-0 active:scale-95">
                <i class="fa-brands fa-discord text-xl"></i> DOŁĄCZ DO SERWERA
            </a>
        </div>
    </section>

    <!-- Footer -->
    <footer class="border-t border-white/10 pt-12 pb-8 px-4">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-6 text-center md:text-left">
            <div>
                <div class="font-heading font-extrabold text-lg text-white mb-1">
                    MCBOSSY<span class="text-emerald-400">.PL</span>
                </div>
                <p class="text-gray-500 text-xs">Wszelkie prawa zastrzeżone &copy; 2026. Niezrzeszony z Mojang AB.</p>
            </div>
            <div class="flex items-center gap-6 text-gray-400 text-sm">
                <a href="#about" class="hover:text-emerald-400 transition-colors">Regulamin</a>
                <a href="#shop" class="hover:text-emerald-400 transition-colors">Kontakt</a>
                <a href="https://discord.gg" target="_blank" class="hover:text-emerald-400 transition-colors">Pomoc</a>
            </div>
        </div>
    </footer>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-8 right-8 glass-card border border-emerald-500/50 px-6 py-4 rounded-2xl flex items-center gap-3 text-white shadow-2xl transition-all duration-300 translate-y-24 opacity-0 z-50">
        <i class="fa-solid fa-circle-check text-emerald-400 text-xl"></i>
        <div>
            <div class="font-bold text-sm">Skopiowano Adres IP!</div>
            <div class="text-xs text-gray-400">Wklej <span class="text-emerald-400 font-mono">mc.mcbossy.pl</span> w grze.</div>
        </div>
    </div>

    <!-- Shop Modal Placeholder -->
    <div id="shopModal" class="fixed inset-0 bg-black/80 backdrop-blur-md hidden z-50 items-center justify-center p-4">
        <div class="glass-card max-w-md w-full p-6 sm:p-8 rounded-3xl border border-white/10 relative">
            <button onclick="closeShopModal()" class="absolute top-4 right-4 text-gray-400 hover:text-white text-xl">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <h3 class="font-heading font-extrabold text-2xl text-white mb-2" id="modalRankTitle">Ranga VIP</h3>
            <p class="text-gray-400 text-sm mb-6">Wpisz swój nick z Minecrafta, aby kontynuować realizację zakupu.</p>
            
            <div class="space-y-4 mb-6">
                <div>
                    <label class="block text-xs font-semibold text-gray-400 mb-2 uppercase">Nick z Gry</label>
                    <input type="text" placeholder="Twój_Nick" class="w-full px-4 py-3 rounded-xl bg-slate-900 border border-white/10 text-white placeholder-gray-600 focus:outline-none focus:border-emerald-500">
                </div>
            </div>

            <button onclick="alert('Przekierowywanie do bramki płatności...'); closeShopModal();" class="w-full py-3 rounded-xl bg-emerald-500 hover:bg-emerald-400 text-slate-950 font-extrabold transition-all">
                Przejdź do Płatności
            </button>
        </div>
    </div>

    <!-- JavaScript Logic -->
    <script>
        // Copy IP with Toast Animation
        function copyIP(ipText) {
            const tempInput = document.createElement('input');
            tempInput.value = ipText;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand('copy');
            document.body.removeChild(tempInput);

            showToast();
        }

        function showToast() {
            const toast = document.getElementById('toast');
            toast.classList.remove('translate-y-24', 'opacity-0');
            
            setTimeout(() => {
                toast.classList.add('translate-y-24', 'opacity-0');
            }, 3000);
        }

        // Toggle Mobile Menu
        function toggleMobileMenu() {
            const mobileMenu = document.getElementById('mobileMenu');
            mobileMenu.classList.toggle('hidden');
        }

        document.getElementById('mobileMenuBtn').addEventListener('click', toggleMobileMenu);

        // Shop Modal Handlers
        function openShopModal(rankName) {
            document.getElementById('modalRankTitle').innerText = 'Ranga ' + rankName;
            const modal = document.getElementById('shopModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeShopModal() {
            const modal = document.getElementById('shopModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        // Simulated Dynamic Online Counter
        setInterval(() => {
            const counter = document.getElementById('playerCount');
            if (counter) {
                let current = parseInt(counter.innerText);
                let change = Math.floor(Math.random() * 5) - 2;
                let newCount = Math.max(90, Math.min(480, current + change));
                counter.innerText = newCount;
            }
        }, 5000);
    </script>
</body>
</html>
