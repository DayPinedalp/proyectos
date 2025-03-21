<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Asignación de Almuerzos</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            background-color: #f8f9fa;
        }
        .container {
            max-width: 600px;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        h2 {
            color: #007bff;
        }
        .btn-primary {
            width: 100%;
        }
        .list-group-item {
            background-color: #e9ecef;
            font-weight: bold;
        }
    </style>
</head>
<body class="d-flex justify-content-center align-items-center vh-100">
    <div class="container text-center">
        <h2 class="mb-4">Asignación de Tiempos de Almuerzo</h2>
        <div class="mb-3">
            <label for="startTime" class="form-label">Hora de Inicio:</label>
            <input type="time" id="startTime" class="form-control" value="12:00">
        </div>
        <div class="mb-3">
            <label for="duration" class="form-label">Duración del Almuerzo (minutos):</label>
            <select id="duration" class="form-control">
                <option value="15">15 minutos</option>
                <option value="20">20 minutos</option>
            </select>
        </div>
        <div class="mb-3">
            <label for="employeeName" class="form-label">Nombre del Empleado:</label>
            <input type="text" id="employeeName" class="form-control" placeholder="Ingrese el nombre">
        </div>
        <button class="btn btn-primary" onclick="addEmployee()">Agregar</button>
        
        <h3 class="mt-4">Horario de Almuerzos</h3>
        <ul id="schedule" class="list-group mt-3"></ul>
    </div>

    <script>
        let employees = [];
        let startTime;
        
        function getStartTime() {
            let timeInput = document.getElementById("startTime").value;
            let [hours, minutes] = timeInput.split(":").map(Number);
            startTime = new Date();
            startTime.setHours(hours, minutes, 0, 0);
        }

        function addEmployee() {
            if (!startTime) getStartTime();
            
            let name = document.getElementById("employeeName").value.trim();
            let duration = parseInt(document.getElementById("duration").value);
            
            if (name !== "") {
                let lunchTime = new Date(startTime);
                let formattedTime = lunchTime.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
                
                employees.push({ name, time: formattedTime });
                
                renderSchedule();
                
                startTime.setMinutes(startTime.getMinutes() + duration); // Ajusta según la duración elegida
                
                document.getElementById("employeeName").value = "";
            }
        }

        function renderSchedule() {
            let scheduleList = document.getElementById("schedule");
            scheduleList.innerHTML = "";
            employees.forEach((employee) => {
                let listItem = document.createElement("li");
                listItem.className = "list-group-item";
                listItem.textContent = `${employee.name} - ${employee.time}`;
                scheduleList.appendChild(listItem);
            });
        }
    </script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
