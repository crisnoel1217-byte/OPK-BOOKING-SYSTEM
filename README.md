<!DOCTYPE html>
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
            text-shadow: 0 0 20px rgba(255, 215, 0, 0.8), 0 0 40px rgba(0, 0, 0, 0.5);
            font-weight: 900;
        }
        .gradient-bg { background: linear-gradient(135deg, #1e1b4b 0%, #2d1b69 30%, #4158d0 60%, #c850c0 100%); }
        .glass { backdrop-filter: blur(25px); background: rgba(255, 255, 255, 0.15); border: 1px solid rgba(255, 255, 255, 0.25); }
        .neon-glow { box-shadow: 0 0 30px rgba(255, 215, 0, 0.6), 0 0 60px rgba(255, 165, 0, 0.3); }
        .pulse-golden { animation: pulse-golden 2s infinite; }
        @keyframes pulse-golden {
            0%, 100% { box-shadow: 0 0 30px rgba(255, 215, 0, 0.6), 0 0 60px rgba(255, 165, 0, 0.3); }
            50% { box-shadow: 0 0 50px rgba(255, 215, 0, 0.9), 0 0 80px rgba(255, 165, 0, 0.5); }
        }
        html { scroll-behavior: smooth; }
        body { overflow-x: hidden; }
    </style>
</head>
<body class="bg-gradient-to-br from-purple-900 via-indigo-900 to-pink-900 min-h-screen pb-32">
    <!-- FIXED Header - Smaller for better scrolling -->
    <header class="gradient-bg shadow-2xl py-6 sticky top-0 z-50">
        <div class="max-w-6xl mx-auto px-6">
            <div class="flex flex-col sm:flex-row justify-between items-center">
                <div class="flex items-center space-x-4">
                    <div class="w-20 h-20 bg-gradient-to-br from-black to-yellow-500 rounded-2xl flex items-center justify-center neon-glow pulse-golden shadow-2xl border-4 border-yellow-400">
                        <span class="cn-black-yellow text-3xl md:text-4xl tracking-widest drop-shadow-lg">CN</span>
                    </div>
                    <div>
                        <h1 class="text-3xl md:text-4xl font-black text-white drop-shadow-2xl mb-1">Bigo OPK</h1>
                        <p class="text-lg md:text-xl text-yellow-300 font-semibold">Reservation System</p>
                    </div>
                </div>
                <div id="adminToggle" class="hidden">
                    <button id="adminBtn" class="glass text-white px-6 py-3 rounded-2xl text-lg font-bold hover:bg-white/30 transition-all duration-300 neon-glow hover:scale-105">
                        <i class="fas fa-crown mr-2 text-yellow-400"></i>Admin
                    </button>
                </div>
            </div>
        </div>
    </header>

    <div class="max-w-6xl mx-auto px-6 py-12">
        <!-- Main Reservation Form -->
        <div id="reservationSection" class="glass rounded-3xl p-12 lg:p-20 shadow-4xl neon-glow mx-auto max-w-5xl mb-20">
            <div class="text-center mb-12">
                <div class="w-24 h-24 bg-gradient-to-br from-black to-yellow-500 rounded-3xl mx-auto mb-6 flex items-center justify-center neon-glow pulse-golden shadow-2xl">
                    <i class="fas fa-calendar-check text-3xl text-white"></i>
                </div>
                <h2 class="text-4xl md:text-6xl font-black bg-gradient-to-r from-white via-yellow-100 to-yellow-300 bg-clip-text text-transparent mb-4 drop-shadow-2xl">
                    Book Your OPK Slot
                </h2>
                <p class="text-xl md:text-2xl text-white/95 max-w-3xl mx-auto leading-relaxed">Secure your <span class="text-yellow-400 font-bold">15-minute slot</span> between <span class="text-yellow-400 font-bold">8:00 PM - 10:15 PM</span></p>
            </div>

            <form id="reservationForm" class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <div>
                    <label class="block text-white font-bold text-lg mb-4">👤 Bigo Name</label>
                    <input type="text" id="bigoName" required class="w-full p-5 text-lg rounded-2xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-4 focus:ring-yellow-400/50 transition-all duration-300 hover:border-yellow-400" placeholder="Your Bigo username">
                </div>
                <div>
                    <label class="block text-white font-bold text-lg mb-4">🆔 Bigo ID</label>
                    <input type="text" id="bigoId" required class="w-full p-5 text-lg rounded-2xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-4 focus:ring-yellow-400/50 transition-all duration-300 hover:border-yellow-400" placeholder="123456789">
                </div>
                <div>
                    <label class="block text-white font-bold text-lg mb-4">⭐ Level</label>
                    <input type="number" id="level" min="1" max="100" required class="w-full p-5 text-lg rounded-2xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-4 focus:ring-yellow-400/50 transition-all duration-300 hover:border-yellow-400" placeholder="LVL 50">
                </div>
                <div>
                    <label class="block text-white font-bold text-lg mb-4">🏢 Agency</label>
                    <input type="text" id="agency" required class="w-full p-5 text-lg rounded-2xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-4 focus:ring-yellow-400/50 transition-all duration-300 hover:border-yellow-400" placeholder="Your agency name">
                </div>
                <div class="lg:col-span-2">
                    <label class="block text-white font-bold text-lg mb-4">📧 Gmail Account</label>
                    <input type="email" id="gmail" required class="w-full p-5 text-lg rounded-2xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-4 focus:ring-yellow-400/50 transition-all duration-300 hover:border-yellow-400" placeholder="your.email@gmail.com">
                </div>
                <div class="lg:col-span-2">
                    <label class="block text-white font-bold text-lg mb-4">📅 Select Date</label>
                    <input type="date" id="date" required class="w-full p-5 text-lg rounded-2xl bg-white/20 border-2 border-white/40 text-white placeholder-white/70 focus:outline-none focus:ring-4 focus:ring-yellow-400/50 transition-all duration-300 hover:border-yellow-400">
                </div>
                <div class="lg:col-span-2">
                    <label class="block text-white font-bold text-lg mb-4">⏰ Select Time Slot (15 mins)</label>
                    <select id="timeSlot" required class="w-full p-5 text-lg rounded-2xl bg-white/20 border-2 border-white/40 text-white focus:outline-none focus:ring-4 focus:ring-yellow-400/50 transition-all duration-300 hover:border-yellow-400">
                        <option value="">Choose your slot (8:00 PM - 10:15 PM)</option>
                    </select>
                </div>
                <div class="lg:col-span-2">
                    <button type="submit" class="w-full bg-gradient-to-r from-black via-yellow-400 to-yellow-500 text-gray-900 font-black py-6 px-8 rounded-3xl text-2xl hover:from-gray-800 hover:via-yellow-500 hover:to-yellow-600 transform hover:scale-105 transition-all duration-300 shadow-2xl hover:shadow-yellow-500/50 neon-glow pulse-golden">
                        <i class="fas fa-lock mr-3"></i>🔒 RESERVE MY SLOT
                    </button>
                </div>
            </form>
            <div id="message" class="mt-8 p-6 rounded-2xl hidden text-xl font-bold"></div>
        </div>

        <!-- Admin Panel -->
        <div id="adminPanel" class="glass rounded-3xl p-12 lg:p-20 shadow-4xl mx-auto max-w-6xl mb-20 hidden">
            <div class="flex justify-between items-center mb-12">
                <h2 class="text-4xl md:text-5xl font-black bg-gradient-to-r from-yellow-400 to-orange-500 bg-clip-text text-transparent flex items-center">
                    <i class="fas fa-crown mr-4 text-5xl text-yellow-400"></i>Admin Dashboard
                </h2>
                <button id="closeAdmin" class="text-white/80 hover:text-white text-3xl p-3 rounded-2xl hover:bg-white/20 transition-all duration-300">
                    <i class="fas fa-times"></i>
                </button>
            </div>

            <!-- Admin PIN -->
            <div id="adminPinSection" class="text-center mb-16 bg-white/10 p-10 rounded-3xl">
                <div class="w-24 h-24 bg-gradient-to-br from-black to-yellow-500 rounded-3xl mx-auto mb-6 flex items-center justify-center neon-glow pulse-golden">
                    <i class="fas fa-key text-3xl text-white"></i>
                </div>
                <input type="password" id="adminPin" maxlength="4" class="w-32 h-20 text-4xl font-black text-center rounded-3xl bg-white/30 border-4 border-yellow-400 mx-auto mb-6 focus:outline-none focus:border-yellow-500" placeholder="PIN">
                <p class="text-xl text-white/90 font-bold">Admin PIN: <span class="cn-black-yellow text-2xl">6969</span></p>
            </div>

            <!-- Dashboard Content -->
            <div id="scheduleSummary" class="hidden">
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-16">
                    <div class="glass p-8 lg:p-12 rounded-3xl h-80 lg:h-96">
                        <h3 class="text-2xl lg:text-3xl font-black text-white mb-8 flex items-center cn-black-yellow">
                            <i class="fas fa-calendar mr-3 text-3xl"></i>Today's Schedule
                        </h3>
                        <div id="todaySchedule" class="space-y-4 max-h-56 lg:max-h-72 overflow-y-auto pr-2"></div>
                    </div>
                    <div class="glass p-8 lg:p-12 rounded-3xl">
                        <h3 class="text-2xl lg:text-3xl font-black text-white mb-8 flex items-center cn-black-yellow">
                            <i class="fas fa-chart-bar mr-3 text-3xl"></i>Booking Stats
                        </h3>
                        <div class="h-48 lg:h-64 mb-8">
                            <canvas id="statsChart"></canvas>
                        </div>
                        <div class="grid grid-cols-2 gap-6">
                            <div class="glass p-6 rounded-2xl neon-glow text-center">
                                <div class="text-4xl lg:text-5xl font-black cn-black-yellow mb-2" id="totalBookings">0</div>
                                <div class="text-lg text-white/90 font-bold">Total Bookings</div>
                            </div>
                            <div class="glass p-6 rounded-2xl neon-glow text-center">
                                <div class="text-4xl lg:text-5xl font-black text-green-400 mb-2" id="availableSlots">19</div>
                                <div class="text-lg text-white/90 font-bold">Available Today</div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="glass p-8 lg:p-12 rounded-3xl">
                    <h3 class="text-2xl lg:text-3xl font-black text-white mb-8 flex items-center cn-black-yellow">
                        <i class="fas fa-list mr-3 text-3xl"></i>All Reservations
                    </h3>
                    <div class="overflow-x-auto">
                        <table class="w-full text-white text-base lg:text-lg">
                            <thead>
                                <tr class="border-b-4 border-yellow-400/50">
                                    <th class="p-4 lg:p-6 text-left font-black text-xl">Date/Time</th>
                                    <th class="p-4 lg:p-6 text-left font-black text-xl">Name</th>
                                    <th class="p-4 lg:p-6 text-left font-black text-xl">ID/LVL</th>
                                    <th class="p-4 lg:p-6 text-left font-black text-xl">Agency</th>
                                    <th class="p-4 lg:p-6 text-left font-black text-xl">Email</th>
                                    <th class="p-4 lg:p-6 text-left font-black text-xl">Action</th>
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
            
            showMessage('🎉 Slot reserved successfully!', 'success');
            this.reset();
            setMinDate();
            updateTimeSlots();
            
            if (isAdmin) updateAdminDashboard();
        });

        function showMessage(text, type) {
            const message = document.getElementById('message');
            message.textContent = text;
            message.className = `mt-8 p-6 rounded-2xl text-xl font-bold ${type === 'success' ? 
                'bg-green-500/30 border-4 border-green-500 text-green-100' : 
                'bg-red-500/30 border-4 border-red-500 text-red-100'}`;
            message.classList.remove('hidden');
            setTimeout(() => message.classList.add('hidden'), 5000);
        }

        document.getElementById('date').addEventListener('change', updateTimeSlots);

        document.getElementById('adminBtn').addEventListener('click', function() {
            document.getElementById('reservationSection').style.display = 'none';
            document.getElementById('adminPanel').classList.remove('hidden');
            document.getElementById('adminPanel').scrollIntoView({ behavior: 'smooth' });
        });

        document.getElementById('closeAdmin').addEventListener('click', function() {
            document.getElementById('adminPanel').classList.add('hidden');
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
