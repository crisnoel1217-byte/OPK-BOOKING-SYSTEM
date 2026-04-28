
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CN Bigo OPK - Admin Ready</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&family=Cinzel:wght@700&display=swap');
        .cn-logo { 
            font-family: 'Cinzel', serif; 
            background: linear-gradient(45deg, #000000 0%, #FFD700 50%, #000000 100%);
            -webkit-background-clip: text;
            background-clip: text;
            font-weight: 900;
            font-size: 2.5rem;
        }
        .glass { 
            background: rgba(255,255,255,0.1); 
            backdrop-filter: blur(20px); 
            border: 1px solid rgba(255,255,255,0.2);
        }
        body { 
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            font-family: 'Poppins', sans-serif;
        }
    </style>
</head>
<body class="min-h-screen py-12 px-4">
    <div class="max-w-6xl mx-auto space-y-12">
        
        <!-- HEADER WITH BIG ADMIN BUTTON -->
        <div class="glass rounded-3xl p-8 text-center shadow-2xl">
            <div class="flex flex-col lg:flex-row items-center justify-between gap-6">
                <div class="flex items-center space-x-4">
                    <div class="w-20 h-20 bg-gradient-to-r from-black to-yellow-500 rounded-2xl flex items-center justify-center shadow-2xl border-4 border-yellow-400">
                        <span class="cn-logo text-white font-bold tracking-wide drop-shadow-lg">CN</span>
                    </div>
                    <div>
                        <h1 class="text-4xl font-bold text-white">Bigo OPK Reservation</h1>
                        <p class="text-xl text-yellow-300">8PM - 10PM • 15min slots</p>
                    </div>
                </div>
                <button id="toggleAdmin" class="bg-gradient-to-r from-yellow-400 to-orange-500 text-black font-bold py-4 px-8 rounded-3xl text-xl shadow-2xl hover:shadow-yellow-500/50 hover:scale-105 transition-all duration-300 w-full lg:w-auto">
                    <i class="fas fa-crown mr-2"></i>👑 OPEN ADMIN PANEL
                </button>
            </div>
        </div>

        <!-- BOOKING FORM -->
        <div id="bookingForm" class="glass rounded-3xl p-8 lg:p-12 shadow-2xl max-w-4xl mx-auto">
            <h2 class="text-3xl font-bold text-white text-center mb-8">📅 Book Your Slot</h2>
            <form id="form" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                    <label class="block text-white font-semibold mb-2">👤 Bigo Name</label>
                    <input id="name" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white placeholder-white/60 focus:ring-4 focus:ring-yellow-400/50" placeholder="Username">
                </div>
                <div>
                    <label class="block text-white font-semibold mb-2">🆔 Bigo ID</label>
                    <input id="id" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white placeholder-white/60 focus:ring-4 focus:ring-yellow-400/50" placeholder="ID number">
                </div>
                <div>
                    <label class="block text-white font-semibold mb-2">⭐ Level</label>
                    <input id="level" type="number" min="1" max="100" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white placeholder-white/60 focus:ring-4 focus:ring-yellow-400/50" placeholder="50">
                </div>
                <div>
                    <label class="block text-white font-semibold mb-2">🏢 Agency</label>
                    <input id="agency" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white placeholder-white/60 focus:ring-4 focus:ring-yellow-400/50" placeholder="Agency name">
                </div>
                <div class="md:col-span-2">
                    <label class="block text-white font-semibold mb-2">📧 Gmail</label>
                    <input id="email" type="email" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white placeholder-white/60 focus:ring-4 focus:ring-yellow-400/50" placeholder="email@gmail.com">
                </div>
                <div class="md:col-span-2">
                    <label class="block text-white font-semibold mb-2">📅 Date</label>
                    <input id="date" type="date" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white focus:ring-4 focus:ring-yellow-400/50">
                </div>
                <div class="md:col-span-2">
                    <label class="block text-white font-semibold mb-2">⏰ Time (15min slots)</label>
                    <select id="time" required class="w-full p-4 rounded-2xl bg-white/20 border border-white/30 text-white focus:ring-4 focus:ring-yellow-400/50">
                        <option value="">Select 8PM-10PM slot</option>
                    </select>
                </div>
                <button type="submit" class="md:col-span-2 bg-gradient-to-r from-green-500 to-emerald-600 text-white font-bold py-5 px-8 rounded-3xl text-xl shadow-2xl hover:shadow-green-500/50 hover:scale-105 transition-all duration-300">
                    <i class="fas fa-check mr-2"></i>✅ BOOK SLOT
                </button>
            </form>
            <div id="status" class="mt-6 p-4 rounded-2xl font-bold text-center hidden"></div>
        </div>

        <!-- ADMIN SUMMARY - FULLY VISIBLE -->
        <div id="adminSummary" class="glass rounded-3xl p-8 lg:p-12 shadow-2xl hidden">
            <div class="flex justify-between items-center mb-8 pb-4 border-b border-white/30">
                <h2 class="text-3xl font-bold text-white flex items-center">
                    <i class="fas fa-crown text-yellow-400 mr-4 text-3xl"></i>
                    <span class="cn-logo">CN</span> OPK BOOKINGS SUMMARY
                </h2>
                <button id="closeAdmin" class="text-white text-2xl p-2 rounded-2xl hover:bg-white/20 transition-all">
                    <i class="fas fa-times"></i>
                </button>
            </div>

            <!-- STATS -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
                <div class="bg-white/10 p-6 rounded-2xl text-center">
                    <div class="text-4xl font-bold text-yellow-400" id="totalCount">0</div>
                    <div class="text-white text-lg">Total Bookings</div>
                </div>
                <div class="bg-white/10 p-6 rounded-2xl text-center">
                    <div class="text-4xl font-bold text-green-400" id="todayCount">0</div>
                    <div class="text-white text-lg">Today's Bookings</div>
                </div>
                <div class="bg-white/10 p-6 rounded-2xl text-center">
                    <div class="text-4xl font-bold text-blue-400" id="openSlots">10</div>
                    <div class="text-white text-lg">Open Slots Today</div>
                </div>
            </div>

            <!-- ALL BOOKINGS TABLE -->
            <div class="overflow-x-auto">
                <table class="w-full text-white">
                    <thead>
                        <tr class="border-b-4 border-yellow-400/50 bg-white/10">
                            <th class="p-4 text-left font-bold">Date & Time</th>
                            <th class="p-4 text-left font-bold">Bigo Name</th>
                            <th class="p-4 text-left font-bold">ID / LVL</th>
                            <th class="p-4 text-left font-bold">Agency</th>
                            <th class="p-4 text-left font-bold">Email</th>
                            <th class="p-4 text-left font-bold">Action</th>
                        </tr>
                    </thead>
                    <tbody id="bookingsTable">
                        <tr>
                            <td colspan="6" class="p-12 text-center text-white/50">
                                <i class="fas fa-list text-4xl mb-4"></i><br>
                                <strong>Click "OPEN ADMIN PANEL" to see bookings</strong>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <script>
        // Data storage
        let bookings = JSON.parse(localStorage.getItem('opkBookings')) || [];
        const slots = ['8:00PM','8:15PM','8:30PM','8:45PM','9:00PM','9:15PM','9:30PM','9:45PM','10:00PM','10:15PM'];

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            initDate();
            updateTimeSlots();
            updateSummary();
            
            document.getElementById('toggleAdmin').onclick = toggleAdminPanel;
            document.getElementById('closeAdmin').onclick = toggleAdminPanel;
            document.getElementById('form').onsubmit = bookSlot;
            document.getElementById('date').onchange = updateTimeSlots;
        });

        function initDate() {
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('date').min = today;
            document.getElementById('date').value = today;
        }

        function updateTimeSlots() {
            const date = document.getElementById('date').value;
            const select = document.getElementById('time');
            select.innerHTML = '<option value="">Select slot</option>';
            
            const dateBookings = bookings.filter(b => b.date === date);
            const bookedSlots = dateBookings.map(b => b.time);
            
            slots.forEach(slot => {
                const option = document.createElement('option');
                option.value = slot;
                option.textContent = bookedSlots.includes(slot) ? `${slot} ❌ TAKEN` : slot;
                if (bookedSlots.includes(slot)) option.disabled = true;
                select.appendChild(option);
            });
        }

        function bookSlot(e) {
            e.preventDefault();
            const booking = {
                name: document.getElementById('name').value,
                id: document.getElementById('id').value,
                level: document.getElementById('level').value,
                agency: document.getElementById('agency').value,
                email: document.getElementById('email').value,
                date: document.getElementById('date').value,
                time: document.getElementById('time').value,
                id: Date.now()
            };

            // Check if slot taken
            const conflict = bookings.find(b => b.date === booking.date && b.time === booking.time);
            if (conflict) {
                showStatus('❌ Slot already taken!', 'error');
                return;
            }

            bookings.push(booking);
            localStorage.setItem('opkBookings', JSON.stringify(bookings));
            
            showStatus('✅ Slot booked successfully!', 'success');
            e.target.reset();
            initDate();
            updateTimeSlots();
            updateSummary();
        }

        function showStatus(msg, type) {
            const status = document.getElementById('status');
            status.textContent = msg;
            status.className = `mt-6 p-4 rounded-2xl font-bold text-center ${type === 'success' ? 'bg-green-500/20 border-2 border-green-500 text-green-100' : 'bg-red-500/20 border-2 border-red-500 text-red-100'}`;
            status.classList.remove('hidden');
            setTimeout(() => status.classList.add('hidden'), 3000);
        }

        // ADMIN PANEL FUNCTIONS
        function toggleAdminPanel() {
            const admin = document.getElementById('adminSummary');
            const form = document.getElementById('bookingForm');
            
            if (admin.classList.contains('hidden')) {
                admin.classList.remove('hidden');
                form.classList.add('hidden');
                updateSummary();
                admin.scrollIntoView({behavior: 'smooth'});
            } else {
                admin.classList.add('hidden');
                form.classList.remove('hidden');
            }
        }

        function updateSummary() {
            const today = new Date().toISOString().split('T')[0];
            const todayBookings = bookings.filter(b => b.date === today);
            
            document.getElementById('totalCount').textContent = bookings.length;
            document.getElementById('todayCount').textContent = todayBookings.length;
            document.getElementById('openSlots').textContent = 10 - todayBookings.length;

            const tbody = document.getElementById('bookingsTable');
            if (bookings.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" class="p-8 text-center text-white/50">No bookings yet</td></tr>';
                return;
            }

            tbody.innerHTML = bookings.map(booking => `
                <tr class="border-b border-white/20 hover:bg-white/10">
                    <td class="p-4 font-bold">${booking.date}<br><span class="text-yellow-400">${booking.time}</span></td>
                    <td class="p-4 font-bold">${booking.name}</td>
                    <td class="p-4">${booking.id}<br><span class="text-yellow-400">LVL ${booking.level}</span></td>
                    <td class="p-4">${booking.agency}</td>
                    <td class="p-4">${booking.email}</td>
                    <td class="p-4">
                        <button onclick="deleteBooking(${booking.id})" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-xl font-bold text-sm transition-all">
                            <i class="fas fa-trash mr-1"></i>Delete
                        </button>
                    </td>
                </tr>
            `).join('');
        }

        function deleteBooking(id) {
            if (confirm('Delete this booking?')) {
                bookings = bookings.filter(b => b.id !== id);
                localStorage.setItem('opkBookings', JSON.stringify(bookings));
                updateSummary();
                updateTimeSlots();
                showStatus('🗑️ Booking deleted!', 'success');
            }
        }

        window.deleteBooking = deleteBooking;
    </script>
</body>
</html>
