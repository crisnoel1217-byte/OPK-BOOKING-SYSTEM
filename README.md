
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CN Bigo OPK - Secure Admin</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');
        * { font-family: 'Inter', sans-serif; }
        
        .cn-logo { 
            font-family: 'Cinzel', serif; 
            background: linear-gradient(45deg, #1a1a1a 0%, #FFD700 50%, #1a1a1a 100%);
            -webkit-background-clip: text;
            background-clip: text;
            font-weight: 900;
            font-size: 2.5rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .glass { 
            background: rgba(255,255,255,0.95); 
            backdrop-filter: blur(20px); 
            border: 1px solid rgba(255,255,255,0.8);
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }
        
        .dark-glass { 
            background: rgba(15,23,42,0.95); 
            backdrop-filter: blur(20px); 
            border: 1px solid rgba(255,255,255,0.1);
        }
        
        .admin-locked { filter: blur(4px); opacity: 0.5; pointer-events: none; }
        .admin-unlocked { filter: none; opacity: 1; pointer-events: all; }
        
        body { 
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 50%, #334155 100%);
            min-height: 100vh;
        }
        
        .pin-input { 
            font-size: 2.5rem !important; 
            font-weight: 800 !important; 
            letter-spacing: 8px;
            text-align: center;
        }
        
        .blink { animation: blink 1s infinite; }
        @keyframes blink { 0%, 50% { opacity: 1; } 51%, 100% { opacity: 0.3; } }
    </style>
</head>
<body class="py-8 px-4 sm:px-6 lg:px-8">
    <div class="max-w-7xl mx-auto space-y-8">
        
        <!-- SECURE HEADER -->
        <div class="glass rounded-3xl p-8 lg:p-12 shadow-2xl border-t-4 border-yellow-400">
            <div class="flex flex-col lg:flex-row items-start lg:items-center justify-between gap-6">
                <div class="flex items-center space-x-6 flex-1">
                    <div class="w-24 h-24 bg-gradient-to-br from-gray-900 to-yellow-500 rounded-2xl flex items-center justify-center shadow-2xl border-4 border-yellow-400 p-2">
                        <span class="cn-logo text-3xl tracking-wider">CN</span>
                    </div>
                    <div>
                        <h1 class="text-4xl lg:text-5xl font-black text-gray-900 tracking-tight">Bigo OPK</h1>
                        <p class="text-xl text-gray-600 font-semibold mt-1">Secure Reservation System</p>
                        <p class="text-lg text-gray-500 mt-1">🔒 Admin PIN Protected</p>
                    </div>
                </div>
                <button id="toggleAdmin" class="bg-gradient-to-r from-yellow-400 to-yellow-600 hover:from-yellow-500 hover:to-yellow-700 text-gray-900 font-bold py-5 px-10 rounded-2xl text-xl shadow-2xl hover:shadow-yellow-500/50 hover:scale-105 transition-all duration-300 border-4 border-yellow-500 whitespace-nowrap">
                    <i class="fas fa-shield-alt mr-3 text-xl"></i>
                    <span class="font-black tracking-wide">🔐 SECURE ADMIN</span>
                </button>
            </div>
        </div>

        <!-- BOOKING FORM -->
        <div id="bookingSection" class="glass rounded-3xl p-8 lg:p-12 shadow-2xl max-w-5xl mx-auto">
            <div class="text-center mb-10">
                <h2 class="text-4xl font-bold text-gray-900 mb-4">📅 Reserve Your Slot</h2>
                <p class="text-xl text-gray-600">Complete all fields • No double booking allowed</p>
            </div>
            
            <form id="bookingForm" class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <div>
                    <label class="block text-gray-800 font-semibold text-lg mb-3">👤 Bigo Username</label>
                    <input id="username" required class="w-full p-4 lg:p-5 rounded-2xl border-2 border-gray-200 text-lg bg-white focus:border-blue-500 focus:ring-4 focus:ring-blue-200 transition-all" placeholder="Enter username">
                </div>
                <div>
                    <label class="block text-gray-800 font-semibold text-lg mb-3">🆔 Bigo ID</label>
                    <input id="bigoId" required class="w-full p-4 lg:p-5 rounded-2xl border-2 border-gray-200 text-lg bg-white focus:border-blue-500 focus:ring-4 focus:ring-blue-200 transition-all" placeholder="ID number">
                </div>
                <div>
                    <label class="block text-gray-800 font-semibold text-lg mb-3">⭐ Level</label>
                    <input id="level" type="number" min="1" max="100" required class="w-full p-4 lg:p-5 rounded-2xl border-2 border-gray-200 text-lg bg-white focus:border-blue-500 focus:ring-4 focus:ring-blue-200 transition-all" placeholder="50">
                </div>
                <div>
                    <label class="block text-gray-800 font-semibold text-lg mb-3">🏢 Agency</label>
                    <input id="agency" required class="w-full p-4 lg:p-5 rounded-2xl border-2 border-gray-200 text-lg bg-white focus:border-blue-500 focus:ring-4 focus:ring-blue-200 transition-all" placeholder="Agency name">
                </div>
                <div class="lg:col-span-2">
                    <label class="block text-gray-800 font-semibold text-lg mb-3">📧 Gmail Account</label>
                    <input id="email" type="email" required class="w-full p-4 lg:p-5 rounded-2xl border-2 border-gray-200 text-lg bg-white focus:border-blue-500 focus:ring-4 focus:ring-blue-200 transition-all" placeholder="name@gmail.com">
                </div>
                <div class="lg:col-span-2">
                    <label class="block text-gray-800 font-semibold text-lg mb-3">📅 Date</label>
                    <input id="date" type="date" required class="w-full p-4 lg:p-5 rounded-2xl border-2 border-gray-200 text-lg bg-white focus:border-blue-500 focus:ring-4 focus:ring-blue-200 transition-all">
                </div>
                <div class="lg:col-span-2">
                    <label class="block text-gray-800 font-semibold text-lg mb-3">⏰ Time Slot (15 mins)</label>
                    <select id="timeSlot" required class="w-full p-4 lg:p-5 rounded-2xl border-2 border-gray-200 text-lg bg-gradient-to-r from-gray-800 to-gray-900 text-white focus:border-blue-500 focus:ring-4 focus:ring-blue-200 transition-all appearance-none">
                        <option value="" class="bg-gray-800 text-white">Select time (8PM-10PM)</option>
                    </select>
                </div>
                <button type="submit" class="lg:col-span-2 bg-gradient-to-r from-emerald-500 to-teal-600 hover:from-emerald-600 hover:to-teal-700 text-white font-black py-6 px-12 rounded-3xl text-2xl shadow-2xl hover:shadow-emerald-500/50 hover:scale-105 transition-all duration-300 border-4 border-emerald-500">
                    <i class="fas fa-check-circle mr-3"></i>CONFIRM RESERVATION
                </button>
            </form>
            <div id="message" class="mt-8 p-6 rounded-2xl font-bold text-xl text-center hidden border-4"></div>
        </div>

        <!-- SECURE ADMIN DASHBOARD -->
        <div id="adminDashboard" class="hidden">
            <!-- PIN LOCK SCREEN -->
            <div id="pinScreen" class="dark-glass rounded-3xl p-16 lg:p-24 shadow-2xl text-center border-t-8 border-red-500 mb-8">
                <div class="w-32 h-32 bg-gradient-to-br from-red-500 to-pink-600 rounded-3xl mx-auto mb-12 flex items-center justify-center shadow-2xl border-8 border-red-400">
                    <i class="fas fa-lock text-5xl text-white"></i>
                </div>
                <h2 class="text-4xl lg:text-5xl font-black text-white mb-6">🔐 Admin Access Required</h2>
                <p class="text-xl text-gray-300 mb-12 max-w-2xl mx-auto">Enter PIN to unlock full dashboard controls</p>
                
                <div class="max-w-md mx-auto">
                    <input type="password" id="adminPin" maxlength="4" class="pin-input w-full h-24 rounded-3xl bg-white/20 border-4 border-yellow-400 text-yellow-500 focus:border-yellow-500 focus:outline-none focus:ring-8 focus:ring-yellow-400/50 text-center font-mono tracking-widest shadow-2xl" placeholder="6969">
                    <p class="text-2xl font-bold text-yellow-400 mt-6 blink mb-2">PIN: <span class="cn-logo text-3xl">6969</span></p>
                    <p class="text-lg text-gray-400">Type 6969 to unlock • Data visible below</p>
                </div>
            </div>

            <!-- DASHBOARD CONTENT (BLURRED UNTIL UNLOCKED) -->
            <div id="dashboardContent" class="admin-locked">
                <!-- DASHBOARD HEADER -->
                <div class="dark-glass rounded-3xl p-8 lg:p-12 shadow-2xl border-t-8 border-yellow-400 mb-8">
                    <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-6">
                        <div>
                            <h1 class="text-4xl lg:text-5xl font-black text-white mb-2 flex items-center">
                                <i class="fas fa-chart-line text-yellow-400 mr-4 text-4xl"></i>
                                <span class="cn-logo">CN</span> Admin Dashboard
                            </h1>
                            <p class="text-xl text-gray-300">Complete OPK booking management • <span id="accessStatus" class="text-red-400 font-semibold">🔒 LOCKED</span></p>
                        </div>
                        <button id="backToForm" class="bg-gradient-to-r from-gray-600 to-gray-700 hover:from-gray-700 hover:to-gray-800 text-white font-bold py-4 px-8 rounded-2xl text-xl shadow-xl hover:shadow-gray-500/50 transition-all">
                            <i class="fas fa-arrow-left mr-2"></i>Back to Booking
                        </button>
                    </div>
                </div>

                <!-- KEY METRICS -->
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-12">
                    <div class="glass p-8 rounded-3xl text-center hover:shadow-xl transition-all border-l-8 border-blue-500">
                        <div class="text-4xl font-black text-blue-600 mb-2" id="totalBookings">0</div>
                        <div class="text-lg font-semibold text-gray-700">Total Bookings</div>
                    </div>
                    <div class="glass p-8 rounded-3xl text-center hover:shadow-xl transition-all border-l-8 border-emerald-500">
                        <div class="text-4xl font-black text-emerald-600 mb-2" id="todayBookings">0</div>
                        <div class="text-lg font-semibold text-gray-700">Today's Bookings</div>
                    </div>
                    <div class="glass p-8 rounded-3xl text-center hover:shadow-xl transition-all border-l-8 border-yellow-500">
                        <div class="text-4xl font-black text-yellow-600 mb-2" id="availableSlots">10</div>
                        <div class="text-lg font-semibold text-gray-700">Open Slots Today</div>
                    </div>
                    <div class="glass p-8 rounded-3xl text-center hover:shadow-xl transition-all border-l-8 border-purple-500">
                        <div class="text-4xl font-black text-purple-600 mb-2" id="topAgency">-</div>
                        <div class="text-lg font-semibold text-gray-700">Top Agency</div>
                    </div>
                </div>

                <!-- BOOKINGS TABLE -->
                <div class="dark-glass rounded-3xl p-8 lg:p-12 shadow-2xl overflow-hidden">
                    <div class="flex justify-between items-center mb-8 pb-4 border-b border-white/30">
                        <h3 class="text-3xl font-bold text-white flex items-center">
                            <i class="fas fa-table mr-4 text-yellow-400"></i>All Reservations
                        </h3>
                        <div class="text-sm text-gray-400">Last updated: <span id="lastUpdate"></span></div>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-sm lg:text-base">
                            <thead>
                                <tr>
                                    <th class="p-4 text-left font-bold bg-gradient-to-r from-blue-600 to-blue-700 text-white rounded-tl-2xl">Date & Time</th>
                                    <th class="p-4 text-left font-bold bg-gradient-to-r from-blue-600 to-blue-700 text-white">Host</th>
                                    <th class="p-4 text-left font-bold bg-gradient-to-r from-blue-600 to-blue-700 text-white">ID/Level</th>
                                    <th class="p-4 text-left font-bold bg-gradient-to-r from-blue-600 to-blue-700 text-white">Agency</th>
                                    <th class="p-4 text-left font-bold bg-gradient-to-r from-blue-600 to-blue-700 text-white">Email</th>
                                    <th class="p-4 text-left font-bold bg-gradient-to-r from-blue-600 to-blue-700 text-white rounded-tr-2xl">Controls</th>
                                </tr>
                            </thead>
                            <tbody id="reservationsTable">
                                <tr>
                                    <td colspan="6" class="p-16 text-center text-gray-500">
                                        <i class="fas fa-key text-6xl mb-6 opacity-50"></i>
                                        <div class="text-2xl font-semibold">Enter PIN above to unlock controls</div>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        let reservations = JSON.parse(localStorage.getItem('cnOpkReservations')) || [];
        let isAdminUnlocked = localStorage.getItem('adminUnlocked') === 'true';
        const ADMIN_PIN = '6969';
        const timeSlots = ['20:00','20:15','20:30','20:45','21:00','21:15','21:30','21:45','22:00','22:15'];

        document.addEventListener('DOMContentLoaded', init);

        function init() {
            setMinDate();
            updateTimeDropdown();
            updateDashboard();
            
            document.getElementById('toggleAdmin').onclick = showAdmin;
            document.getElementById('backToForm').onclick = showForm;
            document.getElementById('bookingForm').onsubmit = submitBooking;
            document.getElementById('date').onchange = updateTimeDropdown;
            document.getElementById('adminPin').oninput = checkAdminPin;
            
            if (isAdminUnlocked) {
                unlockAdmin();
            }
        }

        function setMinDate() {
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('date').value = today;
            document.getElementById('date').min = today;
        }

        function updateTimeDropdown() {
            const date = document.getElementById('date').value;
            const select = document.getElementById('timeSlot');
            select.innerHTML = '<option value="" class="bg-gray-800 text-white">Select time (8PM-10PM)</option>';
            
            const dateBookings = reservations.filter(r => r.date === date);
            const bookedTimes = dateBookings.map(r => r.timeSlot);
            
            timeSlots.forEach(slot => {
                const displayTime = new Date(`2000-01-01T${slot}:00`).toLocaleTimeString('en-US', {hour: 'numeric', minute: '2-digit', hour12: true}).toUpperCase();
                const option = new Option(displayTime, slot);
                if (bookedTimes.includes(slot)) {
                    option.text = displayTime + ' ❌ BOOKED';
                    option.disabled = true;
                }
                select.appendChild(option);
            });
        }

        function submitBooking(e) {
            e.preventDefault();
            const booking = {
                id: Date.now(),
                username: document.getElementById('username').value,
                bigoId: document.getElementById('bigoId').value,
                level: document.getElementById('level').value,
                agency: document.getElementById('agency').value,
                email: document.getElementById('email').value,
                date: document.getElementById('date').value,
                timeSlot: document.getElementById('timeSlot').value,
                timestamp: new Date().toISOString()
            };

            const conflict = reservations.find(r => r.date === booking.date && r.timeSlot === booking.timeSlot);
            if (conflict) {
                showMessage('❌ Time slot already booked!', 'border-red-500 bg-red-100 text-red-800');
                return;
            }

            reservations.push(booking);
            localStorage.setItem('cnOpkReservations', JSON.stringify(reservations));
            
            showMessage('✅ Booking confirmed successfully!', 'border-emerald-500 bg-emerald-100 text-emerald-800');
            e.target.reset();
            setMinDate();
            updateTimeDropdown();
            updateDashboard();
        }

        function showMessage(text, classes) {
            const msg = document.getElementById('message');
            msg.textContent = text;
            msg.className = `mt-8 p-6 rounded-2xl font-bold text-xl text-center ${classes} shadow-lg border-4`;
            msg.classList.remove('hidden');
            setTimeout(() => msg.classList.add('hidden'), 4000);
        }

        function showAdmin() {
            document.getElementById('bookingSection').style.display = 'none';
            document.getElementById('adminDashboard').classList.remove('hidden');
            document.getElementById('adminDashboard').scrollIntoView({behavior: 'smooth'});
            document.getElementById('adminPin').focus();
            updateDashboard();
        }

        function showForm() {
            document.getElementById('adminDashboard').classList.add('hidden');
            document.getElementById('bookingSection').style.display = 'block';
        }

        function checkAdminPin(e) {
            if (e.target.value === ADMIN_PIN) {
                unlockAdmin();
            }
        }

        function unlockAdmin() {
            isAdminUnlocked = true;
            localStorage.setItem('adminUnlocked', 'true');
            
            document.getElementById('pinScreen').style.display = 'none';
            document.getElementById('dashboardContent').classList.remove('admin-locked');
            document.getElementById('dashboardContent').classList.add('admin-unlocked');
            document.getElementById('accessStatus').textContent = '✅ UNLOCKED';
            document.getElementById('accessStatus').className = 'text-emerald-400 font-semibold';
            
            // Re-enable delete buttons
            const buttons = document.querySelectorAll('.delete-btn');
            buttons.forEach(btn => btn.style.display = 'flex');
            
            showMessage('🔓 Admin unlocked successfully!', 'border-emerald-500 bg-emerald-100 text-emerald-800');
        }

        function updateDashboard() {
            const today = new Date().toISOString().split('T')[0];
            const todayBookings = reservations.filter(r => r.date === today);
            
            document.getElementById('totalBookings').textContent = reservations.length;
            document.getElementById('todayBookings').textContent = todayBookings.length;
            document.getElementById('availableSlots').textContent = 10 - todayBookings.length;
            
            const agencyCount = {};
            reservations.forEach(r => agencyCount[r.agency] = (agencyCount[r.agency] || 0) + 1);
            const topAgency = Object.entries(agencyCount).reduce((a, b) => a[1] > b[1] ? a : b, ['', 0])[0];
            document.getElementById('topAgency').textContent = topAgency || '-';

            const tbody = document.getElementById('reservationsTable');
            if (reservations.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" class="p-16 text-center text-gray-500"><i class="fas fa-calendar-check text-5xl mb-4 opacity-50"></i><div class="text-2xl font-semibold mt-2">No reservations yet</div></td></tr>';
                return;
            }

            tbody.innerHTML = reservations.map(r => {
                const timeDisplay = new Date(`2000-01-01T${r.timeSlot}:00`).toLocaleTimeString('en-US', {hour: 'numeric', minute: '2-digit', hour12: true}).toUpperCase();
                return `
                    <tr class="hover:bg-gray-50/50 transition-colors border-b border-white/20">
                        <td class="p-4 font-semibold text-white">
                            <div class="font-bold text-lg">${r.date}</div>
                            <div class="text-blue-300 text-sm">${timeDisplay}</div>
                        </td>
                        <td class="p-4">
                            <div class="font-bold text-white text-lg">${r.username}</div>
                        </td>
                        <td class="p-4">
                            <div class="text-gray-300">${r.bigoId}</div>
                            <div class="font-semibold text-yellow-400">LVL ${r.level}</div>
                        </td>
                        <td class="p-4 font-semibold text-white">${r.agency}</td>
                        <td class="p-4">
                            <div class="text-sm text-gray-300 truncate max-w-xs">${r.email}</div>
                        </td>
                        <td class="p-4">
                            <button class="delete-btn bg-red-500 hover:bg-red-600 text-white px-6 py-2 rounded-xl font-semibold text-sm shadow-md hover:shadow-red-400 transition-all flex items-center ${isAdminUnlocked ? '' : 'hidden'}">
                                <i class="fas fa-trash mr-2"></i>Delete
                            </button>
                        </td>
                    </tr>
                `;
            }).join('');

            document.getElementById('lastUpdate').textContent = new Date().toLocaleString();
        }

        function deleteReservation(id) {
            if (!isAdminUnlocked) {
                alert('🔒 Admin PIN required to delete');
                return;
            }
            if (confirm('Delete this reservation?')) {
                reservations = reservations.filter(r => r.id !== id);
                localStorage.setItem('cnOpkReservations', JSON.stringify(reservations));
                updateDashboard();
                updateTimeDropdown();
                showMessage('🗑️ Reservation deleted!', 'border-red-500 bg-red-100 text-red-800');
            }
        }

        window.deleteReservation = deleteReservation;
    </script>
</body>
</html>
