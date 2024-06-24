<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fitness Tracking Application</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-image: url('https://images.pond5.com/fitness-app-background-sports-technology-084082512_prevstill.jpeg');
            background-size: cover;
            background-repeat: no-repeat;
            background-attachment: fixed;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start; /* Align content to the top */
            min-height: 100vh;
        }

        header {
            background: #50b3a2;
            color: white;
            padding: 20px 0;
            text-align: center;
            border-radius: 10px;
            width: 100%;
            margin-bottom: 20px;
            position: absolute; /* Position header at the top */
            top: 0;
            left: 0;
            right: 0;
        }

        header h1 {
            margin: 0;
            font-size: 24px;
            text-transform: uppercase;
        }

        .container {
            display: flex;
            justify-content: space-around;
            align-items: flex-start; /* Align items to the top of the container */
            width: 100%;
            max-width: 1200px; /* Adjust as needed */
            margin-top: 100px; /* Adjust margin to push content below header */
        }

        .left-column, .right-column {
            width: calc(50% - 20px); /* Adjust width based on your preference */
            background-color: rgba(255, 255, 255, 0.8); /* Adjust background color and transparency */
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }

        .left-column {
            margin-right: 20px;
        }

        .right-column {
            margin-left: 20px;
        }

        .activity-log h2, .progress-dashboard h2 {
            text-align: center;
            margin: 0 0 20px;
            color: #100110; /* Neon color */
        }

        .activity-log, .progress-dashboard {
            color: #150215a8; /* Neon color for text */
        }

        form {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
        }

        form label {
            margin: 10px 0 5px;
            width: 100%;
        }

        form input, form select, form button {
            padding: 10px;
            margin: 5px 0;
            width: calc(33% - 10px);
            border-radius: 5px;
            border: 1px solid #ccc;
        }

        form button {
            background: #50b3a2;
            color: #fff;
            border: 0;
            cursor: pointer;
            transition: background 0.3s;
            width: 100%;
        }

        form button:hover {
            background: #080000;
        }

        .progress-dashboard canvas {
            display: block;
            margin: 20px auto;
        }
    </style>
</head>
<body>
    <header>
        <h1>Fitness Tracker</h1>
    </header>

    <div class="container">
        <div class="left-column">
            <div class="activity-log">
                <h2>Activity Logging Page</h2>
                <form id="activityForm">
                    <label for="activityType">Activity Type:</label>
                    <select id="activityType" required>
                        <option value="Running">Running</option>
                        <option value="Cycling">Cycling</option>
                        <option value="Swimming">Swimming</option>
                        <option value="Jogging">Jogging</option>
                    </select>

                    <label for="duration">Duration (minutes):</label>
                    <input type="number" id="duration" min="1" required>

                    <label for="date">Date:</label>
                    <input type="date" id="date" required>

                    <button type="submit">Log Activity</button>
                </form>
            </div>
        </div>

        <div class="right-column">
            <div class="progress-dashboard">
                <h2>Progress Dashboard</h2>
                <canvas id="progressChart"></canvas>
            </div>
        </div>
    </div>

    <script>
        document.getElementById('activityForm').addEventListener('submit', function(event) {
            event.preventDefault();
            const activityType = document.getElementById('activityType').value;
            const duration = document.getElementById('duration').value;
            const date = document.getElementById('date').value;

            console.log(`Activity: ${activityType}, Duration: ${duration} minutes, Date: ${date}`);

            // Here you can add the code to save the data to MongoDB

            // Update the chart with the new data
            updateChart(activityType, duration, date);
        });

        const ctx = document.getElementById('progressChart').getContext('2d');
        const progressChart = new Chart(ctx, {
            type: 'bar',
            data: {
                labels: [], // Dates
                datasets: [{
                    label: 'Minutes',
                    data: [], // Duration
                    backgroundColor: 'rgba(75, 192, 192, 0.2)',
                    borderColor: 'rgba(75, 192, 192, 1)',
                    borderWidth: 1
                }]
            },
            options: {
                scales: {
                    y: {
                        beginAtZero: true
                    }
                }
            }
        });

        function updateChart(activityType, duration, date) {
            progressChart.data.labels.push(date);
            progressChart.data.datasets[0].data.push(duration);
            progressChart.update();
        }
    </script>
</body>
</html>

