
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CN Bigo OPK Reservation</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&family=Cinzel:wght@400;600;700;900&display=swap');
        * { font-family: 'Poppins', sans-serif; }
        .cn-black-yellow { 
            font-family: 'Cinzel', serif; 
            background: linear-gradient(45deg, #000000 0%, #FFD700 50%, #000000 100%); 
            -webkit-background-clip: text; 
            -webkit-text-fill-color: transparent; 
            background-clip: text;
            text-shadow: 0 0 20px rgba(255, 215, 0, 0.8);
            font-weight: 900;
        }
        .gradient-bg { background: linear-gradient(135deg, #1e1b4b 0%, #2d1b69 30%, #4158d0 60%, #c850c0 100%); }
        .glass { backdrop-filter: blur(25px); background: rgba(255, 255, 255, 0.15); border: 1px solid rgba(255, 255, 255, 0.25); }
        .neon-glow { box-shadow: 0 0 30px rgba(255, 215, 0, 0.6); }
        html { scroll-behavior: smooth; }
        body { overflow-x: hidden; }
    </style>
</head>
<body class="bg-gradient-to-br from-purple-900 via-indigo-900 to-pink-900 min-h-screen pb-20">
    <!-- Header -->
    <header class="gradient-bg shadow-2xl py-6 sticky top-0 z-50">
        <div class="max-w-6xl mx-auto px-6">
            <div class="flex justify-between items-center">
                <div class="flex items-center space-x-4">
                    <div class="w-16 h-16 bg-gradient-to-br from-black to-yellow-500 rounded-2xl flex items-center justify-center shadow-2xl border-4 border-yellow-400 neon-glow">
                        <span class="cn-black-yellow text-3xl tracking-widest">CN</span>
                    </div>
                    <div>
                        <h1 class="text-3xl font-black text-white">Bigo OPK</h1>
                        <p class="text-lg text-yellow-300 font-semibold">Reservation System</p>
                    </div>
                </div>
                <button id="adminBtn" class="glass text-white px-6 py-3 rounded-2xl text-lg font-bold hover:bg-white/30 transition-all duration-300 neon-glow">
                    <i class="fas fa-crown mr-2 text-yellow-400"></i>ADMIN PANEL
                </button>
            </div>
        </div>
    </header>

    <div class="max-w-6xl mx-auto px-6 py-12 space-y-20">
        <!-- Reservation Form -->
        <div id="reservationSection" class="glass rounded-3xl p-12 shadow-4xl mx-auto max-w-5xl">
            <div class="text-center mb-12">
                <div class="w-24 h-24 bg-gradient-to-br from-black to-yellow-500 rounded-3xl mx-auto mb-6 flex items-center justify-center shadow-2xl neon-glow">
                    <i class="fas fa-calendar-check text-3xl text-white"></i>
                </div>
                <h2 class="text-5xl font-black bg-gradient-to-r from-white to-yellow-300 bg-clip-text text-transparent mb-4">
                    Book Your Slot
                </h2>
                <p class="text-2xl text-white/95">15-min slots 8:00 PM - 10:15 PM</p>
            </div>

            <form id="reservationForm" class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <div><label class="block text-white font-bold text-lg mb-3">👤 Bigo Name</label><input type="text" id="bigoName" required class="w-full p-4 text-lg rounded-2xl bg-white/20 border border-white/40 text-white placeholder-white/70 focus:ring-4 focus:ring-yellow-400/50"></div>
                <div><label class="block text-white font-bold text-lg mb-3">🆔 Bigo ID</label><input type="text" id="bigoId" required class="w-full p-4 text-lg rounded-2xl bg-white/20 border border-white/40 text-white placeholder-white/70 focus:ring-4 focus:ring-yellow-400/50"></div>
                <div><label class="block text-white font-bold text-lg mb-3">⭐ Level</label><input type="number" id="level" min="1" max="100" required class="w-full p-4 text-lg rounded-2xl bg-white/20 border border-white/40 text-white placeholder-white/70 focus:ring-4 focus:ring-yellow-400/50"></div>
                <div><label class="block text-white font-bold text-lg mb-3">🏢 Agency</label><input type="text" id="agency" required class="w-full p-4 text-lg rounded-2xl bg-white/20 border border-white/40 text-white placeholder-white/70 focus:ring-4 focus:ring-yellow-400/50"></div>
                <div class="lg:col-span-2"><label class="block text-white font-bold text-lg mb-3">📧 Gmail</label><input type="email" id="gmail" required class="w-full p-4 text-lg rounded-2xl bg-white/20 border border-white/40 text-white placeholder-white/70 focus:ring-4 focus:ring-yellow-400/50"></div>
                <div class="lg:col-span-2"><label class="block text-white font-bold text-lg mb-3">📅 Date</label><input type="date" id="date" required class="w-full p-4 text-lg rounded-2xl bg-white/20 border border-white/40 text-white focus:ring-4 focus:ring-yellow-400/50"></div>
                <div class="lg:col-span-2"><label class="block text-white font-bold text-lg mb-3">⏰ Time Slot</label><select id="timeSlot" required class="w-full p-4 text-lg rounded-2xl bg-white/20 border border-white/40 text-white focus:ring-4 focus:ring-yellow-400/50"><option value="">Choose slot (8PM-10PM)</option></select></div>
                <div class="lg:col-span-2"><button type="submit" class="w-full bg-gradient-to-r from-black to-yellow-500 text-gray-900 font-black py-5 px-8 rounded-3xl text-2xl hover:from-gray-800 hover:to-yellow-600 shadow-2xl hover:shadow-yellow-500/50 transition-all duration-300">🔒 RESERVE SLOT</button></div>
            </form>
            <div id="message" class="mt-8 p-6 rounded-2xl hidden text-xl font-bold"></div>
        </div>

        <!-- ADMIN PANEL - ALWAYS VISIBLE -->
        <div id="adminPanel" class="glass rounded-3xl p-12 shadow-4xl mx-auto max-w-6xl">
            <div class="flex justify-between items-center mb-12 pb-8 border-b border-white/30">
                <h2 class="text-4xl font-black bg-gradient-to-r from-yellow-400 to-orange-500 bg-clip-text text-transparent flex items-center">
                    <i class="fas fa-crown mr-4 text-4xl text-yellow-400"></i>CN Admin Dashboard
                </h2>
                <button id="closeAdmin" class="text-white text-2xl p-3 rounded-2xl hover:bg-white/20 transition-all">
                    <i class="fas fa-times"></i>
                </button>
            </div>

            <!-- QUICK ACCESS PIN -->
            <div id="adminPinSection" class="text-center mb-12 p-8 bg-white/10 rounded-3xl border-2 border-yellow-400">
                <div class="w-20 h-20 bg-gradient-to-br from-black to-yellow-500 rounded-2xl mx-auto mb-6 flex items-center justify-center shadow-2xl">
                    <i class="fas fa-key text-2xl text-white"></i>
                </div>
                <h3 class="text-2xl font-bold text-white mb-4">Enter PIN to Unlock Full Admin</h3>
                <input type="password" id="adminPin" maxlength="4" placeholder="6969" class="w-28 h-16 text-3xl font-black text-center rounded-2xl bg-white/30 border-4 border-yellow-400 mx-auto focus:outline-none focus:border-yellow-500 text-black">
                <p class="text-xl text-yellow-400 mt-4 font-bold blink">PIN: <span class="cn-black-yellow text-2xl">6969</span></p>
            </div>

            <!-- FULL DASHBOARD - IMMEDIATELY VISIBLE EVEN WITHOUT PIN -->
            <div id="scheduleSummary">
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12">
                    <div class="glass p-8 rounded-3xl">
                        <h3 class="text-2xl font-black text-white mb-6 flex items-center cn-black-yellow">
                            <i class="fas fa-calendar mr-3"></i>Today's Schedule
                        </h3>
                        <div id="todaySchedule" class="space-y-4 max-h-64 overflow-y-auto"></div>
                    </div>
                    <div class="glass p-8 rounded-3xl">
                        <h3 class="text-2xl font-black text-white mb-6 flex items-center cn-black-yellow">
                            <i class="fas fa-chart-bar mr-3"></i>Stats
                        </h3>
                        <canvas id="statsChart" class="h-48 w-full"></canvas>
                        <div class="grid grid-cols-2 gap-4 mt-6">
                            <div class="text-center p-4 bg-white/10 rounded-2xl">
                                <div class="text-3xl font-black cn-black-yellow" id="totalBookings">0</div>
                                <div class="text-white text-sm">Total Bookings</div>
                            </div>
                            <div class="text-center p-4 bg-white/10 rounded-2xl">
                                <div class="text-3xl font-black text-green-400" id="availableSlots">19</div>
                                <div class="text-white text-sm">Available Today</div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="glass p-8 rounded-3xl overflow-x-auto">
                    <h3 class="text-2xl font-black text-white mb-6 flex items-center cn-black-yellow">
                        <i class="fas fa-list mr-3"></i>All Reservations
                    </h3>
                    <table class="w-full text-white min-w-[800px]">
                        <thead>
                            <tr class="border-b-4 border-yellow-400/50">
                                <th class="p-4 text-left font-black">Date/Time</th>
                                <th class="p-4 text-left font-black">Name</th>
                                <th class="p-4 text-left font-black">ID/LVL</th>
                                <th class="p-4 text-left font-black">Agency</th>
                                <th class="p-4 text-left font-black">Email</th>
                                <th class="p-4 text-left font-black">Action</th>
                            </tr>
                        </thead>
                        <tbody id="allReservations"></tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <script>
        const timeSlots = ['20:00','20:15','20:30','20:45','21:00','21:15','21:30','21:45','22:00','22:15'];
        let reservations = JSON.parse(localStorage.getItem('bigoReservations')) || [];
        let isAdmin = localStorage.getItem('isAdmin') === 'true';

        // Initialize everything
        init();

        function init() {
            setMinDate();
            updateTimeSlots();
            updateAdminDashboard(); // Always show dashboard
            if (isAdmin) unlockAdmin();
            document.getElementById('adminBtn').addEventListener('click', toggleAdmin);
            document.getElementById('closeAdmin').addEventListener('click', toggleAdmin);
            document.getElementById('adminPin').addEventListener('input', checkPin);
            document.getElementById('reservationForm').addEventListener('submit', handleBooking);
            document.getElementById('date').addEventListener('change', updateTimeSlots);
        }

        function setMinDate() {
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('date').min = today;
            document.getElementById('date').value = today;
        }

        function updateTimeSlots() {
            const date = document.getElementById('date').value;
            const select = document.getElementById('timeSlot');
            select.innerHTML = '<option value="">Choose slot (8PM-10PM)</option>';
            if (!date) return;

            const booked = reservations.filter(r => r.date === date).map(r => r.time);
            timeSlots.forEach(slot => {
                const option = new Option();
                const timeStr = formatTime(slot);
                option.value = slot;
                option.text = booked.includes(slot) ? `${timeStr} ❌ TAKEN` : timeStr;
                if (booked.includes(slot)) option.disabled = true;
                select.add(option);
            });
        }

        function formatTime(slot) {
            const [h, m] = slot.split(':');
            const time = new Date();
            time.setHours(+h, +m);
            return time.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit', hour12: true}).toUpperCase();
        }

        function handleBooking(e) {
            e.preventDefault();
            const data = {
                bigoName: document.getElementById('bigoName').value,
                bigoId: document.getElementById('bigoId').value,
                level: document.getElementById('level').value,
                agency: document.getElementById('agency').value,
                gmail: document.getElementById('gmail').value,
                date: document.getElementById('date').value,
                time: document.getElementById('timeSlot').value,
                timestamp: Date.now().toString()
            };

            if (reservations.find(r => r.date === data.date && r.time === data.time)) {
                showMessage('❌ Slot already taken!', 'error');
                return;
            }

            reservations.push(data);
            localStorage.setItem('bigoReservations', JSON.stringify(reservations));
            showMessage('✅ Slot booked successfully!', 'success');
            e.target.reset();
            setMinDate();
            updateTimeSlots();
            updateAdminDashboard();
        }

        function showMessage(text, type) {
            const msg = document.getElementById('message');
            msg.textContent = text;
            msg.className = `mt-8 p-6 rounded-2xl text-xl font-bold ${type === 'success' ? 'bg-green-500/30 border-4 border-green-500 text-green-100' : 'bg-red-500/30 border-4 border-red-500 text-red-100'}`;
            msg.classList.remove('hidden');
            setTimeout(() => msg.classList.add('hidden'), 4000);
        }

        // ADMIN FUNCTIONS - ALWAYS WORKING
        function toggleAdmin() {
            const resSection = document.getElementById('reservationSection');
            const adminSection = document.getElementById('adminPanel');
            if (resSection.style.display !== 'none') {
                resSection.style.display = 'none';
                adminSection.scrollIntoView({behavior: 'smooth'});
            } else {
                resSection.style.display = 'block';
                adminSection.scrollIntoView({behavior: 'smooth'});
            }
        }

        function checkPin(e) {
            if (e.target.value === '6969') {
                unlockAdmin();
            }
        }

        function unlockAdmin() {
            isAdmin = true;
            localStorage.setItem('isAdmin', 'true');
            document.getElementById('adminPinSection').style.display = 'none';
            enableCancelButtons();
        }

        function enableCancelButtons() {
            document.querySelectorAll('.cancel-btn')?.forEach(btn => {
                btn.style.display = 'inline-block';
            });
        }

        function updateAdminDashboard() {
            updateTodaySchedule();
            updateStats();
            updateAllReservations();
        }

        function updateTodaySchedule() {
            const today = new Date().toISOString().split('T')[0];
            const todayRes = reservations.filter(r => r.date === today);
            document.getElementById('todaySchedule').innerHTML = todayRes.length ? 
                todayRes.map(r => `
                    <div class="glass p-4 rounded-2xl hover:bg-white/20 transition-all">
                        <div class="flex justify-between items-center">
                            <div>
                                <div class="font-black text-xl cn-black-yellow">${formatTime(r.time)}</div>
                                <div class="font-bold">${r.bigoName} (LVL ${r.level})</div>
                                <div class="text-sm text-white/70">${r.agency}</div>
                            </div>
                            ${isAdmin ? `<button class="cancel-btn bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-xl text-sm font-bold transition-all ml-4" onclick="cancelReservation('${r.timestamp}')">❌ Cancel</button>` : ''}
                        </div>
                    </div>
                `).join('') : 
                '<div class="text-center py-8 text-white/60"><i class="fas fa-calendar-times text-4xl mb-4"></i><div class="text-xl">No bookings today</div></div>';
        }

        function updateStats() {
            const today = new Date().toISOString().split('T')[0];
            const todayBookings = reservations.filter(r => r.date === today).length;
            document.getElementById('totalBookings').textContent = reservations.length;
            document.getElementById('availableSlots').textContent = 10 - todayBookings;

            const ctx = document.getElementById('statsChart')?.getContext('2d');
            if (ctx && window.statsChart) window.statsChart.destroy();
            if (ctx) {
                window.statsChart = new Chart(ctx, {
                    type: 'doughnut',
                    data: {
                        datasets: [{
                            data: [todayBookings, 10 - todayBookings],
                            backgroundColor: ['#ef4444', '#10b981'],
                            borderWidth: 0
                        }]
                    },
                    options: {
                        responsive: true,
                        cutout: '65%',
                        plugins: { legend: { display: false }}
                    }
                });
            }
        }

        function updateAllReservations() {
            const tbody = document.getElementById('allReservations');
            if (!reservations.length) {
                tbody.innerHTML = '<tr><td colspan="6" class="p-8 text-center text-white/60">No reservations</td></tr>';
                return;
            }
            tbody.innerHTML = reservations.map(r => `
                <tr class="border-b border-white/20 hover:bg-white/10">
                    <td class="p-4 font-bold cn-black-yellow">${r.date} ${formatTime(r.time)}</td>
                    <td class="p-4 font-bold">${r.bigoName}</td>
                    <td class="p-4">${r.bigoId}<br><span class="cn-black-yellow">LVL ${r.level}</span></td>
                    <td class="p-4">${r.agency}</td>
                    <td class="p-4">${r.gmail}</td>
                    <td class="p-4">${isAdmin ? `<button class="cancel-btn bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-xl font-bold transition-all" onclick="cancelReservation('${r.timestamp}')">Delete</button>` : '🔒'}</td>
                </tr>
            `).join('');
            enableCancelButtons();
        }

        window.cancelReservation = function(timestamp) {
            if (confirm('Cancel reservation?')) {
                reservations = reservations.filter(r => r.timestamp !== timestamp);
                localStorage.setItem('bigoReservations', JSON.stringify(reservations));
                updateAdminDashboard();
                updateTimeSlots();
                showMessage('✅ Cancelled!', 'success');
            }
        }
    </script>
</body>
</html>
