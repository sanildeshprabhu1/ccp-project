<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>📚 UDISE+ India | School Enrollment Dashboard - Complete Analysis</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: #f8fafc;
            color: #0f172a;
            transition: background-color 0.3s ease, color 0.2s ease;
            line-height: 1.5;
        }

        body.dark {
            background: #0a0c10;
            color: #e2e8f0;
        }

        body.dark .card {
            background: #111827;
            border-color: #1f2937;
            box-shadow: 0 8px 20px rgba(0,0,0,0.4);
        }

        body.dark .stat-card {
            background: #0f172a;
            border-left: 4px solid #3b82f6;
        }

        body.dark .navbar {
            background: #0f172a;
            border-bottom: 1px solid #1e293b;
        }

        body.dark .footer {
            background: #0f172a;
            border-top: 1px solid #1e293b;
        }

        body.dark .insight-badge {
            background: #1e293b;
            color: #a5f3fc;
        }

        body.dark .insights-card {
            background: #0f172a;
            border-left: 5px solid #3b82f6;
        }

        body.dark .insights-card li {
            color: #e2e8f0;
        }

        body.dark select, body.dark option {
            background-color: #1f2a3e;
            color: #f1f5f9;
            border-color: #334155;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 24px;
        }

        .navbar {
            background: white;
            backdrop-filter: blur(4px);
            border-bottom: 1px solid #e2e8f0;
            padding: 1rem 0;
            position: sticky;
            top: 0;
            z-index: 50;
            transition: background 0.2s;
        }

        .nav-inner {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 16px;
        }

        .logo h1 {
            font-size: 1.6rem;
            font-weight: 700;
            background: linear-gradient(135deg, #1e3c72, #2b6eaf);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        body.dark .logo h1 {
            background: linear-gradient(135deg, #60a5fa, #a855f7);
            -webkit-background-clip: text;
            background-clip: text;
        }

        .logo i {
            color: #3b82f6;
            margin-right: 8px;
        }

        .theme-toggle {
            background: #eef2ff;
            border: none;
            padding: 10px 18px;
            border-radius: 40px;
            font-weight: 500;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: 0.2s;
        }
        body.dark .theme-toggle {
            background: #1e293b;
            color: #facc15;
        }

        .card {
            background: white;
            border-radius: 24px;
            padding: 1.5rem;
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
            border: 1px solid #eef2ff;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        .card:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 24px -8px rgba(0,0,0,0.1);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 24px;
            margin-bottom: 40px;
        }

        .stat-card {
            background: white;
            border-radius: 24px;
            padding: 1.2rem 1.5rem;
            border-left: 5px solid #3b82f6;
            box-shadow: 0 2px 8px rgba(0,0,0,0.03);
        }

        .stat-card h3 {
            font-size: 0.85rem;
            font-weight: 500;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            color: #475569;
        }
        body.dark .stat-card h3 {
            color: #94a3b8;
        }
        .stat-number {
            font-size: 2.2rem;
            font-weight: 800;
            margin-top: 8px;
            color: #0f172a;
        }
        body.dark .stat-number {
            color: #f1f5f9;
        }

        .chart-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(450px, 1fr));
            gap: 28px;
            margin-bottom: 40px;
        }

        .full-width {
            margin-bottom: 40px;
        }

        canvas {
            max-height: 320px;
            width: 100%;
        }

        .insight-badge {
            background: #eef2ff;
            border-radius: 40px;
            padding: 6px 14px;
            font-size: 0.75rem;
            font-weight: 500;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            margin-top: 12px;
        }

        .insights-card {
            background: #f1f5f9;
            border-radius: 24px;
            padding: 1.5rem;
            border-left: 5px solid #3b82f6;
            margin-bottom: 32px;
        }
        body.dark .insights-card {
            background: #0f172a;
        }
        .insights-card h3 {
            margin-bottom: 12px;
            font-size: 1.2rem;
        }
        .insights-card ul {
            margin-top: 12px;
            list-style: none;
        }
        .insights-card li {
            margin-bottom: 10px;
            padding-left: 8px;
            color: #1e293b;
        }
        body.dark .insights-card li {
            color: #cbd5e1;
        }

        .footer {
            background: white;
            border-top: 1px solid #e2e8f0;
            padding: 2rem 0;
            text-align: center;
            margin-top: 3rem;
            font-size: 0.85rem;
        }

        .footer p {
            margin: 4px 0;
        }

        @media (max-width: 760px) {
            .chart-row {
                grid-template-columns: 1fr;
            }
            .stats-grid {
                grid-template-columns: 1fr;
            }
        }
        
        .chart-title {
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }
    </style>
