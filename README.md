# HeartRate
HR Test
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Target Heart Rate Calculator - Find Your Perfect Training Zones</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            line-height: 1.6;
            color: #1e293b;
            background-color: #f8fafc;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
        }

        .header h1 {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 12px;
            color: #1e293b;
        }

        .header .subtitle {
            font-size: 1.25rem;
            color: #64748b;
            margin-bottom: 8px;
        }

        .header .description {
            font-size: 1rem;
            color: #64748b;
            max-width: 600px;
            margin: 0 auto;
        }

        .card {
            background: white;
            border-radius: 8px;
            box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1);
            padding: 24px;
            margin-bottom: 24px;
        }

        .card-header {
            border-bottom: 1px solid #e2e8f0;
            padding-bottom: 16px;
            margin-bottom: 24px;
        }

        .card-title {
            font-size: 1.5rem;
            font-weight: 600;
            color: #1e293b;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-label {
            display: block;
            font-weight: 500;
            margin-bottom: 8px;
            color: #1e293b;
        }

        .form-input, .form-select {
            width: 100%;
            padding: 12px 16px;
            border: 1px solid #e2e8f0;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.2s;
        }

        .form-input:focus, .form-select:focus {
            outline: none;
            border-color: #dc2626;
            box-shadow: 0 0 0 3px rgba(220, 38, 38, 0.1);
        }

        .btn {
            display: inline-block;
            padding: 12px 24px;
            font-size: 1rem;
            font-weight: 500;
            text-align: center;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-primary {
            background-color: #dc2626;
            color: white;
            width: 100%;
        }

        .btn-primary:hover {
            background-color: #b91c1c;
            transform: translateY(-1px);
        }

        .btn-secondary {
            background-color: #64748b;
            color: white;
        }

        .results {
            display: none;
            margin-top: 24px;
        }

        .results.show {
            display: block;
            animation: fadeInUp 0.4s ease-out;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .zones-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 16px;
            margin: 24px 0;
        }

        .zone-card {
            background: linear-gradient(135deg, #dc2626, #b91c1c);
            color: white;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
        }

        .zone-card.fat-burn {
            background: linear-gradient(135deg, #10b981, #059669);
        }

        .zone-card.aerobic {
            background: linear-gradient(135deg, #3b82f6, #2563eb);
        }

        .zone-card.anaerobic {
            background: linear-gradient(135deg, #f59e0b, #d97706);
        }

        .zone-card.max {
            background: linear-gradient(135deg, #dc2626, #b91c1c);
        }

        .zone-title {
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 8px;
        }

        .zone-range {
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 4px;
        }

        .zone-description {
            font-size: 0.9rem;
            opacity: 0.9;
        }

        .education-section {
            background: #f1f5f9;
            border-radius: 8px;
            padding: 24px;
            margin: 32px 0;
        }

        .education-title {
            font-size: 1.5rem;
            font-weight: 600;
            margin-bottom: 16px;
            color: #1e293b;
        }

        .flex {
            display: flex;
        }

        .gap-4 {
            gap: 1rem;
        }

        .justify-center {
            justify-content: center;
        }

        .mt-4 {
            margin-top: 1rem;
        }

        .text-center {
            text-align: center;
        }

        .mb-4 {
            margin-bottom: 1rem;
        }

        @media (max-width: 768px) {
            .container {
                padding: 16px;
            }

            .header h1 {
                font-size: 2rem;
            }

            .zones-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header class="header">
            <h1>Target Heart Rate Calculator</h1>
            <p class="subtitle">Find Your Perfect Training Zones</p>
            <p class="description">Stop guessing your target heart rate. Get personalized training zones based on your age, fitness level, and goals.</p>
        </header>

        <div class="card">
            <div class="card-header">
                <h2 class="card-title">Calculate Your Personal Heart Rate Zones</h2>
            </div>

            <form id="heartRateForm">
                <div class="form-group">
                    <label class="form-label" for="age">Your Age:</label>
                    <input type="number" id="age" class="form-input" placeholder="Enter your age" min="15" max="80" required>
                </div>

                <div class="form-group">
                    <label class="form-label" for="restingHR">Resting Heart Rate (optional):</label>
                    <input type="number" id="restingHR" class="form-input" placeholder="60-100 bpm (leave blank if unknown)" min="40" max="120">
                    <small style="color: #64748b; font-size: 0.875rem;">Measure first thing in the morning before getting out of bed</small>
                </div>

                <div class="form-group">
                    <label class="form-label" for="fitnessLevel">Current Fitness Level:</label>
                    <select id="fitnessLevel" class="form-select" required>
                        <option value="">Choose your fitness level...</option>
                        <option value="beginner">Beginner (little to no regular exercise)</option>
                        <option value="intermediate">Intermediate (exercise 2-3 times per week)</option>
                        <option value="advanced">Advanced (exercise 4+ times per week)</option>
                        <option value="athlete">Athlete (competitive or intense training)</option>
                    </select>
                </div>

                <div class="form-group">
                    <label class="form-label" for="goal">Primary Training Goal:</label>
                    <select id="goal" class="form-select" required>
                        <option value="">What's your main goal?</option>
                        <option value="fat-loss">Fat loss / Weight management</option>
                        <option value="endurance">Endurance / Cardiovascular health</option>
                        <option value="performance">Performance / Speed improvement</option>
                        <option value="general">General fitness / Health</option>
                    </select>
                </div>

                <button type="submit" class="btn btn-primary">
                    Calculate My Heart Rate Zones
                </button>
            </form>
        </div>

        <div id="results" class="results">
            <div class="card">
                <h3 class="text-center mb-4">Your Personalized Heart Rate Zones</h3>
                
                <div class="zones-grid" id="zonesGrid">
                    <!-- Zones will be populated by JavaScript -->
                </div>

                <div class="education-section">
                    <h4>How to Use Your Zones</h4>
                    <div id="goalSpecificAdvice">
                        <!-- Goal-specific advice will be populated by JavaScript -->
                    </div>
                </div>

                <div class="flex gap-4 justify-center mt-4">
                    <button onclick="resetCalculator()" class="btn btn-secondary">Calculate Again</button>
                </div>
            </div>
        </div>

        <div class="education-section">
            <h3 class="education-title">Understanding Heart Rate Training</h3>
            <div class="education-content">
                <p>Heart rate training isn't just for elite athletes. It's the most effective way to ensure you're exercising at the right intensity for your goals.</p>
                
                <h4>Why Heart Rate Zones Matter</h4>
                <ul style="margin: 12px 0; padding-left: 20px;">
                    <li style="margin-bottom: 8px;"><strong>Fat Burning Zone (50-70%):</strong> Your body primarily burns fat for fuel. Perfect for longer, easier workouts.</li>
                    <li style="margin-bottom: 8px;"><strong>Aerobic Zone (70-85%):</strong> Improves cardiovascular efficiency and endurance. Most of your training should happen here.</li>
                    <li style="margin-bottom: 8px;"><strong>Anaerobic Zone (85-95%):</strong> Builds power and speed. Use sparingly for interval training.</li>
                    <li style="margin-bottom: 8px;"><strong>Max Effort Zone (95%+):</strong> Neuromuscular power. Only for very short, intense efforts.</li>
                </ul>
            </div>
        </div>

        <footer style="text-align: center; margin-top: 48px; padding: 24px; color: #64748b;">
            <p>This is a <strong>blogifact</strong> - interactive content that provides personalized results.</p>
            <p>Want to build your own blogifacts? <a href="https://blogifact.com" style="color: #dc2626;">Learn more at blogifact.com</a></p>
        </footer>
    </div>

    <script>
        document.getElementById('heartRateForm').addEventListener('submit', function(e) {
            e.preventDefault();
            calculateHeartRateZones();
        });

        function calculateHeartRateZones() {
            const age = parseInt(document.getElementById('age').value);
            const restingHR = parseInt(document.getElementById('restingHR').value) || 70;
            const fitnessLevel = document.getElementById('fitnessLevel').value;
            const goal = document.getElementById('goal').value;

            // Calculate max heart rate
            const maxHR = 220 - age;
            
            // Calculate heart rate reserve (Karvonen method)
            const hrReserve = maxHR - restingHR;

            // Calculate zones based on heart rate reserve
            const zones = {
                fatBurn: {
                    min: Math.round(restingHR + (hrReserve * 0.5)),
                    max: Math.round(restingHR + (hrReserve * 0.7)),
                    title: "Fat Burning Zone",
                    description: "Easy pace, primarily burns fat"
                },
                aerobic: {
                    min: Math.round(restingHR + (hrReserve * 0.7)),
                    max: Math.round(restingHR + (hrReserve * 0.85)),
                    title: "Aerobic Zone", 
                    description: "Comfortable hard, builds endurance"
                },
                anaerobic: {
                    min: Math.round(restingHR + (hrReserve * 0.85)),
                    max: Math.round(restingHR + (hrReserve * 0.95)),
                    title: "Anaerobic Zone",
                    description: "Hard effort, builds power"
                },
                max: {
                    min: Math.round(restingHR + (hrReserve * 0.95)),
                    max: maxHR,
                    title: "Max Effort Zone",
                    description: "All-out effort, very short duration"
                }
            };

            displayResults(zones, goal, fitnessLevel);
        }

        function displayResults(zones, goal, fitnessLevel) {
            const zonesGrid = document.getElementById('zonesGrid');
            const goalAdvice = document.getElementById('goalSpecificAdvice');

            // Clear previous results
            zonesGrid.innerHTML = '';

            // Create zone cards
            Object.entries(zones).forEach(([key, zone]) => {
                const zoneCard = document.createElement('div');
                zoneCard.className = `zone-card ${key.replace(/([A-Z])/g, '-$1').toLowerCase()}`;
                zoneCard.innerHTML = `
                    <div class="zone-title">${zone.title}</div>
                    <div class="zone-range">${zone.min}-${zone.max} bpm</div>
                    <div class="zone-description">${zone.description}</div>
                `;
                zonesGrid.appendChild(zoneCard);
            });

            // Add goal-specific advice
            const advice = getGoalSpecificAdvice(goal, zones, fitnessLevel);
            goalAdvice.innerHTML = advice;

            // Show results
            document.getElementById('results').classList.add('show');
            document.getElementById('results').scrollIntoView({ 
                behavior: 'smooth',
                block: 'start'
            });
        }

        function getGoalSpecificAdvice(goal, zones, fitnessLevel) {
            const recommendations = {
                'fat-loss': `
                    <h4>For Fat Loss:</h4>
                    <p>Spend 70-80% of your training time in the <strong>Fat Burning Zone (${zones.fatBurn.min}-${zones.fatBurn.max} bpm)</strong>. This teaches your body to efficiently burn fat as fuel.</p>
                    <p>Add 1-2 sessions per week in the <strong>Aerobic Zone</strong> to boost your metabolism and cardiovascular health.</p>
                `,
                'endurance': `
                    <h4>For Endurance:</h4>
                    <p>Build your aerobic base with 80% of training in the <strong>Aerobic Zone (${zones.aerobic.min}-${zones.aerobic.max} bpm)</strong>.</p>
                    <p>Include one tempo session per week in the lower <strong>Anaerobic Zone</strong> to improve your lactate threshold.</p>
                `,
                'performance': `
                    <h4>For Performance:</h4>
                    <p>Follow the 80/20 rule: 80% easy training in <strong>Fat Burning and Aerobic Zones</strong>, 20% high-intensity in <strong>Anaerobic and Max Zones</strong>.</p>
                    <p>Include 2-3 high-intensity sessions per week, but always allow full recovery between them.</p>
                `,
                'general': `
                    <h4>For General Fitness:</h4>
                    <p>Focus on the <strong>Aerobic Zone (${zones.aerobic.min}-${zones.aerobic.max} bpm)</strong> for most of your workouts.</p>
                    <p>This zone improves your cardiovascular health, builds endurance, and is sustainable for long-term fitness.</p>
                `
            };

            return recommendations[goal] || recommendations['general'];
        }

        function resetCalculator() {
            document.getElementById('heartRateForm').reset();
            document.getElementById('results').classList.remove('show');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }
    </script>
</body>
</html>
