# REAL-COUNT-PILKADES-PELANGAN
Web
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Real Count Pilkades Desa Pelangan (2027-2035)</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- FontAwesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                }
            }
        }
    </script>
</head>
<body class="bg-slate-50 text-slate-800 font-sans min-h-screen flex flex-col">

    <!-- Top Header -->
    <header class="bg-emerald-800 text-white shadow-md sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 py-3 flex flex-col sm:flex-row justify-between items-center gap-3">
            <div class="flex items-center space-x-3">
                <!-- Full Screen Button on Top-Left (Next to Logo/Title) -->
                <button onclick="toggleFullScreen()" id="btnFullScreen" title="Layar Penuh (Full Screen)" class="bg-emerald-700 hover:bg-emerald-600 text-emerald-100 p-2.5 rounded-xl border border-emerald-600 transition flex items-center justify-center shadow-sm">
                    <i class="fa-solid fa-expand text-sm" id="fullScreenIcon"></i>
                </button>
                <div class="bg-emerald-700 p-2 rounded-lg border border-emerald-600 shadow-inner">
                    <i class="fa-solid fa-box-archive text-xl text-emerald-200"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg leading-tight tracking-wide">PILKADES DESA PELANGAN</h1>
                    <p class="text-xs text-emerald-200">Periode 2027 - 2035 | Sistem Informasi Real Count</p>
                </div>
            </div>
            <div class="flex items-center gap-2 flex-wrap justify-center">
                <button onclick="switchRole('public')" id="btnRolePublic" class="px-3.5 py-1.5 text-xs font-medium rounded-lg bg-emerald-900 text-emerald-200 border border-emerald-700 hover:bg-emerald-700 transition flex items-center gap-1.5 shadow-sm">
                    <i class="fa-solid fa-chart-pie"></i> Dashboard Publik
                </button>
                <button onclick="switchRole('witness')" id="btnRoleWitness" class="px-3.5 py-1.5 text-xs font-medium rounded-lg bg-emerald-700 text-white hover:bg-emerald-600 transition flex items-center gap-1.5 shadow-sm">
                    <i class="fa-solid fa-pen-to-square"></i> Panel Saksi/TPS
                </button>
                <button onclick="openAdminLogin()" id="btnRoleAdmin" class="px-3.5 py-1.5 text-xs font-medium rounded-lg bg-amber-600 text-white hover:bg-amber-500 transition flex items-center gap-1.5 shadow-sm">
                    <i class="fa-solid fa-shield-halved"></i> Panel Admin
                </button>
                <button onclick="openDeployGuide()" class="px-3 py-1.5 text-xs font-medium rounded-lg bg-blue-700 text-white hover:bg-blue-600 transition flex items-center gap-1.5 shadow-sm" title="Panduan Online-kan Aplikasi">
                    <i class="fa-solid fa-cloud-arrow-up"></i> Panduan Online
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 py-6">

        <!-- NOTIFICATION BANNER / ALERT BOX -->
        <div id="alertBox" class="hidden mb-6 p-4 rounded-xl shadow-md border flex items-start gap-3 transition-all duration-300">
            <div id="alertIcon" class="text-xl pt-0.5"></div>
            <div class="flex-grow">
                <h4 id="alertTitle" class="font-semibold text-sm"></h4>
                <p id="alertMessage" class="text-xs mt-0.5"></p>
            </div>
            <button onclick="hideAlert()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
        </div>

        <!-- ================= VIEW 1: DASHBOARD / PUBLIK ================= -->
        <div id="viewPublic" class="space-y-6">
            <!-- Quick Stats Banner -->
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-4">
                <div class="bg-white p-5 rounded-2xl shadow-sm border border-slate-200 flex items-center justify-between">
                    <div>
                        <p class="text-xs font-medium text-slate-500 uppercase tracking-wider">Progress TPS Masuk</p>
                        <h3 id="statProgress" class="text-2xl font-bold text-slate-800 mt-1">0 / 0</h3>
                        <p id="statProgressPct" class="text-xs text-emerald-600 font-semibold mt-1"><i class="fa-solid fa-chart-line"></i> 0% Selesai</p>
                    </div>
                    <div class="bg-emerald-50 text-emerald-600 p-3.5 rounded-xl">
                        <i class="fa-solid fa-square-poll-horizontal text-2xl"></i>
                    </div>
                </div>
                <div class="bg-white p-5 rounded-2xl shadow-sm border border-slate-200 flex items-center justify-between">
                    <div>
                        <p class="text-xs font-medium text-slate-500 uppercase tracking-wider">Suara Sah</p>
                        <h3 id="statSuaraSah" class="text-2xl font-bold text-slate-800 mt-1">0</h3>
                        <p id="statSahPct" class="text-xs text-emerald-600 font-semibold mt-1">0% dari suara masuk</p>
                    </div>
                    <div class="bg-indigo-50 text-indigo-600 p-3.5 rounded-xl">
                        <i class="fa-solid fa-check-to-slot text-2xl"></i>
                    </div>
                </div>
                <div class="bg-white p-5 rounded-2xl shadow-sm border border-slate-200 flex items-center justify-between">
                    <div>
                        <p class="text-xs font-medium text-slate-500 uppercase tracking-wider">Suara Tidak Sah</p>
                        <h3 id="statSuaraTdkSah" class="text-2xl font-bold text-slate-800 mt-1">0</h3>
                        <p id="statTdkSahPct" class="text-xs text-rose-600 font-semibold mt-1">0% dari suara masuk</p>
                    </div>
                    <div class="bg-rose-50 text-rose-600 p-3.5 rounded-xl">
                        <i class="fa-solid fa-triangle-exclamation text-2xl"></i>
                    </div>
                </div>
                <div class="bg-white p-5 rounded-2xl shadow-sm border border-slate-200 flex items-center justify-between">
                    <div>
                        <p class="text-xs font-medium text-slate-500 uppercase tracking-wider">Suara Tidak Terpakai</p>
                        <h3 id="statSuaraTdkTerpakai" class="text-2xl font-bold text-slate-800 mt-1">0</h3>
                        <p class="text-xs text-amber-600 font-semibold mt-1">Surat suara sisa</p>
                    </div>
                    <div class="bg-amber-50 text-amber-600 p-3.5 rounded-xl">
                        <i class="fa-solid fa-file-excel text-2xl"></i>
                    </div>
                </div>
                <div class="bg-white p-5 rounded-2xl shadow-sm border border-slate-200 flex items-center justify-between">
                    <div>
                        <p class="text-xs font-medium text-slate-500 uppercase tracking-wider">Partisipasi (Turnout)</p>
                        <h3 id="statTurnout" class="text-2xl font-bold text-slate-800 mt-1">0%</h3>
                        <p id="statTotalDpt" class="text-xs text-slate-500 mt-1">Dari total DPT</p>
                    </div>
                    <div class="bg-blue-50 text-blue-600 p-3.5 rounded-xl">
                        <i class="fa-solid fa-users text-2xl"></i>
                    </div>
                </div>
            </div>

            <!-- Chart & Leading Candidate Section -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Chart Container -->
                <div class="lg:col-span-2 bg-white p-6 rounded-2xl shadow-sm border border-slate-200 flex flex-col justify-between">
                    <div class="flex justify-between items-center mb-4">
                        <div>
                            <h3 class="font-bold text-slate-800 text-lg">Grafik Perolehan Suara Pasangan Calon</h3>
                            <p class="text-xs text-slate-500">Real-time update berdasarkan data TPS yang masuk</p>
                        </div>
                        <span class="bg-emerald-50 text-emerald-700 text-xs px-2.5 py-1 rounded-full font-medium border border-emerald-200">
                            <i class="fa-solid fa-circle text-[8px] animate-pulse text-emerald-600"></i> Live Count
                        </span>
                    </div>
                    <div class="relative h-72 w-full flex items-center justify-center">
                        <canvas id="voteChart"></canvas>
                    </div>
                </div>

                <!-- Leaderboard / Leading Card -->
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200 flex flex-col justify-between">
                    <div>
                        <h3 class="font-bold text-slate-800 text-lg mb-1">Pimpinan Sementara</h3>
                        <p class="text-xs text-slate-500 mb-4">Urutan perolehan suara terbanyak</p>
                        <div id="leaderboardList" class="space-y-3">
                            <!-- Populated dynamically -->
                        </div>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 text-center">
                        <p class="text-[11px] text-slate-400">Timses Pilkades Desa Pelangan 2027-2035</p>
                    </div>
                </div>
            </div>

            <!-- Detailed Paslon Cards -->
            <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200">
                <h3 class="font-bold text-slate-800 text-lg mb-4">Daftar Pasangan Calon Kepala Desa Pelangan</h3>
                <div id="publicPaslonGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <!-- Populated dynamically -->
                </div>
            </div>

            <!-- Recap by TPS Table -->
            <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200 overflow-hidden">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 mb-4">
                    <div>
                        <h3 class="font-bold text-slate-800 text-lg">Rekapitulasi Per TPS</h3>
                        <p class="text-xs text-slate-500">Detail suara masuk, tidak sah, dan surat suara tidak terpakai di setiap TPS Desa Pelangan</p>
                    </div>
                    <div class="relative w-full sm:w-64">
                        <span class="absolute inset-y-0 left-0 flex items-center pl-3 text-slate-400">
                            <i class="fa-solid fa-search text-xs"></i>
                        </span>
                        <input type="text" id="searchTpsPublic" oninput="renderPublicTpsTable()" placeholder="Cari TPS atau Dusun..." class="w-full pl-9 pr-4 py-2 text-xs bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600">
                    </div>
                </div>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse text-xs">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 uppercase font-semibold text-[11px]">
                                <th class="p-3 rounded-l-lg">No TPS</th>
                                <th class="p-3">Lokasi / Dusun</th>
                                <th class="p-3 text-center">Status</th>
                                <th class="p-3 text-right">DPT</th>
                                <th class="p-3 text-right">Suara Sah</th>
                                <th class="p-3 text-right">Tdk Sah</th>
                                <th class="p-3 text-right">Tdk Terpakai</th>
                                <th class="p-3 text-right rounded-r-lg">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="publicTpsTableBody" class="divide-y divide-slate-100">
                            <!-- Populated dynamically -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>


        <!-- ================= VIEW 2: PANEL SAKSI / USER ================= -->
        <div id="viewWitness" class="hidden space-y-6 max-w-4xl mx-auto">
            <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200">
                <div class="flex items-center justify-between pb-4 mb-6 border-b border-slate-100">
                    <div>
                        <h2 class="font-bold text-slate-800 text-xl"><i class="fa-solid fa-pen-nib text-emerald-600 mr-2"></i>Panel Input Data Saksi TPS</h2>
                        <p class="text-xs text-slate-500 mt-0.5">Masukkan perolehan suara resmi serta surat suara tidak terpakai sesuai Formulir C.Hasil-KWK TPS.</p>
                    </div>
                    <span class="bg-blue-50 text-blue-700 text-xs px-3 py-1 rounded-full font-medium border border-blue-200">
                        <i class="fa-solid fa-user-shield"></i> Portal Saksi
                    </span>
                </div>

                <!-- Witness Form Select TPS & Credentials -->
                <form id="witnessForm" onsubmit="handleWitnessSubmit(event)" class="space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 mb-1.5">Pilih TPS Tugas Anda *</label>
                            <select id="witnessTpsSelect" onchange="loadTpsDataIntoForm(this.value)" required class="w-full px-3.5 py-2.5 text-xs bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600">
                                <option value="">-- Pilih TPS --</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 mb-1.5">Nama Saksi / Pelapor *</label>
                            <input type="text" id="witnessName" placeholder="Contoh: Ahmad Zulkarnain" required class="w-full px-3.5 py-2.5 text-xs bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600">
                        </div>
                    </div>

                    <!-- TPS Information Display -->
                    <div id="witnessTpsInfoCard" class="hidden bg-emerald-50 border border-emerald-200 rounded-xl p-4 text-xs space-y-1">
                        <p class="font-semibold text-emerald-800">Lokasi: <span id="infoLoc" class="font-normal"></span></p>
                        <p class="font-semibold text-emerald-800">Jumlah DPT: <span id="infoDpt" class="font-normal"></span> pemilih</p>
                    </div>

                    <!-- Paslon Vote Inputs -->
                    <div>
                        <h3 class="font-bold text-slate-800 text-sm mb-3">Perolehan Suara Pasangan Calon</h3>
                        <div id="witnessPaslonInputs" class="space-y-3">
                            <!-- Populated dynamically -->
                        </div>
                    </div>

                    <!-- Additional Ballot Info -->
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 pt-2">
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 mb-1.5">Suara Tidak Sah *</label>
                            <input type="number" id="witnessInvalidVotes" min="0" value="0" required class="w-full px-3.5 py-2.5 text-xs bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 mb-1.5">Suara Tidak Terpakai *</label>
                            <input type="number" id="witnessUnusedVotes" min="0" value="0" required class="w-full px-3.5 py-2.5 text-xs bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600" placeholder="Sisa surat suara">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 mb-1.5">Upload Foto C.Hasil (Simulasi)</label>
                            <input type="file" id="witnessPhoto" accept="image/*" class="w-full text-xs text-slate-500 file:mr-2 file:py-2 file:px-3 file:rounded-xl file:border-0 file:text-xs file:font-semibold file:bg-emerald-50 file:text-emerald-700 hover:file:bg-emerald-100">
                        </div>
                    </div>

                    <!-- Confirmation Checkbox -->
                    <div class="flex items-start gap-2 pt-2">
                        <input type="checkbox" id="witnessConfirm" required class="mt-0.5 rounded text-emerald-600 focus:ring-emerald-500">
                        <label for="witnessConfirm" class="text-xs text-slate-600">
                            Saya menyatakan bahwa data perolehan suara dan suara tidak terpakai di atas adalah benar sesuai dengan hasil resmi di TPS.
                        </label>
                    </div>

                    <div class="flex justify-end gap-3 pt-4 border-t border-slate-100">
                        <button type="submit" class="px-6 py-2.5 text-xs font-semibold rounded-xl bg-emerald-600 text-white hover:bg-emerald-500 transition shadow-md flex items-center gap-2">
                            <i class="fa-solid fa-paper-plane"></i> Kirim / Update Data TPS
                        </button>
                    </div>
                </form>
            </div>
        </div>


        <!-- ================= VIEW 3: PANEL ADMIN ================= -->
        <div id="viewAdmin" class="hidden space-y-6">
            <!-- Admin Top Navigation Bar -->
            <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-200 flex flex-wrap justify-between items-center gap-4">
                <div class="flex items-center space-x-2">
                    <span class="bg-amber-100 text-amber-800 p-2 rounded-xl text-sm"><i class="fa-solid fa-user-gear"></i></span>
                    <div>
                        <h3 class="font-bold text-slate-800 text-sm">Panel Administrator Desa Pelangan</h3>
                        <p class="text-[11px] text-slate-500">Kelola data paslon, TPS, verifikasi suara, dan kontrol sistem.</p>
                    </div>
                </div>
                <div class="flex items-center gap-2 flex-wrap">
                    <button onclick="switchAdminTab('dashboard')" id="adminTabBtnDashboard" class="px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-emerald-600 text-white transition flex items-center gap-1.5">
                        <i class="fa-solid fa-gauge"></i> Ringkasan Admin
                    </button>
                    <button onclick="switchAdminTab('paslon')" id="adminTabBtnPaslon" class="px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-slate-100 text-slate-700 hover:bg-slate-200 transition flex items-center gap-1.5">
                        <i class="fa-solid fa-users-rectangle"></i> Manajemen Paslon
                    </button>
                    <button onclick="switchAdminTab('tps')" id="adminTabBtnTps" class="px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-slate-100 text-slate-700 hover:bg-slate-200 transition flex items-center gap-1.5">
                        <i class="fa-solid fa-location-dot"></i> Manajemen TPS
                    </button>
                    <button onclick="switchAdminTab('settings')" id="adminTabBtnSettings" class="px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-slate-100 text-slate-700 hover:bg-slate-200 transition flex items-center gap-1.5">
                        <i class="fa-solid fa-gear"></i> Pengaturan & Data
                    </button>
                </div>
            </div>

            <!-- ADMIN SUB-TAB 1: DASHBOARD / OVERVIEW & VERIFICATION -->
            <div id="adminTabDashboard" class="space-y-6">
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200">
                    <div class="flex justify-between items-center mb-4">
                        <div>
                            <h3 class="font-bold text-slate-800 text-base">Verifikasi & Status Masuk TPS</h3>
                            <p class="text-xs text-slate-500">Daftar seluruh TPS di Desa Pelangan beserta status pelaporan suara saksi & surat suara tidak terpakai</p>
                        </div>
                        <button onclick="resetAllData()" class="px-3 py-1.5 text-xs font-semibold rounded-xl bg-rose-50 text-rose-600 hover:bg-rose-100 border border-rose-200 transition flex items-center gap-1.5">
                            <i class="fa-solid fa-rotate-right"></i> Reset Data Bawaan
                        </button>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse text-xs">
                            <thead>
                                <tr class="bg-slate-100 text-slate-700 uppercase font-semibold text-[11px]">
                                    <th class="p-3 rounded-l-lg">No TPS</th>
                                    <th class="p-3">Lokasi / Dusun</th>
                                    <th class="p-3 text-right">DPT</th>
                                    <th class="p-3 text-center">Status</th>
                                    <th class="p-3">Nama Saksi</th>
                                    <th class="p-3 text-right">Suara Sah</th>
                                    <th class="p-3 text-right">Tdk Sah</th>
                                    <th class="p-3 text-right">Tdk Terpakai</th>
                                    <th class="p-3 text-right rounded-r-lg">Aksi Admin</th>
                                </tr>
                            </thead>
                            <tbody id="adminTpsTableBody" class="divide-y divide-slate-100">
                                <!-- Populated dynamically -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- ADMIN SUB-TAB 2: MANAJEMEN PASLON -->
            <div id="adminTabPaslon" class="hidden space-y-6">
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200">
                    <div class="flex justify-between items-center mb-6">
                        <div>
                            <h3 class="font-bold text-slate-800 text-base">Manajemen Pasangan Calon Kepala Desa</h3>
                            <p class="text-xs text-slate-500">Tambah, edit, atau hapus data kandidat calon kepala desa periode 2027-2035</p>
                        </div>
                        <button onclick="openPaslonModal()" class="px-4 py-2 text-xs font-semibold rounded-xl bg-emerald-600 text-white hover:bg-emerald-500 transition shadow-sm flex items-center gap-2">
                            <i class="fa-solid fa-user-plus"></i> Tambah Paslon Baru
                        </button>
                    </div>
                    <div id="adminPaslonGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                        <!-- Populated dynamically -->
                    </div>
                </div>
            </div>

            <!-- ADMIN SUB-TAB 3: MANAJEMEN TPS -->
            <div id="adminTabTps" class="hidden space-y-6">
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200">
                    <div class="flex justify-between items-center mb-6">
                        <div>
                            <h3 class="font-bold text-slate-800 text-base">Manajemen Titik Pemungutan Suara (TPS)</h3>
                            <p class="text-xs text-slate-500">Kelola jumlah TPS, dusun, dan DPT di Desa Pelangan</p>
                        </div>
                        <button onclick="openTpsModal()" class="px-4 py-2 text-xs font-semibold rounded-xl bg-emerald-600 text-white hover:bg-emerald-500 transition shadow-sm flex items-center gap-2">
                            <i class="fa-solid fa-plus"></i> Tambah TPS Baru
                        </button>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse text-xs">
                            <thead>
                                <tr class="bg-slate-100 text-slate-700 uppercase font-semibold text-[11px]">
                                    <th class="p-3 rounded-l-lg">No TPS</th>
                                    <th class="p-3">Lokasi / Dusun</th>
                                    <th class="p-3 text-right">Jumlah DPT</th>
                                    <th class="p-3 text-center rounded-r-lg">Aksi</th>
                                </tr>
                            </thead>
                            <tbody id="adminTpsListTableBody" class="divide-y divide-slate-100">
                                <!-- Populated dynamically -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- ADMIN SUB-TAB 4: PENGATURAN & BACKUP/RESTORE -->
            <div id="adminTabSettings" class="hidden space-y-6">
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200 max-w-2xl space-y-6">
                    <div>
                        <h3 class="font-bold text-slate-800 text-base">Pengaturan Sistem & Backup Data</h3>
                        <p class="text-xs text-slate-500">Export atau import database lokal aplikasi real count</p>
                    </div>
                    <div class="p-4 bg-slate-50 border border-slate-200 rounded-xl space-y-3">
                        <h4 class="font-semibold text-xs text-slate-700">Backup & Restore Database (JSON)</h4>
                        <p class="text-xs text-slate-500">Simpan seluruh data paslon, TPS, dan perolehan suara ke file JSON atau muat ulang data backup.</p>
                        <div class="flex flex-wrap gap-3 pt-2">
                            <button onclick="exportDatabase()" class="px-4 py-2 text-xs font-semibold rounded-xl bg-blue-600 text-white hover:bg-blue-500 transition flex items-center gap-2">
                                <i class="fa-solid fa-download"></i> Export Database JSON
                            </button>
                            <label class="px-4 py-2 text-xs font-semibold rounded-xl bg-slate-200 text-slate-700 hover:bg-slate-300 transition flex items-center gap-2 cursor-pointer">
                                <i class="fa-solid fa-upload"></i> Import Database JSON
                                <input type="file" id="importFile" accept=".json" onchange="importDatabase(event)" class="hidden">
                            </label>
                        </div>
                    </div>

                    <div class="p-4 bg-rose-50 border border-rose-200 rounded-xl space-y-3">
                <h4 class="font-semibold text-xs text-rose-800">Zona Bahaya</h4>
                <p class="text-xs text-rose-600">Menghapus seluruh data perolehan suara atau mengembalikan pengaturan ke awal.</p>
                <button onclick="resetAllData()" class="px-4 py-2 text-xs font-semibold rounded-xl bg-rose-600 text-white hover:bg-rose-500 transition flex items-center gap-2">
                    <i class="fa-solid fa-triangle-exclamation"></i> Reset Seluruh Data & Kembali ke Default
                </button>
            </div>
        </div>
    </div>
    </main>

    <!-- ================= MODALS ================= -->

    <!-- Deployment Guide Modal -->
    <div id="modalDeployGuide" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden">
        <div class="bg-white rounded-2xl shadow-xl border border-slate-200 w-full max-w-xl p-6 m-4 space-y-4 max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center pb-3 border-b border-slate-100">
                <h3 class="font-bold text-slate-800 text-base"><i class="fa-solid fa-globe text-blue-600 mr-2"></i>Panduan Mempublikasikan Aplikasi Secara Online</h3>
                <button onclick="closeModal('modalDeployGuide')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div class="space-y-4 text-xs text-slate-700 leading-relaxed">
                <p>Aplikasi ini berbasis <strong>Single-File HTML</strong> (HTML, CSS, dan JavaScript digabung menjadi satu file mandiri). Hal ini sangat memudahkan Anda untuk meng-host aplikasi ini secara gratis agar bisa diakses oleh banyak orang secara online (panitia, saksi, dan warga).</p>
                
                <div class="p-3 bg-blue-50 border border-blue-200 rounded-xl space-y-2">
                    <h4 class="font-bold text-blue-900"><i class="fa-brands fa-github mr-1"></i> Cara 1: GitHub Pages (Gratis & Sangat Mudah)</h4>
                    <ol class="list-decimal list-inside space-y-1 text-slate-600">
                        <li>Buat akun di <a href="https://github.com" target="_blank" class="text-blue-600 underline">GitHub.com</a>.</li>
                        <li>Buat Repository baru (misal: <code>pilkades-pelangan</code>) dengan status <strong>Public</strong>.</li>
                        <li>Upload file HTML ini dan beri nama <code>index.html</code>.</li>
                        <li>Masuk ke menu <strong>Settings</strong> > <strong>Pages</strong>.</li>
                        <li>Pada bagian Branch, pilih <code>main</code> (atau <code>master</code>) / <code>root</code>, lalu klik <strong>Save</strong>.</li>
                        <li>Dalam 1-2 menit, link website Anda akan aktif dan siap dibagikan ke panitia & saksi!</li>
                    </ol>
                </div>

                <div class="p-3 bg-emerald-50 border border-emerald-200 rounded-xl space-y-2">
                    <h4 class="font-bold text-emerald-900"><i class="fa-solid fa-bolt mr-1"></i> Cara 2: Netlify Drop atau Vercel (Instan Tanpa Ribet)</h4>
                    <ol class="list-decimal list-inside space-y-1 text-slate-600">
                        <li>Buka situs <a href="https://drop.netlify.com" target="_blank" class="text-emerald-600 underline">Netlify Drop</a>.</li>
                        <li>Drag & Drop (seret) file HTML aplikasi ini ke kotak yang disediakan di web Netlify.</li>
                        <li>Netlify akan langsung memberikan URL online instan yang bisa langsung diakses oleh siapa saja!</li>
                    </ol>
                </div>
            </div>
            <div class="pt-2 flex justify-end">
                <button onclick="closeModal('modalDeployGuide')" class="px-4 py-2 text-xs font-semibold rounded-xl bg-slate-100 text-slate-600 hover:bg-slate-200">Tutup Panduan</button>
            </div>
        </div>
    </div>

    <!-- Admin Login Modal -->
    <div id="modalAdminLogin" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden">
        <div class="bg-white rounded-2xl shadow-xl border border-slate-200 w-full max-w-md p-6 m-4 space-y-4">
            <div class="flex justify-between items-center pb-3 border-b border-slate-100">
                <h3 class="font-bold text-slate-800 text-base"><i class="fa-solid fa-lock text-amber-600 mr-2"></i>Login Admin Pilkades</h3>
                <button onclick="closeModal('modalAdminLogin')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <form onsubmit="handleAdminLogin(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Username Admin</label>
                    <input type="text" id="adminUser" placeholder="admin" value="admin" required class="w-full px-3.5 py-2 text-xs bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-amber-600">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Password</label>
                    <input type="password" id="adminPass" placeholder="pelangan2027" value="pelangan2027" required class="w-full px-3.5 py-2 text-xs bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-amber-600">
                </div>
                <div class="pt-2 flex justify-end gap-2">
                    <button type="button" onclick="closeModal('modalAdminLogin')" class="px-4 py-2 text-xs font-semibold rounded-xl bg-slate-100 text-slate-600 hover:bg-slate-200">Batal</button>
                    <button type="submit" class="px-4 py-2 text-xs font-semibold rounded-xl bg-amber-600 text-white hover:bg-amber-500 shadow-sm">Masuk Admin</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Paslon Add/Edit Modal -->
    <div id="modalPaslon" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden">
        <div class="bg-white rounded-2xl shadow-xl border border-slate-200 w-full max-w-lg p-6 m-4 space-y-4">
            <div class="flex justify-between items-center pb-3 border-b border-slate-100">
                <h3 id="modalPaslonTitle" class="font-bold text-slate-800 text-base">Tambah / Edit Paslon</h3>
                <button onclick="closeModal('modalPaslon')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <form id="paslonForm" onsubmit="savePaslon(event)" class="space-y-4 text-xs">
                <input type="hidden" id="editPaslonId">
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Nomor Urut *</label>
                        <input type="number" id="paslonNo" min="1" required class="w-full px-3.5 py-2 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600">
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Warna Badge / Grafik *</label>
                        <input type="color" id="paslonColor" value="#059669" class="w-full h-9 px-2 py-1 bg-slate-50 border border-slate-200 rounded-xl cursor-pointer">
                    </div>
                </div>
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Nama Calon Kepala Desa *</label>
                    <input type="text" id="paslonName" placeholder="Contoh: H. Lalu M. Saufi, S.Pd." required class="w-full px-3.5 py-2 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600">
                </div>
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Visi & Misi Singkat</label>
                    <textarea id="paslonVision" rows="3" placeholder="Visi misi atau latar belakang..." class="w-full px-3.5 py-2 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600"></textarea>
                </div>
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">URL Foto / Gambar Kandidat</label>
                    <input type="url" id="paslonPhoto" placeholder="https://example.com/foto.jpg (Kosongkan jika pakai default)" class="w-full px-3.5 py-2 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600">
                </div>
                <div class="pt-2 flex justify-end gap-2">
                    <button type="button" onclick="closeModal('modalPaslon')" class="px-4 py-2 font-semibold rounded-xl bg-slate-100 text-slate-600 hover:bg-slate-200">Batal</button>
                    <button type="submit" class="px-4 py-2 font-semibold rounded-xl bg-emerald-600 text-white hover:bg-emerald-500 shadow-sm">Simpan Paslon</button>
                </div>
            </form>
        </div>
    </div>

    <!-- TPS Add/Edit Modal -->
    <div id="modalTps" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden">
        <div class="bg-white rounded-2xl shadow-xl border border-slate-200 w-full max-w-md p-6 m-4 space-y-4">
            <div class="flex justify-between items-center pb-3 border-b border-slate-100">
                <h3 id="modalTpsTitle" class="font-bold text-slate-800 text-base">Tambah / Edit TPS</h3>
                <button onclick="closeModal('modalTps')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <form id="tpsForm" onsubmit="saveTps(event)" class="space-y-4 text-xs">
                <input type="hidden" id="editTpsId">
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Nomor TPS *</label>
                    <input type="number" id="tpsNo" min="1" required class="w-full px-3.5 py-2 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600">
                </div>
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Lokasi / Dusun *</label>
                    <input type="text" id="tpsLocation" placeholder="Contoh: Dusun Pelangan Utara / Kantor Desa" required class="w-full px-3.5 py-2 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600">
                </div>
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Jumlah Pemilih DPT *</label>
                    <input type="number" id="tpsDpt" min="1" value="400" required class="w-full px-3.5 py-2 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-emerald-600">
                </div>
                <div class="pt-2 flex justify-end gap-2">
                    <button type="button" onclick="closeModal('modalTps')" class="px-4 py-2 font-semibold rounded-xl bg-slate-100 text-slate-600 hover:bg-slate-200">Batal</button>
                    <button type="submit" class="px-4 py-2 font-semibold rounded-xl bg-emerald-600 text-white hover:bg-emerald-500 shadow-sm">Simpan TPS</button>
                </div>
            </form>
        </div>
    </div>

    <!-- TPS Detail / Evidence Preview Modal -->
    <div id="modalDetail" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden">
        <div class="bg-white rounded-2xl shadow-xl border border-slate-200 w-full max-w-lg p-6 m-4 space-y-4 max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center pb-3 border-b border-slate-100">
                <h3 id="modalDetailTitle" class="font-bold text-slate-800 text-base">Detail Laporan TPS</h3>
                <button onclick="closeModal('modalDetail')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div id="modalDetailContent" class="space-y-4 text-xs">
                <!-- Populated dynamically -->
            </div>
            <div class="pt-2 flex justify-end">
                <button onclick="closeModal('modalDetail')" class="px-4 py-2 text-xs font-semibold rounded-xl bg-slate-100 text-slate-600 hover:bg-slate-200">Tutup</button>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="bg-white border-t border-slate-200 py-6 mt-12 text-center text-xs text-slate-500">
        <div class="max-w-7xl mx-auto px-4 space-y-2">
            <p class="font-medium text-slate-700">Aplikasi Real Count Pemilihan Kepala Desa (Pilkades) Desa Pelangan Periode 2027 - 2035</p>
            <p class="text-[11px] text-slate-400">Panitia Pemilihan Kepala Desa Pelangan, Kecamatan Sekotong, Kabupaten Lombok Barat, Nusa Tenggara Barat.</p>
            <div class="pt-3 border-t border-slate-100 flex items-center justify-center gap-1.5 text-slate-600 font-medium">
                <span class="inline-block w-1.5 h-1.5 rounded-full bg-emerald-600 animate-pulse"></span>
                <span>Created By <strong class="text-slate-800 tracking-wide">Gifran Afandi</strong></span>
            </div>
        </div>
    </footer>

    <!-- JavaScript Application Logic -->
    <script>
        // Full Screen Toggle Function
        function toggleFullScreen() {
            const icon = document.getElementById('fullScreenIcon');
            if (!document.fullscreenElement) {
                document.documentElement.requestFullscreen().catch(err => {
                    alert(`Error attempting to enable full-screen mode: ${err.message} (${err.name})`);
                });
                if(icon) icon.className = "fa-solid fa-compress text-sm";
            } else {
                if (document.exitFullscreen) {
                    document.exitFullscreen();
                }
                if(icon) icon.className = "fa-solid fa-expand text-sm";
            }
        }

        function openDeployGuide() {
            document.getElementById('modalDeployGuide').classList.remove('hidden');
        }

        // Default Initial Data
        const DEFAULT_PASLON = [
            { id: 1, no: 1, name: "H. Lalu M. Saufi, S.Pd.", vision: "Mewujudkan Desa Pelangan yang Mandiri, Religius, dan Berbudaya.", color: "#059669", photo: "https://placehold.co/150x150/059669/ffffff?text=Paslon+1" },
            { id: 2, no: 2, name: "Muh. Zainuddin, S.Sos.", vision: "Transparansi Anggaran Desa dan Peningkatan Infrastruktur Ekonomi Pertanian.", color: "#2563eb", photo: "https://placehold.co/150x150/2563eb/ffffff?text=Paslon+2" },
            { id: 3, no: 3, name: "Hj. Siti Aminah, Amd.Keb.", vision: "Pelayanan Kesehatan Prima, Pemberdayaan UMKM, dan Pemuda Desa.", color: "#d97706", photo: "https://placehold.co/150x150/d97706/ffffff?text=Paslon+3" }
        ];

        const DEFAULT_TPS = [
            { id: 1, no: 1, location: "Dusun Pelangan Daye", dpt: 420, status: "pending", witness: "", votes: {}, invalidVotes: 0, unusedVotes: 20, photo: "" },
            { id: 2, no: 2, location: "Dusun Pelangan Lauk", dpt: 390, status: "pending", witness: "", votes: {}, invalidVotes: 0, unusedVotes: 15, photo: "" },
            { id: 3, no: 3, location: "Dusun Belongas", dpt: 450, status: "pending", witness: "", votes: {}, invalidVotes: 0, unusedVotes: 25, photo: "" },
            { id: 4, no: 4, location: "Dusun Teluk Sepi", dpt: 380, status: "pending", witness: "", votes: {}, invalidVotes: 0, unusedVotes: 10, photo: "" },
            { id: 5, no: 5, location: "Dusun Batu Glodok", dpt: 410, status: "pending", witness: "", votes: {}, invalidVotes: 0, unusedVotes: 18, photo: "" }
        ];

        // State variables
        let paslonList = [];
        let tpsList = [];
        let currentRole = 'public'; // public, witness, admin
        let voteChartInstance = null;

        // Initialize App on load
        window.onload = function() {
            loadFromLocalStorage();
            initChart();
            renderAll();
        };

        function loadFromLocalStorage() {
            const savedPaslon = localStorage.getItem('pelangan_paslon');
            const savedTps = localStorage.getItem('pelangan_tps');
            
            paslonList = savedPaslon ? JSON.parse(savedPaslon) : DEFAULT_PASLON;
            tpsList = savedTps ? JSON.parse(savedTps) : DEFAULT_TPS;
        }

        function saveToLocalStorage() {
            localStorage.setItem('pelangan_paslon', JSON.stringify(paslonList));
            localStorage.setItem('pelangan_tps', JSON.stringify(tpsList));
        }

        function showAlert(title, message, type = 'success') {
            const alertBox = document.getElementById('alertBox');
            const alertTitle = document.getElementById('alertTitle');
            const alertMessage = document.getElementById('alertMessage');
            const alertIcon = document.getElementById('alertIcon');

            alertTitle.textContent = title;
            alertMessage.textContent = message;

            alertBox.className = "mb-6 p-4 rounded-xl shadow-md border flex items-start gap-3 transition-all duration-300 ";
            if(type === 'success') {
                alertBox.classList.add('bg-emerald-50', 'border-emerald-200', 'text-emerald-800');
                alertIcon.innerHTML = '<i class="fa-solid fa-circle-check text-emerald-600"></i>';
            } else if(type === 'error') {
                alertBox.classList.add('bg-rose-50', 'border-rose-200', 'text-rose-800');
                alertIcon.innerHTML = '<i class="fa-solid fa-triangle-exclamation text-rose-600"></i>';
            } else {
                alertBox.classList.add('bg-blue-50', 'border-blue-200', 'text-blue-800');
                alertIcon.innerHTML = '<i class="fa-solid fa-circle-info text-blue-600"></i>';
            }

            alertBox.classList.remove('hidden');
            setTimeout(() => { hideAlert(); }, 5000);
        }

        function hideAlert() {
            document.getElementById('alertBox').classList.add('hidden');
        }

        // Navigation / Role Switcher
        function switchRole(role) {
            currentRole = role;
            document.getElementById('viewPublic').classList.add('hidden');
            document.getElementById('viewWitness').classList.add('hidden');
            document.getElementById('viewAdmin').classList.add('hidden');

            document.getElementById('btnRolePublic').className = "px-3.5 py-1.5 text-xs font-medium rounded-lg bg-emerald-900 text-emerald-200 border border-emerald-700 hover:bg-emerald-700 transition flex items-center gap-1.5 shadow-sm";
            document.getElementById('btnRoleWitness').className = "px-3.5 py-1.5 text-xs font-medium rounded-lg bg-emerald-700 text-white hover:bg-emerald-600 transition flex items-center gap-1.5 shadow-sm";
            document.getElementById('btnRoleAdmin').className = "px-3.5 py-1.5 text-xs font-medium rounded-lg bg-amber-600 text-white hover:bg-amber-500 transition flex items-center gap-1.5 shadow-sm";

            if(role === 'public') {
                document.getElementById('viewPublic').classList.remove('hidden');
                document.getElementById('btnRolePublic').className = "px-3.5 py-1.5 text-xs font-medium rounded-lg bg-white text-emerald-900 font-semibold shadow-sm";
                renderPublicDashboard();
            } else if(role === 'witness') {
                document.getElementById('viewWitness').classList.remove('hidden');
                document.getElementById('btnRoleWitness').className = "px-3.5 py-1.5 text-xs font-medium rounded-lg bg-white text-emerald-800 font-semibold shadow-sm";
                initWitnessForm();
            } else if(role === 'admin') {
                document.getElementById('viewAdmin').classList.remove('hidden');
                document.getElementById('btnRoleAdmin').className = "px-3.5 py-1.5 text-xs font-medium rounded-lg bg-white text-amber-900 font-semibold shadow-sm";
                renderAdminDashboard();
            }
        }

        function openAdminLogin() {
            document.getElementById('modalAdminLogin').classList.remove('hidden');
        }

        function handleAdminLogin(e) {
            e.preventDefault();
            const u = document.getElementById('adminUser').value;
            const p = document.getElementById('adminPass').value;
            if(u === 'admin' && p === 'pelangan2027') {
                closeModal('modalAdminLogin');
                switchRole('admin');
                showAlert('Login Berhasil', 'Selamat datang di Panel Administrator Pilkades Pelangan.', 'success');
            } else {
                showAlert('Login Gagal', 'Username atau password salah! (Gunakan admin / pelangan2027)', 'error');
            }
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.add('hidden');
        }

        // Render All Data
        function renderAll() {
            renderPublicDashboard();
            if(currentRole === 'witness') initWitnessForm();
            if(currentRole === 'admin') renderAdminDashboard();
        }

        // ================= PUBLIC DASHBOARD LOGIC =================
        function renderPublicDashboard() {
            let totalDpt = tpsList.reduce((acc, t) => acc + Number(t.dpt), 0);
            let submittedTps = tpsList.filter(t => t.status === 'verified' || t.status === 'submitted');
            let totalSuaraSah = 0;
            let totalSuaraTdkSah = tpsList.reduce((acc, t) => acc + (Number(t.invalidVotes) || 0), 0);
            let totalSuaraTdkTerpakai = tpsList.reduce((acc, t) => acc + (Number(t.unusedVotes) || 0), 0);

            let paslonTotals = {};
            paslonList.forEach(p => paslonTotals[p.id] = 0);

            submittedTps.forEach(t => {
                if(t.votes) {
                    for(let pId in t.votes) {
                        let v = Number(t.votes[pId]) || 0;
                        if(paslonTotals[pId] !== undefined) {
                            paslonTotals[pId] += v;
                        }
                        totalSuaraSah += v;
                    }
                }
            });

            let totalSuaraMasuk = totalSuaraSah + totalSuaraTdkSah;
            let turnoutPct = totalDpt > 0 ? Math.round((totalSuaraMasuk / totalDpt) * 100) : 0;
            let progressPct = tpsList.length > 0 ? Math.round((submittedTps.length / tpsList.length) * 100) : 0;

            document.getElementById('statProgress').textContent = `${submittedTps.length} / ${tpsList.length} TPS`;
            document.getElementById('statProgressPct').innerHTML = `<i class="fa-solid fa-chart-line"></i> ${progressPct}% Selesai`;
            document.getElementById('statSuaraSah').textContent = totalSuaraSah.toLocaleString('id-ID');
            document.getElementById('statSahPct').textContent = totalSuaraMasuk > 0 ? Math.round((totalSuaraSah/totalSuaraMasuk)*100) + '% dari suara masuk' : '0%';
            document.getElementById('statSuaraTdkSah').textContent = totalSuaraTdkSah.toLocaleString('id-ID');
            document.getElementById('statTdkSahPct').textContent = totalSuaraMasuk > 0 ? Math.round((totalSuaraTdkSah/totalSuaraMasuk)*100) + '% dari suara masuk' : '0%';
            document.getElementById('statSuaraTdkTerpakai').textContent = totalSuaraTdkTerpakai.toLocaleString('id-ID');
            document.getElementById('statTurnout').textContent = `${turnoutPct}%`;
            document.getElementById('statTotalDpt').textContent = `Dari total ${totalDpt.toLocaleString('id-ID')} DPT`;

            // Render Leaderboard & Paslon Cards
            let sortedPaslon = [...paslonList].sort((a,b) => paslonTotals[b.id] - paslonTotals[a.id]);
            
            let lbHtml = '';
            sortedPaslon.forEach((p, idx) => {
                let votes = paslonTotals[p.id] || 0;
                let pct = totalSuaraSah > 0 ? ((votes / totalSuaraSah) * 100).toFixed(1) : 0;
                lbHtml += `
                    <div class="flex items-center justify-between p-3 rounded-xl bg-slate-50 border border-slate-100">
                        <div class="flex items-center gap-3">
                            <span class="w-6 h-6 rounded-full bg-emerald-800 text-white flex items-center justify-center text-xs font-bold">${idx+1}</span>
                            <div>
                                <h4 class="font-bold text-xs text-slate-800">No.${p.no} - ${p.name}</h4>
                                <p class="text-[11px] text-slate-500">${votes.toLocaleString('id-ID')} suara (${pct}%)</p>
                            </div>
                        </div>
                        <div class="w-16 bg-slate-200 rounded-full h-2 overflow-hidden">
                            <div class="bg-emerald-600 h-full rounded-full" style="width: ${pct}%"></div>
                        </div>
                    </div>
                `;
            });
            document.getElementById('leaderboardList').innerHTML = lbHtml;

            // Public Paslon Grid
            let gridHtml = '';
            paslonList.forEach(p => {
                let votes = paslonTotals[p.id] || 0;
                let pct = totalSuaraSah > 0 ? ((votes / totalSuaraSah) * 100).toFixed(1) : 0;
                gridHtml += `
                    <div class="bg-slate-50 rounded-2xl p-5 border border-slate-200 flex flex-col justify-between">
                        <div>
                            <div class="flex items-center gap-4 mb-4">
                                <img src="${p.photo}" onerror="this.src='https://placehold.co/150x150/059669/ffffff?text=Paslon'" class="w-16 h-16 rounded-2xl object-cover shadow-sm border border-slate-300" alt="Paslon">
                                <div>
                                    <span class="inline-block px-2 py-0.5 rounded-md text-[10px] font-bold text-white mb-1" style="background-color: ${p.color}">Nomor Urut ${p.no}</span>
                                    <h4 class="font-bold text-slate-800 text-sm leading-snug">${p.name}</h4>
                                </div>
                            </div>
                            <p class="text-xs text-slate-600 italic mb-4">"${p.vision || 'Tanpa keterangan visi'}"</p>
                        </div>
                        <div class="pt-4 border-t border-slate-200">
                            <div class="flex justify-between items-center mb-1 text-xs">
                                <span class="text-slate-500 font-medium">Perolehan Suara:</span>
                                <span class="font-bold text-slate-800">${votes.toLocaleString('id-ID')} (${pct}%)</span>
                            </div>
                            <div class="w-full bg-slate-200 rounded-full h-2 overflow-hidden">
                                <div class="h-full rounded-full transition-all duration-500" style="width: ${pct}%; background-color: ${p.color}"></div>
                            </div>
                        </div>
                    </div>
                `;
            });
            document.getElementById('publicPaslonGrid').innerHTML = gridHtml;

            renderPublicTpsTable();
            updateChart(paslonTotals);
        }

        function renderPublicTpsTable() {
            const query = (document.getElementById('searchTpsPublic')?.value || '').toLowerCase();
            let tbody = document.getElementById('publicTpsTableBody');
            let html = '';

            tpsList.filter(t => t.location.toLowerCase().includes(query) || String(t.no).includes(query)).forEach(t => {
                let totalTpsVotes = 0;
                if(t.votes) {
                    for(let id in t.votes) totalTpsVotes += Number(t.votes[id]) || 0;
                }
                let statusBadge = t.status === 'verified' ? '<span class="px-2 py-0.5 rounded-full text-[10px] bg-emerald-100 text-emerald-800 font-semibold"><i class="fa-solid fa-check-circle"></i> Terverifikasi</span>' :
                                  t.status === 'submitted' ? '<span class="px-2 py-0.5 rounded-full text-[10px] bg-blue-100 text-blue-800 font-semibold"><i class="fa-solid fa-clock"></i> Masuk (Draft)</span>' :
                                  '<span class="px-2 py-0.5 rounded-full text-[10px] bg-slate-100 text-slate-600 font-semibold">Belum Masuk</span>';

                html += `
                    <tr class="hover:bg-slate-50 transition">
                        <td class="p-3 font-semibold text-slate-800">TPS ${t.no}</td>
                        <td class="p-3 text-slate-600">${t.location}</td>
                        <td class="p-3 text-center">${statusBadge}</td>
                        <td class="p-3 text-right font-medium">${t.dpt}</td>
                        <td class="p-3 text-right font-bold text-emerald-700">${totalTpsVotes.toLocaleString('id-ID')}</td>
                        <td class="p-3 text-right font-medium text-rose-600">${t.invalidVotes || 0}</td>
                        <td class="p-3 text-right font-medium text-amber-600">${t.unusedVotes || 0}</td>
                        <td class="p-3 text-right">
                            <button onclick="viewTpsDetail(${t.id})" class="px-2.5 py-1 text-[11px] font-semibold bg-slate-100 text-slate-700 rounded-lg hover:bg-slate-200 transition">Detail</button>
                        </td>
                    </tr>
                `;
            });
            tbody.innerHTML = html;
        }

        // Chart.js Setup
        function initChart() {
            const ctx = document.getElementById('voteChart').getContext('2d');
            voteChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: paslonList.map(p => `Paslon ${p.no}: ${p.name.split(',')[0]}`),
                    datasets: [{
                        label: 'Perolehan Suara',
                        data: paslonList.map(p => 0),
                        backgroundColor: paslonList.map(p => p.color),
                        borderRadius: 8,
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false }
                    },
                    scales: {
                        y: { beginAtZero: true, grid: { color: '#f1f5f9' } },
                        x: { grid: { display: false } }
                    }
                }
            });
        }

        function updateChart(paslonTotals) {
            if(!voteChartInstance) return;
            voteChartInstance.data.labels = paslonList.map(p => `No.${p.no} (${p.name.split(',')[0]})`);
            voteChartInstance.data.datasets[0].data = paslonList.map(p => paslonTotals[p.id] || 0);
            voteChartInstance.data.datasets[0].backgroundColor = paslonList.map(p => p.color);
            voteChartInstance.update();
        }

        // ================= WITNESS / USER PANEL LOGIC =================
        function initWitnessForm() {
            const select = document.getElementById('witnessTpsSelect');
            let html = '<option value="">-- Pilih TPS Anda --</option>';
            tpsList.forEach(t => {
                html += `<option value="${t.id}">TPS ${t.no} - ${t.location} (${t.dpt} DPT)</option>`;
            });
            select.innerHTML = html;
            document.getElementById('witnessTpsInfoCard').classList.add('hidden');
            document.getElementById('witnessPaslonInputs').innerHTML = '<p class="text-xs text-slate-400 italic">Silakan pilih TPS terlebih dahulu.</p>';
        }

        function loadTpsDataIntoForm(tpsId) {
            if(!tpsId) {
                document.getElementById('witnessTpsInfoCard').classList.add('hidden');
                document.getElementById('witnessPaslonInputs').innerHTML = '<p class="text-xs text-slate-400 italic">Silakan pilih TPS terlebih dahulu.</p>';
                return;
            }

            const tps = tpsList.find(t => t.id == tpsId);
            if(!tps) return;

            document.getElementById('infoLoc').textContent = tps.location;
            document.getElementById('infoDpt').textContent = tps.dpt;
            document.getElementById('witnessTpsInfoCard').classList.remove('hidden');
            document.getElementById('witnessName').value = tps.witness || '';
            document.getElementById('witnessInvalidVotes').value = tps.invalidVotes || 0;
            document.getElementById('witnessUnusedVotes').value = tps.unusedVotes || 0;

            let paslonHtml = '';
            paslonList.forEach(p => {
                let existingVote = (tps.votes && tps.votes[p.id] !== undefined) ? tps.votes[p.id] : 0;
                paslonHtml += `
                    <div class="flex items-center justify-between p-3 rounded-xl bg-slate-50 border border-slate-200 gap-4">
                        <div class="flex items-center gap-3">
                            <span class="w-7 h-7 rounded-lg text-white font-bold flex items-center justify-center text-xs" style="background-color: ${p.color}">${p.no}</span>
                            <div>
                                <h4 class="font-bold text-slate-800 text-xs">${p.name}</h4>
                                <p class="text-[10px] text-slate-500">Pasangan Calon No. Urut ${p.no}</p>
                            </div>
                        </div>
                        <div class="w-32">
                            <input type="number" min="0" name="vote_paslon_${p.id}" value="${existingVote}" required class="w-full px-3 py-1.5 text-xs bg-white border border-slate-300 rounded-lg focus:outline-none focus:border-emerald-600 font-semibold text-right">
                        </div>
                    </div>
                `;
            });
            document.getElementById('witnessPaslonInputs').innerHTML = paslonHtml;
        }

        function handleWitnessSubmit(e) {
            e.preventDefault();
            const tpsId = document.getElementById('witnessTpsSelect').value;
            const witnessName = document.getElementById('witnessName').value;
            const invalidVotes = Number(document.getElementById('witnessInvalidVotes').value) || 0;
            const unusedVotes = Number(document.getElementById('witnessUnusedVotes').value) || 0;

            let tps = tpsList.find(t => t.id == tpsId);
            if(!tps) return;

            let votes = {};
            paslonList.forEach(p => {
                let inputVal = document.querySelector(`[name="vote_paslon_${p.id}"]`).value;
                votes[p.id] = Number(inputVal) || 0;
            });

            tps.witness = witnessName;
            tps.invalidVotes = invalidVotes;
            tps.unusedVotes = unusedVotes;
            tps.votes = votes;
            tps.status = 'submitted';

            saveToLocalStorage();
            renderAll();
            showAlert('Berhasil Mengirim Data', `Perolehan suara & surat suara tidak terpakai untuk TPS ${tps.no} berhasil disimpan!`, 'success');
        }

        // ================= ADMIN PANEL LOGIC =================
        function switchAdminTab(tab) {
            document.getElementById('adminTabDashboard').classList.add('hidden');
            document.getElementById('adminTabPaslon').classList.add('hidden');
            document.getElementById('adminTabTps').classList.add('hidden');
            document.getElementById('adminTabSettings').classList.add('hidden');

            document.getElementById('adminTabBtnDashboard').className = "px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-slate-100 text-slate-700 hover:bg-slate-200 transition flex items-center gap-1.5";
            document.getElementById('adminTabBtnPaslon').className = "px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-slate-100 text-slate-700 hover:bg-slate-200 transition flex items-center gap-1.5";
            document.getElementById('adminTabBtnTps').className = "px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-slate-100 text-slate-700 hover:bg-slate-200 transition flex items-center gap-1.5";
            document.getElementById('adminTabBtnSettings').className = "px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-slate-100 text-slate-700 hover:bg-slate-200 transition flex items-center gap-1.5";

            if(tab === 'dashboard') {
                document.getElementById('adminTabDashboard').classList.remove('hidden');
                document.getElementById('adminTabBtnDashboard').className = "px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-emerald-600 text-white transition flex items-center gap-1.5";
            } else if(tab === 'paslon') {
                document.getElementById('adminTabPaslon').classList.remove('hidden');
                document.getElementById('adminTabBtnPaslon').className = "px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-emerald-600 text-white transition flex items-center gap-1.5";
                renderAdminPaslon();
            } else if(tab === 'tps') {
                document.getElementById('adminTabTps').classList.remove('hidden');
                document.getElementById('adminTabBtnTps').className = "px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-emerald-600 text-white transition flex items-center gap-1.5";
                renderAdminTpsList();
            } else if(tab === 'settings') {
                document.getElementById('adminTabSettings').classList.remove('hidden');
                document.getElementById('adminTabBtnSettings').className = "px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-emerald-600 text-white transition flex items-center gap-1.5";
            }
        }

        function renderAdminDashboard() {
            let tbody = document.getElementById('adminTpsTableBody');
            let html = '';

            tpsList.forEach(t => {
                let totalTpsVotes = 0;
                if(t.votes) {
                    for(let id in t.votes) totalTpsVotes += Number(t.votes[id]) || 0;
                }
                let statusBadge = t.status === 'verified' ? '<span class="px-2 py-0.5 rounded-full text-[10px] bg-emerald-100 text-emerald-800 font-semibold"><i class="fa-solid fa-check-circle"></i> Terverifikasi</span>' :
                                  t.status === 'submitted' ? '<span class="px-2 py-0.5 rounded-full text-[10px] bg-blue-100 text-blue-800 font-semibold"><i class="fa-solid fa-clock"></i> Masuk (Draft)</span>' :
                                  '<span class="px-2 py-0.5 rounded-full text-[10px] bg-slate-100 text-slate-600 font-semibold">Belum Masuk</span>';

                let actionBtn = t.status === 'submitted' ? 
                    `<button onclick="verifyTps(${t.id})" class="px-2.5 py-1 text-[11px] font-semibold bg-emerald-600 text-white rounded-lg hover:bg-emerald-500 transition mr-1">Verifikasi</button>` :
                    t.status === 'verified' ? `<button onclick="unverifyTps(${t.id})" class="px-2.5 py-1 text-[11px] font-semibold bg-amber-500 text-white rounded-lg hover:bg-amber-400 transition mr-1">Batalkan</button>` : '';

                html += `
                    <tr class="hover:bg-slate-50 transition">
                        <td class="p-3 font-semibold text-slate-800">TPS ${t.no}</td>
                        <td class="p-3 text-slate-600">${t.location}</td>
                        <td class="p-3 text-right font-medium">${t.dpt}</td>
                        <td class="p-3 text-center">${statusBadge}</td>
                        <td class="p-3 text-slate-600">${t.witness || '-'}</td>
                        <td class="p-3 text-right font-bold text-emerald-700">${totalTpsVotes.toLocaleString('id-ID')}</td>
                        <td class="p-3 text-right font-medium text-rose-600">${t.invalidVotes || 0}</td>
                        <td class="p-3 text-right font-medium text-amber-600">${t.unusedVotes || 0}</td>
                        <td class="p-3 text-right">
                            ${actionBtn}
                            <button onclick="viewTpsDetail(${t.id})" class="px-2.5 py-1 text-[11px] font-semibold bg-slate-100 text-slate-700 rounded-lg hover:bg-slate-200 transition">Detail</button>
                        </td>
                    </tr>
                `;
            });
            tbody.innerHTML = html;
        }

        function verifyTps(id) {
            let t = tpsList.find(x => x.id === id);
            if(t) {
                t.status = 'verified';
                saveToLocalStorage();
                renderAll();
                showAlert('Berhasil', `TPS ${t.no} berhasil diverifikasi oleh Admin.`, 'success');
            }
        }

        function unverifyTps(id) {
            let t = tpsList.find(x => x.id === id);
            if(t) {
                t.status = 'submitted';
                saveToLocalStorage();
                renderAll();
                showAlert('Informasi', `Verifikasi TPS ${t.no} dibatalkan.`, 'info');
            }
        }

        // --- Paslon Admin Management ---
        function renderAdminPaslon() {
            let grid = document.getElementById('adminPaslonGrid');
            let html = '';
            paslonList.forEach(p => {
                html += `
                    <div class="bg-slate-50 rounded-2xl p-5 border border-slate-200 flex flex-col justify-between">
                        <div>
                            <div class="flex items-center gap-4 mb-3">
                                <img src="${p.photo}" onerror="this.src='https://placehold.co/150x150/059669/ffffff?text=Paslon'" class="w-14 h-14 rounded-2xl object-cover shadow-sm border border-slate-300">
                                <div>
                                    <span class="inline-block px-2 py-0.5 rounded-md text-[10px] font-bold text-white mb-1" style="background-color: ${p.color}">No. Urut ${p.no}</span>
                                    <h4 class="font-bold text-slate-800 text-sm">${p.name}</h4>
                                </div>
                            </div>
                            <p class="text-xs text-slate-600 italic mb-4">"${p.vision || '-'}"</p>
                        </div>
                        <div class="flex items-center justify-end gap-2 pt-3 border-t border-slate-200">
                            <button onclick="editPaslon(${p.id})" class="px-3 py-1.5 text-xs font-semibold bg-amber-50 text-amber-700 rounded-xl hover:bg-amber-100 border border-amber-200 transition"><i class="fa-solid fa-pen"></i> Edit</button>
                            <button onclick="deletePaslon(${p.id})" class="px-3 py-1.5 text-xs font-semibold bg-rose-50 text-rose-700 rounded-xl hover:bg-rose-100 border border-rose-200 transition"><i class="fa-solid fa-trash"></i> Hapus</button>
                        </div>
                    </div>
                `;
            });
            grid.innerHTML = html;
        }

        function openPaslonModal(paslon = null) {
            document.getElementById('paslonForm').reset();
            if(paslon) {
                document.getElementById('modalPaslonTitle').textContent = 'Edit Data Pasangan Calon';
                document.getElementById('editPaslonId').value = paslon.id;
                document.getElementById('paslonNo').value = paslon.no;
                document.getElementById('paslonName').value = paslon.name;
                document.getElementById('paslonVision').value = paslon.vision;
                document.getElementById('paslonColor').value = paslon.color;
                document.getElementById('paslonPhoto').value = paslon.photo;
            } else {
                document.getElementById('modalPaslonTitle').textContent = 'Tambah Pasangan Calon Baru';
                document.getElementById('editPaslonId').value = '';
                document.getElementById('paslonColor').value = '#059669';
                document.getElementById('paslonNo').value = paslonList.length + 1;
            }
            document.getElementById('modalPaslon').classList.remove('hidden');
        }

        function editPaslon(id) {
            let p = paslonList.find(x => x.id === id);
            if(p) openPaslonModal(p);
        }

        function savePaslon(e) {
            e.preventDefault();
            let id = document.getElementById('editPaslonId').value;
            let no = Number(document.getElementById('paslonNo').value);
            let name = document.getElementById('paslonName').value;
            let vision = document.getElementById('paslonVision').value;
            let color = document.getElementById('paslonColor').value;
            let photo = document.getElementById('paslonPhoto').value || `https://placehold.co/150x150/059669/ffffff?text=Paslon+${no}`;

            if(id) {
                let p = paslonList.find(x => x.id == id);
                if(p) {
                    p.no = no; p.name = name; p.vision = vision; p.color = color; p.photo = photo;
                }
            } else {
                let newId = paslonList.length > 0 ? Math.max(...paslonList.map(x => x.id)) + 1 : 1;
                paslonList.push({ id: newId, no, name, vision, color, photo });
            }

            saveToLocalStorage();
            renderAll();
            closeModal('modalPaslon');
            showAlert('Berhasil', 'Data pasangan calon berhasil disimpan.', 'success');
        }

        function deletePaslon(id) {
            if(confirm('Apakah Anda yakin ingin menghapus paslon ini?')) {
                paslonList = paslonList.filter(x => x.id !== id);
                saveToLocalStorage();
                renderAll();
                showAlert('Berhasil', 'Paslon berhasil dihapus.', 'success');
            }
        }

        // --- TPS Admin Management ---
        function renderAdminTpsList() {
            let tbody = document.getElementById('adminTpsListTableBody');
            let html = '';
            tpsList.forEach(t => {
                html += `
                    <tr class="hover:bg-slate-50 transition">
                        <td class="p-3 font-semibold text-slate-800">TPS ${t.no}</td>
                        <td class="p-3 text-slate-600">${t.location}</td>
                        <td class="p-3 text-right font-medium">${t.dpt}</td>
                        <td class="p-3 text-center">
                            <button onclick="editTps(${t.id})" class="px-2.5 py-1 text-[11px] font-semibold bg-amber-50 text-amber-700 rounded-lg hover:bg-amber-100 border border-amber-200 transition mr-1"><i class="fa-solid fa-pen"></i> Edit</button>
                            <button onclick="deleteTps(${t.id})" class="px-2.5 py-1 text-[11px] font-semibold bg-rose-50 text-rose-700 rounded-lg hover:bg-rose-100 border border-rose-200 transition"><i class="fa-solid fa-trash"></i> Hapus</button>
                        </td>
                    </tr>
                `;
            });
            tbody.innerHTML = html;
        }

        function openTpsModal(tps = null) {
            document.getElementById('tpsForm').reset();
            if(tps) {
                document.getElementById('modalTpsTitle').textContent = 'Edit TPS';
                document.getElementById('editTpsId').value = tps.id;
                document.getElementById('tpsNo').value = tps.no;
                document.getElementById('tpsLocation').value = tps.location;
                document.getElementById('tpsDpt').value = tps.dpt;
            } else {
                document.getElementById('modalTpsTitle').textContent = 'Tambah TPS Baru';
                document.getElementById('editTpsId').value = '';
                document.getElementById('tpsNo').value = tpsList.length + 1;
                document.getElementById('tpsDpt').value = 400;
            }
            document.getElementById('modalTps').classList.remove('hidden');
        }

        function editTps(id) {
            let t = tpsList.find(x => x.id === id);
            if(t) openTpsModal(t);
        }

        function saveTps(e) {
            e.preventDefault();
            let id = document.getElementById('editTpsId').value;
            let no = Number(document.getElementById('tpsNo').value);
            let location = document.getElementById('tpsLocation').value;
            let dpt = Number(document.getElementById('tpsDpt').value);

            if(id) {
                let t = tpsList.find(x => x.id == id);
                if(t) {
                    t.no = no; t.location = location; t.dpt = dpt;
                }
            } else {
                let newId = tpsList.length > 0 ? Math.max(...tpsList.map(x => x.id)) + 1 : 1;
                tpsList.push({ id: newId, no, location, dpt, status: 'pending', witness: '', votes: {}, invalidVotes: 0, photo: '' });
            }

            saveToLocalStorage();
            renderAll();
            closeModal('modalTps');
            showAlert('Berhasil', 'Data TPS berhasil disimpan.', 'success');
        }

        function deleteTps(id) {
            if(confirm('Apakah Anda yakin ingin menghapus TPS ini?')) {
                tpsList = tpsList.filter(x => x.id !== id);
                saveToLocalStorage();
                renderAll();
                showAlert('Berhasil', 'TPS berhasil dihapus.', 'success');
            }
        }

        // --- Detailed Modal View for TPS ---
        function viewTpsDetail(id) {
            let t = tpsList.find(x => x.id === id);
            if(!t) return;

            document.getElementById('modalDetailTitle').textContent = `Detail Perolehan Suara - TPS ${t.no} (${t.location})`;
            
            let totalSah = 0;
            if(t.votes) {
                for(let id in t.votes) totalSah += Number(t.votes[id]) || 0;
            }

            let paslonDetailHtml = '';
            paslonList.forEach(p => {
                let v = (t.votes && t.votes[p.id]) ? t.votes[p.id] : 0;
                paslonDetailHtml += `
                    <div class="flex justify-between items-center p-2 rounded-lg bg-slate-50 border border-slate-100">
                        <span class="font-medium text-slate-700">No.${p.no} - ${p.name}</span>
                        <span class="font-bold text-slate-800">${v.toLocaleString('id-ID')} suara</span>
                    </div>
                `;
            });

            let html = `
                <div class="space-y-3">
                    <div class="grid grid-cols-2 gap-2 p-3 bg-emerald-50 rounded-xl border border-emerald-200">
                        <div>
                            <p class="text-[11px] text-emerald-700 font-semibold">Status Pelaporan</p>
                            <p class="font-bold text-emerald-900">${t.status === 'verified' ? 'Terverifikasi' : t.status === 'submitted' ? 'Masuk (Draft)' : 'Belum Masuk'}</p>
                        </div>
                        <div>
                            <p class="text-[11px] text-emerald-700 font-semibold">Nama Saksi</p>
                            <p class="font-bold text-emerald-900">${t.witness || '-'}</p>
                        </div>
                        <div>
                            <p class="text-[11px] text-emerald-700 font-semibold">Jumlah DPT</p>
                            <p class="font-bold text-emerald-900">${t.dpt} pemilih</p>
                        </div>
                        <div>
                            <p class="text-[11px] text-emerald-700 font-semibold">Suara Tidak Sah</p>
                            <p class="font-bold text-rose-700">${t.invalidVotes || 0}</p>
                        </div>
                        <div class="col-span-2">
                            <p class="text-[11px] text-emerald-700 font-semibold">Suara Tidak Terpakai (Sisa Surat Suara)</p>
                            <p class="font-bold text-amber-700">${t.unusedVotes || 0}</p>
                        </div>
                    </div>
                    <div>
                        <h4 class="font-semibold text-slate-800 mb-2">Perolehan Suara Calon:</h4>
                        <div class="space-y-1.5">
                            ${paslonDetailHtml}
                        </div>
                    </div>
                    <div class="pt-2 border-t border-slate-100 flex justify-between font-bold text-slate-800 text-xs">
                        <span>Total Suara Sah:</span>
                        <span>${totalSah.toLocaleString('id-ID')} Suara</span>
                    </div>
                </div>
            `;
            document.getElementById('modalDetailContent').innerHTML = html;
            document.getElementById('modalDetail').classList.remove('hidden');
        }

        // --- Backup & Restore Database ---
        function exportDatabase() {
            const data = { paslon: paslonList, tps: tpsList };
            const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `backup_pilkades_pelangan_2027_${new Date().toISOString().slice(0,10)}.json`;
            a.click();
            showAlert('Backup Berhasil', 'Database berhasil di-export ke file JSON.', 'success');
        }

        function importDatabase(e) {
            const file = e.target.files[0];
            if(!file) return;
            const reader = new FileReader();
            reader.onload = function(evt) {
                try {
                    const data = JSON.parse(evt.target.result);
                    if(data.paslon && data.tps) {
                        paslonList = data.paslon;
                        tpsList = data.tps;
                        saveToLocalStorage();
                        renderAll();
                        showAlert('Import Berhasil', 'Database berhasil dipulihkan dari file JSON.', 'success');
                    } else {
                        showAlert('Format Salah', 'File JSON tidak sesuai dengan struktur database Pilkades Pelangan.', 'error');
                    }
                } catch(err) {
                    showAlert('Gagal Membaca File', 'Terjadi kesalahan saat menguraikan file JSON.', 'error');
                }
            };
            reader.readAsText(file);
        }

        function resetAllData() {
            if(confirm('PERINGATAN: Seluruh data suara dan perubahan akan dikembalikan ke data awal default. Lanjutkan?')) {
                localStorage.removeItem('pelangan_paslon');
                localStorage.removeItem('pelangan_tps');
                paslonList = JSON.parse(JSON.stringify(DEFAULT_PASLON));
                tpsList = JSON.parse(JSON.stringify(DEFAULT_TPS));
                renderAll();
                showAlert('Reset Berhasil', 'Aplikasi telah dikembalikan ke data default awal.', 'info');
            }
        }
    </script>
</body>
</html>