</head>
<body>

<div class="navbar">
    <div class="container nav-inner">
        <div class="logo">
            <h1><i class="fas fa-chalkboard-user"></i> UDISE+ Dashboard</h1>
            <div class="insight-badge" style="margin-top: 6px;">
                <i class="fas fa-chart-line"></i> School Enrollment • India (2012–2020) • Complete Analysis
            </div>
        </div>
        <div>
            <button class="theme-toggle" id="darkModeToggle">
                <i class="fas fa-moon"></i> <span>Dark Mode</span>
            </button>
        </div>
    </div>
</div>

<main class="container" style="margin-top: 2rem;">
    <!-- Key Metrics -->
    <div class="stats-grid">
        <div class="stat-card">
            <h3><i class="fas fa-school"></i> Total Students (All India)</h3>
            <div class="stat-number" id="totalStudents">—</div>
            <span style="font-size: 0.75rem;">Overall enrollment across all classes</span>
        </div>
        <div class="stat-card">
            <h3><i class="fas fa-venus-mars"></i> Gender Ratio (Girls/Boys)</h3>
            <div class="stat-number" id="genderRatio">—</div>
            <span>National average ratio</span>
        </div>
        <div class="stat-card">
            <h3><i class="fas fa-chart-simple"></i> Top State by Enrollment</h3>
            <div class="stat-number" id="topState">—</div>
            <span>Highest student count</span>
        </div>
        <div class="stat-card">
            <h3><i class="fas fa-graduation-cap"></i> Peak Enrollment Class</h3>
            <div class="stat-number" id="peakClass">—</div>
            <span>Class with most students</span>
        </div>
    </div>

    <!-- Row 1: State Bar Chart + Class Trend -->
    <div class="chart-row">
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-bar"></i> Enrollment by State (Top 12)</div>
            <canvas id="stateChart" height="300"></canvas>
        </div>
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-line"></i> Class-wise Enrollment Trend</div>
            <canvas id="classTrendChart" height="300"></canvas>
        </div>
    </div>

    <!-- Row 2: Gender Pie + Boys vs Girls Scatter -->
    <div class="chart-row">
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-pie"></i> Gender Distribution</div>
            <canvas id="genderPieChart" height="280"></canvas>
        </div>
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-scatter"></i> Boys vs Girls Correlation</div>
            <canvas id="scatterChart" height="280"></canvas>
        </div>
    </div>

    <!-- Row 3: Density Distribution + Gender Ratio Distribution -->
    <div class="chart-row">
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-simple"></i> Enrollment Density Distribution</div>
            <canvas id="densityChart" height="280"></canvas>
        </div>
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-line"></i> Gender Ratio Distribution</div>
            <canvas id="genderRatioDistChart" height="280"></canvas>
        </div>
    </div>

    <!-- Row 4: Top States by Count + Box Plot -->
    <div class="chart-row">
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-bar"></i> Top States by Record Count</div>
            <canvas id="topStatesCountChart" height="280"></canvas>
        </div>
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-box"></i> Student Distribution per State (Box Plot)</div>
            <canvas id="boxplotChart" height="280"></canvas>
        </div>
    </div>

    <!-- Row 5: Violin Plot + Scatter Plot -->
    <div class="chart-row">
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-line"></i> Distribution Shape per State (Violin)</div>
            <canvas id="violinChart" height="280"></canvas>
        </div>
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-scatter"></i> Boys vs Girls Relationship</div>
            <canvas id="scatterPlotChart" height="280"></canvas>
        </div>
    </div>

    <!-- Row 6: Class Line Chart + KDE Plot -->
    <div class="chart-row">
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-line"></i> Class-wise Enrollment Trend (Detailed)</div>
            <canvas id="classLineChart" height="280"></canvas>
        </div>
        <div class="card">
            <div class="chart-title"><i class="fas fa-chart-line"></i> Density Plot of Total Students (KDE)</div>
            <canvas id="kdeChart" height="280"></canvas>
        </div>
    </div>

    <!-- Insights section -->
    <div class="insights-card">
        <h3><i class="fas fa-clipboard-list"></i> Key Educational Insights</h3>
        <ul style="margin-top: 12px; list-style: none;">
            <li>🏆 <strong>Uttar Pradesh</strong> leads with highest total enrollment, reflecting demographic scale.</li>
            <li>📉 Enrollment declines gradually from Class 1 to Class 12 (dropout trend visible).</li>
            <li>⚖️ Gender ratio ~0.96 (Girls per Boy) shows near parity across India.</li>
            <li>📈 Strong positive correlation between boys and girls enrollment (equitable distribution).</li>
            <li>📊 Density plot reveals majority of districts have moderate student strength (right-skewed).</li>
            <li>📈 Gender ratio distribution shows most districts have ratios between 0.9 and 1.1.</li>
            <li>🏫 Box plots and violin plots reveal significant state-level variations in enrollment patterns.</li>
        </ul>
    </div>
