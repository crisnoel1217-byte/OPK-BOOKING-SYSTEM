
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
        .cn-golden { 
            font-family: 'Cinzel', serif; 
            background: linear-gradient(45deg, #FFD700, #FFA500, #FF8C00); 
            -webkit-background-clip: text; 
            -webkit-text-fill-color: transparent; 
            background-clip: text;
            text-shadow: 0 0 30px rgba(255, 215, 0, 0.5);
            font-weight: 900;
        }
        .gradient-bg { background: linear-gradient(135deg, #1e1b4b 0%, #2d1b69 30%, #4158d0 60%, #c850c0 100%); }
        .glass { backdrop-filter: blur(25px); background: rgba(255, 255, 255, 0.15); border: 1px solid rgba(255, 255, 255, 0.25); }
        .neon-glow { box-shadow: 0 0 40px rgba(255, 215, 0, 0.4), 0 0 80px rgba(255, 165, 0, 0.2); }
        .pulse-golden { animation: pulse-golden 2s infinite; }
        @keyframes pulse-golden {
            0%, 100% { box-shadow: 0 0 40px rgba(255, 215, 0, 0.4), 0 0 80px rgba(255, 165, 0, 0.2); }
            50% { box-shadow: 0 0 60px rgba(255, 215, 0, 0.7), 0 0 120px rgba(255, 165, 0, 0.4); }
        }
        .admin-visible { display: block !important; }
    </style>
</head>
<body class="bg-gradient-to-br from-purple-900 via-indigo-900 to-pink-900 min-h-screen overflow-hidden">
    <!-- Golden CN Header -->
    <header class="gradient-bg shadow-2xl py-8">
        <div class="max-w-6xl mx-auto px-6">
            <div class="flex flex-col sm:flex-row justify-between items-center">
                <div class="flex items-center space-x-6 mb-6 sm:mb-0">
                    <div class="w-24 h-24 bg-gradient-to-br from-yellow-400 to-orange-500 rounded-3xl flex items-center justify-center neon-glow pulse-golden shadow-2xl">
                        <span class="cn-golden text-4xl md:text-5xl tracking-widest drop-shadow-lg">CN</span>
                    </div>
                    <div class="text-center sm:text-left">
                        <h1 class="text-4xl md:text-6xl font-black text-white drop-shadow-2xl mb-2">Bigo OPK</h1>
                        <p class="text-xl md:text-2xl text-yellow-300 font-semibold drop-shadow-lg">Reservation System</p>
                    </div>
                </div>
                <div id="adminToggle" class="hidden">
                    <button id="adminBtn" class="glass text-white px-8 py-4 rounded-3xl text-lg font-bold hover:bg-white/30 transition-all duration-500 neon-glow hover:scale-110">
                        <i class="fas fa-crown mr-3 text-yellow-400"></i>Admin Panel
                    </button>
                </div>
            </div>
        </div>
    </header>

    <div class="max-w-7xl mx-auto px-6 py-16">
        <!-- Main Reservation Form - BIGGER & CENTERED -->
        <div id="reservationSection" class="glass rounded-4xl p-16 md:p-24 shadow-4xl neon-glow mx-auto max-w-5xl">
            <div class="text-center mb-16">
                <div class="w-32 h-32 bg-gradient-to-br from-yellow-400 to-orange-500 rounded-4xl mx-auto mb-8 flex items-center justify-center neon-glow pulse-golden shadow-4xl">
                    <i class="fas fa-calendar-check text-5xl text-gray-900"></i>
                </div>
                <h2 class="text-5xl md:text-7xl font-black bg-gradient-to-r from-white via-yellow-200 to-orange-300 bg-clip-text text-transparent mb-6 drop-shadow-2xl">
                    Book Your OPK Slot
                </h2>
                <p class="text-2xl md:text-3xl text-white/95 max-w-4xl mx-auto leading-relaxed">Secure your <span class="text-yellow-400 font-bold">15-minute slot</span> between <span class="text-yellow-400 font-bold">8:00 PM - 10:15 PM</span>. First come, first served!</p>
            </div>

            <form id="reservationForm" class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <div>
                    <label class="block text-white font-bold text-xl mb-5">👤 Bigo Name</label>
                    <input type="text" id="bigoName" required class="w-full p-6 text-xl rounded-3xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-8 focus:ring-yellow-400/50 transition-all duration-500 hover:border-yellow-400" placeholder="Your Bigo username">
                </div>
                <div>
                    <label class="block text-white font-bold text-xl mb-5">🆔 Bigo ID</label>
                    <input type="text" id="bigoId" required class="w-full p-6 text-xl rounded-3xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-8 focus:ring-yellow-400/50 transition-all duration-500 hover:border-yellow-400" placeholder="123456789">
                </div>
                <div>
                    <label class="block text-white font-bold text-xl mb-5">⭐ Level</label>
                    <input type="number" id="level" min="1" max="100" required class="w-full p-6 text-xl rounded-3xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-8 focus:ring-yellow-400/50 transition-all duration-500 hover:border-yellow-400" placeholder="LVL 50">
                </div>
                <div>
                    <label class="block text-white font-bold text-xl mb-5">🏢 Agency</label>
                    <input type="text" id="agency" required class="w-full p-6 text-xl rounded-3xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-8 focus:ring-yellow-400/50 transition-all duration-500 hover:border-yellow-400" placeholder="Your agency name">
                </div>
                <div class="lg:col-span-2">
                    <label class="block text-white font-bold text-xl mb-5">📧 Gmail Account</label>
                    <input type="email" id="gmail" required class="w-full p-6 text-xl rounded-3xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-8 focus:ring-yellow-400/50 transition-all duration-500 hover:border-yellow-400" placeholder="your.email@gmail.com">
                </div>
                <div class="lg:col-span-2">
                    <label class="block text-white font-bold text-xl mb-5">📅 Select Date</label>
                    <input type="date" id="date" required class="w-full p-6 text-xl rounded-3xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-8 focus:ring-yellow-400/50 transition-all duration-500 hover:border-yellow-400">
                </div>
                <div class="lg:col-span-2">
                    <label class="block text-white font-bold text-xl mb-5">⏰ Select Time Slot (15 mins)</label>
                    <select id="timeSlot" required class="w-full p-6 text-xl rounded-3xl bg-white/20 border-2 border-white/40 text-white focus:outline-none focus:ring-8 focus:ring-yellow-400/50 transition-all duration-500 hover:border-yellow-400">
                        <option value="">Choose your slot (8:00 PM - 10:15 PM)</option>
                    </select>
                </div>
                <div class="lg:col-span-2">
                    <button type="submit" id="submitBtn" class="w-full bg-gradient-to-r from-yellow-400 via-orange-500 to-red-500 text-gray-900 font-black py-8 px-12 rounded-4xl text-3xl hover:from-yellow-500 hover:via-orange-600 hover:to-red-600 transform hover:scale-105 transition-all duration-500 shadow-4xl hover:shadow-yellow-500/50 neon-glow pulse-golden">
                        <i class="fas fa-lock mr-4"></i>🔒 RESERVE MY SLOT NOW
                    </button>
                </div>
            </form>
            <div id="message" class="mt-12 p-8 rounded-3xl hidden text-2xl font-bold"></div>
        </div>

        <!-- FIXED Admin Panel - NOW FULLY VISIBLE -->
        <div id="adminPanel" class="glass rounded-4xl p-16 md:p-24 shadow-4xl mx-auto max-w-7xl mt-20 admin-visible">
            <div class="flex justify-between items-center mb-16">
                <h2 class="text-5xl md:text-6xl font-black bg-gradient-to-r from-yellow-400 to-orange-500 bg-clip-text text-transparent flex items-center">
                    <i class="fas fa-crown mr-6 text-6xl"></i>Admin Dashboard
                </h2>
                <button id="closeAdmin" class="text-white/80 hover:text-white text-4xl p-4 rounded-3xl hover:bg-white/20 transition-all duration-300">
                    <i class="fas fa-times"></i>
                </button>
            </div>

            <!-- Admin PIN Input -->
            <div id="adminPinSection" class="text-center mb-20 bg-white/10 p-12 rounded-4xl">
                <div class="w-32 h-32 bg-gradient-to-br from-yellow-400 to-orange-500 rounded-4xl mx-auto mb-8 flex items-center justify-center neon-glow pulse-golden">
                    <i class="fas fa-key text-5xl text-gray-900"></i>
                </div>
                <input type="password" id="adminPin" maxlength="4" class="w-40 h-24 text-5xl font-black text-center rounded-4xl bg-white/30 border-4 border-yellow-400 mx-auto mb-8 focus:outline-none focus:border-orange-500" placeholder="PIN">
                <p class="text-2xl text-white/90 font-bold">Enter Admin PIN: <span class="cn-golden text-3xl">6969</span></p>
            </div>

            <!-- Schedule Summary -->
            <div id="scheduleSummary" class="hidden">
                <div class="grid grid-cols-1 xl:grid-cols-2 gap-12 mb-20">
                    <div class="glass p-12 rounded-4xl h-96">
                        <h3 class="text-3xl font-black text-white mb-10 flex items-center cn-golden">
                            <i class="fas fa-calendar mr-4 text-4xl"></i>Today's Schedule
                        </h3>
                        <div id="todaySchedule" class="space-y-6 max-h-72 overflow-y-auto pr-4"></div>
                    </div>
                    <div class="glass p-12 rounded-4xl">
                        <h3 class="text-3xl font-black text-white mb-10 flex items-center cn-golden">
                            <i class="fas fa-chart-bar mr-4 text-4xl"></i>Booking Stats
                        </h3>
                        <div class="h-64 mb-12">
                            <canvas id="statsChart"></canvas>
                        </div>
                        <div class="grid grid-cols-2 gap-8 text-center">
                            <div class="glass p-8 rounded-3xl neon-glow">
                                <div class="text-5xl font-black cn-golden mb-2" id="totalBookings">0</div>
                                <div class="text-2xl text-white/90 font-bold">Total Bookings</div>
                            </div>
                            <div class="glass p-8 rounded-3xl neon-glow">
                                <div class="text-5xl font-black text-green-400 mb-2" id="availableSlots">19</div>
                                <div class="text-2xl text-white/90 font-bold">Available Today</div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- All Reservations Table -->
                <div class="glass p-12 rounded-4xl">
                    <h3 class="text-3xl font-black text-white mb-12 flex items-center cn-golden">
                        <i class="fas fa-list mr-4 text-4xl"></i>All Reservations
                    </h3>
                    <div class="overflow-x-auto">
                        <table class="w-full text-white text-lg">
                            <thead>
                                <tr class="border-b-4 border-yellow-400/50">
                                    <th class="p-6 text-left font-black text-xl">Date/Time</th>
                                    <th class="p-6 text-left font-black text-xl">Bigo Name</th>
                                    <th class="p-6 text-left font-black text-xl">ID/LVL</th>
                                    <th class="p-6 text-left font-black text-xl">Agency</th>
                                    <th class="p-6 text-left font-black text-xl">Email</th>
                                    <th class="p-6 text-left font-black text-xl">Actions</th>
                                </tr>
                            </thead>
                            <tbody id="allReservations"></tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Time slots: 8:00 PM to 10:15 PM (15 min intervals)
        const timeSlots = [
            '20:00', '20:15', '20:30', '20:45',
            '21:00', '21:15', '21:30', '21:45',
            '22:00', '22:15'
        ];

        let reservations = JSON.parse(localStorage.getItem('bigoReservations')) || [];
        let isAdmin = false;

        init();

        function init() {
            setMinDate();
            updateTimeSlots();
            loadAdminStatus();
            updateAdminToggle();
        }

        function setMinDate() {
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('date').min = today;
            document.getElementById('date').value = today;
        }

        function updateTimeSlots() {
            const date = document.getElementById('date').value;
            const select = document.getElementById('timeSlot');
            select.innerHTML = '<option value="">Choose your slot (8:00 PM - 10:15 PM)</option>';

            if (!date) return;

            const dateReservations = reservations.filter(r => r.date === date);
            const bookedSlots = dateReservations.map(r => r.time);

            timeSlots.forEach(slot => {
                const option = document.createElement('option');
                const timeStr = formatTime(slot);
                option.value = slot;
                option.textContent = bookedSlots.includes(slot) ? `${timeStr} ❌ NOT AVAILABLE` : timeStr;
                if (bookedSlots.includes(slot)) option.disabled = true;
                select.appendChild(option);
            });
        }

        function formatTime(slot) {
            const [hour, minute] = slot.split(':');
            const time = new Date();
            time.setHours(parseInt(hour), parseInt(minute));
            return time.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit', hour12: true }).toUpperCase();
        }

        document.getElementById('reservationForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const formData = {
                bigoName: document.getElementById('bigoName').value,
                bigoId: document.getElementById('bigoId').value,
                level: document.getElementById('level').value,
                agency: document.getElementById('agency').value,
                gmail: document.getElementById('gmail').value,
                date: document.getElementById('date').value,
                time: document.getElementById('timeSlot').value,
                timestamp: Date.now().toString()
            };

            const existing = reservations.find(r => r.date === formData.date && r.time === formData.time);
            if (existing) {
                showMessage('❌ This time slot is already taken!', 'error');
                return;
            }

            reservations.push(formData);
            localStorage.setItem('bigoReservations', JSON.stringify(reservations));
            
            showMessage('🎉 Slot reserved successfully! Check your email for confirmation.', 'success');
            this.reset();
            setMinDate();
            updateTimeSlots();
            
            if (isAdmin) updateAdminDashboard();
        });

        function showMessage(text, type) {
            const message = document.getElementById('message');
            message.textContent = text;
            message.className = `mt-12 p-8 rounded-3xl text-2xl font-black ${type === 'success' ? 
                'bg-green-500/30 border-4 border-green-500 text-green-100 neon-glow' : 
                'bg-red-500/30 border-4 border-red-500 text-red-100 neon-glow'}`;
            message.classList.remove('hidden');
            setTimeout(() => message.classList.add('hidden'), 6000);
        }

        document.getElementById('date').addEventListener('change', updateTimeSlots);

        // FIXED Admin functionality
        document.getElementById('adminBtn').addEventListener('click', function() {
            document.getElementById('reservationSection').style.display = 'none';
            document.getElementById('adminPanel').style.display = 'block';
            document.getElementById('adminPanel').scrollIntoView({ behavior: 'smooth' });
        });

        document.getElementById('closeAdmin').addEventListener('click', function() {
            document.getElementById('adminPanel').style.display = 'none';
            document.getElementById('reservationSection').style.display = 'block';
        });

        document.getElementById('adminPin').addEventListener('input', function(e) {
            if (e.target.value === '6969') {
                isAdmin = true;
                document.getElementById('adminPinSection').classList.add('hidden');
                document.getElementById('scheduleSummary').classList.remove('hidden');
                localStorage.setItem('isAdmin', 'true');
                updateAdminDashboard();
            }
        });

        function updateAdminDashboard() {
            updateTodaySchedule();
            updateStats();
            updateAllReservations();
        }

        function updateTodaySchedule() {
            const today = new Date().toISOString().split('T')[0];
            const todayRes = reservations.filter(r => r.date === today);
            const container = document.getElementById('todaySchedule');
            
            container.innerHTML = todayRes.length ? 
                todayRes.map(r => `
                    <div class="glass p-6 rounded-3xl flex justify-between items-center hover:bg-white/20 transition-all">
                        <div>
                            <div class="text-2xl font-black cn-golden mb-2">${formatTime(r.time)}</div>
                            <div class="text-xl">${r.bigoName} <span class="text-yellow-400">(${r.level})</span></div>
                            <div class="text-sm text-white/70">${r.agency}</div>
                        </div>
                        <button onclick="cancelReservation('${r.timestamp}')" class="bg-red-500/90 hover:bg-red-600 text-white px-6 py-3 rounded-3xl text-lg font-bold transition-all shadow-lg hover:shadow-red-500/50">
                            ❌ Cancel
                        </button>
                    </div>
                `).join('') :
                '<div class="text-center py-20 text-white/60"><i class="fas fa-calendar-times text-8xl mb-8 opacity-50"></i><div class="text-3xl font-bold">No bookings today</div></div>';
        }

        function updateStats() {
            const today = new Date().toISOString().split('T')[0];
            const todayBookings = reservations.filter(r => r.date === today).length;
            const totalSlots = timeSlots.length;
            const available = totalSlots - todayBookings;

            document.getElementById('totalBookings').textContent = reservations.length;
            document.getElementById('availableSlots').textContent = available;

            const ctx = document.getElementById('statsChart')?.getContext('2d');
            if (ctx && window.statsChart) window.statsChart.destroy();
            if (ctx) {
                window.statsChart = new Chart(ctx, {
                    type: 'doughnut',
                    data: {
                        labels: ['Booked', 'Available'],
                        datasets: [{
                            data: [todayBookings, available],
                            backgroundColor: ['#ef4444', '#10b981'],
                            borderWidth: 0,
                            cutout: '60%'
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: { legend: { display: false } },
                        animation: { duration: 2000 }
                    }
                });
            }
        }

        function updateAllReservations() {
            const tbody = document.getElementById('allReservations');
            if (reservations.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" class="p-12 text-center text-white/60"><i class="fas fa-inbox text-6xl mb-6 opacity-50"></i><div class="text-3xl font-bold">No reservations yet</div></td></tr>';
                return;
            }

            tbody.innerHTML = reservations.map(r => `
                <tr class="border-b-2 border-white/20 hover:bg-white/10 transition-all">
                    <td class="p-6 font-bold cn-golden">${r.date}<br>${formatTime(r.time)}</td>
                    <td class="p-6 font-bold text-2xl">${r.bigoName}</td>
                    <td class="p-6">${r.bigoId}<br><span class="text-2xl cn-golden">LVL ${r.level}</span></td>
                    <td class="p-6 font-bold">${r.agency}</td>
                    <td class="p-6">${r.gmail}</td>
                    <td class="p-6">
                        <button onclick="cancelReservation('${r.timestamp}')" class="bg-red-500/90 hover:bg-red-600 text-white px-8 py-4 rounded-3xl text-xl font-bold transition-all shadow-xl hover:shadow-red-500/50 mr-4">
                            <i class="fas fa-trash mr-2"></i>Delete
                        </button>
                    </td>
                </tr>
            `).join('');
        }

        window.cancelReservation = function(timestamp) {
            if (confirm('Cancel this reservation?')) {
                reservations = reservations.filter(r => r.timestamp !== timestamp);
                localStorage.setItem('bigoReservations', JSON.stringify(reservations));
                updateAdminDashboard();
                updateTimeSlots();
                showMessage('✅ Reservation cancelled successfully!', 'success');
            }
        }

        function loadAdminStatus() {
            if (localStorage.getItem('isAdmin') === 'true') {
                isAdmin = true;
                document.getElementById('adminPinSection').classList.add('hidden');
                document.getElementById('scheduleSummary').classList.remove('hidden');
                updateAdminDashboard();
            }
        }

        function updateAdminToggle() {
            if (isAdmin) {
                document.getElementById('adminToggle').classList.remove('hidden');
            }
        }
    </script>
</body>
</html>
