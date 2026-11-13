
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Real Count Pilkades Desa Pelangan (2027 - 2035)</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col">

    <!-- TOP BAR / HEADER -->
    <header class="bg-slate-900 text-white shadow-md sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 py-3 flex flex-wrap items-center justify-between gap-3">
            
            <!-- Tombol Full Screen & Branding Logo Desa di Kiri Atas -->
            <div class="flex items-center space-x-3">
                <button onclick="toggleFullScreen()" id="fsBtn" title="Mode Layar Penuh" class="bg-emerald-600 hover:bg-emerald-500 text-white p-2.5 rounded-xl transition flex items-center justify-center shadow-sm">
                    <i id="fsIcon" class="fa-solid fa-expand text-lg"></i>
                </button>
                <div id="headerLogoContainer" class="flex items-center space-x-3 cursor-pointer" onclick="switchTab('public')">
                    <img id="navVillageLogo" src="" alt="Logo Desa" class="w-10 h-10 object-cover rounded-full border-2 border-emerald-400 bg-slate-800 hidden">
                    <div id="navVillageLogoFallback" class="w-10 h-10 rounded-full bg-emerald-600 flex items-center justify-center text-white font-bold text-lg shadow-sm">
                        <i class="fa-solid fa-landmark"></i>
                    </div>
                    <div>
                        <h1 class="font-bold text-base md:text-lg tracking-wide leading-tight" id="navTitle">Pilkades Desa Pelangan</h1>
                        <p class="text-xs text-emerald-400 font-medium" id="navSubtitle">Periode 2027 - 2035</p>
                    </div>
                </div>
            </div>

            <!-- Navigasi Menu Utama -->
            <nav class="flex items-center space-x-1 md:space-x-2 bg-slate-800/80 p-1.5 rounded-xl border border-slate-700/60 overflow-x-auto">
                <button onclick="switchTab('public')" id="tab-public" class="px-3 py-2 rounded-lg text-xs md:text-sm font-semibold transition bg-emerald-600 text-white shadow shrink-0">
                    <i class="fa-solid fa-chart-pie mr-1"></i> Dashboard
                </button>
                <button onclick="switchTab('witness')" id="tab-witness" class="px-3 py-2 rounded-lg text-xs md:text-sm font-semibold transition text-slate-300 hover:text-white hover:bg-slate-700/50 shrink-0">
                    <i class="fa-solid fa-pen-to-square mr-1"></i> Input Saksi
                </button>
                <button onclick="switchTab('admin')" id="tab-admin" class="px-3 py-2 rounded-lg text-xs md:text-sm font-semibold transition text-slate-300 hover:text-white hover:bg-slate-700/50 shrink-0">
                    <i class="fa-solid fa-lock mr-1"></i> Admin
                </button>
                <button onclick="switchTab('music')" id="tab-music" class="px-3 py-2 rounded-lg text-xs md:text-sm font-semibold transition text-slate-300 hover:text-white hover:bg-slate-700/50 shrink-0">
                    <i class="fa-solid fa-music mr-1"></i> Gending & Musik
                </button>
            </nav>
        </div>
    </header>

    <!-- KONTEN UTAMA -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 py-6">

        <!-- ================= 1. TAB DASHBOARD PUBLIK ================= -->
        <section id="content-public" class="space-y-6">
            <!-- Banner Utama dengan Tempat Unggah Logo Banner Independen (Ukuran Besar) -->
            <div class="bg-gradient-to-r from-emerald-800 via-teal-700 to-slate-900 rounded-3xl p-6 md:p-8 text-white shadow-xl relative overflow-hidden flex flex-col md:flex-row items-center justify-between gap-6">
                <div class="absolute -right-10 -bottom-10 w-64 h-64 bg-emerald-500/10 rounded-full blur-3xl pointer-events-none"></div>
                
                <!-- Sisi Kiri: Teks Identitas Desa -->
                <div class="space-y-3 z-10 text-center md:text-left">
                    <span class="inline-flex items-center px-3 py-1 rounded-full text-xs font-semibold bg-emerald-500/20 text-emerald-300 border border-emerald-400/30">
                        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse mr-2"></span> REAL COUNT LIVE PEMILIHAN KEPALA DESA
                    </span>
                    <h2 class="text-2xl md:text-4xl font-extrabold tracking-tight" id="bannerVillageName">Desa Pelangan</h2>
                    <p class="text-emerald-100 text-sm md:text-base max-w-lg">
                        Transparansi hasil pemungutan suara pemilihan Kepala Desa Pelangan periode <span id="bannerPeriode" class="font-bold text-white">2027 - 2035</span>. Data bersumber langsung dari formulir C.Hasil saksi TPS.
                    </p>
                </div>

                <!-- Sisi Tengah: Tempat Unggah & Preview Logo Khusus Banner (Tidak Tersinkron ke Header) -->
                <div class="z-10 flex flex-col items-center bg-white/10 backdrop-blur-md p-5 rounded-3xl border border-white/20 text-center shadow-inner">
                    <div class="relative group cursor-pointer" onclick="document.getElementById('bannerLogoInputFile').click()" title="Klik untuk mengunggah logo khusus banner">
                        <div id="bannerLogoDisplay" class="w-28 h-28 rounded-full bg-emerald-600 border-4 border-emerald-300 flex items-center justify-center text-white text-4xl font-bold shadow-lg overflow-hidden">
                            <i class="fa-solid fa-landmark"></i>
                        </div>
                        <img id="bannerLogoImg" src="" alt="Logo Banner" class="w-28 h-28 rounded-full object-cover border-4 border-emerald-300 shadow-lg hidden">
                        <div class="absolute inset-0 bg-black/60 rounded-full flex flex-col items-center justify-center opacity-0 group-hover:opacity-100 transition text-white text-xs font-bold gap-1">
                            <i class="fa-solid fa-camera text-lg"></i>
                            <span>Ganti Logo</span>
                        </div>
                    </div>
                    <input type="file" id="bannerLogoInputFile" accept="image/*" class="hidden" onchange="uploadBannerLogoOnly(event)">
                </div>

                <!-- Sisi Kanan: Progress TPS Masuk -->
                <div class="z-10 flex flex-col items-center bg-white/10 backdrop-blur-md px-6 py-4 rounded-2xl border border-white/20 text-center shadow-inner">
                    <span class="text-xs uppercase tracking-wider text-emerald-200 font-medium">Progress TPS Masuk</span>
                    <div class="text-3xl font-black text-white mt-1"><span id="pubTpsMasuk">0</span> / <span id="pubTpsTotal">0</span></div>
                    <span id="pubTpsPercent" class="text-xs bg-emerald-500 text-slate-900 font-bold px-2 py-0.5 rounded-full mt-1">0% Masuk</span>
                </div>
            </div>

            <!-- Kartu Statistik Utama -->
            <div class="grid grid-cols-2 md:grid-cols-5 gap-3 md:gap-4">
                <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-200/80 flex flex-col justify-between">
                    <div class="flex items-center justify-between text-slate-500 mb-2">
                        <span class="text-xs font-semibold uppercase tracking-wider">Total DPT</span>
                        <div class="w-8 h-8 rounded-xl bg-blue-50 text-blue-600 flex items-center justify-center font-bold text-sm"><i class="fa-solid fa-users"></i></div>
                    </div>
                    <div>
                        <div class="text-xl md:text-2xl font-black text-slate-900" id="statDpt">0</div>
                        <p class="text-xs text-slate-400 mt-0.5">Daftar Pemilih Tetap</p>
                    </div>
                </div>
                <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-200/80 flex flex-col justify-between">
                    <div class="flex items-center justify-between text-slate-500 mb-2">
                        <span class="text-xs font-semibold uppercase tracking-wider">Suara Sah</span>
                        <div class="w-8 h-8 rounded-xl bg-emerald-50 text-emerald-600 flex items-center justify-center font-bold text-sm"><i class="fa-solid fa-square-poll-vertical"></i></div>
                    </div>
                    <div>
                        <div class="text-xl md:text-2xl font-black text-emerald-600" id="statSuaraSah">0</div>
                        <p class="text-xs text-slate-400 mt-0.5">Akumulasi suara sah</p>
                    </div>
                </div>
                <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-200/80 flex flex-col justify-between">
                    <div class="flex items-center justify-between text-slate-500 mb-2">
                        <span class="text-xs font-semibold uppercase tracking-wider">Suara Tidak Sah</span>
                        <div class="w-8 h-8 rounded-xl bg-amber-50 text-amber-600 flex items-center justify-center font-bold text-sm"><i class="fa-solid fa-triangle-exclamation"></i></div>
                    </div>
                    <div>
                        <div class="text-xl md:text-2xl font-black text-amber-600" id="statSuaraTdkSah">0</div>
                        <p class="text-xs text-slate-400 mt-0.5">Surat suara rusak/tidak sah</p>
                    </div>
                </div>
                <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-200/80 flex flex-col justify-between">
                    <div class="flex items-center justify-between text-slate-500 mb-2">
                        <span class="text-xs font-semibold uppercase tracking-wider">Tidak Terpakai</span>
                        <div class="w-8 h-8 rounded-xl bg-purple-50 text-purple-600 flex items-center justify-center font-bold text-sm"><i class="fa-solid fa-box-archive"></i></div>
                    </div>
                    <div>
                        <div class="text-xl md:text-2xl font-black text-purple-600" id="statSuaraTdkTerpakai">0</div>
                        <p class="text-xs text-slate-400 mt-0.5">Sisa surat suara TPS</p>
                    </div>
                </div>
                <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-200/80 col-span-2 md:col-span-1 flex flex-col justify-between">
                    <div class="flex items-center justify-between text-slate-500 mb-2">
                        <span class="text-xs font-semibold uppercase tracking-wider">Partisipasi (Turnout)</span>
                        <div class="w-8 h-8 rounded-xl bg-teal-50 text-teal-600 flex items-center justify-center font-bold text-sm"><i class="fa-solid fa-chart-line"></i></div>
                    </div>
                    <div>
                        <div class="text-xl md:text-2xl font-black text-teal-700" id="statTurnout">0%</div>
                        <p class="text-xs text-slate-400 mt-0.5">Kehadiran pemilih</p>
                    </div>
                </div>
            </div>

            <!-- Grafik & Perolehan Suara (Urutan Berdasarkan Nomor Urut Paslon) -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Grafik Batang -->
                <div class="lg:col-span-2 bg-white p-6 rounded-3xl shadow-sm border border-slate-200/80 flex flex-col">
                    <div class="flex flex-wrap items-center justify-between gap-3 mb-6">
                        <div>
                            <h3 class="font-bold text-lg text-slate-900">Grafik Perolehan Suara Calon</h3>
                            <p class="text-xs text-slate-500">Urutan grafik tetap berdasarkan Nomor Urut Paslon</p>
                        </div>
                        <div class="flex items-center space-x-2">
                            <label class="text-xs font-semibold text-slate-600 flex items-center gap-1.5 cursor-pointer bg-slate-100 px-3 py-1.5 rounded-xl border border-slate-200">
                                <input type="checkbox" id="filterVerifiedOnly" onchange="renderPublicDashboard()" class="accent-emerald-600 w-4 h-4 rounded">
                                Hanya Terverifikasi Admin
                            </label>
                        </div>
                    </div>
                    <div class="relative flex-grow min-h-[320px] flex items-center justify-center">
                        <canvas id="voteChart"></canvas>
                    </div>
                </div>

                <!-- Leaderboard / Pimpinan Sementara -->
                <div class="bg-white p-6 rounded-3xl shadow-sm border border-slate-200/80 flex flex-col">
                    <h3 class="font-bold text-lg text-slate-900 mb-1">Pimpinan Sementara</h3>
                    <p class="text-xs text-slate-500 mb-4">Urutan perolehan suara terbanyak</p>
                    <div id="leaderboardList" class="space-y-3 overflow-y-auto max-h-[360px] pr-1">
                        <!-- Render via JS -->
                    </div>
                </div>
            </div>

            <!-- Tabel Rekapitulasi Suara Per Paslon (Urutan No. Urut) -->
            <div class="bg-white rounded-3xl shadow-sm border border-slate-200/80 overflow-hidden">
                <div class="p-6 border-b border-slate-100">
                    <h3 class="font-bold text-lg text-slate-900">Tabel Rekapitulasi Perolehan Suara Calon</h3>
                    <p class="text-xs text-slate-500">Rincian perolehan suara sah dan capaian persentase kandidat sesuai nomor urut</p>
                </div>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-50 text-slate-500 text-xs uppercase tracking-wider border-b border-slate-200">
                                <th class="p-4 font-bold">No. Urut & Kandidat</th>
                                <th class="p-4 font-bold">Nama Calon Kepala Desa</th>
                                <th class="p-4 font-bold text-center">Total Suara Sah</th>
                                <th class="p-4 font-bold text-center">Capaian (%)</th>
                                <th class="p-4 font-bold">Progress Visual</th>
                            </tr>
                        </thead>
                        <tbody id="publicPaslonTableBody" class="divide-y divide-slate-100 text-sm">
                            <!-- Render via JS -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Tabel Rekapitulasi Per TPS -->
            <div class="bg-white rounded-3xl shadow-sm border border-slate-200/80 overflow-hidden">
                <div class="p-6 border-b border-slate-100">
                    <h3 class="font-bold text-lg text-slate-900">Rekapitulasi Detail Per TPS</h3>
                    <p class="text-xs text-slate-500">Rincian suara per TPS beserta status verifikasi admin</p>
                </div>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse" id="tpsRecapTable">
                        <thead>
                            <tr class="bg-slate-50 text-slate-500 text-xs uppercase tracking-wider border-b border-slate-200" id="tpsRecapHeader">
                                <!-- Rendered dynamically -->
                            </tr>
                        </thead>
                        <tbody id="tpsRecapBody" class="divide-y divide-slate-100 text-sm">
                            <!-- Rendered dynamically -->
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- ================= 2. TAB INPUT SAKSI / TPS ================= -->
        <section id="content-witness" class="space-y-6 hidden">
            <div class="bg-white rounded-3xl p-6 md:p-8 shadow-sm border border-slate-200/80 max-w-3xl mx-auto">
                <div class="flex items-center space-x-4 mb-6 pb-4 border-b border-slate-100">
                    <div class="w-12 h-12 rounded-2xl bg-emerald-50 text-emerald-600 flex items-center justify-center text-xl font-bold">
                        <i class="fa-solid fa-file-signature"></i>
                    </div>
                    <div>
                        <h2 class="text-xl font-extrabold text-slate-900">Panel Saksi / TPS Pelangan</h2>
                        <p class="text-xs text-slate-500">Silakan pilih TPS Anda dan masukkan PIN Saksi untuk melaporkan hasil C.Hasil</p>
                    </div>
                </div>

                <!-- Login Saksi TPS -->
                <div id="witnessLoginBox" class="bg-slate-50 p-6 rounded-2xl border border-slate-200 space-y-4">
                    <h3 class="font-bold text-slate-800 text-sm"><i class="fa-solid fa-key text-emerald-600 mr-2"></i> Otorisasi Saksi TPS</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-semibold text-slate-600 mb-1">Pilih TPS</label>
                            <select id="witnessSelectTps" class="w-full bg-white border border-slate-300 rounded-xl px-3.5 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                                <!-- Rendered via JS -->
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-600 mb-1">PIN Saksi</label>
                            <div class="flex gap-2">
                                <input type="password" id="witnessPinInput" placeholder="Masukkan PIN" class="w-full bg-white border border-slate-300 rounded-xl px-3.5 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                                <button onclick="loginWitness()" class="bg-emerald-600 hover:bg-emerald-500 text-white font-bold px-5 py-2.5 rounded-xl text-sm transition shadow-sm">Masuk</button>
                            </div>
                        </div>
                    </div>
                    <p class="text-xs text-slate-400 italic">Info: PIN default setiap TPS (1001 s.d 1006 sesuai nomor TPS) atau dapat diatur di admin.</p>
                </div>

                <!-- Form Input Suara Saksi (Hidden sebelum login) -->
                <div id="witnessFormContainer" class="hidden space-y-6">
                    <div class="flex items-center justify-between bg-emerald-50 border border-emerald-200 p-4 rounded-2xl text-emerald-900">
                        <div>
                            <span class="text-xs font-semibold text-emerald-600 uppercase tracking-wider">Sedang Mengisi Sebagai:</span>
                            <div id="witnessActiveTitle" class="font-bold text-base">TPS 1</div>
                        </div>
                        <button onclick="logoutWitness()" class="text-xs font-bold text-red-600 hover:text-red-700 bg-white px-3 py-1.5 rounded-lg border border-red-200 shadow-xs">Keluar TPS</button>
                    </div>

                    <form id="formCahasil" onsubmit="submitWitnessForm(event)" class="space-y-6">
                        <div>
                            <h4 class="font-bold text-slate-900 mb-3 flex items-center justify-between">
                                <span>Perolehan Suara Sah Paslon</span>
                                <span class="text-xs font-normal text-slate-500">Sesuai Form C.Hasil-KWK</span>
                            </h4>
                            <div id="witnessPaslonInputs" class="space-y-3">
                                <!-- Rendered via JS -->
                            </div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 pt-2">
                            <div>
                                <label class="block text-xs font-semibold text-slate-700 mb-1">Suara Tidak Sah</label>
                                <input type="number" min="0" id="inputSuaraTdkSah" required oninput="calculateWitnessTotal()" class="w-full bg-white border border-slate-300 rounded-xl px-3.5 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-700 mb-1">Suara Tidak Terpakai (Sisa Surat Suara)</label>
                                <input type="number" min="0" id="inputSuaraTdkTerpakai" required oninput="calculateWitnessTotal()" class="w-full bg-white border border-slate-300 rounded-xl px-3.5 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                            </div>
                        </div>

                        <div class="bg-slate-50 p-4 rounded-2xl border border-slate-200 flex flex-wrap items-center justify-between gap-3">
                            <div>
                                <span class="text-xs text-slate-500 block">Total Penggunaan Surat Suara</span>
                                <div class="text-lg font-black text-slate-900"><span id="witnessTotalPenggunaan">0</span> Suara <span class="text-xs font-normal text-slate-500">(Sah + Tidak Sah)</span></div>
                            </div>
                            <div>
                                <span class="text-xs text-slate-500 block">Batas Maksimal DPT + 2.5% Cadangan</span>
                                <div class="text-lg font-black text-blue-600"><span id="witnessMaxDpt">0</span> Surat Suara</div>
                            </div>
                        </div>

                        <div>
                            <label class="block text-xs font-semibold text-slate-700 mb-1">Catatan Kejadian Khusus / Sanggahan Saksi (Opsional)</label>
                            <textarea id="witnessCatatan" rows="3" placeholder="Tuliskan catatan khusus jika ada..." class="w-full bg-white border border-slate-300 rounded-xl p-3.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none"></textarea>
                        </div>

                        <div class="flex items-center justify-end gap-3 pt-2">
                            <button type="submit" class="w-full md:w-auto bg-emerald-600 hover:bg-emerald-500 text-white font-bold px-8 py-3 rounded-xl text-sm transition shadow-md flex items-center justify-center gap-2">
                                <i class="fa-solid fa-paper-plane"></i> Kirim / Perbarui Laporan C.Hasil
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </section>

        <!-- ================= 3. TAB PEMUTAR MUSIK & UPLOAD AUDIO LOKAL ================= -->
        <section id="content-music" class="space-y-6 hidden">
            <div class="bg-white rounded-3xl p-6 md:p-8 shadow-sm border border-slate-200/80 max-w-3xl mx-auto space-y-6">
                <div class="flex items-center space-x-4 pb-4 border-b border-slate-100">
                    <div class="w-12 h-12 rounded-2xl bg-teal-50 text-teal-600 flex items-center justify-center text-xl font-bold">
                        <i class="fa-solid fa-music"></i>
                    </div>
                    <div>
                        <h2 class="text-xl font-extrabold text-slate-900">Pemutar Musik & Gending Tradisional</h2>
                        <p class="text-xs text-slate-500">Unggah file audio (.mp3 / .wav) dari perangkat Anda untuk menemani proses Pilkades Desa Pelangan</p>
                    </div>
                </div>

                <!-- Active Player Box -->
                <div class="bg-gradient-to-br from-slate-900 to-emerald-950 text-white p-6 rounded-3xl shadow-lg space-y-4">
                    <div class="flex items-center justify-between">
                        <span class="text-xs uppercase font-extrabold tracking-wider bg-emerald-500/20 text-emerald-300 px-3 py-1 rounded-full border border-emerald-400/30">
                            <i class="fa-solid fa-compact-disc animate-spin mr-1.5"></i> Sedang Diputar
                        </span>
                        <span id="nowPlayingIndex" class="text-xs text-slate-300 font-mono">Track 1 dari 1</span>
                    </div>

                    <div class="text-center space-y-1 py-2">
                        <h3 id="currentTrackTitle" class="text-lg md:text-xl font-bold">Belum ada musik</h3>
                        <p id="currentTrackArtist" class="text-xs text-emerald-300">Silakan upload file audio (.mp3) di bawah</p>
                    </div>

                    <!-- Audio Element -->
                    <div class="pt-2">
                        <audio id="audioPlayer" controls class="w-full accent-emerald-500" onended="playNextTrack()">
                            Your browser does not support the audio element.
                        </audio>
                    </div>
                </div>

                <!-- Form Upload File Musik Manual dari Perangkat -->
                <div class="bg-slate-50 p-5 rounded-2xl border border-slate-200 space-y-4">
                    <h3 class="font-bold text-slate-900 text-sm flex items-center gap-2">
                        <i class="fa-solid fa-cloud-arrow-up text-emerald-600"></i> Upload File Musik / Gending (.mp3)
                    </h3>
                    <form onsubmit="uploadLocalMusicTrack(event)" class="space-y-3">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
                            <div>
                                <label class="block text-xs font-semibold text-slate-700 mb-1">Judul Gending / Lagu</label>
                                <input type="text" id="uploadTrackTitle" required placeholder="Contoh: Gendang Beleq Pelangan" class="w-full bg-white border border-slate-300 rounded-xl px-3.5 py-2 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-700 mb-1">Nama Artis / Pencipta</label>
                                <input type="text" id="uploadTrackArtist" required placeholder="Contoh: Seniman Lokal" class="w-full bg-white border border-slate-300 rounded-xl px-3.5 py-2 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                            </div>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 mb-1">Pilih File Audio dari Perangkat (.mp3 / .wav)</label>
                            <input type="file" id="uploadAudioFile" accept="audio/*" required class="w-full bg-white border border-slate-300 rounded-xl px-3.5 py-2 text-sm file:mr-4 file:py-1 file:px-4 file:rounded-lg file:border-0 file:text-xs file:font-bold file:bg-emerald-50 file:text-emerald-700 hover:file:bg-emerald-100 cursor-pointer">
                        </div>
                        <div class="flex justify-end pt-1">
                            <button type="submit" class="bg-emerald-600 hover:bg-emerald-500 text-white font-bold px-5 py-2.5 rounded-xl text-xs transition shadow-sm flex items-center gap-2">
                                <i class="fa-solid fa-upload"></i> Upload & Simpan ke Playlist
                            </button>
                        </div>
                    </form>
                </div>

                <!-- Playlist Daftar Lagu / Gending -->
                <div class="space-y-3">
                    <h3 class="font-bold text-slate-900 text-sm">Daftar Putar (Playlist Gending & Lagu)</h3>
                    <div id="playlistContainer" class="space-y-2">
                        <!-- Render via JS -->
                    </div>
                </div>
            </div>
        </section>

        <!-- ================= 4. TAB PANEL ADMIN ================= -->
        <section id="content-admin" class="space-y-6 hidden">
            <!-- Login Admin -->
            <div id="adminLoginBox" class="bg-white rounded-3xl p-8 shadow-sm border border-slate-200/80 max-w-md mx-auto my-12 text-center">
                <div class="w-16 h-16 bg-slate-900 text-white rounded-2xl mx-auto flex items-center justify-center text-2xl mb-4 shadow">
                    <i class="fa-solid fa-shield-halved"></i>
                </div>
                <h2 class="text-xl font-extrabold text-slate-900 mb-1">Otorisasi Admin Pelangan</h2>
                <p class="text-xs text-slate-500 mb-6">Masukkan PIN Admin untuk mengakses panel kontrol penuh</p>
                
                <form onsubmit="loginAdmin(event)" class="space-y-4 text-left">
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 mb-1">PIN Admin</label>
                        <input type="password" id="adminPinInput" placeholder="Masukkan PIN Admin (default: admin123)" required class="w-full bg-slate-50 border border-slate-300 rounded-xl px-4 py-3 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                    </div>
                    <button type="submit" class="w-full bg-slate-900 hover:bg-slate-800 text-white font-bold py-3 rounded-xl text-sm transition shadow-sm">Masuk Dashboard Admin</button>
                </form>
            </div>

            <!-- Dashboard Kontrol Admin (Hidden sebelum login) -->
            <div id="adminDashboardContainer" class="hidden space-y-6">
                <div class="bg-white p-6 rounded-3xl shadow-sm border border-slate-200/80 flex flex-col md:flex-row md:items-center justify-between gap-4">
                    <div class="flex items-center space-x-4">
                        <div class="w-12 h-12 rounded-2xl bg-slate-900 text-white flex items-center justify-center text-xl font-bold">
                            <i class="fa-solid fa-gauge-high"></i>
                        </div>
                        <div>
                            <h2 class="text-xl font-extrabold text-slate-900">Panel Kontrol Admin Utama</h2>
                            <p class="text-xs text-slate-500">Kelola verifikasi suara, data paslon, data TPS, dan pengaturan desa</p>
                        </div>
                    </div>
                    <button onclick="logoutAdmin()" class="bg-red-50 hover:bg-red-100 text-red-600 font-semibold px-4 py-2.5 rounded-xl text-xs transition border border-red-200 flex items-center gap-2 self-start md:self-auto">
                        <i class="fa-solid fa-right-from-bracket"></i> Keluar Admin
                    </button>
                </div>

                <!-- Submenu Navigasi Admin -->
                <div class="flex flex-wrap gap-2 border-b border-slate-200 pb-2">
                    <button onclick="switchAdminSubTab('verification')" id="admin-tab-verification" class="px-4 py-2 rounded-xl text-xs font-bold transition bg-emerald-600 text-white shadow-xs">
                        <i class="fa-solid fa-clipboard-check mr-1.5"></i> Verifikasi Suara TPS
                    </button>
                    <button onclick="switchAdminSubTab('paslon')" id="admin-tab-paslon" class="px-4 py-2 rounded-xl text-xs font-bold transition bg-slate-200 text-slate-700 hover:bg-slate-300">
                        <i class="fa-solid fa-users-rectangle mr-1.5"></i> Manajemen Paslon
                    </button>
                    <button onclick="switchAdminSubTab('tps')" id="admin-tab-tps" class="px-4 py-2 rounded-xl text-xs font-bold transition bg-slate-200 text-slate-700 hover:bg-slate-300">
                        <i class="fa-solid fa-house-chimney mr-1.5"></i> Manajemen TPS & DPT
                    </button>
                    <button onclick="switchAdminSubTab('settings')" id="admin-tab-settings" class="px-4 py-2 rounded-xl text-xs font-bold transition bg-slate-200 text-slate-700 hover:bg-slate-300">
                        <i class="fa-solid fa-gear mr-1.5"></i> Pengaturan & Data
                    </button>
                </div>

                <!-- SUBTAB 1: VERIFIKASI SUARA TPS -->
                <div id="admin-sub-verification" class="space-y-6">
                    <div class="bg-white p-6 rounded-3xl shadow-sm border border-slate-200/80 flex items-center justify-between flex-wrap gap-4">
                        <div>
                            <h3 class="font-bold text-lg text-slate-900">Verifikasi Laporan C.Hasil Saksi TPS</h3>
                            <p class="text-xs text-slate-500">Setujui atau tolak laporan agar masuk ke perhitungan resmi dashboard publik</p>
                        </div>
                        <button onclick="verifyAllTps()" class="bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-bold px-4 py-2.5 rounded-xl transition shadow-xs">
                            <i class="fa-solid fa-check-double mr-1"></i> Verifikasi Semua TPS
                        </button>
                    </div>

                    <div id="adminTpsVerificationList" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <!-- Rendered via JS -->
                    </div>
                </div>

                <!-- SUBTAB 2: MANAJEMEN PASLON -->
                <div id="admin-sub-paslon" class="space-y-6 hidden">
                    <div class="bg-white p-6 rounded-3xl shadow-sm border border-slate-200/80 flex items-center justify-between flex-wrap gap-4">
                        <div>
                            <h3 class="font-bold text-lg text-slate-900">Daftar Kandidat Calon Kepala Desa</h3>
                            <p class="text-xs text-slate-500">Tambah, edit foto, atau hapus data paslon</p>
                        </div>
                        <button onclick="openPaslonModal()" class="bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-bold px-4 py-2.5 rounded-xl transition shadow-xs flex items-center gap-2">
                            <i class="fa-solid fa-plus"></i> Tambah Paslon Baru
                        </button>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6" id="adminPaslonCards">
                        <!-- Rendered via JS -->
                    </div>
                </div>

                <!-- SUBTAB 3: MANAJEMEN TPS & DPT -->
                <div id="admin-sub-tps" class="space-y-6 hidden">
                    <div class="bg-white p-6 rounded-3xl shadow-sm border border-slate-200/80 flex items-center justify-between flex-wrap gap-4">
                        <div>
                            <h3 class="font-bold text-lg text-slate-900">Daftar TPS & Jumlah DPT</h3>
                            <p class="text-xs text-slate-500">Atur jumlah DPT per TPS dan PIN saksi</p>
                        </div>
                        <button onclick="openTpsModal()" class="bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-bold px-4 py-2.5 rounded-xl transition shadow-xs flex items-center gap-2">
                            <i class="fa-solid fa-plus"></i> Tambah TPS Baru
                        </button>
                    </div>

                    <div class="bg-white rounded-3xl shadow-sm border border-slate-200/80 overflow-hidden">
                        <div class="overflow-x-auto">
                            <table class="w-full text-left border-collapse">
                                <thead>
                                    <tr class="bg-slate-50 text-slate-500 text-xs uppercase tracking-wider border-b border-slate-200">
                                        <th class="p-4 font-bold">No. TPS</th>
                                        <th class="p-4 font-bold">Nama / Lokasi TPS</th>
                                        <th class="p-4 font-bold">Jumlah DPT</th>
                                        <th class="p-4 font-bold">PIN Saksi</th>
                                        <th class="p-4 font-bold">Status Laporan</th>
                                        <th class="p-4 font-bold text-center">Aksi</th>
                                    </tr>
                                </thead>
                                <tbody id="adminTpsTableBody" class="divide-y divide-slate-100 text-sm">
                                    <!-- Rendered via JS -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- SUBTAB 4: PENGATURAN & DATA -->
                <div id="admin-sub-settings" class="space-y-6 hidden">
                    <div class="bg-white p-6 rounded-3xl shadow-sm border border-slate-200/80 space-y-6 max-w-2xl">
                        <div>
                            <h3 class="font-bold text-lg text-slate-900 mb-1">Pengaturan Identitas Desa & Logo Header</h3>
                            <p class="text-xs text-slate-500">Sesuaikan nama desa, periode pilkades, dan unggah logo resmi untuk bagian Header Atas</p>
                        </div>

                        <form onsubmit="saveVillageSettings(event)" class="space-y-4">
                            <div>
                                <label class="block text-xs font-semibold text-slate-700 mb-1">Nama Desa</label>
                                <input type="text" id="settingVillageName" required class="w-full bg-slate-50 border border-slate-300 rounded-xl px-4 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-700 mb-1">Periode Pilkades</label>
                                <input type="text" id="settingPeriode" required class="w-full bg-slate-50 border border-slate-300 rounded-xl px-4 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-700 mb-1">Upload Logo Header Atas (PNG/JPG/WebP)</label>
                                <div class="flex items-center gap-4">
                                    <input type="file" id="settingVillageLogoFile" accept="image/*" onchange="previewVillageLogo(event)" class="w-full bg-slate-50 border border-slate-300 rounded-xl px-4 py-2 text-sm">
                                    <img id="settingVillageLogoPreview" src="" alt="Preview" class="w-12 h-12 object-cover rounded-full border hidden">
                                </div>
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-700 mb-1">Ganti PIN Admin</label>
                                <input type="password" id="settingAdminPin" placeholder="Kosongkan jika tidak ingin mengubah PIN" class="w-full bg-slate-50 border border-slate-300 rounded-xl px-4 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                            </div>
                            <button type="submit" class="bg-emerald-600 hover:bg-emerald-500 text-white font-bold px-6 py-2.5 rounded-xl text-sm transition shadow-sm">Simpan Pengaturan</button>
                        </form>

                        <hr class="border-slate-200">

                        <!-- Backup & Restore -->
                        <div class="space-y-3">
                            <h4 class="font-bold text-slate-900 text-sm">Pencadangan & Pemulihan Data (Backup / Restore)</h4>
                            <p class="text-xs text-slate-500">Simpan seluruh database aplikasi ke file JSON atau pulihkan dari cadangan sebelumnya.</p>
                            <div class="flex flex-wrap gap-3">
                                <button onclick="exportDataJson()" class="bg-slate-800 hover:bg-slate-700 text-white font-semibold px-4 py-2.5 rounded-xl text-xs transition flex items-center gap-2">
                                    <i class="fa-solid fa-download"></i> Download Backup JSON
                                </button>
                                <label class="bg-slate-200 hover:bg-slate-300 text-slate-800 font-semibold px-4 py-2.5 rounded-xl text-xs transition cursor-pointer flex items-center gap-2">
                                    <i class="fa-solid fa-upload"></i> Restore JSON
                                    <input type="file" id="importJsonFile" accept=".json" onchange="importDataJson(event)" class="hidden">
                                </label>
                                <button onclick="resetDefaultData()" class="bg-red-50 hover:bg-red-100 text-red-600 font-semibold px-4 py-2.5 rounded-xl text-xs transition border border-red-200 flex items-center gap-2">
                                    <i class="fa-solid fa-rotate-right"></i> Reset Data Default
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- MODAL FORM PASLON (TAMBAH/EDIT) -->
    <div id="paslonModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-xs z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 shadow-2xl border border-slate-100 space-y-4">
            <div class="flex items-center justify-between pb-3 border-b border-slate-100">
                <h3 id="paslonModalTitle" class="font-bold text-lg text-slate-900">Tambah Kandidat Paslon</h3>
                <button onclick="closePaslonModal()" class="text-slate-400 hover:text-slate-600 text-lg"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <form id="paslonForm" onsubmit="savePaslon(event)" class="space-y-4">
                <input type="hidden" id="paslonEditIndex" value="-1">
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Nomor Urut</label>
                    <input type="number" min="1" id="paslonNo" required class="w-full bg-slate-50 border border-slate-300 rounded-xl px-3.5 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Nama Lengkap Calon</label>
                    <input type="text" id="paslonName" required class="w-full bg-slate-50 border border-slate-300 rounded-xl px-3.5 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Foto Calon (PNG/JPG/WebP)</label>
                    <div class="flex items-center gap-3">
                        <input type="file" id="paslonPhotoFile" accept="image/*" onchange="previewPaslonPhoto(event)" class="w-full bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-sm">
                        <img id="paslonPhotoPreview" src="" alt="Preview" class="w-12 h-12 object-cover rounded-full border hidden">
                    </div>
                    <input type="hidden" id="paslonPhotoBase64">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Warna Grafik (Hex / Warna)</label>
                    <input type="color" id="paslonColor" value="#059669" class="w-full h-10 bg-slate-50 border border-slate-300 rounded-xl px-2 py-1 cursor-pointer">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Visi Singkat</label>
                    <textarea id="paslonVisi" rows="2" class="w-full bg-slate-50 border border-slate-300 rounded-xl p-3 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none" placeholder="Visi kandidat..."></textarea>
                </div>
                <div class="flex justify-end gap-2 pt-2">
                    <button type="button" onclick="closePaslonModal()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 font-semibold px-4 py-2.5 rounded-xl text-xs transition">Batal</button>
                    <button type="submit" class="bg-emerald-600 hover:bg-emerald-500 text-white font-bold px-6 py-2.5 rounded-xl text-xs transition shadow-sm">Simpan Paslon</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL FORM TPS (TAMBAH/EDIT) -->
    <div id="tpsModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-xs z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 shadow-2xl border border-slate-100 space-y-4">
            <div class="flex items-center justify-between pb-3 border-b border-slate-100">
                <h3 id="tpsModalTitle" class="font-bold text-lg text-slate-900">Tambah TPS Baru</h3>
                <button onclick="closeTpsModal()" class="text-slate-400 hover:text-slate-600 text-lg"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <form id="tpsForm" onsubmit="saveTps(event)" class="space-y-4">
                <input type="hidden" id="tpsEditIndex" value="-1">
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Nomor TPS</label>
                    <input type="number" min="1" id="tpsNo" required class="w-full bg-slate-50 border border-slate-300 rounded-xl px-3.5 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Nama / Lokasi TPS</label>
                    <input type="text" id="tpsName" required placeholder="Contoh: Dusun Pelangan I" class="w-full bg-slate-50 border border-slate-300 rounded-xl px-3.5 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Jumlah DPT (Daftar Pemilih Tetap)</label>
                    <input type="number" min="1" id="tpsDpt" required class="w-full bg-slate-50 border border-slate-300 rounded-xl px-3.5 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">PIN Saksi TPS</label>
                    <input type="text" id="tpsPin" required class="w-full bg-slate-50 border border-slate-300 rounded-xl px-3.5 py-2.5 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                </div>
                <div class="flex justify-end gap-2 pt-2">
                    <button type="button" onclick="closeTpsModal()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 font-semibold px-4 py-2.5 rounded-xl text-xs transition">Batal</button>
                    <button type="submit" class="bg-emerald-600 hover:bg-emerald-500 text-white font-bold px-6 py-2.5 rounded-xl text-xs transition shadow-sm">Simpan TPS</button>
                </div>
            </form>
        </div>
    </div>

    <!-- FOOTER -->
    <footer class="bg-white border-t border-slate-200/80 py-6 mt-auto">
        <div class="max-w-7xl mx-auto px-4 text-center space-y-1">
            <p class="text-xs md:text-sm font-bold text-slate-700">Real Count Pemilihan Kepala Desa <span id="footerVillageName">Desa Pelangan</span></p>
            <p class="text-xs text-slate-400">Sistem Informasi Rekapitulasi Suara Pilkades Berbasis Transparan & Akurat</p>
            <div class="pt-2">
                <span class="inline-block bg-slate-100 border border-slate-200/80 text-slate-700 text-xs font-extrabold px-4 py-1 rounded-full shadow-xs">
                    Created By Gifran Afandi
                </span>
            </div>
        </div>
    </footer>

    <!-- SCRIPT APLIKASI -->
    <script>
        // --- DATABASE STATE ---
        const DEFAULT_DATA = {
            villageName: "Desa Pelangan",
            periode: "2027 - 2035",
            adminPin: "admin123",
            villageLogo: "",       // Logo Header Atas
            bannerLogo: "",        // Logo Khusus Banner Utama (Independen / Tidak Disinkronkan)
            paslon: [
                { no: 1, name: "H. Ahmad Fauzi, S.Pd.", visi: "Membangun Desa Pelangan yang Mandiri, Religius, dan Sejahtera.", color: "#059669", photo: "" },
                { no: 2, name: "Siti Rahmawati, S.E.", visi: "Transparansi Anggaran dan Pemberdayaan Ekonomi Kreatif Pemuda Desa.", color: "#2563EB", photo: "" },
                { no: 3, name: "Baharuddin, S.H.", visi: "Peningkatan Infrastruktur Merata dan Pelayanan Publik yang Prima.", color: "#D97706", photo: "" }
            ],
            tps: [
                { id: 1, name: "Dusun Pelangan Barat", dpt: 450, pin: "1001" },
                { id: 2, name: "Dusun Pelangan Timur", dpt: 480, pin: "1002" },
                { id: 3, name: "Dusun Teluk Aji", dpt: 390, pin: "1003" },
                { id: 4, name: "Dusun Selong", dpt: 510, pin: "1004" },
                { id: 5, name: "Dusun Karang Baru", dpt: 420, pin: "1005" },
                { id: 6, name: "Dusun Pesisir Indah", dpt: 350, pin: "1006" }
            ],
            playlist: [],
            results: {}
        };

        let appData = JSON.parse(localStorage.getItem('pilkades_pelangan_db')) || DEFAULT_DATA;
        if(!appData.playlist) appData.playlist = [];
        if(appData.bannerLogo === undefined) appData.bannerLogo = "";

        let currentTrackIdx = 0;
        let activeWitnessTpsId = null;
        let isAdminLoggedIn = false;
        let voteChartInstance = null;
        let chartImagesCache = {};

        function saveDb() {
            localStorage.setItem('pilkades_pelangan_db', JSON.stringify(appData));
        }

        // --- FULL SCREEN FUNCTIONALITY (TOP-LEFT) ---
        function toggleFullScreen() {
            if (!document.fullscreenElement && !document.webkitFullscreenElement && !document.msFullscreenElement) {
                if (document.documentElement.requestFullscreen) {
                    document.documentElement.requestFullscreen();
                } else if (document.documentElement.webkitRequestFullscreen) {
                    document.documentElement.webkitRequestFullscreen();
                } else if (document.documentElement.msRequestFullscreen) {
                    document.documentElement.msRequestFullscreen();
                }
            } else {
                if (document.exitFullscreen) {
                    document.exitFullscreen();
                } else if (document.webkitExitFullscreen) {
                    document.webkitExitFullscreen();
                } else if (document.msExitFullscreen) {
                    document.msExitFullscreen();
                }
            }
        }

        document.addEventListener('fullscreenchange', updateFsIcon);
        document.addEventListener('webkitfullscreenchange', updateFsIcon);
        document.addEventListener('msfullscreenchange', updateFsIcon);

        function updateFsIcon() {
            const isFs = document.fullscreenElement || document.webkitFullscreenElement || document.msFullscreenElement;
            const icon = document.getElementById('fsIcon');
            const btn = document.getElementById('fsBtn');
            if (isFs) {
                icon.className = "fa-solid fa-compress text-lg";
                btn.title = "Keluar Layar Penuh";
            } else {
                icon.className = "fa-solid fa-expand text-lg";
                btn.title = "Mode Layar Penuh";
            }
        }

        // --- NAVIGASI TAB UTAMA ---
        function switchTab(tabId) {
            ['public', 'witness', 'music', 'admin'].forEach(t => {
                const sec = document.getElementById(`content-${t}`);
                if(sec) sec.classList.add('hidden');
                const btn = document.getElementById(`tab-${t}`);
                if(btn) {
                    btn.className = "px-3 py-2 rounded-lg text-xs md:text-sm font-semibold transition text-slate-300 hover:text-white hover:bg-slate-700/50 shrink-0";
                }
            });
            const targetSec = document.getElementById(`content-${tabId}`);
            if(targetSec) targetSec.classList.remove('hidden');
            const activeBtn = document.getElementById(`tab-${tabId}`);
            if(activeBtn) {
                activeBtn.className = "px-3 py-2 rounded-lg text-xs md:text-sm font-semibold transition bg-emerald-600 text-white shadow shrink-0";
            }

            if(tabId === 'public') renderPublicDashboard();
            if(tabId === 'witness') renderWitnessSelect();
            if(tabId === 'music') initMusicPlayer();
            if(tabId === 'admin') {
                if(isAdminLoggedIn) renderAdminDashboard();
            }
        }

        // --- INISIALISASI APLIKASI ---
        window.addEventListener('DOMContentLoaded', () => {
            applyBranding();
            renderPublicDashboard();
            renderWitnessSelect();
            buildPlaylistUI();
        });

        function applyBranding() {
            document.getElementById('navTitle').innerText = `Pilkades ${appData.villageName}`;
            document.getElementById('navSubtitle').innerText = `Periode ${appData.periode}`;
            document.getElementById('bannerVillageName').innerText = appData.villageName;
            document.getElementById('bannerPeriode').innerText = appData.periode;
            document.getElementById('footerVillageName').innerText = appData.villageName;

            // Header Top-Left Logo
            const logoImg = document.getElementById('navVillageLogo');
            const logoFallback = document.getElementById('navVillageLogoFallback');

            if(appData.villageLogo) {
                logoImg.src = appData.villageLogo;
                logoImg.classList.remove('hidden');
                logoFallback.classList.add('hidden');
            } else {
                logoImg.classList.add('hidden');
                logoFallback.classList.remove('hidden');
            }

            // Banner Center Logo (Independen)
            const bannerLogoImg = document.getElementById('bannerLogoImg');
            const bannerLogoDisplay = document.getElementById('bannerLogoDisplay');

            if(appData.bannerLogo) {
                bannerLogoImg.src = appData.bannerLogo;
                bannerLogoImg.classList.remove('hidden');
                bannerLogoDisplay.classList.add('hidden');
            } else {
                bannerLogoImg.classList.add('hidden');
                bannerLogoDisplay.classList.remove('hidden');
            }
        }

        // --- UPLOAD LOGO KHUSUS BANNER UTAMA (TIDAK TERSINKRON KE HEADER) ---
        function uploadBannerLogoOnly(e) {
            const file = e.target.files[0];
            if(file) {
                compressImageFile(file, 300, 300, function(base64Str) {
                    appData.bannerLogo = base64Str;
                    saveDb();
                    applyBranding();
                    alert("Logo khusus Banner Utama berhasil diunggah dan diperbarui!");
                });
            }
        }

        // --- PEMUTAR MUSIK & UPLOAD AUDIO LOKAL ---
        function initMusicPlayer() {
            if(appData.playlist.length > 0 && currentTrackIdx >= appData.playlist.length) {
                currentTrackIdx = 0;
            }
            buildPlaylistUI();
            if(appData.playlist.length > 0) {
                loadTrack(currentTrackIdx);
            } else {
                document.getElementById('currentTrackTitle').innerText = "Belum ada musik";
                document.getElementById('currentTrackArtist').innerText = "Silakan upload file audio (.mp3) di bawah";
            }
        }

        function buildPlaylistUI() {
            let html = '';
            if(appData.playlist.length === 0) {
                html = `<p class="text-xs text-slate-400 italic text-center py-4">Belum ada file gending/lagu yang diunggah. Silakan unggah file MP3 melalui form di atas.</p>`;
            } else {
                appData.playlist.forEach((track, idx) => {
                    html += `
                        <div class="flex items-center justify-between p-3.5 rounded-2xl border transition ${idx === currentTrackIdx ? 'bg-emerald-50 border-emerald-300 text-emerald-900 font-bold' : 'bg-slate-50 border-slate-200 hover:bg-slate-100 text-slate-700'}">
                            <div onclick="selectTrack(${idx})" class="flex items-center space-x-3 cursor-pointer flex-grow">
                                <div class="w-9 h-9 rounded-xl ${idx === currentTrackIdx ? 'bg-emerald-600 text-white' : 'bg-slate-200 text-slate-700'} flex items-center justify-center font-bold text-xs shrink-0">
                                    ${idx === currentTrackIdx ? '<i class="fa-solid fa-volume-high"></i>' : (idx + 1)}
                                </div>
                                <div>
                                    <h4 class="text-sm leading-tight">${track.title}</h4>
                                    <p class="text-xs text-slate-500 font-normal">${track.artist}</p>
                                </div>
                            </div>
                            <div class="flex items-center gap-2">
                                <button onclick="selectTrack(${idx})" class="text-xs font-semibold px-3 py-1.5 rounded-lg ${idx === currentTrackIdx ? 'bg-emerald-600 text-white' : 'bg-slate-200 hover:bg-slate-300 text-slate-700'}">
                                    ${idx === currentTrackIdx ? 'Memutar' : 'Putar'}
                                </button>
                                <button onclick="deleteMusicTrack(${idx})" class="text-xs font-semibold px-2.5 py-1.5 rounded-lg bg-red-50 hover:bg-red-100 text-red-600" title="Hapus Lagu">
                                    <i class="fa-solid fa-trash"></i>
                                </button>
                            </div>
                        </div>
                    `;
                });
            }
            const container = document.getElementById('playlistContainer');
            if(container) container.innerHTML = html;
        }

        function loadTrack(idx) {
            if(appData.playlist.length === 0) return;
            currentTrackIdx = idx;
            const track = appData.playlist[idx];
            document.getElementById('currentTrackTitle').innerText = track.title;
            document.getElementById('currentTrackArtist').innerText = track.artist;
            document.getElementById('nowPlayingIndex').innerText = `Track ${idx + 1} dari ${appData.playlist.length}`;
            
            const player = document.getElementById('audioPlayer');
            if(player) {
                player.src = track.src;
                player.play().catch(err => console.log("Autoplay waiting user interaction"));
            }
            buildPlaylistUI();
        }

        function selectTrack(idx) {
            loadTrack(idx);
        }

        function playNextTrack() {
            if(appData.playlist.length === 0) return;
            currentTrackIdx = (currentTrackIdx + 1) % appData.playlist.length;
            loadTrack(currentTrackIdx);
        }

        function uploadLocalMusicTrack(e) {
            e.preventDefault();
            let title = document.getElementById('uploadTrackTitle').value;
            let artist = document.getElementById('uploadTrackArtist').value;
            let fileInput = document.getElementById('uploadAudioFile');
            let file = fileInput.files[0];

            if(!file) {
                alert("Silakan pilih file audio (.mp3 / .wav) terlebih dahulu!");
                return;
            }

            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = function(evt) {
                let base64Audio = evt.target.result;
                appData.playlist.push({ title: title, artist: artist, src: base64Audio });
                saveDb();
                buildPlaylistUI();

                document.getElementById('uploadTrackTitle').value = '';
                document.getElementById('uploadTrackArtist').value = '';
                fileInput.value = '';
                alert("File audio berhasil diunggah dan ditambahkan ke playlist!");

                if(appData.playlist.length === 1) {
                    loadTrack(0);
                }
            };
            reader.onerror = function() {
                alert("Gagal membaca file audio.");
            };
        }

        function deleteMusicTrack(idx) {
            if(confirm("Hapus gending/lagu ini dari playlist?")) {
                appData.playlist.splice(idx, 1);
                saveDb();
                buildPlaylistUI();
                if(appData.playlist.length > 0) {
                    if(currentTrackIdx >= appData.playlist.length) {
                        currentTrackIdx = 0;
                    }
                    loadTrack(currentTrackIdx);
                } else {
                    const player = document.getElementById('audioPlayer');
                    if(player) { player.pause(); player.src = ''; }
                    document.getElementById('currentTrackTitle').innerText = "Belum ada musik";
                    document.getElementById('currentTrackArtist').innerText = "Silakan upload file audio (.mp3) di bawah";
                }
            }
        }

        // --- KOMPRESI GAMBAR KANVAS (LOGO & FOTO PASLON) ---
        function compressImageFile(file, maxWidth, maxHeight, callback) {
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = function(event) {
                const img = new Image();
                img.src = event.target.result;
                img.onload = function() {
                    let width = img.width;
                    let height = img.height;
                    if (width > height) {
                        if (width > maxWidth) {
                            height *= maxWidth / width;
                            width = maxWidth;
                        }
                    } else {
                        if (height > maxHeight) {
                            width *= maxHeight / height;
                            height = maxHeight;
                        }
                    }
                    const canvas = document.createElement('canvas');
                    canvas.width = width;
                    canvas.height = height;
                    const ctx = canvas.getContext('2d');
                    ctx.drawImage(img, 0, 0, width, height);
                    callback(canvas.toDataURL('image/jpeg', 0.8));
                }
            }
        }

        // --- DASHBOARD PUBLIK & GRAFIK (DIURUTKAN BERDASARKAN NOMOR URUT PASLON) ---
        function renderPublicDashboard() {
            let totalDpt = appData.tps.reduce((acc, t) => acc + Number(t.dpt), 0);
            let totalSuaraSah = 0;
            let totalSuaraTdkSah = 0;
            let totalSuaraTdkTerpakai = 0;
            let tpsMasukCount = 0;

            let paslonVotes = {};
            appData.paslon.forEach(p => paslonVotes[p.no] = 0);

            const verifiedOnly = document.getElementById('filterVerifiedOnly').checked;

            appData.tps.forEach(t => {
                let res = appData.results[t.id];
                if (res && (!verifiedOnly || res.verified)) {
                    tpsMasukCount++;
                    totalSuaraTdkSah += Number(res.tdkSah || 0);
                    totalSuaraTdkTerpakai += Number(res.tdkTerpakai || 0);
                    if(res.votes) {
                        for(let pNo in res.votes) {
                            let cnt = Number(res.votes[pNo] || 0);
                            paslonVotes[pNo] = (paslonVotes[pNo] || 0) + cnt;
                            totalSuaraSah += cnt;
                        }
                    }
                }
            });

            document.getElementById('statDpt').innerText = totalDpt.toLocaleString();
            document.getElementById('statSuaraSah').innerText = totalSuaraSah.toLocaleString();
            document.getElementById('statSuaraTdkSah').innerText = totalSuaraTdkSah.toLocaleString();
            document.getElementById('statSuaraTdkTerpakai').innerText = totalSuaraTdkTerpakai.toLocaleString();
            
            let totalSuaraMasuk = totalSuaraSah + totalSuaraTdkSah;
            let turnoutPercent = totalDpt > 0 ? ((totalSuaraMasuk / totalDpt) * 100).toFixed(1) : 0;
            document.getElementById('statTurnout').innerText = `${turnoutPercent}%`;

            document.getElementById('pubTpsMasuk').innerText = tpsMasukCount;
            document.getElementById('pubTpsTotal').innerText = appData.tps.length;
            let tpsPercent = appData.tps.length > 0 ? Math.round((tpsMasukCount / appData.tps.length) * 100) : 0;
            document.getElementById('pubTpsPercent').innerText = `${tpsPercent}% Masuk`;

            let orderedPaslon = [...appData.paslon].sort((a, b) => a.no - b.no);
            let sortedByVotes = [...appData.paslon].sort((a, b) => (paslonVotes[b.no] || 0) - (paslonVotes[a.no] || 0));

            let lbHtml = '';
            sortedByVotes.forEach((p, idx) => {
                let votes = paslonVotes[p.no] || 0;
                let percent = totalSuaraSah > 0 ? ((votes / totalSuaraSah) * 100).toFixed(1) : 0;
                let rankBadge = idx === 0 ? 'bg-amber-100 text-amber-700 border-amber-300' : 'bg-slate-100 text-slate-700 border-slate-200';
                
                lbHtml += `
                    <div class="flex items-center justify-between p-3 rounded-2xl border ${rankBadge} bg-white shadow-2xs">
                        <div class="flex items-center space-x-3">
                            <div class="w-10 h-10 rounded-full bg-slate-900 text-white font-black flex items-center justify-center shrink-0 overflow-hidden border border-slate-200">
                                ${p.photo ? `<img src="${p.photo}" class="w-full h-full object-cover">` : `<span>0${p.no}</span>`}
                            </div>
                            <div>
                                <h4 class="font-bold text-slate-900 text-sm leading-tight">${p.name}</h4>
                                <p class="text-xs text-slate-500">No. Urut ${p.no} • ${percent}%</p>
                            </div>
                        </div>
                        <div class="text-right">
                            <div class="text-base font-black text-slate-900">${votes.toLocaleString()}</div>
                            <span class="text-[10px] uppercase font-bold text-emerald-600">Suara Sah</span>
                        </div>
                    </div>
                `;
            });
            document.getElementById('leaderboardList').innerHTML = lbHtml;

            let tBodyHtml = '';
            orderedPaslon.forEach(p => {
                let votes = paslonVotes[p.no] || 0;
                let percent = totalSuaraSah > 0 ? ((votes / totalSuaraSah) * 100).toFixed(2) : '0.00';
                tBodyHtml += `
                    <tr class="hover:bg-slate-50/80 transition">
                        <td class="p-4 font-bold text-slate-900">
                            <div class="flex items-center space-x-3">
                                <div class="w-9 h-9 rounded-full bg-slate-200 overflow-hidden flex items-center justify-center font-bold text-slate-700 shrink-0">
                                    ${p.photo ? `<img src="${p.photo}" class="w-full h-full object-cover">` : p.no}
                                </div>
                                <span class="bg-emerald-100 text-emerald-800 text-xs px-2.5 py-1 rounded-lg font-extrabold">Paslon 0${p.no}</span>
                            </div>
                        </td>
                        <td class="p-4 font-bold text-slate-800">${p.name}</td>
                        <td class="p-4 text-center font-black text-emerald-600 text-base">${votes.toLocaleString()}</td>
                        <td class="p-4 text-center font-extrabold text-slate-700">${percent}%</td>
                        <td class="p-4 w-48">
                            <div class="w-full bg-slate-100 rounded-full h-2.5 overflow-hidden">
                                <div class="h-2.5 rounded-full" style="width: ${percent}%; background-color: ${p.color};"></div>
                            </div>
                        </td>
                    </tr>
                `;
            });
            document.getElementById('publicPaslonTableBody').innerHTML = tBodyHtml;

            renderTpsRecapTable();
            renderVoteChart(orderedPaslon, paslonVotes);
        }

        const paslonAvatarChartPlugin = {
            id: 'paslonAvatarChartPlugin',
            afterDatasetsDraw(chart, args, options) {
                const { ctx, data } = chart;
                const meta = chart.getDatasetMeta(0);
                meta.data.forEach((bar, index) => {
                    const p = data.paslons[index];
                    if (p && p.photo) {
                        let img = chartImagesCache[p.no];
                        if (!img) {
                            img = new Image();
                            img.src = p.photo;
                            chartImagesCache[p.no] = img;
                            img.onload = () => chart.draw();
                        }
                        if (img.complete) {
                            ctx.save();
                            const size = 32;
                            const x = bar.x - size / 2;
                            const y = bar.y - size - 12;
                            ctx.beginPath();
                            ctx.arc(bar.x, y + size/2, size/2, 0, Math.PI * 2, true);
                            ctx.closePath();
                            ctx.clip();
                            ctx.drawImage(img, x, y, size, size);
                            ctx.strokeStyle = p.color || '#059669';
                            ctx.lineWidth = 2;
                            ctx.stroke();
                            ctx.restore();
                        }
                    }
                });
            }
        };

        function renderVoteChart(orderedPaslon, paslonVotes) {
            const ctx = document.getElementById('voteChart').getContext('2d');
            if (voteChartInstance) {
                voteChartInstance.destroy();
            }

            let labels = orderedPaslon.map(p => `Paslon 0${p.no} (${p.name.split(',')[0]})`);
            let dataValues = orderedPaslon.map(p => paslonVotes[p.no] || 0);
            let backgroundColors = orderedPaslon.map(p => p.color || '#059669');

            voteChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    paslons: orderedPaslon,
                    datasets: [{
                        label: 'Perolehan Suara Sah',
                        data: dataValues,
                        backgroundColor: backgroundColors,
                        borderRadius: 12,
                        borderSkipped: false,
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return ` Suara Sah: ${context.parsed.y.toLocaleString()}`;
                                }
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            grid: { color: '#f1f5f9' },
                            ticks: { font: { family: 'Plus Jakarta Sans', weight: '600' } }
                        },
                        x: {
                            grid: { display: false },
                            ticks: { font: { family: 'Plus Jakarta Sans', weight: '600' } }
                        }
                    }
                },
                plugins: [paslonAvatarChartPlugin]
            });
        }

        function renderTpsRecapTable() {
            let orderedPaslon = [...appData.paslon].sort((a, b) => a.no - b.no);
            let headerHtml = `<th class="p-4 font-bold">No. TPS & Lokasi</th><th class="p-4 font-bold text-center">DPT</th>`;
            orderedPaslon.forEach(p => {
                headerHtml += `<th class="p-4 font-bold text-center">Paslon 0${p.no}</th>`;
            });
            headerHtml += `<th class="p-4 font-bold text-center">Sah</th><th class="p-4 font-bold text-center">Tdk Sah</th><th class="p-4 font-bold text-center">Tdk Terpakai</th><th class="p-4 font-bold text-center">Status</th>`;
            document.getElementById('tpsRecapHeader').innerHTML = headerHtml;

            let bodyHtml = '';
            appData.tps.forEach(t => {
                let res = appData.results[t.id];
                let isVerified = res && res.verified;
                let statusBadge = !res ? `<span class="bg-slate-100 text-slate-500 text-xs px-2.5 py-1 rounded-full font-bold">Belum Masuk</span>` :
                                  (isVerified ? `<span class="bg-emerald-100 text-emerald-800 text-xs px-2.5 py-1 rounded-full font-bold"><i class="fa-solid fa-check mr-1"></i> Terverifikasi</span>` : 
                                                `<span class="bg-amber-100 text-amber-800 text-xs px-2.5 py-1 rounded-full font-bold"><i class="fa-solid fa-clock mr-1"></i> Menunggu Verifikasi</span>`);

                let rowVotesHtml = '';
                let totalSahTps = 0;
                orderedPaslon.forEach(p => {
                    let v = res && res.votes ? (res.votes[p.no] || 0) : 0;
                    totalSahTps += Number(v);
                    rowVotesHtml += `<td class="p-4 text-center font-bold text-slate-700">${v.toLocaleString()}</td>`;
                });

                bodyHtml += `
                    <tr class="hover:bg-slate-50/80 transition">
                        <td class="p-4 font-bold text-slate-900">TPS ${t.id} - ${t.name}</td>
                        <td class="p-4 text-center font-semibold text-slate-600">${t.dpt}</td>
                        ${rowVotesHtml}
                        <td class="p-4 text-center font-black text-emerald-600">${totalSahTps.toLocaleString()}</td>
                        <td class="p-4 text-center font-semibold text-amber-600">${res ? (res.tdkSah || 0) : 0}</td>
                        <td class="p-4 text-center font-semibold text-purple-600">${res ? (res.tdkTerpakai || 0) : 0}</td>
                        <td class="p-4 text-center">${statusBadge}</td>
                    </tr>
                `;
            });
            document.getElementById('tpsRecapBody').innerHTML = bodyHtml;
        }

        // --- PANEL SAKSI / TPS ---
        function renderWitnessSelect() {
            let select = document.getElementById('witnessSelectTps');
            let html = '<option value="">-- Pilih TPS Anda --</option>';
            appData.tps.forEach(t => {
                html += `<option value="${t.id}">TPS ${t.id} - ${t.name} (DPT: ${t.dpt})</option>`;
            });
            select.innerHTML = html;
        }

        function loginWitness() {
            let tpsId = document.getElementById('witnessSelectTps').value;
            let pin = document.getElementById('witnessPinInput').value;
            if(!tpsId) {
                alert("Silakan pilih TPS terlebih dahulu!");
                return;
            }
            let tpsObj = appData.tps.find(t => t.id == tpsId);
            if(tpsObj.pin !== pin) {
                alert("PIN Saksi TPS salah! Silakan hubungi admin.");
                return;
            }

            activeWitnessTpsId = Number(tpsId);
            document.getElementById('witnessLoginBox').classList.add('hidden');
            document.getElementById('witnessFormContainer').classList.remove('hidden');
            document.getElementById('witnessActiveTitle').innerText = `TPS ${tpsObj.id} - ${tpsObj.name} (DPT: ${tpsObj.dpt})`;
            document.getElementById('witnessMaxDpt').innerText = Math.round(tpsObj.dpt * 1.025);

            let orderedPaslon = [...appData.paslon].sort((a, b) => a.no - b.no);
            let paslonInputHtml = '';
            orderedPaslon.forEach(p => {
                let existingVal = (appData.results[tpsId] && appData.results[tpsId].votes) ? (appData.results[tpsId].votes[p.no] || '') : '';
                paslonInputHtml += `
                    <div class="flex items-center justify-between gap-4 bg-slate-50 p-3.5 rounded-2xl border border-slate-200">
                        <div class="flex items-center space-x-3">
                            <div class="w-10 h-10 rounded-full bg-emerald-600 text-white font-bold flex items-center justify-center shrink-0 overflow-hidden">
                                ${p.photo ? `<img src="${p.photo}" class="w-full h-full object-cover">` : `<span>0${p.no}</span>`}
                            </div>
                            <div>
                                <h5 class="font-bold text-slate-900 text-sm">Paslon 0${p.no}: ${p.name}</h5>
                                <p class="text-xs text-slate-500">Perolehan suara sah</p>
                            </div>
                        </div>
                        <input type="number" min="0" required name="vote_paslon_${p.no}" value="${existingVal}" oninput="calculateWitnessTotal()" class="w-32 bg-white border border-slate-300 rounded-xl px-3 py-2 text-right font-bold text-slate-900 focus:ring-2 focus:ring-emerald-500 focus:outline-none">
                    </div>
                `;
            });
            document.getElementById('witnessPaslonInputs').innerHTML = paslonInputHtml;

            if(appData.results[tpsId]) {
                document.getElementById('inputSuaraTdkSah').value = appData.results[tpsId].tdkSah || '';
                document.getElementById('inputSuaraTdkTerpakai').value = appData.results[tpsId].tdkTerpakai || '';
                document.getElementById('witnessCatatan').value = appData.results[tpsId].catatan || '';
            } else {
                document.getElementById('inputSuaraTdkSah').value = '';
                document.getElementById('inputSuaraTdkTerpakai').value = '';
                document.getElementById('witnessCatatan').value = '';
            }
            calculateWitnessTotal();
        }

        function logoutWitness() {
            activeWitnessTpsId = null;
            document.getElementById('witnessFormContainer').classList.add('hidden');
            document.getElementById('witnessLoginBox').classList.remove('hidden');
            document.getElementById('witnessPinInput').value = '';
        }

        function calculateWitnessTotal() {
            let totalSah = 0;
            appData.paslon.forEach(p => {
                let inp = document.querySelector(`[name="vote_paslon_${p.no}"]`);
                if(inp) totalSah += Number(inp.value || 0);
            });
            let tdkSah = Number(document.getElementById('inputSuaraTdkSah').value || 0);
            document.getElementById('witnessTotalPenggunaan').innerText = (totalSah + tdkSah).toLocaleString();
        }

        function submitWitnessForm(e) {
            e.preventDefault();
            if(!activeWitnessTpsId) return;

            let votes = {};
            appData.paslon.forEach(p => {
                let inp = document.querySelector(`[name="vote_paslon_${p.no}"]`);
                votes[p.no] = Number(inp.value || 0);
            });
            let tdkSah = Number(document.getElementById('inputSuaraTdkSah').value || 0);
            let tdkTerpakai = Number(document.getElementById('inputSuaraTdkTerpakai').value || 0);
            let catatan = document.getElementById('witnessCatatan').value;

            let existingVerified = appData.results[activeWitnessTpsId] ? appData.results[activeWitnessTpsId].verified : false;

            appData.results[activeWitnessTpsId] = {
                votes: votes,
                tdkSah: tdkSah,
                tdkTerpakai: tdkTerpakai,
                catatan: catatan,
                verified: existingVerified
            };

            saveDb();
            alert("Laporan C.Hasil TPS berhasil dikirim/diperbarui!");
            switchTab('public');
            logoutWitness();
        }

        // --- PANEL ADMIN ---
        function loginAdmin(e) {
            e.preventDefault();
            let pin = document.getElementById('adminPinInput').value;
            if(pin === appData.adminPin) {
                isAdminLoggedIn = true;
                document.getElementById('adminLoginBox').classList.add('hidden');
                document.getElementById('adminDashboardContainer').classList.remove('hidden');
                renderAdminDashboard();
            } else {
                alert("PIN Admin salah!");
            }
        }

        function logoutAdmin() {
            isAdminLoggedIn = false;
            document.getElementById('adminDashboardContainer').classList.add('hidden');
            document.getElementById('adminLoginBox').classList.remove('hidden');
            document.getElementById('adminPinInput').value = '';
        }

        function switchAdminSubTab(subTab) {
            ['verification', 'paslon', 'tps', 'settings'].forEach(st => {
                document.getElementById(`admin-sub-${st}`).classList.add('hidden');
                document.getElementById(`admin-tab-${st}`).className = "px-4 py-2 rounded-xl text-xs font-bold transition bg-slate-200 text-slate-700 hover:bg-slate-300";
            });
            document.getElementById(`admin-sub-${subTab}`).classList.remove('hidden');
            document.getElementById(`admin-tab-${subTab}`).className = "px-4 py-2 rounded-xl text-xs font-bold transition bg-emerald-600 text-white shadow-xs";

            if(subTab === 'verification') renderAdminVerificationList();
            if(subTab === 'paslon') renderAdminPaslonCards();
            if(subTab === 'tps') renderAdminTpsTable();
            if(subTab === 'settings') loadSettingsForm();
        }

        function renderAdminDashboard() {
            renderAdminVerificationList();
            renderAdminPaslonCards();
            renderAdminTpsTable();
        }

        function renderAdminVerificationList() {
            let html = '';
            appData.tps.forEach(t => {
                let res = appData.results[t.id];
                let isVerified = res && res.verified;
                let hasReport = !!res;

                let totalSahTps = 0;
                if(hasReport && res.votes) {
                    for(let pNo in res.votes) totalSahTps += Number(res.votes[pNo] || 0);
                }

                html += `
                    <div class="bg-white p-5 rounded-3xl shadow-sm border border-slate-200 flex flex-col justify-between space-y-4">
                        <div class="flex items-center justify-between">
                            <div>
                                <span class="text-xs font-extrabold text-emerald-600 uppercase tracking-wider">TPS ${t.id}</span>
                                <h4 class="font-bold text-slate-900 text-base">${t.name}</h4>
                            </div>
                            <div>
                                ${isVerified ? `<span class="bg-emerald-100 text-emerald-800 text-xs px-3 py-1 rounded-full font-bold"><i class="fa-solid fa-circle-check mr-1"></i> Terverifikasi</span>` :
                                  (hasReport ? `<span class="bg-amber-100 text-amber-800 text-xs px-3 py-1 rounded-full font-bold"><i class="fa-solid fa-clock mr-1"></i> Menunggu Verifikasi</span>` :
                                               `<span class="bg-slate-100 text-slate-500 text-xs px-3 py-1 rounded-full font-bold">Belum Ada Laporan</span>`)}
                            </div>
                        </div>
                        ${hasReport ? `
                            <div class="bg-slate-50 p-3 rounded-2xl text-xs space-y-1 text-slate-600">
                                <div>Total Suara Sah: <b class="text-slate-900">${totalSahTps}</b> | Suara Tidak Sah: <b class="text-slate-900">${res.tdkSah}</b></div>
                                <div>Catatan: ${res.catatan || '-'}</div>
                            </div>
                        ` : `<div class="text-xs text-slate-400 italic">Saksi TPS belum mengirimkan data C.Hasil.</div>`}

                        <div class="flex items-center justify-end gap-2 pt-2 border-t border-slate-100">
                            ${hasReport ? `
                                <button onclick="toggleVerifyTps(${t.id})" class="${isVerified ? 'bg-amber-500 hover:bg-amber-600' : 'bg-emerald-600 hover:bg-emerald-500'} text-white text-xs font-bold px-4 py-2 rounded-xl transition shadow-xs">
                                    ${isVerified ? 'Batalkan Verifikasi' : 'Verifikasi Data'}
                                </button>
                            ` : ''}
                        </div>
                    </div>
                `;
            });
            document.getElementById('adminTpsVerificationList').innerHTML = html;
        }

        function toggleVerifyTps(tpsId) {
            if(appData.results[tpsId]) {
                appData.results[tpsId].verified = !appData.results[tpsId].verified;
                saveDb();
                renderAdminVerificationList();
                renderPublicDashboard();
            }
        }

        function verifyAllTps() {
            let updated = false;
            for(let tpsId in appData.results) {
                if(!appData.results[tpsId].verified) {
                    appData.results[tpsId].verified = true;
                    updated = true;
                }
            }
            if(updated) {
                saveDb();
                renderAdminVerificationList();
                renderPublicDashboard();
                alert("Semua laporan TPS berhasil diverifikasi!");
            } else {
                alert("Tidak ada laporan baru yang perlu diverifikasi.");
            }
        }

        function renderAdminPaslonCards() {
            let orderedPaslon = [...appData.paslon].sort((a, b) => a.no - b.no);
            let html = '';
            orderedPaslon.forEach((p) => {
                let actualIndex = appData.paslon.findIndex(item => item.no === p.no);
                html += `
                    <div class="bg-white p-6 rounded-3xl shadow-sm border border-slate-200 flex flex-col justify-between space-y-4">
                        <div class="flex items-center space-x-4">
                            <div class="w-16 h-16 rounded-full bg-slate-900 text-white font-black text-xl flex items-center justify-center shrink-0 overflow-hidden border-2 border-slate-200 shadow">
                                ${p.photo ? `<img src="${p.photo}" class="w-full h-full object-cover">` : `<span>0${p.no}</span>`}
                            </div>
                            <div>
                                <span class="bg-emerald-100 text-emerald-800 text-xs px-2.5 py-0.5 rounded-md font-extrabold">No. Urut 0${p.no}</span>
                                <h4 class="font-bold text-slate-900 text-base mt-1">${p.name}</h4>
                            </div>
                        </div>
                        <p class="text-xs text-slate-500 italic">"${p.visi || '-'}"</p>
                        <div class="flex items-center justify-end gap-2 pt-2 border-t border-slate-100">
                            <button onclick="openPaslonModal(${actualIndex})" class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-bold px-3.5 py-2 rounded-xl transition">Edit</button>
                            <button onclick="deletePaslon(${actualIndex})" class="bg-red-50 hover:bg-red-100 text-red-600 text-xs font-bold px-3.5 py-2 rounded-xl transition">Hapus</button>
                        </div>
                    </div>
                `;
            });
            document.getElementById('adminPaslonCards').innerHTML = html;
        }

        function openPaslonModal(index = -1) {
            document.getElementById('paslonModal').classList.remove('hidden');
            document.getElementById('paslonEditIndex').value = index;
            document.getElementById('paslonPhotoPreview').classList.add('hidden');
            document.getElementById('paslonPhotoFile').value = '';
            document.getElementById('paslonPhotoBase64').value = '';

            if(index >= 0) {
                let p = appData.paslon[index];
                document.getElementById('paslonModalTitle').innerText = "Edit Kandidat Paslon";
                document.getElementById('paslonNo').value = p.no;
                document.getElementById('paslonName').value = p.name;
                document.getElementById('paslonVisi').value = p.visi;
                document.getElementById('paslonColor').value = p.color || '#059669';
                if(p.photo) {
                    document.getElementById('paslonPhotoPreview').src = p.photo;
                    document.getElementById('paslonPhotoPreview').classList.remove('hidden');
                    document.getElementById('paslonPhotoBase64').value = p.photo;
                }
            } else {
                document.getElementById('paslonModalTitle').innerText = "Tambah Kandidat Paslon";
                document.getElementById('paslonNo').value = appData.paslon.length + 1;
                document.getElementById('paslonName').value = '';
                document.getElementById('paslonVisi').value = '';
                document.getElementById('paslonColor').value = '#059669';
            }
        }

        function closePaslonModal() {
            document.getElementById('paslonModal').classList.add('hidden');
        }

        function previewPaslonPhoto(e) {
            const file = e.target.files[0];
            if(file) {
                compressImageFile(file, 300, 300, function(base64Str) {
                    document.getElementById('paslonPhotoBase64').value = base64Str;
                    document.getElementById('paslonPhotoPreview').src = base64Str;
                    document.getElementById('paslonPhotoPreview').classList.remove('hidden');
                });
            }
        }

        function savePaslon(e) {
            e.preventDefault();
            let index = Number(document.getElementById('paslonEditIndex').value);
            let no = Number(document.getElementById('paslonNo').value);
            let name = document.getElementById('paslonName').value;
            let visi = document.getElementById('paslonVisi').value;
            let color = document.getElementById('paslonColor').value;
            let photo = document.getElementById('paslonPhotoBase64').value;

            if(index >= 0) {
                if(!photo) photo = appData.paslon[index].photo || '';
                appData.paslon[index] = { no, name, visi, color, photo };
            } else {
                appData.paslon.push({ no, name, visi, color, photo });
            }

            saveDb();
            closePaslonModal();
            renderAdminPaslonCards();
            renderPublicDashboard();
        }

        function deletePaslon(index) {
            if(confirm("Apakah Anda yakin ingin menghapus kandidat paslon ini?")) {
                appData.paslon.splice(index, 1);
                saveDb();
                renderAdminPaslonCards();
                renderPublicDashboard();
            }
        }

        function renderAdminTpsTable() {
            let html = '';
            appData.tps.forEach((t, index) => {
                let res = appData.results[t.id];
                let statusBadge = res ? `<span class="bg-emerald-100 text-emerald-800 text-xs px-2.5 py-1 rounded-full font-bold">Masuk</span>` : `<span class="bg-slate-100 text-slate-500 text-xs px-2.5 py-1 rounded-full font-bold">Belum</span>`;

                html += `
                    <tr class="hover:bg-slate-50/80 transition">
                        <td class="p-4 font-bold text-slate-900">TPS ${t.id}</td>
                        <td class="p-4 font-bold text-slate-800">${t.name}</td>
                        <td class="p-4 font-semibold text-slate-600">${t.dpt.toLocaleString()} pemilih</td>
                        <td class="p-4 font-mono text-xs font-bold text-slate-700">${t.pin}</td>
                        <td class="p-4">${statusBadge}</td>
                        <td class="p-4 text-center space-x-2">
                            <button onclick="openTpsModal(${index})" class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-bold px-3 py-1.5 rounded-xl transition">Edit</button>
                            <button onclick="deleteTps(${index})" class="bg-red-50 hover:bg-red-100 text-red-600 text-xs font-bold px-3 py-1.5 rounded-xl transition">Hapus</button>
                        </td>
                    </tr>
                `;
            });
            document.getElementById('adminTpsTableBody').innerHTML = html;
        }

        function openTpsModal(index = -1) {
            document.getElementById('tpsModal').classList.remove('hidden');
            document.getElementById('tpsEditIndex').value = index;
            if(index >= 0) {
                let t = appData.tps[index];
                document.getElementById('tpsModalTitle').innerText = "Edit Data TPS";
                document.getElementById('tpsNo').value = t.id;
                document.getElementById('tpsName').value = t.name;
                document.getElementById('tpsDpt').value = t.dpt;
                document.getElementById('tpsPin').value = t.pin;
            } else {
                document.getElementById('tpsModalTitle').innerText = "Tambah TPS Baru";
                document.getElementById('tpsNo').value = appData.tps.length + 1;
                document.getElementById('tpsName').value = '';
                document.getElementById('tpsDpt').value = 400;
                document.getElementById('tpsPin').value = "100" + (appData.tps.length + 1);
            }
        }

        function closeTpsModal() {
            document.getElementById('tpsModal').classList.add('hidden');
        }

        function saveTps(e) {
            e.preventDefault();
            let index = Number(document.getElementById('tpsEditIndex').value);
            let id = Number(document.getElementById('tpsNo').value);
            let name = document.getElementById('tpsName').value;
            let dpt = Number(document.getElementById('tpsDpt').value);
            let pin = document.getElementById('tpsPin').value;

            if(index >= 0) {
                appData.tps[index] = { id, name, dpt, pin };
            } else {
                appData.tps.push({ id, name, dpt, pin });
            }

            saveDb();
            closeTpsModal();
            renderAdminTpsTable();
            renderPublicDashboard();
            renderWitnessSelect();
        }

        function deleteTps(index) {
            if(confirm("Hapus data TPS ini?")) {
                appData.tps.splice(index, 1);
                saveDb();
                renderAdminTpsTable();
                renderPublicDashboard();
                renderWitnessSelect();
            }
        }

        function loadSettingsForm() {
            document.getElementById('settingVillageName').value = appData.villageName;
            document.getElementById('settingPeriode').value = appData.periode;
            document.getElementById('settingAdminPin').value = '';
            if(appData.villageLogo) {
                document.getElementById('settingVillageLogoPreview').src = appData.villageLogo;
                document.getElementById('settingVillageLogoPreview').classList.remove('hidden');
            } else {
                document.getElementById('settingVillageLogoPreview').classList.add('hidden');
            }
        }

        function previewVillageLogo(e) {
            const file = e.target.files[0];
            if(file) {
                compressImageFile(file, 250, 250, function(base64Str) {
                    appData.villageLogo = base64Str;
                    document.getElementById('settingVillageLogoPreview').src = base64Str;
                    document.getElementById('settingVillageLogoPreview').classList.remove('hidden');
                });
            }
        }

        function saveVillageSettings(e) {
            e.preventDefault();
            appData.villageName = document.getElementById('settingVillageName').value;
            appData.periode = document.getElementById('settingPeriode').value;
            let newPin = document.getElementById('settingAdminPin').value;
            if(newPin) {
                appData.adminPin = newPin;
            }
            saveDb();
            applyBranding();
            renderPublicDashboard();
            alert("Pengaturan desa berhasil disimpan!");
        }

        function exportDataJson() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(appData, null, 2));
            const downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute("href", dataStr);
            downloadAnchor.setAttribute("download", `backup_pilkades_pelangan_${new Date().toISOString().slice(0,10)}.json`);
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            downloadAnchor.remove();
        }

        function importDataJson(e) {
            const file = e.target.files[0];
            if(file) {
                const reader = new FileReader();
                reader.onload = function(evt) {
                    try {
                        const parsed = JSON.parse(evt.target.result);
                        if(parsed.paslon && parsed.tps) {
                            appData = parsed;
                            if(!appData.playlist) appData.playlist = [];
                            if(appData.bannerLogo === undefined) appData.bannerLogo = "";
                            saveDb();
                            applyBranding();
                            renderPublicDashboard();
                            renderWitnessSelect();
                            if(isAdminLoggedIn) renderAdminDashboard();
                            alert("Data berhasil dipulihkan dari file JSON!");
                        } else {
                            alert("Format file JSON tidak valid.");
                        }
                    } catch(err) {
                        alert("Gagal membaca file JSON.");
                    }
                };
                reader.readAsText(file);
            }
        }

        function resetDefaultData() {
            if(confirm("PERHATIAN: Seluruh data suara dan perubahan akan dikembalikan ke setelan awal. Lanjutkan?")) {
                appData = JSON.parse(JSON.stringify(DEFAULT_DATA));
                saveDb();
                applyBranding();
                renderPublicDashboard();
                renderWitnessSelect();
                if(isAdminLoggedIn) renderAdminDashboard();
                alert("Aplikasi telah di-reset ke data default.");
            }
        }
    </script>
</body>
</html>