</main>

<footer class="footer">
    <div class="container">
        <p><i class="fas fa-chart-line"></i> Dashboard visualizes key trends from 2012–2020 UDISE+ data</p>
        <p><i class="fas fa-database"></i> Data source: UDISE+ simulated enrollment dataset | Complete Analysis Dashboard</p>
        <p style="margin-top: 8px;">© 2025 Education Analytics</p>
    </div>
</footer>

<script>
    // ============================================================
    // DATA DEFINITIONS
    // ============================================================
    
    // State enrollment data
    const stateLabels = [
        "Uttar Pradesh", "Maharashtra", "Bihar", "West Bengal", "Madhya Pradesh",
        "Rajasthan", "Tamil Nadu", "Karnataka", "Gujarat", "Andhra Pradesh",
        "Odisha", "Telangana"
    ];
    const stateEnrollments = [
        48600000, 19800000, 18700000, 14200000, 12900000,
        12400000, 10800000, 9700000, 9100000, 7900000,
        6700000, 6100000
    ];
    
    // Class totals
    const classLabels = Array.from({length: 12}, (_, i) => `Class ${i+1}`);
    const classTotals = [
        18500000, 18200000, 17900000, 17600000, 17300000,
        16800000, 16200000, 15700000, 14200000, 12800000,
        11200000, 9800000
    ];
    
    // Gender totals
    const totalBoys = 156400000;
    const totalGirls = 150200000;
    const totalStudentsAll = totalBoys + totalGirls;
    
    // Scatter data
    const scatterData = [];
    for (let i = 0; i < 150; i++) {
        let base = 1000 + Math.random() * 150000;
        let boys = base + (Math.random() - 0.5) * 12000;
        let girls = base * 0.95 + (Math.random() - 0.5) * 10000;
        scatterData.push({x: Math.max(0, boys), y: Math.max(0, girls)});
    }
    
    // Density data
    const densityData = [];
    for (let i = 0; i < 400; i++) {
        let val = 5000 + Math.pow(Math.random(), 1.5) * 280000;
        densityData.push(val);
    }
    
    // Gender ratio data
    const genderRatioData = [];
    for (let i = 0; i < 500; i++) {
        let ratio = 0.88 + Math.random() * 0.2;
        genderRatioData.push(ratio);
    }
    
    // Top states by count
    const topStatesByCount = ["Uttar Pradesh", "Maharashtra", "Bihar", "West Bengal", "Madhya Pradesh", "Rajasthan", "Tamil Nadu", "Karnataka", "Gujarat", "Andhra Pradesh"];
    const stateRecordCounts = [12450, 8920, 7650, 6840, 6210, 5980, 5450, 5120, 4890, 4560];
    
    // Box plot data
    const statesForBox = ["Uttar Pradesh", "Maharashtra", "Bihar", "West Bengal", "Madhya Pradesh"];
    const boxplotData = {};
    for (let s of statesForBox) {
        let values = [];
        let mean = 30000 + Math.random() * 50000;
        for (let i = 0; i < 200; i++) {
            values.push(mean + (Math.random() - 0.5) * 30000);
        }
        values.sort((a,b) => a-b);
        boxplotData[s] = {
            min: values[0],
            q1: values[Math.floor(values.length * 0.25)],
            median: values[Math.floor(values.length * 0.5)],
            q3: values[Math.floor(values.length * 0.75)],
            max: values[values.length - 1]
        };
    }
    
    // Violin data
    const violinData = {};
    for (let s of statesForBox) {
        let values = [];
        let mean = 30000 + Math.random() * 50000;
        for (let i = 0; i < 500; i++) {
            values.push(mean + (Math.random() - 0.5) * 40000);
        }
        violinData[s] = values;
    }
    
    // Class line data
    const classNumbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
    const classTotalsLine = [18500000, 18200000, 17900000, 17600000, 17300000, 16800000, 16200000, 15700000, 14200000, 12800000, 11200000, 9800000];
    
    // KDE data
    const kdeData = [];
    for (let i = 0; i < 1000; i++) {
        kdeData.push(20000 + Math.pow(Math.random(), 1.3) * 280000);
    }
    
    // Update metrics
    document.getElementById('totalStudents').innerText = (totalStudentsAll / 1e6).toFixed(1) + ' Cr';
    document.getElementById('genderRatio').innerText = (totalGirls / totalBoys).toFixed(2);
    document.getElementById('topState').innerText = "Uttar Pradesh";
    document.getElementById('peakClass').innerText = "Class 1";
    
    // ============================================================
    // CHART INITIALIZATION
    // ============================================================
    
    // 1. State Bar Chart
    new Chart(document.getElementById('stateChart'), {
        type: 'bar',
        data: {
            labels: stateLabels,
            datasets: [{
                label: 'Total Students (Lakhs)',
                data: stateEnrollments.map(v => v / 100000),
                backgroundColor: 'rgba(59, 130, 246, 0.7)',
                borderRadius: 8
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: true,
            plugins: { tooltip: { callbacks: { label: (ctx) => `${(ctx.raw * 100000).toLocaleString()} students` } } },
            scales: { y: { title: { display: true, text: 'Students (Lakhs)' } }, x: { ticks: { maxRotation: 35 } } }
        }
    });
    
    // 2. Class Trend Chart
    new Chart(document.getElementById('classTrendChart'), {
        type: 'line',
        data: {
            labels: classLabels,
            datasets: [{
                label: 'Enrollment per Class',
                data: classTotals.map(v => v / 1000),
                borderColor: '#f97316',
                backgroundColor: 'rgba(249, 115, 22, 0.05)',
                tension: 0.3,
                fill: true,
                pointBackgroundColor: '#f97316'
            }]
        },
        options: {
            responsive: true,
            plugins: { tooltip: { callbacks: { label: (ctx) => `${(ctx.raw * 1000).toLocaleString()} students` } } },
            scales: { y: { title: { display: true, text: 'Students (Thousands)' } } }
        }
    });
    
    // 3. Gender Pie Chart
    new Chart(document.getElementById('genderPieChart'), {
        type: 'pie',
        data: {
            labels: ['Girls', 'Boys'],
            datasets: [{ data: [totalGirls, totalBoys], backgroundColor: ['#ec489a', '#3b82f6'], borderWidth: 0 }]
        },
        options: {
            responsive: true,
            plugins: { tooltip: { callbacks: { label: (ctx) => `${ctx.label}: ${(ctx.raw / 1e6).toFixed(1)} Cr (${((ctx.raw / totalStudentsAll)*100).toFixed(1)}%)` } } }
        }
    });
    
    // 4. Scatter Chart (Boys vs Girls)
    new Chart(document.getElementById('scatterChart'), {
        type: 'scatter',
        data: { datasets: [{ label: 'Districts', data: scatterData, backgroundColor: '#10b981', pointRadius: 4 }] },
        options: { responsive: true, scales: { x: { title: { display: true, text: 'Boys per District' } }, y: { title: { display: true, text: 'Girls per District' } } } }
    });
    
    // 5. Density Chart
    const maxVal = Math.max(...densityData);
    const bins = 35;
    const binWidth = maxVal / bins;
    let hist = new Array(bins).fill(0);
    densityData.forEach(v => { let idx = Math.floor(v / binWidth); if (idx >= bins) idx = bins-1; hist[idx]++; });
    new Chart(document.getElementById('densityChart'), {
        type: 'line',
        data: { labels: Array.from({length: bins}, (_, i) => Math.round(i * binWidth / 1000) + 'k'), datasets: [{ label: 'Districts', data: hist, borderColor: '#8b5cf6', backgroundColor: 'rgba(139, 92, 246, 0.2)', fill: true, tension: 0.4, pointRadius: 0 }] },
        options: { responsive: true, scales: { x: { title: { display: true, text: 'Students (thousands)' } }, y: { title: { display: true, text: 'Number of Districts' } } } }
    });
    
    // 6. Gender Ratio Distribution
    const genderBins = 30;
    const genderMin = 0.7, genderMax = 1.2;
    const genderBinWidth = (genderMax - genderMin) / genderBins;
    let genderHist = new Array(genderBins).fill(0);
    genderRatioData.forEach(v => { let idx = Math.floor((v - genderMin) / genderBinWidth); if (idx >= 0 && idx < genderBins) genderHist[idx]++; });
    new Chart(document.getElementById('genderRatioDistChart'), {
        type: 'line',
        data: { labels: Array.from({length: genderBins}, (_, i) => (genderMin + i * genderBinWidth).toFixed(2)), datasets: [{ label: 'Districts', data: genderHist, borderColor: '#06b6d4', backgroundColor: 'rgba(6, 182, 212, 0.2)', fill: true, tension: 0.3, pointRadius: 0 }] },
        options: { responsive: true, scales: { x: { title: { display: true, text: 'Gender Ratio' } }, y: { title: { display: true, text: 'Number of Districts' } } } }
    });
    
    // 7. Top States Count Chart
    new Chart(document.getElementById('topStatesCountChart'), {
        type: 'bar',
        data: { labels: topStatesByCount, datasets: [{ label: 'Records', data: stateRecordCounts, backgroundColor: 'rgba(139, 92, 246, 0.7)', borderRadius: 8 }] },
        options: { responsive: true, scales: { y: { title: { display: true, text: 'Number of Records' } }, x: { ticks: { maxRotation: 45 } } } }
    });
    
    // 8. Box Plot
    new Chart(document.getElementById('boxplotChart'), {
        type: 'bar',
        data: {
            labels: statesForBox,
            datasets: [
                { label: 'Min', data: statesForBox.map(s => boxplotData[s].min / 1000), backgroundColor: 'rgba(16, 185, 129, 0.6)' },
                { label: 'Q1', data: statesForBox.map(s => boxplotData[s].q1 / 1000), backgroundColor: 'rgba(59, 130, 246, 0.5)' },
                { label: 'Median', data: statesForBox.map(s => boxplotData[s].median / 1000), backgroundColor: 'rgba(249, 115, 22, 0.7)' },
                { label: 'Q3', data: statesForBox.map(s => boxplotData[s].q3 / 1000), backgroundColor: 'rgba(59, 130, 246, 0.5)' },
                { label: 'Max', data: statesForBox.map(s => boxplotData[s].max / 1000), backgroundColor: 'rgba(239, 68, 68, 0.6)' }
            ]
        },
        options: { responsive: true, plugins: { tooltip: { callbacks: { label: (ctx) => `${ctx.dataset.label}: ${(ctx.raw).toFixed(0)}k students` } } }, scales: { y: { title: { display: true, text: 'Students (Thousands)' } } } }
    });
    
    // 9. Violin Plot (simplified using area charts)
    const violinColors = ['#3b82f6', '#ef4444', '#10b981', '#f59e0b', '#8b5cf6'];
    const violinDatasets = [];
    let violinMin = Infinity, violinMax = -Infinity;
    statesForBox.forEach((state, idx) => {
        let values = violinData[state];
        let hist = new Array(30).fill(0);
        let minVal = Math.min(...values), maxVal = Math.max(...values);
        violinMin = Math.min(violinMin, minVal);
        violinMax = Math.max(violinMax, maxVal);
        let binW = (maxVal - minVal) / 30;
        values.forEach(v => { let binIdx = Math.floor((v - minVal) / binW); if (binIdx >= 0 && binIdx < 30) hist[binIdx]++; });
        let maxCount = Math.max(...hist);
        let normalized = hist.map(h => h / maxCount * 50);
        violinDatasets.push({ label: state, data: normalized, borderColor: violinColors[idx], backgroundColor: violinColors[idx] + '20', fill: true, tension: 0.3, pointRadius: 0 });
    });
    new Chart(document.getElementById('violinChart'), {
        type: 'line',
        data: { labels: Array.from({length: 30}, (_, i) => `${Math.round((violinMin + i * (violinMax - violinMin) / 30) / 1000)}k`), datasets: violinDatasets },
        options: { responsive: true, plugins: { tooltip: { callbacks: { label: (ctx) => `${ctx.dataset.label}: Density ${ctx.raw.toFixed(2)}` } } }, scales: { y: { title: { display: true, text: 'Density (Normalized)' } }, x: { title: { display: true, text: 'Student Count' } } } }
    });
    
    // 10. Scatter Plot (Boys vs Girls Relationship)
    const scatterPlotData = [];
    for (let i = 0; i < 200; i++) { let boys = 10000 + Math.random() * 150000; let girls = boys * (0.88 + Math.random() * 0.16); scatterPlotData.push({x: boys, y: girls}); }
    new Chart(document.getElementById('scatterPlotChart'), {
        type: 'scatter',
        data: { datasets: [{ label: 'Districts', data: scatterPlotData, backgroundColor: '#f97316', pointRadius: 3 }] },
        options: { responsive: true, scales: { x: { title: { display: true, text: 'Boys Enrollment' } }, y: { title: { display: true, text: 'Girls Enrollment' } } } }
    });
    
    // 11. Class Line Chart
    new Chart(document.getElementById('classLineChart'), {
        type: 'line',
        data: { labels: classNumbers.map(c => `Class ${c}`), datasets: [{ label: 'Total Enrollment', data: classTotalsLine.map(v => v / 1e6), borderColor: '#10b981', backgroundColor: 'rgba(16, 185, 129, 0.1)', tension: 0.3, fill: true, pointRadius: 4 }] },
        options: { responsive: true, plugins: { tooltip: { callbacks: { label: (ctx) => `${(ctx.raw * 1e6).toLocaleString()} students` } } }, scales: { y: { title: { display: true, text: 'Students (Millions)' } } } }
    });
    
    // 12. KDE Chart
    const kdeBins = 40;
    const kdeMaxVal = Math.max(...kdeData);
    const kdeBinW = kdeMaxVal / kdeBins;
    let kdeHist = new Array(kdeBins).fill(0);
    kdeData.forEach(v => { let idx = Math.floor(v / kdeBinW); if (idx >= kdeBins) idx = kdeBins - 1; kdeHist[idx]++; });
    new Chart(document.getElementById('kdeChart'), {
        type: 'line',
        data: { labels: Array.from({length: kdeBins}, (_, i) => Math.round(i * kdeBinW / 1000) + 'k'), datasets: [{ label: 'Student Density', data: kdeHist, borderColor: '#a855f7', backgroundColor: 'rgba(168, 85, 247, 0.2)', fill: true, tension: 0.4, pointRadius: 0 }] },
        options: { responsive: true, scales: { x: { title: { display: true, text: 'Students (thousands)' } }, y: { title: { display: true, text: 'Density' } } } }
    });

    // Dark Mode Toggle
    const toggleBtn = document.getElementById('darkModeToggle');
    const body = document.body;
    const moonIcon = toggleBtn.querySelector('i');
    const spanText = toggleBtn.querySelector('span');
    
    body.classList.remove('dark');
    
    function updateToggleUI(isDark) {
        if (isDark) {
            moonIcon.className = 'fas fa-sun';
            spanText.innerText = ' Light Mode';
        } else {
            moonIcon.className = 'fas fa-moon';
            spanText.innerText = ' Dark Mode';
        }
    }
    updateToggleUI(false);
    
    toggleBtn.addEventListener('click', () => {
        const isDark = body.classList.toggle('dark');
        localStorage.setItem('theme', isDark ? 'dark' : 'light');
        updateToggleUI(isDark);
    });
</script>
</body>
</html>
