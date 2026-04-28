
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bigo OPK Reservation System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        * { font-family: 'Poppins', sans-serif; }
        .gradient-bg { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .glass { backdrop-filter: blur(20px); background: rgba(255, 255, 255, 0.1); border: 1px solid rgba(255, 255, 255, 0.2); }
        .neon-glow { box-shadow: 0 0 20px rgba(102, 126, 234, 0.5); }
        .pulse { animation: pulse 2s infinite; }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: .5; } }
    </style>
</head>
<body class="bg-gradient-to-br from-purple-900 via-indigo-900 to-pink-900 min-h-screen">
    <!-- Header -->
    <header class="gradient-bg shadow-2xl">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center py-6">
                <div class="flex items-center space-x-3">
                    <div class="w-12 h-12 bg-white/20 rounded-2xl flex items-center justify-center neon-glow">
                        <i class="fas fa-microphone-alt text-white text-xl"></i>
                    </div>
                    <div>
                        <h1 class="text-3xl font-bold text-white drop-shadow-lg">Bigo OPK</h1>
                        <p class="text-white/80 text-sm">Reservation System</p>
                    </div>
                </div>
                <div id="adminToggle" class="hidden">
                    <button id="adminBtn" class="glass text-white px-6 py-2 rounded-2xl hover:bg-white/20 transition-all duration-300">
                        <i class="fas fa-crown mr-2"></i>Admin Panel
                    </button>
                </div>
            </div>
        </div>
    </header>

    <div class="max-w-4xl mx-auto px-4 py-12">
        <!-- Main Reservation Form -->
        <div id="reservationSection" class="glass rounded-3xl p-8 md:p-12 shadow-2xl neon-glow mb-12">
            <div class="text-center mb-10">
                <div class="w-24 h-24 bg-white/20 rounded-3xl mx-auto mb-6 flex items-center justify-center neon-glow">
                    <i class="fas fa-calendar-check text-3xl text-white"></i>
                </div>
                <h2 class="text-4xl md:text-5xl font-bold bg-gradient-to-r from-white to-gray-200 bg-clip-text text-transparent mb-4">
                    Book Your OPK Slot
                </h2>
                <p class="text-xl text-white/90 max-w-2xl mx-auto">Secure your 15-minute slot between 8:00 PM - 10:15 PM. First come, first served!</p>
            </div>

            <form id="reservationForm" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                    <label class="block text-white font-semibold mb-3">Bigo Name</label>
                    <input type="text" id="bigoName" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white placeholder-white/60 focus:outline-none focus:ring-4 focus:ring-white/30 transition-all duration-300" placeholder="Your Bigo username">
                </div>
                <div>
                    <label class="block text-white font-semibold mb-3">Bigo ID</label>
                    <input type="text" id="bigoId" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white placeholder-white/60 focus:outline-none focus:ring-4 focus:ring-white/30 transition-all duration-300" placeholder="123456789">
                </div>
                <div>
                    <label class="block text-white font-semibold mb-3">Level</label>
                    <input type="number" id="level" min="1" max="100" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white placeholder-white/60 focus:outline-none focus:ring-4 focus:ring-white/30 transition-all duration-300" placeholder="LVL 50">
                </div>
                <div>
                    <label class="block text-white font-semibold mb-3">Agency</label>
                    <input type="text" id="agency" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white placeholder-white/60 focus:outline-none focus:ring-4 focus:ring-white/30 transition-all duration-300" placeholder="Your agency name">
                </div>
                <div class="md:col-span-2">
                    <label class="block text-white font-semibold mb-3">Gmail Account</label>
                    <input type="email" id="gmail" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white placeholder-white/60 focus:outline-none focus:ring-4 focus:ring-white/30 transition-all duration-300" placeholder="your.email@gmail.com">
                </div>
                <div class="md:col-span-2">
                    <label class="block text-white font-semibold mb-3">Select Date</label>
                    <input type="date" id="date" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white placeholder-white/60 focus:outline-none focus:ring-4 focus:ring-white/30 transition-all duration-300">
                </div>
                <div class="md:col-span-2">
                    <label class="block text-white font-semibold mb-3">Select Time Slot (15 mins)</label>
                    <select id="timeSlot" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white focus:outline-none focus:ring-4 focus:ring-white/30 transition-all duration-300">
                        <option value="">Choose your slot (8:00 PM - 10:15 PM)</option>
                    </select>
                </div>
                <div class="md:col-span-2">
                    <button type="submit" id="submitBtn" class="w-full bg-gradient-to-r from-pink-500 to-purple-600 text-white font-bold py-6 px-8 rounded-3xl text-xl hover:from-pink-600 hover:to-purple-700 transform hover:scale-105 transition-all duration-300 shadow-2xl hover:shadow-purple-500/25 neon-glow">
                        <i class="fas fa-lock mr-3"></i>Reserve My Slot
                    </button>
                </div>
            </form>
            <div id="message" class="mt-8 p-6 rounded-2xl hidden"></div>
        </div>

        <!-- Admin Panel -->
        <div id="adminPanel" class="glass rounded-3xl p-8 md:p-12 shadow-2xl neon-glow hidden">
            <div class="flex justify-between items-center mb-10">
                <h2 class="text-4xl font-bold bg-gradient-to-r from-yellow-400 to-orange-500 bg-clip-text text-transparent">
                    <i class="fas fa-crown mr-4"></i>Admin Dashboard
                </h2>
                <button id="closeAdmin" class="text-white/80 hover:text-white text-2xl">
                    <i class="fas fa-times"></i>
                </button>
            </div>

            <!-- Admin PIN Input -->
            <div id="adminPinSection" class="text-center mb-12">
                <input type="password" id="adminPin" maxlength="4" class="w-32 h-20 text-4xl font-bold text-center rounded-2xl bg-white/20 border-4 border-white/30 text-white focus:outline-none focus:border-yellow-400 mx-auto" placeholder="PIN">
                <p class="text-white/80 mt-4">Enter Admin PIN: <span class="font-bold text-yellow-400">6969</span></p>
            </div>

            <!-- Schedule Summary -->
            <div id="scheduleSummary" class="hidden">
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12">
                    <div class="glass p-8 rounded-2xl">
                        <h3 class="text-2xl font-bold text-white mb-6 flex items-center">
                            <i class="fas fa-calendar mr-3 text-yellow-400"></i>Today's Schedule
                        </h3>
                        <div id="todaySchedule" class="space-y-4 max-h-96 overflow-y-auto"></div>
                    </div>
                    <div class="glass p-8 rounded-2xl">
                        <h3 class="text-2xl font-bold text-white mb-6 flex items-center">
                            <i class="fas fa-chart-bar mr-3 text-green-400"></i>Booking Stats
                        </h3>
                        <canvas id="statsChart" height="200"></canvas>
                        <div class="mt-6 grid grid-cols-2 gap-4 text-center">
                            <div class="glass p-4 rounded-xl">
                                <div class="text-3xl font-bold text-green-400" id="totalBookings">0</div>
                                <div class="text-white/80 text-sm">Total Bookings</div>
                            </div>
                            <div class="glass p-4 rounded-xl">
                                <div class="text-3xl font-bold text-yellow-400" id="availableSlots">19</div>
                                <div class="text-white/80 text-sm">Available Today</div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- All Reservations -->
                <div class="glass p-8 rounded-2xl">
                    <h3 class="text-2xl font-bold text-white mb-6 flex items-center">
                        <i class="fas fa-list mr-3 text-blue-400"></i>All Reservations
                    </h3>
                    <div class="overflow-x-auto">
                        <table class="w-full text-white">
                            <thead>
                                <tr class="border-b border-white/20">
                                    <th class="p-4 text-left font-semibold">Date/Time</th>
                                    <th class="p-4 text-left font-semibold">Bigo Name</th>
                                    <th class="p-4 text-left font-semibold">ID/LVL</th>
                                    <th class="p-4 text-left font-semibold">Agency</th>
                                    <th class="p-4 text-left font-semibold">Email</th>
                                    <th class="p-4 text-left font-semibold">Actions</th>
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

        // Reservations data (persists in localStorage)
        let reservations = JSON.parse(localStorage.getItem('bigoReservations')) || [];
        let isAdmin = false;

        // Initialize
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
                option.textContent = timeStr;
                if (bookedSlots.includes(slot)) {
                    option.textContent = `${timeStr} ❌ NOT AVAILABLE`;
                    option.disabled = true;
                }
                select.appendChild(option);
            });
        }

        function formatTime(slot) {
            const [hour, minute] = slot.split(':');
            const time = new Date();
            time.setHours(parseInt(hour), parseInt(minute));
            return time.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
        }

        // Form submission
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
                timestamp: new Date().toISOString()
            };

            // Check if slot is available
            const existing = reservations.find(r => r.date === formData.date && r.time === formData.time);
            if (existing) {
                showMessage('❌ This time slot is already taken!', 'error');
                return;
            }

            // Save reservation
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
            message.className = `mt-8 p-6 rounded-2xl text-xl font-semibold ${type === 'success' ? 'bg-green-500/20 border-2 border-green-500 text-green-100' : 'bg-red-500/20 border-2 border-red-500 text-red-100'}`;
            message.classList.remove('hidden');
            
            setTimeout(() => message.classList.add('hidden'), 5000);
        }

        // Date change listener
        document.getElementById('date').addEventListener('change', updateTimeSlots);

        // Admin functionality
        document.getElementById('adminBtn').addEventListener('click', () => {
            document.getElementById('adminPanel').classList.remove('hidden');
            document.getElementById('reservationSection').classList.add('hidden');
        });

        document.getElementById('closeAdmin').addEventListener('click', () => {
            document.getElementById('adminPanel').classList.add('hidden');
            document.getElementById('reservationSection').classList.remove('hidden');
        });

        document.getElementById('adminPin').addEventListener('input', function(e) {
            if (e.target.value === '6969') {
                isAdmin = true;
                document.getElementById('adminPinSection').classList.add('hidden');
                document.getElementById('scheduleSummary').classList.remove('hidden');
                updateAdminDashboard();
                localStorage.setItem('isAdmin', 'true');
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
                    <div class="glass p-4 rounded-xl flex justify-between items-center">
                        <div>
                            <div class="font-bold text-lg">${formatTime(r.time)}</div>
                            <div class="text-sm text-white/70">${r.bigoName} (${r.level})</div>
                        </div>
                        <button onclick="cancelReservation('${r.timestamp}')" class="bg-red-500/80 hover:bg-red-600 text-white px-4 py-2 rounded-xl text-sm font-semibold transition-all">
                            Cancel
                        </button>
                    </div>
                `).join('') :
                '<div class="text-center py-12 text-white/60"><i class="fas fa-calendar-times text-4xl mb-4"></i><div>No bookings today</div></div>';
        }

        function updateStats() {
            const today = new Date().toISOString().split('T')[0];
            const todayBookings = reservations.filter(r => r.date === today).length;
            const totalSlots = timeSlots.length;
            const available = totalSlots - todayBookings;

            document.getElementById('totalBookings').textContent = reservations.length;
            document.getElementById('availableSlots').textContent = available;

            // Update chart
            const ctx = document.getElementById('statsChart').getContext('2d');
            if (window.statsChart) window.statsChart.destroy();
            window.statsChart = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['Booked', 'Available'],
                    datasets: [{
                        data: [todayBookings, available],
                        backgroundColor: ['#ef4444', '#10b981'],
                        borderWidth: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } }
                }
            });
        }

        function updateAllReservations() {
            const tbody = document.getElementById('allReservations');
            if (reservations.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" class="p-12 text-center text-white/60">No reservations yet</td></tr>';
                return;
            }

            tbody.innerHTML = reservations.map(r => `
                <tr class="border-b border-white/10 hover:bg-white/10 transition-all">
                    <td class="p-4">${r.date} ${formatTime(r.time)}</td>
                    <td class="p-4 font-semibold">${r.bigoName}</td>
                    <td class="p-4">${r.bigoId}<br><span class="text-sm text-yellow-400">LVL ${r.level}</span></td>
                    <td class="p-4">${r.agency}</td>
                    <td class="p-4">${r.gmail}</td>
                    <td class="p-4">
                        <button onclick="cancelReservation('${r.timestamp}')" class="bg-red-500/80 hover:bg-red-600 text-white px-4 py-2 rounded-xl text-sm font-semibold transition-all mr-2">
                            <i class="fas fa-trash"></i>
                        </button>
                    </td>
                </tr>
            `).join('');
        }

        function cancelReservation(timestamp) {
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
