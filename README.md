<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Transport Driver Assignment & Availability Dashboard</title>
<style>
  /* Reset */
  * {
    box-sizing: border-box;
  }
  body {
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
    margin: 0;
    background: #f4f7fa;
    color: #333;
  }
  header {
    background-color: #0d6efd;
    color: #fff;
    padding: 1rem 2rem;
    font-size: 1.5rem;
    font-weight: 700;
    box-shadow: 0 3px 6px rgba(0,0,0,0.1);
  }
  main {
    display: flex;
    min-height: calc(100vh - 64px);
  }
  nav {
    width: 220px;
    background-color: #0056b3;
    color: white;
    padding: 1rem 0;
    display: flex;
    flex-direction: column;
    gap: 1px;
  }
  nav button {
    background: none;
    border: none;
    color: #cfd9ff;
    padding: 12px 25px;
    text-align: left;
    font-size: 1rem;
    cursor: pointer;
    transition: background 0.3s, color 0.3s;
  }
  nav button.active, nav button:hover {
    background-color: #0d6efd;
    color: #fff;
    font-weight: 600;
  }
  section.content {
    flex-grow: 1;
    padding: 2rem;
    background-color: white;
    box-shadow: 0 3px 8px rgba(0,0,0,0.07);
    border-radius: 8px;
    margin: 1rem;
    overflow-y: auto;
  }
  h2 {
    margin-top: 0;
    margin-bottom: 1rem;
    border-bottom: 2px solid #0d6efd;
    padding-bottom: 0.25rem;
    color: #0d6efd;
  }
  /* Overview Cards */
  .overview-cards {
    display: grid;
    grid-template-columns: repeat(auto-fit,minmax(180px,1fr));
    gap: 1rem 1.5rem;
    margin-bottom: 2rem;
  }
  .card {
    background: #e7f1ff;
    border-radius: 8px;
    padding: 1.25rem;
    text-align: center;
    box-shadow: inset 0 0 20px #d0e6ff;
    font-weight: 600;
    font-size: 1.25rem;
    color: #0056b3;
  }
  .card .label {
    font-weight: 400;
    font-size: 0.9rem;
    margin-top: 0.25rem;
    color: #3a5276;
  }
  /* Forms */
  form {
    margin-bottom: 2rem;
    max-width: 700px;
  }
  form > div {
    display: flex;
    gap: 1rem;
    margin-bottom: 1rem;
    flex-wrap: wrap;
  }
  label {
    flex: 1 0 130px;
    font-weight: 600;
    align-self: center;
  }
  select, input[type="text"], input[type="datetime-local"], input[type="date"] {
    flex: 2 0 220px;
    padding: 0.5rem;
    border-radius: 5px;
    border: 1.5px solid #ccc;
    font-size: 1rem;
    transition: border-color 0.3s;
  }
  select:focus, input[type="datetime-local"]:focus, input[type="date"]:focus, input[type="text"]:focus {
    border-color: #0d6efd;
    outline: none;
  }
  button {
    background-color: #0d6efd;
    color: white;
    border: none;
    padding: 0.65rem 1.5rem;
    border-radius: 5px;
    font-weight: 700;
    cursor: pointer;
    box-shadow: 0 3px 6px rgb(13 110 253 / 0.5);
    transition: background-color 0.3s ease;
  }
  button:hover {
    background-color: #0047d4;
  }
  /* Tables */
  table {
    border-collapse: collapse;
    width: 100%;
    margin-bottom: 2rem;
  }
  th, td {
    border: 1px solid #d1d9e6;
    padding: 10px;
    text-align: left;
    font-size: 0.9rem;
  }
  th {
    background-color: #e5f0ff;
    color: #0056b3;
    font-weight: 700;
  }
  tbody tr:nth-child(even) {
    background-color: #f9fbff;
  }
  .btn-delete {
    background-color: #dc3545;
    padding: 0.3rem 0.7rem;
    border-radius: 4px;
    color: white;
    font-weight: 600;
    cursor: pointer;
    border: none;
    transition: background-color 0.3s ease;
  }
  .btn-delete:hover {
    background-color: #a71d2a;
  }
  /* Utilization display */
  .util-box {
    max-width: 700px;
    margin-bottom: 1rem;
  }
  /* Responsive tweaks */
  @media (max-width: 768px) {
    main {
      flex-direction: column;
    }
    nav {
      width: 100%;
      display: flex;
      flex-wrap: wrap;
      gap: 5px;
      justify-content: space-around;
      background-color: #0d6efd;
    }
    nav button {
      flex: 1 1 auto;
      border-radius: 5px;
      margin: 4px 0;
      text-align: center;
    }
    section.content {
      margin: 0.5rem;
      border-radius: 0;
      box-shadow: none;
      padding: 1rem;
    }
    form > div {
      flex-direction: column;
    }
    label, select, input[type="datetime-local"], input[type="date"], input[type="text"] {
      flex: 1 0 auto;
      width: 100%;
    }
  }
