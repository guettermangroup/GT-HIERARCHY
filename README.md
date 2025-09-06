

<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Team Hierarchy Management System</title>

    <script src="https://cdn.tailwindcss.com"></script>

    <style>

        .neon-green { color: #39ff14; }

        .bg-neon-green { background-color: #39ff14; }

        .border-neon-green { border-color: #39ff14; }

        .hover-neon-green:hover { background-color: #39ff14; }

        .glow { box-shadow: 0 0 10px #39ff14; }

        .hierarchy-line {

            position: absolute;

            background-color: #39ff14;

            z-index: 1;

        }

        .employee-card {

            position: relative;

            z-index: 2;

        }

        .page { display: none; }

        .page.active { display: block; }

    </style>

</head>

<body class="bg-black text-white min-h-screen">

    <!-- Navigation -->

    <nav class="bg-gray-900 border-b border-gray-700 p-4">

        <div class="max-w-7xl mx-auto flex justify-between items-center">

            <h1 class="text-2xl font-bold neon-green">Team Hierarchy System</h1>

            <div class="space-x-4">

                <button id="adminTab" class="px-4 py-2 rounded-lg bg-neon-green text-black font-semibold">Admin Panel</button>

                <button id="displayTab" class="px-4 py-2 rounded-lg border border-neon-green text-neon-green hover:bg-neon-green hover:text-black transition-colors">Display Page</button>

            </div>

        </div>

    </nav>

 

    <!-- Admin Page -->

    <div id="adminPage" class="page active p-6">

        <div class="max-w-7xl mx-auto">

            <!-- Admin Header -->

            <div class="text-center mb-8">

                <h2 class="text-3xl font-bold neon-green mb-4">Admin Control Panel</h2>

                <p class="text-gray-300">Manage your team hierarchy data</p>

            </div>

 

            <!-- Upload Section -->

            <div class="bg-gray-900 rounded-lg p-8 mb-8 border border-gray-700">

                <h3 class="text-xl font-semibold neon-green mb-6">Upload Team Data</h3>

                <div class="flex flex-col items-center">

                    <label for="csvFile" class="bg-neon-green text-black px-8 py-4 rounded-lg font-semibold cursor-pointer hover:bg-green-400 transition-colors mb-6 text-lg">

                        📁 Choose CSV File

                    </label>

                    <input type="file" id="csvFile" accept=".csv" class="hidden">

                    <p class="text-sm text-gray-400 mb-4">CSV format: Agent ID, Name, Role, Direct To, Manager ID, Phone, Picture</p>

                    <button id="loadSample" class="text-neon-green hover:underline mb-4">Load Sample Data for Testing</button>

                    <button id="clearData" class="text-red-400 hover:underline">Clear All Data</button>

                </div>

            </div>

 

            <!-- Data Status -->

            <div class="bg-gray-900 rounded-lg p-6 mb-8 border border-gray-700">

                <h3 class="text-xl font-semibold neon-green mb-4">Data Status</h3>

                <div id="dataStatus" class="text-gray-400">

                    Loading...

                </div>

            </div>

 

            <!-- CSV Format Instructions -->

            <div class="bg-gray-900 rounded-lg p-6 border border-gray-700">

                <h3 class="text-xl font-semibold neon-green mb-4">CSV Format Instructions</h3>

                <div class="text-gray-300 space-y-3">

                    <p><strong>Required Columns (in order):</strong></p>

                    <ul class="list-disc list-inside ml-4 space-y-1">

                        <li><strong>Agent ID:</strong> Unique identifier for each employee</li>

                        <li><strong>Name:</strong> Full name of the employee</li>

                        <li><strong>Role:</strong> Job title or position</li>

                        <li><strong>Direct To:</strong> Name of the person they report to</li>

                        <li><strong>Manager ID:</strong> Agent ID of their manager</li>

                        <li><strong>Phone:</strong> Contact phone number</li>

                        <li><strong>Picture:</strong> URL to profile picture (optional)</li>

                    </ul>

                    <p><strong>Example CSV content:</strong></p>

                    <div class="bg-black p-4 rounded mt-3 font-mono text-sm overflow-x-auto">

                        001,John Smith,CEO,,000,555-0101,https://example.com/john.jpg<br>

                        002,Jane Doe,CTO,John Smith,001,555-0102,https://example.com/jane.jpg<br>

                        003,Mike Johnson,Developer,Jane Doe,002,555-0103,

                    </div>

                    <p class="text-sm text-gray-400">💡 Leave Manager ID empty for top-level positions. Picture URLs are optional.</p>

                    <p class="text-sm text-neon-green mt-4">✨ Data automatically saves and syncs between tabs!</p>

                </div>

            </div>

        </div>

    </div>

 

    <!-- Display Page -->

    <div id="displayPage" class="page p-6">

        <div class="max-w-7xl mx-auto">

            <!-- Display Header -->

            <div class="text-center mb-8">

                <h2 class="text-4xl font-bold neon-green mb-4">Team Hierarchy</h2>

                <p class="text-gray-300">Our organizational structure</p>

            </div>

 

            <!-- Hierarchy Chart -->

            <div id="chartContainer" class="relative bg-gray-900 rounded-lg p-8 min-h-96 border border-gray-700">

                <div id="noData" class="text-center text-gray-400 py-20">

                    <svg class="mx-auto mb-4 w-16 h-16 text-gray-600" fill="currentColor" viewBox="0 0 20 20">

                        <path d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"></path>

                    </svg>

                    <p class="text-lg">No team data available</p>

                    <p class="text-sm mt-2">Please upload data through the admin panel</p>

                </div>

                <div id="hierarchyChart" class="hidden"></div>

            </div>

        </div>

    </div>

 

    <script>

        let hierarchyData = [];

       

        // Sample data

        const sampleData = [

            { agentId: "001", name: "Sarah Wilson", role: "CEO", directTo: "", managerId: "", phone: "555-0101", picture: "" },

            { agentId: "002", name: "David Chen", role: "CTO", directTo: "Sarah Wilson", managerId: "001", phone: "555-0102", picture: "" },

            { agentId: "003", name: "Lisa Rodriguez", role: "CFO", directTo: "Sarah Wilson", managerId: "001", phone: "555-0103", picture: "" },

            { agentId: "004", name: "Mark Thompson", role: "VP Marketing", directTo: "Sarah Wilson", managerId: "001", phone: "555-0104", picture: "" },

            { agentId: "005", name: "Alex Kim", role: "Senior Developer", directTo: "David Chen", managerId: "002", phone: "555-0105", picture: "" },

            { agentId: "007", name: "Ryan Foster", role: "Financial Analyst", directTo: "Lisa Rodriguez", managerId: "003", phone: "555-0107", picture: "" },

            { agentId: "008", name: "Sophie Turner", role: "Marketing Manager", directTo: "Mark Thompson", managerId: "004", phone: "555-0108", picture: "" },

            { agentId: "009", name: "James Wilson", role: "Junior Developer", directTo: "Alex Kim", managerId: "005", phone: "555-0109", picture: "" },

            { agentId: "010", name: "Maya Patel", role: "Content Specialist", directTo: "Sophie Turner", managerId: "008", phone: "555-0110", picture: "" }

        ];

 

        // Load data from localStorage on page load

        function loadStoredData() {

            const stored = localStorage.getItem('hierarchyData');

            if (stored) {

                try {

                    hierarchyData = JSON.parse(stored);

                } catch (e) {

                    console.error('Error loading stored data:', e);

                    hierarchyData = [];

                }

            }

            updateDataStatus();

            renderHierarchy();

        }

 

        // Save data to localStorage

        function saveData() {

            localStorage.setItem('hierarchyData', JSON.stringify(hierarchyData));

            localStorage.setItem('hierarchyDataTimestamp', new Date().toISOString());

            updateDataStatus();

            renderHierarchy(); // Auto-refresh display

        }

 

        // Navigation

        document.getElementById('adminTab').addEventListener('click', function() {

            showPage('admin');

        });

 

        document.getElementById('displayTab').addEventListener('click', function() {

            showPage('display');

        });

 

        function showPage(page) {

            // Hide all pages

            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));

           

            // Show selected page

            if (page === 'admin') {

                document.getElementById('adminPage').classList.add('active');

                document.getElementById('adminTab').className = 'px-4 py-2 rounded-lg bg-neon-green text-black font-semibold';

                document.getElementById('displayTab').className = 'px-4 py-2 rounded-lg border border-neon-green text-neon-green hover:bg-neon-green hover:text-black transition-colors';

            } else {

                document.getElementById('displayPage').classList.add('active');

                document.getElementById('displayTab').className = 'px-4 py-2 rounded-lg bg-neon-green text-black font-semibold';

                document.getElementById('adminTab').className = 'px-4 py-2 rounded-lg border border-neon-green text-neon-green hover:bg-neon-green hover:text-black transition-colors';

                renderHierarchy(); // Refresh display when switching to display page

            }

        }

 

        // File upload handler

        document.getElementById('csvFile').addEventListener('change', function(e) {

            const file = e.target.files[0];

            if (file) {

                const reader = new FileReader();

                reader.onload = function(e) {

                    const csv = e.target.result;

                    parseCSV(csv);

                };

                reader.readAsText(file);

            }

        });

 

        // Load sample data

        document.getElementById('loadSample').addEventListener('click', function() {

            hierarchyData = [...sampleData];

            saveData();

            alert('Sample data loaded successfully!');

        });

 

        // Clear data

        document.getElementById('clearData').addEventListener('click', function() {

            if (confirm('Are you sure you want to clear all data?')) {

                hierarchyData = [];

                saveData();

                alert('All data cleared successfully!');

            }

        });

 

        // Parse CSV data

        function parseCSV(csv) {

            const lines = csv.trim().split('\n');

            hierarchyData = [];

           

            for (let i = 0; i < lines.length; i++) {

                const line = lines[i].trim();

                if (line) {

                    const [agentId, name, role, directTo, managerId, phone, picture] = line.split(',').map(item => item.trim());

                    if (agentId && name && role) {

                        hierarchyData.push({

                            agentId: agentId,

                            name: name,

                            role: role,

                            directTo: directTo || "",

                            managerId: managerId || "",

                            phone: phone || "",

                            picture: picture || ""

                        });

                    }

                }

            }

           

            if (hierarchyData.length > 0) {

                saveData();

                alert(`Successfully uploaded ${hierarchyData.length} employee records!`);

            } else {

                alert('No valid data found in CSV file. Please check the format.');

            }

        }

 

        // Update data status

        function updateDataStatus() {

            const statusDiv = document.getElementById('dataStatus');

            if (hierarchyData.length === 0) {

                statusDiv.innerHTML = '<span class="text-red-400">❌ No data uploaded yet</span>';

            } else {

                const timestamp = localStorage.getItem('hierarchyDataTimestamp');

                const lastUpdated = timestamp ? new Date(timestamp).toLocaleString() : 'Unknown';

                statusDiv.innerHTML = `

                    <div class="text-neon-green">✅ Data loaded successfully</div>

                    <div class="mt-2 text-sm">

                        <span class="text-gray-300">Total employees: <strong>${hierarchyData.length}</strong></span><br>

                        <span class="text-gray-300">Last updated: <strong>${lastUpdated}</strong></span><br>

                        <span class="text-gray-300">Status: <strong class="text-neon-green">Saved & Ready</strong></span>

                    </div>

                `;

            }

        }

 

        // Build hierarchy tree

        function buildHierarchyTree(data) {

            const tree = {};

            const employees = {};

            const employeesByName = {};

           

            // Create employee objects

            data.forEach(emp => {

                employees[emp.agentId] = {

                    ...emp,

                    children: []

                };

                employeesByName[emp.name] = employees[emp.agentId];

            });

           

            // Build tree structure

            data.forEach(emp => {

                if (!emp.managerId || emp.managerId === "") {

                    tree[emp.agentId] = employees[emp.agentId];

                } else if (employees[emp.managerId]) {

                    employees[emp.managerId].children.push(employees[emp.agentId]);

                } else if (emp.directTo && employeesByName[emp.directTo]) {

                    employeesByName[emp.directTo].children.push(employees[emp.agentId]);

                }

            });

           

            return tree;

        }

 

        // Render hierarchy

        function renderHierarchy() {

            const tree = buildHierarchyTree(hierarchyData);

            const chartContainer = document.getElementById('hierarchyChart');

            const noData = document.getElementById('noData');

           

            if (hierarchyData.length === 0) {

                noData.classList.remove('hidden');

                chartContainer.classList.add('hidden');

                return;

            }

           

            noData.classList.add('hidden');

            chartContainer.classList.remove('hidden');

            chartContainer.innerHTML = '';

           

            // Render each top-level employee

            Object.values(tree).forEach((employee, index) => {

                const employeeElement = renderEmployee(employee, 0, index);

                chartContainer.appendChild(employeeElement);

            });

        }

 

        // Render individual employee card

        function renderEmployee(employee, level, index) {

            const container = document.createElement('div');

            container.className = 'mb-10';

           

            // Employee card

            const card = document.createElement('div');

            card.className = `employee-card bg-gray-800 border-2 border-neon-green rounded-lg p-4 cursor-pointer hover:glow transition-all duration-300 inline-block min-w-80`;

            card.style.marginLeft = `${level * 60}px`;

           

            // Card content

            card.innerHTML = `

                <div class="flex items-center justify-between">

                    <div class="flex items-center space-x-4">

                        ${employee.picture && employee.picture !== '' ? `

                            <img src="${employee.picture}" alt="${employee.name}" class="w-12 h-12 rounded-full border-2 border-neon-green object-cover" onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';">

                            <div class="w-12 h-12 rounded-full bg-neon-green flex items-center justify-center text-black font-bold text-lg" style="display: none;">

                                ${employee.name.split(' ').map(n => n[0]).join('').substring(0, 2)}

                            </div>

                        ` : `

                            <div class="w-12 h-12 rounded-full bg-neon-green flex items-center justify-center text-black font-bold text-lg">

                                ${employee.name.split(' ').map(n => n[0]).join('').substring(0, 2)}

                            </div>

                        `}

                        <div>

                            <h3 class="font-bold text-lg neon-green">${employee.name}</h3>

                            <p class="text-white font-medium">${employee.role}</p>

                            <p class="text-gray-400 text-sm">ID: ${employee.agentId}</p>

                            ${employee.phone ? `<p class="text-gray-400 text-sm">📞 ${employee.phone}</p>` : ''}

                        </div>

                    </div>

                    ${employee.children.length > 0 ? `

                        <svg class="w-5 h-5 neon-green transform transition-transform duration-300" fill="currentColor" viewBox="0 0 20 20">

                            <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd"></path>

                        </svg>

                    ` : ''}

                </div>

            `;

           

            container.appendChild(card);

           

            // Children container

            if (employee.children.length > 0) {

                const childrenContainer = document.createElement('div');

                childrenContainer.className = 'children-container mt-8 ml-12 hidden';

               

                employee.children.forEach((child, childIndex) => {

                    const childElement = renderEmployee(child, level + 1, childIndex);

                    childrenContainer.appendChild(childElement);

                });

               

                container.appendChild(childrenContainer);

               

                // Toggle functionality

                card.addEventListener('click', function() {

                    const isHidden = childrenContainer.classList.contains('hidden');

                    const arrow = card.querySelector('svg');

                   

                    if (isHidden) {

                        childrenContainer.classList.remove('hidden');

                        if (arrow) arrow.style.transform = 'rotate(180deg)';

                    } else {

                        childrenContainer.classList.add('hidden');

                        if (arrow) arrow.style.transform = 'rotate(0deg)';

                    }

                });

            }

           

            return container;

        }

 

        // Listen for storage changes from other tabs

        window.addEventListener('storage', function(e) {

            if (e.key === 'hierarchyData') {

                loadStoredData();

            }

        });

 

        // Initialize

        document.addEventListener('DOMContentLoaded', function() {

            loadStoredData();

        });

    </script>

<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'97b00af161461216',t:'MTc1NzE4MzQ4MC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>

</html>
