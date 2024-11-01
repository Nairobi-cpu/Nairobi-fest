<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Invitación a la NAIROBI FEST</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #1c1c1c, #2a2a2a);
            color: #eaeaea;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
            position: relative; /* Permitir posicionamiento absoluto */
        }
        .container {
            max-width: 500px;
            padding: 30px;
            background: #333;
            border-radius: 12px;
            box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.5);
            margin-top: 20px;
        }
        .title {
            font-size: 2em;
            color: #ffffff;
            margin: 0;
            font-weight: bold;
        }
        .countdown {
            font-size: 1.4em;
            margin: 20px 0;
            color: #c5c5c5;
            font-weight: lighter;
        }
        .description {
            font-size: 1em;
            margin: 15px 0;
            color: #b5b5b5;
        }
        .rsvp-button {
            padding: 12px 25px;
            font-size: 1em;
            background-color: #555;
            color: #eaeaea;
            border: 1px solid #777;
            border-radius: 5px;
            cursor: pointer;
            text-decoration: none;
            transition: background-color 0.3s, transform 0.3s;
        }
        .rsvp-button:hover {
            background-color: #777;
            transform: scale(1.05);
        }
        .contact {
            font-size: 1em;
            color: #b5b5b5;
            margin: 15px 0;
        }
        .admin-section {
            margin-top: 20px;
            display: none;
        }
        .admin-input {
            display: block;
            margin: 10px 0;
            padding: 8px;
            width: calc(100% - 16px);
        }
        .admin-toggle {
            position: absolute;
            top: 20px;
            right: 20px;
            cursor: pointer;
            color: #ffffff;
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <span class="admin-toggle" id="adminToggle">Admin</span>
    <div class="container">
        <h1 class="title" id="eventTitle">NAIROBI Producc. te invita a la NAIROBI FEST</h1>
        <p id="eventDescription">Hola fiestero, ¿listo para una noche inolvidable?</p>
        <div class="countdown" id="countdown">00d 00h 00m 00s</div>
        <p class="description">No te pierdas una noche inolvidable llena de música, diversión y grandes sorpresas.</p>
        <a class="rsvp-button" href="#formulario">Reserva tu entrada</a>
    </div>

    <div id="formulario" class="container" style="display: none;">
        <h2>Formulario de Reservación</h2>
        <form id="reservationForm">
            <label for="name">Nombre:</label><br>
            <input type="text" id="name" name="name" required><br><br>
            <label>Teléfono de contacto:</label><br>
            <p class="contact">+51 960296039</p>
            <button type="submit" class="rsvp-button">Enviar</button>
        </form>
    </div>

    <!-- Sección de Administración -->
    <div class="admin-section" id="adminSection">
        <h2>Administración</h2>
        <input type="password" id="adminPassword" class="admin-input" placeholder="Ingresa la contraseña">
        <button id="adminButton" class="rsvp-button">Entrar</button>
        <div id="editSection" style="display:none; margin-top: 10px;">
            <h3>Editar Evento</h3>
            <input type="text" id="editTitle" class="admin-input" placeholder="Nuevo Título del Evento">
            <textarea id="editDescription" class="admin-input" placeholder="Nueva Descripción del Evento"></textarea>
            <button id="saveButton" class="rsvp-button">Guardar Cambios</button>
        </div>
    </div>

    <script>
        const fechaEvento = new Date("November 23, 2024 20:40:10").getTime();

        function actualizarCuentaRegresiva() {
            const ahora = new Date().getTime();
            const distancia = fechaEvento - ahora;

            const dias = Math.floor(distancia / (1000 * 60 * 60 * 24));
            const horas = Math.floor((distancia % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutos = Math.floor((distancia % (1000 * 60 * 60)) / (1000 * 60));
            const segundos = Math.floor((distancia % (1000 * 60)) / 1000);

            document.getElementById("countdown").textContent = `${dias}d ${horas}h ${minutos}m ${segundos}s`;
        }

        const intervalo = setInterval(actualizarCuentaRegresiva, 1000);

        document.querySelector('.rsvp-button').addEventListener('click', function(event) {
            event.preventDefault();
            document.getElementById('formulario').style.display = 'block';
        });

        document.getElementById('reservationForm').addEventListener('submit', function(event) {
            event.preventDefault();
            const name = document.getElementById('name').value;
            alert(`Gracias por tu reserva. Ahora comunícate al número:\n+51 960296039`);
            document.getElementById('formulario').style.display = 'none';
        });

        // Mostrar y ocultar la sección de administración
        document.getElementById('adminToggle').addEventListener('click', function() {
            const adminSection = document.getElementById('adminSection');
            if (adminSection.style.display === 'none' || adminSection.style.display === '') {
                adminSection.style.display = 'block';
            } else {
                adminSection.style.display = 'none';
            }
        });

        document.getElementById('adminButton').addEventListener('click', function() {
            const password = document.getElementById('adminPassword').value;
            if (password === 'geraukbro') { // Contraseña actualizada
                document.getElementById('editSection').style.display = 'block';
                document.getElementById('adminPassword').value = ''; // Limpiar el campo de contraseña
            } else {
                alert('Contraseña incorrecta');
            }
        });

        document.getElementById('saveButton').addEventListener('click', function() {
            const newTitle = document.getElementById('editTitle').value;
            const newDescription = document.getElementById('editDescription').value;

            if (newTitle) {
                document.getElementById('eventTitle').textContent = newTitle;
            }
            if (newDescription) {
                document.getElementById('eventDescription').textContent = newDescription;
            }
            alert('Cambios guardados!');
            document.getElementById('editTitle').value = ''; // Limpiar el campo
            document.getElementById('editDescription').value = ''; // Limpiar el campo
        });
    </script>
</body>
</html>
