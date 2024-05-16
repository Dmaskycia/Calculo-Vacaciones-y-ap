<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Calculadora de Días de Vacaciones y Asuntos Propios</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            font-size: 18px; /* Tamaño de letra aumentado */
            margin: 40px;
            background-color: #f4f4f9;
        }

        label {
            margin-right: 10px;
        }

        input, button, select {
            margin-bottom: 20px;
            font-size: 18px; /* Tamaño de letra aumentado */
        }

        button {
            cursor: pointer;
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 18px; /* Tamaño de letra aumentado */
        }

        #result {
            margin-top: 20px;
            font-size: 20px;
        }

        .logo {
            background-color: red;
            color: white;
            padding: 10px;
            text-align: center;
            font-size: 24px;
        }

        img {
            height: 50px;
        }
    </style>
</head>
<body>
    <div class="logo">
        <img src="305882583_548221643771156_742996996962679323_n.jpg" alt="Logo">
    </div>
    <h1>Calculadora de Días de Vacaciones y Asuntos Propios</h1>
    <form id="calculatorForm">
        <label for="timeType">Tipo de entrada:</label>
        <select id="timeType" onchange="toggleInputFields()">
            <option value="days">Días trabajados</option>
            <option value="months">Meses trabajados</option>
        </select><br>

        <label for="workedDays">Días trabajados en el año:</label>
        <input type="number" id="workedDays" required><br>

        <label for="monthsWorked" style="display: none;">Meses completos trabajados en el año:</label>
        <input type="number" id="monthsWorked" min="0" max="12" style="display: none;"><br>

        <label for="yearsOfService">Años de servicio:</label>
        <input type="number" id="yearsOfService" min="0" required><br>

        <button type="button" onclick="calculateDays()">Calcular Días</button>
    </form>
    <div id="result"></div>

    <script>
        function toggleInputFields() {
            const selection = document.getElementById('timeType').value;
            const daysInput = document.getElementById('workedDays');
            const monthsInput = document.getElementById('monthsWorked');
            const daysLabel = daysInput.previousElementSibling;
            const monthsLabel = monthsInput.previousElementSibling;

            if (selection === 'days') {
                daysInput.style.display = 'block';
                daysLabel.style.display = 'block';
                monthsInput.style.display = 'none';
                monthsLabel.style.display = 'none';
            } else {
                daysInput.style.display = 'none';
                daysLabel.style.display = 'none';
                monthsInput.style.display = 'block';
                monthsLabel.style.display = 'block';
            }
        }

        function calculateDays() {
            const type = document.getElementById('timeType').value;
            const yearsOfService = parseInt(document.getElementById('yearsOfService').value);
            let workedDays;

            if (type === 'months') {
                const monthsWorked = parseFloat(document.getElementById('monthsWorked').value);
                const daysPerMonth = 365 / 12; // Promedio de días por mes
                workedDays = monthsWorked * daysPerMonth;
            } else {
                workedDays = parseFloat(document.getElementById('workedDays').value);
            }

            let vacationDaysPerYear = 22; // Días hábiles de vacaciones por año
            let ownAffairsDaysPerYear = 7; // Días de asuntos propios por año

            // Ajuste de días de vacaciones por antigüedad
            if (yearsOfService >= 30) {
                vacationDaysPerYear += 4;
            } else if (yearsOfService >= 25) {
                vacationDaysPerYear += 3;
            } else if (yearsOfService >= 20) {
                vacationDaysPerYear += 2;
            } else if (yearsOfService >= 15) {
                vacationDaysPerYear += 1;
            }

            // Ajuste de días de asuntos propios por antigüedad
            if (yearsOfService >= 18) {
                ownAffairsDaysPerYear += 2;
            }
            if (yearsOfService >= 27) {
                ownAffairsDaysPerYear += Math.floor((yearsOfService - 27) / 3) + 1;
            }

            const vacationDays = (workedDays / 365) * vacationDaysPerYear;
            const ownAffairsDays = (workedDays / 365) * ownAffairsDaysPerYear;

            const resultDiv = document.getElementById('result');
            resultDiv.innerHTML = `Basado en ${workedDays.toFixed(0)} días trabajados y ${yearsOfService} años de servicio, te corresponden ${vacationDays.toFixed(2)} días de vacaciones y ${ownAffairsDays.toFixed(2)} días de asuntos propios 2024.`;
        }
    </script>
</body>
</html>