</style>
<!-- Chart.js CDN -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
<header>Transport Driver Assignment & Availability Dashboard</header>
<main>
  <nav>
    <button class="active" data-section="dashboard">Dashboard</button>
    <button data-section="assignments">Assignments</button>
    <button data-section="availability">Availability</button>
    <button data-section="utilization">Utilization</button>
    <button data-section="settings">Settings</button>
  </nav>

  <section class="content" id="dashboard">
    <h2>Dashboard Overview</h2>
    <div class="overview-cards">
      <div class="card">
        1
        <div class="label">Total Drivers</div>
      </div>
      <div class="card">
        1
        <div class="label">Total Vehicles</div>
      </div>
      <div class="card">
        1
        <div class="label">Active Assignments</div>
      </div>
      <div class="card">
        1
        <div class="label">Available Drivers</div>
      </div>
      <div class="card">
        5
        <div class="label">Vehicles Due for Maintenance</div>
      </div>
    </div>
  </section>

  <section class="content" id="assignments" hidden>
    <h2>Driver & Vehicle Assignments</h2>
    <form id="assignment-form">
      <div>
        <label for="assign-driver">Select Driver</label>
        <select id="assign-driver" required>
          <option value="" disabled selected>Select a driver</option>
        </select>
      </div>
      <div>
        <label for="assign-vehicle">Select Vehicle</label>
        <select id="assign-vehicle" required>
          <option value="" disabled selected>Select a vehicle</option>
        </select>
      </div>
      <div>
        <label for="route-select">Select Route</label>
        <select id="route-select" required>
          <option value="" disabled selected>Select a route</option>
        </select>
      </div>
      <div>
        <label for="journey-start">Journey Start Date & Time</label>
        <input type="datetime-local" id="journey-start" required />
      </div>
      <div>
        <label for="expected-arrival">Estimated Arrival Date & Time</label>
        <input type="datetime-local" id="expected-arrival" readonly placeholder="Auto-calculated" />
      </div>
      <div>
        <label>Status</label>
        <input type="text" value="Scheduled" disabled />
      </div>
      <div style="flex:1 0 100%; text-align:right;">
        <button type="submit">Add Assignment</button>
      </div>
    </form>

    <table id="assignment-table" aria-label="Driver and Vehicle Assignments">
      <thead>
        <tr>
          <th>Driver</th>
          <th>Vehicle</th>
          <th>Route</th>
          <th>Journey Start</th>
          <th>Expected Arrival</th>
          <th>Status</th>
          <th>Delete</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </section>

  <section class="content" id="availability" hidden>
    <h2>Driver Availability</h2>
    <form id="availability-form">
      <div>
        <label for="availability-driver">Select Driver</label>
        <select id="availability-driver" required>
          <option value="" disabled selected>Select a driver</option>
        </select>
      </div>
      <div>
        <label for="availability-date">Date</label>
        <input type="date" id="availability-date" required />
      </div>
      <div>
        <label for="availability-status">Availability Status</label>
        <select id="availability-status" required>
          <option value="" disabled selected>Select status</option>
          <option value="Available">Available</option>
          <option value="On Leave">On Leave</option>
          <option value="Unavailable">Unavailable</option>
        </select>
      </div>
      <div style="flex:1 0 100%; text-align:right;">
        <button type="submit">Update Availability</button>
      </div>
    </form>

    <table id="availability-table" aria-label="Driver Availability">
      <thead>
        <tr>
          <th>Date</th>
          <th>Driver</th>
          <th>Status</th>
          <th>Delete</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </section>

  <section class="content" id="utilization" hidden>
    <h2>Vehicle-wise Utilization (24 hrs %)</h2>
    <div class="util-box">
      <canvas id="utilChart" style="max-width: 700px; height: 300px;"></canvas>
    </div>
    <p style="margin-top: 1rem; color: #555;">
      * Chart displays vehicle utilization percentage of 24 hours (running time).
    </p>
  </section>

  <section class="content" id="settings" hidden>
    <h2>Settings</h2>
    <p>Manage drivers, vehicles, and other configurations here.</p>
    <hr />
    <form id="settings-driver-form">
      <h3>Add New Driver</h3>
      <div>
        <label for="new-driver-name">Driver Name</label>
        <input type="text" id="new-driver-name" placeholder="Enter driver name" />
      </div>
      <div style="flex:1 0 100%; text-align:right; margin-bottom: 1rem;">
        <button type="submit">Add Driver</button>
      </div>
    </form>

    <form id="settings-vehicle-form">
      <h3>Add New Vehicle</h3>
      <div>
        <label for="new-vehicle-name">Vehicle Name</label>
        <input type="text" id="new-vehicle-name" placeholder="Enter vehicle name" />
      </div>
      <div style="flex:1 0 100%; text-align:right;">
        <button type="submit">Add Vehicle</button>
      </div>
    </form>

    <h3>Current Drivers</h3>
    <ul id="driver-list" style="list-style:none; padding-left:0; max-width: 400px;"></ul>

    <h3>Current Vehicles</h3>
    <ul id="vehicle-list" style="list-style:none; padding-left:0; max-width: 400px;"></ul>
  </section>
