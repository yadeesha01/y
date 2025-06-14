<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yadeesha's Study Dashboard</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #FF2400; /* Vibrant Pink */
            --secondary: #8b5cf6; /* Amethyst Purple */
            --accent: #4ade80; /* Bright Green */
            --dark: #0c0c0c;
            --light: #ffffff;
            --glass: rgba(255, 255, 255, 0.1); /* Lighter glass for dark background */
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif; /* Changed to Poppins for consistency */
            color: var(--light);
            background: linear-gradient(135deg, #0c0c0c 0%, #1a1a2e 100%);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }

        /* Profile Section */
        .profile-section {
            position: fixed;
            top: 20px;
            right: 30px;
            display: flex;
            align-items: center;
            gap: 10px;
            z-index: 100;
            background: rgba(0, 0, 0, 0.5);
            padding: 10px 15px;
            border-radius: 30px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: background 0.3s ease, border 0.3s ease;
        }

        .profile-name {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--primary);
        }

        .profile-status {
            font-size: 0.8rem;
            color: var(--light); /* Default color */
            display: flex;
            align-items: center;
            gap: 5px;
            transition: color 0.3s ease;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            background: #ccc; /* Default grey for inactive */
            border-radius: 50%;
            transition: background 0.3s ease, box-shadow 0.3s ease;
        }

        .profile-status.active .status-dot {
            background: var(--accent); /* Green for active */
            box-shadow: 0 0 8px var(--accent);
            animation: pulse 1.5s infinite;
        }

        .profile-status.active {
            color: var(--accent); /* Green text for active */
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.5; transform: scale(1.2); }
        }

        /* Main Layout */
        .main-layout {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            padding: 90px 20px 30px;
            max-width: 1400px;
            margin: 0 auto;
        }

        /* Panels */
        .panel {
            background: var(--glass);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: all 0.3s ease;
        }

        .panel:hover {
            border-color: var(--primary);
            box-shadow: 0 15px 40px rgba(255, 51, 102, 0.3);
        }

        .panel h3 {
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: var(--primary);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            padding-bottom: 10px;
        }

        /* Countdown Panel */
        .countdown-panel {
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
            min-height: 300px;
            grid-column: 1 / -1; /* Span full width for prominence */
        }

        .countdown-panel::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url('https://source.unsplash.com/random/1600x900/?study,space') center/cover no-repeat; /* Random study image */
            opacity: 0.15; /* Slightly less opaque */
            z-index: -1;
            filter: grayscale(50%); /* Subtle filter */
        }

        .countdown-title {
            font-size: 2rem; /* Larger title */
            margin-bottom: 25px;
            color: var(--accent); /* Changed to accent for contrast */
            text-shadow: 0 0 15px rgba(74, 222, 128, 0.5);
            font-weight: 700;
        }

        .countdown-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr)); /* More flexible grid */
            gap: 20px;
            width: 100%;
            max-width: 600px; /* Constrain width */
        }

        .countdown-item {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 20px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: all 0.3s ease;
        }

        .countdown-item:hover {
            transform: translateY(-8px); /* More pronounced hover */
            box-shadow: 0 10px 20px rgba(220,255,63);
            border-color: var(--secondary);
        }

        .countdown-number {
            font-size: 2.8rem; /* Larger numbers */
            font-weight: bold;
            color: var(--light);
            margin-bottom: 8px;
        }

        .countdown-label {
            font-size: 1rem; /* Slightly larger label */
            color: var(--primary); /* Changed to primary */
            text-transform: uppercase;
            letter-spacing: 1.5px;
        }

        /* Study Tracker */
        .study-tracker {
            text-align: center;
        }

        .study-tracker .quote {
            font-style: italic;
            font-size: 1rem; /* Slightly smaller for better fit */
            padding: 15px;
            margin-bottom: 25px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 10px;
            border-left: 3px solid var(--secondary);
            color: #ccc;
        }

        .bar-chart {
            display: flex;
            justify-content: space-around;
            align-items: flex-end;
            height: 200px;
            margin: 30px 0;
            gap: 8px; /* Slightly less gap */
            border-bottom: 1px solid rgba(255, 255, 255, 0.1); /* Subtle base line */
            padding-bottom: 10px;
        }

        .bar {
            flex-grow: 1;
            max-width: 50px; /* Constrain bar width */
            background: linear-gradient(to top, rgba(255, 51, 102, 0.3), var(--primary)); /* Gradient for depth */
            border-radius: 8px 8px 0 0;
            transition: all 0.5s ease;
            display: flex;
            flex-direction: column; /* For number and label */
            justify-content: flex-end;
            align-items: center;
            padding-top: 5px; /* Space for number */
            color: white;
            font-weight: bold;
            position: relative;
        }
        
        .bar .hour-value {
            font-size: 0.85rem;
            margin-bottom: 5px;
            opacity: 0.8;
        }

        .bar span { /* Day label */
            font-size: 0.75rem;
            color: var(--light);
            opacity: 0.7;
        }

        .bar:hover {
            transform: translateY(-15px); /* More hover effect */
            box-shadow: 0 10px 25px rgba(255, 51, 102, 0.5);
            background: linear-gradient(to top, var(--primary), var(--secondary)); /* Different hover gradient */
        }

        .bar.active {
            background: linear-gradient(to top, rgba(74, 222, 128, 0.3), var(--accent)); /* Green gradient when active */
        }

        .bar.active:hover {
            background: linear-gradient(to top, var(--accent), var(--secondary));
        }

        .stats-summary {
            display: flex;
            justify-content: space-around;
            margin: 20px 0;
            text-align: center;
            flex-wrap: wrap; /* Wrap on small screens */
            gap: 15px; /* Gap between stat boxes */
        }

        .stat-box {
            padding: 12px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            min-width: 130px; /* Slightly larger min-width */
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        .stat-box p {
            font-size: 0.9rem;
            color: #ccc;
        }

        .stat-box strong {
            color: var(--accent); /* Changed to accent */
            font-size: 1.2rem;
            display: block; /* Make it a block for spacing */
            margin-top: 5px;
        }

        .input-controls {
            display: flex;
            flex-wrap: wrap;
            gap: 15px; /* Increased gap */
            justify-content: center;
            align-items: center;
            margin: 30px 0; /* More margin */
            padding-top: 20px;
            border-top: 1px dashed rgba(255, 255, 255, 0.1);
        }

        .input-controls label {
            font-weight: bold;
            color: var(--secondary);
            font-size: 0.95rem;
        }

        .input-controls select,
        .input-controls input {
            padding: 10px 14px; /* Larger padding */
            background: rgba(255, 255, 255, 0.15); /* Slightly less transparent */
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 10px; /* More rounded */
            color: white;
            font-size: 1rem;
            outline: none; /* Remove outline on focus */
            transition: border-color 0.3s ease;
        }
        
        .input-controls select:focus,
        .input-controls input:focus {
            border-color: var(--primary);
            box-shadow: 0 0 8px rgba(255, 51, 102, 0.3);
        }


        .input-controls button {
            padding: 10px 20px; /* Larger buttons */
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            border: none;
            border-radius: 10px; /* More rounded */
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.3);
        }

        .input-controls button:hover {
            transform: translateY(-5px); /* More pronounced hover */
            box-shadow: 0 8px 20px rgba(255, 51, 102, 0.5);
        }

        .digital-clock {
            font-family: 'Share Tech Mono', monospace; /* More futuristic font for clock */
            font-size: 2.5rem; /* Larger clock */
            text-align: center;
            margin: 25px 0;
            color: var(--accent);
            letter-spacing: 4px; /* More spacing */
            text-shadow: 0 0 15px rgba(74, 222, 128, 0.5);
        }

        /* Past Papers & Timetable */
        .panel-list {
            list-style: none;
            padding: 0;
        }

        .panel-list li {
            padding: 12px 0; /* More padding */
            border-bottom: 1px solid rgba(255, 255, 255, 0.08); /* Stronger divider */
            transition: all 0.3s ease;
        }

        .panel-list li:last-child {
            border-bottom: none; /* No border for last item */
        }

        .panel-list li:hover {
            transform: translateX(8px); /* More pronounced hover */
            color: var(--primary); /* Highlight text on hover */
        }

        .panel-list a {
            color: var(--secondary);
            text-decoration: none;
            transition: all 0.3s ease;
            font-size: 1rem;
            display: block; /* Make the entire list item clickable via link */
        }

        .panel-list a:hover {
            color: var(--primary);
        }
        
        .panel-list strong { /* For timetable days */
            color: var(--accent);
        }

        /* Session Controls */
        .session-controls {
            position: fixed;
            bottom: 30px;
            right: 30px;
            z-index: 100;
        }

        .session-btn {
            padding: 15px 30px; /* Larger button */
            background: linear-gradient(45deg, var(--accent), #22c55e);
            border: none;
            border-radius: 35px; /* More rounded */
            color: white;
            font-weight: bold;
            font-size: 1.1rem; /* Larger font */
            cursor: pointer;
            box-shadow: 0 8px 25px rgba(74, 222, 128, 0.5);
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .session-btn:hover {
            transform: translateY(-5px) scale(1.02);
            box-shadow: 0 10px 30px rgba(74, 222, 128, 0.7);
        }
        
        .session-btn.active {
            background: linear-gradient(45deg, #f04e8a, var(--primary)); /* Reddish gradient when active (to stop) */
            box-shadow: 0 8px 25px rgba(255, 51, 102, 0.5);
        }

        .session-btn.active:hover {
            background: linear-gradient(45deg, var(--primary), #cc0033);
            box-shadow: 0 10px 30px rgba(255, 51, 102, 0.7);
        }

        /* Popup */
        .popup {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.8); /* Slightly smaller initial scale */
            background: rgba(0, 0, 0, 0.95);
            backdrop-filter: blur(20px);
            border: 2px solid var(--primary);
            border-radius: 25px; /* More rounded */
            padding: 40px; /* More padding */
            width: 90%;
            max-width: 450px; /* Slightly larger max-width */
            text-align: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            box-shadow: 0 15px 40px rgba(255, 51, 102, 0.5);
        }

        .popup.active {
            opacity: 1;
            visibility: visible;
            transform: translate(-50%, -50%) scale(1);
        }

        .popup h3 {
            font-size: 1.8rem; /* Larger title */
            color: var(--accent); /* Accent color for success popups */
            margin-bottom: 20px;
            text-shadow: 0 0 10px rgba(74, 222, 128, 0.3);
        }

        .popup p {
            font-size: 1.1rem; /* Larger text */
            line-height: 1.6;
            margin-bottom: 30px;
            color: #e0e0e0; /* Lighter grey for better contrast */
        }

        .popup-btn {
            padding: 12px 25px; /* Larger button */
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            border: none;
            border-radius: 30px; /* More rounded */
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }

        .popup-btn:hover {
            transform: scale(1.08); /* More pronounced hover */
            box-shadow: 0 8px 20px rgba(255, 51, 102, 0.7);
        }
        
        /* Toast Notification (if added later, not in this version as popups replace it) */
        /*
        .toast-notification { ... }
        */

        /* Responsive Design */
        @media (max-width: 768px) {
            .main-layout {
                grid-template-columns: 1fr;
                padding-top: 100px; /* Adjust for fixed profile */
                padding-bottom: 120px; /* Adjust for fixed session button */
            }
            
            .profile-section {
                top: 15px;
                right: 15px;
                padding: 8px 12px;
            }
            
            .countdown-grid {
                grid-template-columns: repeat(2, 1fr); /* Keep 2 columns on small tablets */
                gap: 10px;
            }
            
            .countdown-number {
                font-size: 2.2rem;
            }

            .countdown-label {
                font-size: 0.9rem;
            }

            .session-controls {
                bottom: 20px;
                right: 20px;
            }
            
            .session-btn {
                padding: 12px 24px;
                font-size: 1rem;
            }

            .bar {
                max-width: 40px;
            }

            .stat-box {
                min-width: unset; /* Remove min-width to allow wrapping */
                width: 48%; /* Two columns per row */
            }

            .input-controls {
                gap: 10px;
            }

            .digital-clock {
                font-size: 2rem;
            }

            .popup {
                padding: 30px;
            }
        }

        @media (max-width: 480px) {
            .profile-section {
                flex-direction: column; /* Stack name and status */
                align-items: flex-end;
                gap: 5px;
                background: none; /* Make it transparent on very small screens */
                backdrop-filter: none;
                border: none;
                padding: 5px;
            }
            
            .profile-name {
                font-size: 1.1rem;
            }

            .profile-status {
                font-size: 0.7rem;
            }

            .main-layout {
                padding: 80px 15px 100px;
                gap: 15px;
            }

            .panel {
                padding: 20px;
            }

            .countdown-title {
                font-size: 1.6rem;
            }

            .countdown-grid {
                grid-template-columns: 1fr; /* Single column on smallest screens */
            }

            .countdown-number {
                font-size: 2rem;
            }

            .countdown-label {
                font-size: 0.8rem;
            }

            .bar {
                width: 30px;
            }

            .stats-summary {
                flex-direction: column; /* Stack stats vertically */
                align-items: center;
            }

            .stat-box {
                width: 90%; /* Almost full width */
            }

            .input-controls {
                flex-direction: column; /* Stack inputs vertically */
                align-items: stretch;
            }

            .input-controls select,
            .input-controls input,
            .input-controls button {
                width: 100%; /* Full width for inputs and buttons */
                box-sizing: border-box;
            }
            
            .digital-clock {
                font-size: 1.8rem;
            }

            .session-btn {
                padding: 10px 20px;
                font-size: 0.9rem;
            }

            .popup {
                padding: 25px;
            }

            .popup h3 {
                font-size: 1.5rem;
            }
            .popup p {
                font-size: 1rem;
            }
        }

    </style>
</head>
<body>
    <div class="profile-section">
        <div class="profile-info">
            <div class="profile-name">Yadeesha</div>
            <div class="profile-status" id="profileStatus">
                <div class="status-dot" id="statusDot"></div>
                Inactive Learning
            </div>
        </div>
    </div>

    <div class="main-layout">
        <div class="panel countdown-panel">
            <h2 class="countdown-title">Countdown to Exam: 2025 A/L</h2>
            <div class="countdown-grid">
                <div class="countdown-item">
                    <div class="countdown-number" id="days">0</div>
                    <div class="countdown-label">Days</div>
                </div>
                <div class="countdown-item">
                    <div class="countdown-number" id="hours">0</div>
                    <div class="countdown-label">Hours</div>
                </div>
                <div class="countdown-item">
                    <div class="countdown-number" id="minutes">0</div>
                    <div class="countdown-label">Minutes</div>
                </div>
                <div class="countdown-item">
                    <div class="countdown-number" id="seconds">0</div>
                    <div class="countdown-label">Seconds</div>
                </div>
            </div>
        </div>

        <div class="panel study-tracker">
            <div class="quote" id="quote"></div>
            <h3>Study Time Analyzer</h3>
            
            <div class="bar-chart">
                <div class="bar" id="Mon"><span class="hour-value">0h</span><span>Mon</span></div>
                <div class="bar" id="Tue"><span class="hour-value">0h</span><span>Tue</span></div>
                <div class="bar" id="Wed"><span class="hour-value">0h</span><span>Wed</span></div>
                <div class="bar" id="Thu"><span class="hour-value">0h</span><span>Thu</span></div>
                <div class="bar" id="Fri"><span class="hour-value">0h</span><span>Fri</span></div>
                <div class="bar" id="Sat"><span class="hour-value">0h</span><span>Sat</span></div>
                <div class="bar" id="Sun"><span class="hour-value">0h</span><span>Sun</span></div>
            </div>
            
            <div class="stats-summary">
                <div class="stat-box">
                    <p>Average:</p> <strong id="avg">0.0 hours</strong>
                </div>
                <div class="stat-box">
                    <p>Weekly:</p> <strong id="weekly">0.0 hours</strong>
                </div>
                <div class="stat-box">
                    <p>Monthly:</p> <strong id="monthly">0.0 hours</strong>
                </div>
            </div>
            
            <div class="input-controls">
                <label for="day">Day:</label>
                <select id="day">
                    <option>Mon</option>
                    <option>Tue</option>
                    <option>Wed</option>
                    <option>Thu</option>
                    <option>Fri</option>
                    <option>Sat</option>
                    <option>Sun</option>
                </select>
                
                <label for="hours">Hours:</label>
                <input type="number" id="hoursInput" min="0" max="24" value="0" step="0.5">
                
                <button onclick="updateBar()">Update Manually</button>
                <button onclick="clearData()">Clear All Data</button>
            </div>
            
            <div class="digital-clock" id="digitalClock"></div>
        </div>

        <div class="panel">
            <h3>Engineering Tech Papers (2012–2024)</h3>
            <ul class="panel-list">
                <li><a href="https://pastpapers.wiki/2012-a-l-engineering-technology-paper-sinhala/" target="_blank">2012 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2013-a-l-engineering-technology-paper-sinhala/" target="_blank">2013 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2014-a-l-engineering-technology-paper-sinhala/" target="_blank">2014 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2015-a-l-engineering-technology-paper-sinhala/" target="_blank">2015 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2016-a-l-engineering-technology-paper-sinhala/" target="_blank">2016 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2017-a-l-engineering-technology-paper-sinhala/" target="_blank">2017 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2018-a-l-engineering-technology-paper-sinhala/" target="_blank">2018 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2019-a-l-engineering-technology-paper-sinhala/" target="_blank">2019 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2020-a-l-engineering-technology-paper-sinhala/" target="_blank">2020 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2021-a-l-engineering-technology-paper-sinhala/" target="_blank">2021 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2022-a-l-engineering-technology-paper-sinhala/" target="_blank">2022 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2023-a-l-engineering-technology-paper-sinhala/" target="_blank">2023 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2024-a-l-engineering-technology-paper-sinhala/" target="_blank">2024 Paper</a></li>
            </ul>
        </div>

        <div class="panel">
            <h3>A/L ICT Past Papers (2012–2024)</h3>
            <ul class="panel-list">
                <li><a href="https://pastpapers.wiki/2012-a-l-ict-past-paper-sinhala-medium/" target="_blank">2012 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2013-a-l-ict-past-paper-sinhala-medium/" target="_blank">2013 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2014-a-l-ict-past-paper-sinhala-medium/" target="_blank">2014 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2015-a-l-ict-past-paper-sinhala-medium/" target="_blank">2015 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2016-a-l-ict-past-paper-sinhala-medium/" target="_blank">2016 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2017-a-l-ict-past-paper-sinhala-medium/" target="_blank">2017 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2018-a-l-ict-past-paper-sinhala-medium/" target="_blank">2018 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2019-a-l-ict-past-paper-sinhala-medium/" target="_blank">2019 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2020-a-l-ict-past-paper-sinhala-medium/" target="_blank">2020 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2021-a-l-ict-past-paper-sinhala-medium/" target="_blank">2021 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2022-a-l-ict-past-paper-sinhala-medium/" target="_blank">2022 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2023-a-l-ict-past-paper-sinhala-medium/" target="_blank">2023 Paper</a></li>
                <li><a href="https://pastpapers.wiki/2024-a-l-ict-past-paper-sinhala-medium/" target="_blank">2024 Paper</a></li>
            </ul>
        </div>

        <div class="panel">
            <h3>Class Timetable</h3>
            <ul class="panel-list">
                <li><strong>Monday:</strong> Mathematics 9AM–11AM</li>
                <li><strong>Tuesday:</strong> Physics 2PM–4PM</li>
                <li><strong>Wednesday:</strong> ICT Revision 9AM–11AM / 7PM–9PM</li>
                <li><strong>Thursday:</strong> Engineering Tech 2PM–4PM</li>
                <li><strong>Friday:</strong> Chemistry 10AM–12PM</li>
                <li><strong>Saturday:</strong> Combined Science 3PM–5PM</li>
                <li><strong>Sunday:</strong> Revision Day</li>
            </ul>
        </div>
    </div>

    <div class="session-controls">
        <button class="session-btn" id="sessionBtn">Start Learning Session</button>
    </div>

    <div class="popup" id="popup">
        <h3 id="popupTitle">Session Started!</h3>
        <p id="popupMessage">Your focused learning session has begun.</p>
        <button class="popup-btn" id="popupBtn">Got it!</button>
    </div>

    <script>
        // Quotes array
        const quotes = [
            "හීන වලට ගිහින් එන්න කෙටි පාරක් නෑ",
         
        ];

        // Data storage
        const hoursData = JSON.parse(localStorage.getItem("hoursData")) || {
            Mon: 0, Tue: 0, Wed: 0, Thu: 0, Fri: 0, Sat: 0, Sun: 0
        };

        // Session variables
        let sessionActive = false;
        let sessionStartTime;
        let timerInterval;
        let totalSeconds = 0;

        // DOM Elements
        const sessionBtn = document.getElementById('sessionBtn');
        const popup = document.getElementById('popup');
        const popupTitle = document.getElementById('popupTitle');
        const popupMessage = document.getElementById('popupMessage');
        const popupBtn = document.getElementById('popupBtn');
        const profileStatus = document.getElementById('profileStatus');
        const statusDot = document.getElementById('statusDot');

        // Initialize on page load
        document.addEventListener('DOMContentLoaded', () => {
            document.getElementById("quote").textContent = quotes[new Date().getDate() % quotes.length];
            renderChart();
            updateCountdown();
            updateClock(); // Initial clock update
            setInterval(updateCountdown, 1000);
            setInterval(updateClock, 1000); // Keep digital clock updated
        });

        // Event Listeners
        sessionBtn.addEventListener('click', toggleSession);
        popupBtn.addEventListener('click', () => {
            popup.classList.remove('active');
        });

        // Functions
        function updateBar() {
            const day = document.getElementById("day").value;
            const hours = parseFloat(document.getElementById("hoursInput").value);
            
            if (isNaN(hours) || hours < 0 || hours > 24) { // Max hours changed to 24 for manual entry
                showPopup("Invalid Input", "Please enter a valid number between 0 and 24.");
                return;
            }
            
            hoursData[day] = hours;
            localStorage.setItem("hoursData", JSON.stringify(hoursData));
            renderChart();
            showPopup("Manual Update Done!", `Study hours for ${day} updated to ${hours.toFixed(1)}.`);
        }

        function renderChart() {
            let total = 0;
            let maxHoursDay = 24; // Default max height for 8 hours

            // Find the maximum hours for dynamic scaling of the bar chart
            for (const day in hoursData) {
                if (hoursData[day] > maxHoursDay) {
                    maxHoursDay = hoursData[day];
                }
                total += hoursData[day];
            }

            for (const day in hoursData) {
                const hours = hoursData[day];
                const bar = document.getElementById(day);
                
                // Calculate height relative to maxHoursDay, with a minimum visible height
                const barHeight = (hours / maxHoursDay) * 100; // Scale to 100% of chart height
                bar.style.height = `${Math.max(barHeight, 5)}%`; // Ensure min 5% height for visibility
                
                bar.classList.toggle("active", hours > 0);

                const hourValueSpan = bar.querySelector('.hour-value');
                if (hourValueSpan) {
                    hourValueSpan.textContent = `${hours.toFixed(1)}h`;
                }
            }

            const avg = total / 7;
            const monthTotal = avg * (365 / 12); // More accurate monthly average
            document.getElementById("avg").textContent = avg.toFixed(1) + " hours";
            document.getElementById("weekly").textContent = total.toFixed(1) + " hours";
            document.getElementById("monthly").textContent = monthTotal.toFixed(1) + " hours";
        }

        function clearData() {
            if (confirm("සියලුම ඉගෙනුම් දත්ත ඉවත් කිරීමට ඔබ නිසැකද?")) {
                for (const day in hoursData) hoursData[day] = 0;
                localStorage.setItem("hoursData", JSON.stringify(hoursData));
                renderChart();
                showPopup("Data Cleared", "All study data has been reset.");
            }
        }

        function updateCountdown() {
            // Exam date set to November 11, 2025, 9:00 AM (Singapore time zone offset)
            const examDate = new Date("2025-11-11T09:00:00+08:00").getTime(); 
            const now = new Date().getTime();
            const diff = examDate - now;
            
            if (diff <= 0) {
                document.getElementById("days").textContent = "0";
                document.getElementById("hours").textContent = "0";
                document.getElementById("minutes").textContent = "0";
                document.getElementById("seconds").textContent = "0";
                document.querySelector('.countdown-title').textContent = "Exam Time Passed!";
                return;
            }
            
            const days = Math.floor(diff / (1000 * 60 * 60 * 24));
            const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((diff % (1000 * 60)) / 1000);
            
            document.getElementById("days").textContent = days;
            document.getElementById("hours").textContent = hours;
            document.getElementById("minutes").textContent = minutes;
            document.getElementById("seconds").textContent = seconds;
        }

        function updateClock() {
            const now = new Date();
            const timeString = now.toLocaleTimeString('en-US', { hour12: true, hour: '2-digit', minute: '2-digit', second: '2-digit' });
            document.getElementById("digitalClock").textContent = timeString;
        }

        function toggleSession() {
            if (!sessionActive) {
                startSession();
            } else {
                endSession();
            }
        }

        function startSession() {
            sessionActive = true;
            sessionStartTime = new Date();
            totalSeconds = 0;
            
            sessionBtn.classList.add('active');
            profileStatus.classList.add('active');
            profileStatus.textContent = "Active Learning"; // Update text
            statusDot.style.background = 'var(--accent)'; // Ensure dot color is correct
            
            // Update button text with timer
            timerInterval = setInterval(() => {
                totalSeconds++;
                sessionBtn.textContent = `Studying: ${formatDuration(totalSeconds)}`;
            }, 1000);
            
            showPopup("Session Started!", "Your focused learning session has begun. Let's make every second count!");
        }

        function endSession() {
            sessionActive = false;
            clearInterval(timerInterval);
            sessionBtn.textContent = "Start Learning Session";
            sessionBtn.classList.remove('active');
            
            profileStatus.classList.remove('active');
            profileStatus.textContent = "Inactive Learning"; // Update text
            statusDot.style.background = '#ccc'; // Reset dot color
            
            const sessionDurationHours = totalSeconds / 3600;
            
            // Get today's day of the week
            const today = new Date();
            const dayOfWeek = today.toLocaleString('en-US', { weekday: 'short' }); // e.g., "Mon"
            
            // Add session duration to today's data, preserving existing data for the day
            hoursData[dayOfWeek] = (hoursData[dayOfWeek] || 0) + sessionDurationHours;
            localStorage.setItem("hoursData", JSON.stringify(hoursData));
            renderChart(); // Re-render chart with new data

            const durationFormatted = formatDuration(totalSeconds);
            showPopup("Great Work!", `You studied for ${durationFormatted}. Your progress has been recorded.`);
        }

        function formatDuration(seconds) {
            const hrs = Math.floor(seconds / 3600);
            const mins = Math.floor((seconds % 3600) / 60);
            const secs = seconds % 60;
            return `${hrs.toString().padStart(2, '0')}:${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
        }

        function showPopup(title, message) {
            popupTitle.textContent = title;
            popupMessage.textContent = message;
            popup.classList.add('active');
        }
    </script>
</body>
</html>