</main>

<script>
  // Data storage in localStorage for persistence
  let drivers = JSON.parse(localStorage.getItem('drivers')) || ['Lisa Wong', 'Carlos Diaz', 'John Smith', 'Maria Garcia'];
  let vehicles = JSON.parse(localStorage.getItem('vehicles')) || ['Truck #12'];
  // routes now with fixed distance (kilometers) and speed (km/h)
  let routes = JSON.parse(localStorage.getItem('routes')) || [
    { name: 'Route A - City to Town', distanceKm: 600, speedKmh: 60 }, // duration 10h
    { name: 'Route B - City to Airport', distanceKm: 180, speedKmh: 60 }, // 3h
    { name: 'Route C - Town to Village', distanceKm: 240, speedKmh: 60 } // 4h
  ];
  let assignments = JSON.parse(localStorage.getItem('assignments')) || [
    { driver: 'Lisa Wong', vehicle: 'Truck #12', route: 'Route A - City to Town', journeyStart: '2024-06-15T08:00', expectedArrival: '2024-06-15T18:00', status: 'Active' }
  ];
  let availability = JSON.parse(localStorage.getItem('availability')) || [
    { date: '2024-06-15', driver: 'John Smith', status: 'Available' },
    { date: '2024-06-16', driver: 'Maria Garcia', status: 'On Leave' }
  ];

  function saveData() {
    localStorage.setItem('drivers', JSON.stringify(drivers));
    localStorage.setItem('vehicles', JSON.stringify(vehicles));
    localStorage.setItem('routes', JSON.stringify(routes));
    localStorage.setItem('assignments', JSON.stringify(assignments));
    localStorage.setItem('availability', JSON.stringify(availability));
  }

  // Navigation buttons
  const navButtons = document.querySelectorAll('nav button');
  const sections = document.querySelectorAll('section.content');
  navButtons.forEach(btn => {
    btn.addEventListener('click', () => {
      navButtons.forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      const target = btn.getAttribute('data-section');
      sections.forEach(s => s.hidden = s.id !== target);
      if (target === 'utilization') updateUtilizationChart();
    });
  });

  // Populate dropdowns in forms
  function populateDropdowns() {
    const assignDriver = document.getElementById('assign-driver');
    const assignVehicle = document.getElementById('assign-vehicle');
    const availabilityDriver = document.getElementById('availability-driver');
    const routeSelect = document.getElementById('route-select');

    assignDriver.innerHTML = `<option value="" disabled selected>Select a driver</option>` +
      drivers.map(d => `<option value="${d}">${d}</option>`).join('');
    assignVehicle.innerHTML = `<option value="" disabled selected>Select a vehicle</option>` +
      vehicles.map(v => `<option value="${v}">${v}</option>`).join('');
    availabilityDriver.innerHTML = `<option value="" disabled selected>Select a driver</option>` +
      drivers.map(d => `<option value="${d}">${d}</option>`).join('');
    routeSelect.innerHTML = `<option value="" disabled selected>Select a route</option>` +
      routes.map(r => `<option value="${r.name}">${r.name} (${r.distanceKm} km)</option>`).join('');
  }
  populateDropdowns();

  // Format datetime-local string to readable format dd/mm/yyyy hh:mm AM/PM
  function formatDateTime(dt) {
    const d = new Date(dt);
    if (isNaN(d)) return dt;
    const date = d.toLocaleDateString('en-GB');
    let hours = d.getHours();
    const minutes = d.getMinutes().toString().padStart(2,'0');
    const ampm = hours >= 12 ? 'PM' : 'AM';
    hours = hours % 12 || 12;
    return `${date} ${hours}:${minutes} ${ampm}`;
  }

  // Render assignments table
  const assignmentTableBody = document.querySelector('#assignment-table tbody');
  function renderAssignments() {
    assignmentTableBody.innerHTML = assignments.map((a, i) => `
      <tr>
        <td>${a.driver}</td>
        <td>${a.vehicle}</td>
        <td>${a.route || ''}</td>
        <td>${formatDateTime(a.journeyStart)}</td>
        <td>${formatDateTime(a.expectedArrival)}</td>
        <td>${a.status}</td>
        <td><button class="btn-delete" data-index="${i}">Delete</button></td>
      </tr>
    `).join('');
  }
  renderAssignments();

  // Render availability table
  const availabilityTableBody = document.querySelector('#availability-table tbody');
  function renderAvailability() {
    availabilityTableBody.innerHTML = availability.map((a, i) => `
      <tr>
        <td>${a.date}</td>
        <td>${a.driver}</td>
        <td>${a.status}</td>
        <td><button class="btn-delete" data-index="${i}">Delete</button></td>
      </tr>
    `).join('');
  }
  renderAvailability();

  // Render current drivers and vehicles in settings
  const driverList = document.getElementById('driver-list');
  const vehicleList = document.getElementById('vehicle-list');
  function renderSettingsLists() {
    driverList.innerHTML = drivers.map((d,i) => `<li>${d} <button class="btn-delete" data-index="${i}" data-type="driver">Delete</button></li>`).join('');
    vehicleList.innerHTML = vehicles.map((v,i) => `<li>${v} <button class="btn-delete" data-index="${i}" data-type="vehicle">Delete</button></li>`).join('');
  }
  renderSettingsLists();

  // Calculate expected arrival based on journey start and route distance and speed
  function calculateExpectedArrival() {
    const journeyStartInput = document.getElementById('journey-start');
    const routeSelect = document.getElementById('route-select');
    const expectedArrivalInput = document.getElementById('expected-arrival');
    const journeyStartVal = journeyStartInput.value;
    const routeName = routeSelect.value;
    if (!journeyStartVal || !routeName) {
      expectedArrivalInput.value = '';
      return;
    }
    const route = routes.find(r => r.name === routeName);
    if (!route) {
      expectedArrivalInput.value = '';
      return;
    }
    const startDate = new Date(journeyStartVal);
    if (isNaN(startDate)) {
      expectedArrivalInput.value = '';
      return;
    }
    // duration in milliseconds = distance/speed * 3600000 ms
    const durationMs = (route.distanceKm / route.speedKmh) * 3600000;
    const arrivalDate = new Date(startDate.getTime() + durationMs);
    expectedArrivalInput.value = arrivalDate.toISOString().slice(0,16);
  }

  // Listen to changes on journey start or route to recalc expected arrival
  document.getElementById('journey-start').addEventListener('change', calculateExpectedArrival);
  document.getElementById('route-select').addEventListener('change', calculateExpectedArrival);

  // Add Assignment
  document.getElementById('assignment-form').addEventListener('submit', e => {
    e.preventDefault();
    const driver = e.target['assign-driver'].value;
    const vehicle = e.target['assign-vehicle'].value;
    const journeyStart = e.target['journey-start'].value;
    const expectedArrival = e.target['expected-arrival'].value;
    const routeName = e.target['route-select'].value;
    if (!driver || !vehicle || !journeyStart || !expectedArrival || !routeName) return alert("Please fill all fields!");
    assignments.push({ driver, vehicle, route: routeName, journeyStart, expectedArrival, status: 'Scheduled' });
    saveData();
    renderAssignments();
    clearForm(e.target);
    updateDashboardCards();
    updateUtilizationChart();
  });

  // Delete Assignment
  assignmentTableBody.addEventListener('click', e => {
    if (!e.target.classList.contains('btn-delete')) return;
    const idx = parseInt(e.target.getAttribute('data-index'));
    if (isNaN(idx)) return;
    assignments.splice(idx, 1);
    saveData();
    renderAssignments();
    updateDashboardCards();
    updateUtilizationChart();
  });

  // Update Availability
  document.getElementById('availability-form').addEventListener('submit', e => {
    e.preventDefault();
    const driver = e.target['availability-driver'].value;
    const date = e.target['availability-date'].value;
    const status = e.target['availability-status'].value;
    if (!driver || !date || !status) return alert("Please fill all availability fields!");
    availability.push({ driver, date, status });
    saveData();
    renderAvailability();
    clearForm(e.target);
    updateDashboardCards();
  });

  // Delete Availability
  availabilityTableBody.addEventListener('click', e => {
    if (!e.target.classList.contains('btn-delete')) return;
    const idx = parseInt(e.target.getAttribute('data-index'));
    if (isNaN(idx)) return;
    availability.splice(idx,1);
    saveData();
    renderAvailability();
    updateDashboardCards();
  });

  // Add Driver in Settings
  document.getElementById('settings-driver-form').addEventListener('submit', e => {
    e.preventDefault();
    const nameInput = e.target['new-driver-name'];
    const name = nameInput.value.trim();
    if (!name) return alert("Driver name cannot be empty");
    if (drivers.includes(name)) return alert('Driver already exists.');
    drivers.push(name);
    saveData();
    populateDropdowns();
    renderSettingsLists();
    nameInput.value = '';
    updateDashboardCards();
  });

  // Add Vehicle in Settings
  document.getElementById('settings-vehicle-form').addEventListener('submit', e => {
    e.preventDefault();
    const nameInput = e.target['new-vehicle-name'];
    const name = nameInput.value.trim();
    if (!name) return alert("Vehicle name cannot be empty");
    if (vehicles.includes(name)) return alert('Vehicle already exists.');
    vehicles.push(name);
    saveData();
    populateDropdowns();
    renderSettingsLists();
    nameInput.value = '';
    updateDashboardCards();
  });

  // Delete Driver or Vehicle from Settings
  driverList.addEventListener('click', e => {
    if (!e.target.classList.contains('btn-delete')) return;
    const idx = parseInt(e.target.getAttribute('data-index'));
    if (isNaN(idx)) return;
    const driverName = drivers[idx];
    drivers.splice(idx,1);
    assignments = assignments.filter(a => a.driver !== driverName);
    availability = availability.filter(av => av.driver !== driverName);
    saveData();
    populateDropdowns();
    renderAssignments();
    renderAvailability();
    renderSettingsLists();
    updateDashboardCards();
    updateUtilizationChart();
  });

  vehicleList.addEventListener('click', e => {
    if (!e.target.classList.contains('btn-delete')) return;
    const idx = parseInt(e.target.getAttribute('data-index'));
    if (isNaN(idx)) return;
    const vehicleName = vehicles[idx];
    vehicles.splice(idx,1);
    assignments = assignments.filter(a => a.vehicle !== vehicleName);
    saveData();
    populateDropdowns();
    renderAssignments();
    renderSettingsLists();
    updateDashboardCards();
    updateUtilizationChart();
  });

  // Clear form inputs
  function clearForm(form) {
    form.reset();
    if (form.id === 'assignment-form') {
      document.getElementById('expected-arrival').value = '';
    }
  }

  // Update overview dashboard cards metrics
  function updateDashboardCards() {
    // Total Drivers
    document.querySelector('.overview-cards .card:nth-child(1)').innerHTML = drivers.length + '<div class="label">Total Drivers</div>';
    // Total Vehicles
    document.querySelector('.overview-cards .card:nth-child(2)').innerHTML = vehicles.length + '<div class="label">Total Vehicles</div>';
    // Active Assignments (Scheduled or Active considered)
    const activeCount = assignments.filter(a => a.status && (a.status.toLowerCase() === 'active' || a.status.toLowerCase() === 'scheduled')).length;
    document.querySelector('.overview-cards .card:nth-child(3)').innerHTML = activeCount + '<div class="label">Active Assignments</div>';
    // Available Drivers roughly = total drivers - drivers with active assignment now
    const now = new Date();
    const busyDrivers = assignments.filter(a => {
      const start = new Date(a.journeyStart);
      const end = new Date(a.expectedArrival);
      return now >= start && now <= end;
    }).map(a => a.driver);
    const availableCount = drivers.filter(d => !busyDrivers.includes(d)).length;
    document.querySelector('.overview-cards .card:nth-child(4)').innerHTML = availableCount + '<div class="label">Available Drivers</div>';
    // Vehicles due for maintenance remain mocked as 5
    document.querySelector('.overview-cards .card:nth-child(5)').innerHTML = '5<div class="label">Vehicles Due for Maintenance</div>';
  }
  updateDashboardCards();

  // UTILIZATION CHART - vehicle-wise utilization % of 24h
  const ctx = document.getElementById('utilChart').getContext('2d');
  let utilizationChart = null;

  // Calculate total running hours per vehicle over all assignments
  function getUtilizationData() {
    const durationHours = (startStr, endStr) => (new Date(endStr) - new Date(startStr)) / (1000*3600);

    // Sum duration per vehicle
    const durations = {};
    vehicles.forEach(v => durations[v] = 0);
    assignments.forEach(a => {
      if (durations[a.vehicle] !== undefined) {
        durations[a.vehicle] += durationHours(a.journeyStart, a.expectedArrival);
      }
    });

    // convert to percentage of 24h (capping at 100%)
    const percentages = vehicles.map(v => {
      const pct = durations[v] ? Math.min(100, (durations[v]/24)*100) : 0;
      return pct.toFixed(1);
    });

    return {
      labels: vehicles,
      datasets: [{
        label: 'Utilization % (24h)',
        data: percentages,
        backgroundColor: 'rgba(13, 110, 253, 0.7)',
        borderColor: '#084298',
        borderWidth: 1,
        borderRadius: 4,
      }]
    };
  }

  // Create or update utilization chart
  function updateUtilizationChart() {
    const data = getUtilizationData();
    if (utilizationChart) {
      utilizationChart.data = data;
      utilizationChart.update();
    } else {
      utilizationChart = new Chart(ctx, {
        type: 'bar',
        data: data,
        options: {
          scales: {
            y: {
              beginAtZero: true,
              max: 100,
              ticks: {
                callback: val => val + '%'
              },
              title: {
                display: true,
                text: 'Utilization (%)'
              }
            }
          },
          plugins: {
            legend: { display: false },
            tooltip: {
              callbacks: {
                label: ctx => ctx.parsed.y + '%'
              }
            }
          },
          responsive: true,
          maintainAspectRatio: false,
          animation: {
            duration: 500
          }
        }
      });
    }
  }
  updateUtilizationChart();

</script>
</body>
</html>


