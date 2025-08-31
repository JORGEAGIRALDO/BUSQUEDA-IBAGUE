# BUSQUEDA-IBAGUE
PAGINA PARA BUSCAR INFORMACION TORNEO DE IBAGUE
TYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Búsqueda de Participante</title>
    <!-- Incluye Tailwind CSS para un diseño moderno y responsivo -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6;
            min-height: 100vh;
        }
    </style>
</head>
<body class="flex items-center justify-center p-4">

    <!-- Contenedor principal de la aplicación -->
    <div class="bg-white p-8 rounded-2xl shadow-2xl w-full max-w-lg space-y-6">

        <!-- Título y descripción -->
        <div class="text-center">
            <h1 class="text-3xl md:text-4xl font-bold text-gray-800">Buscar mi Información</h1>
            <p class="mt-2 text-gray-500">Ingresa tu nombre o número de cédula para ver tus datos.</p>
        </div>

        <!-- Formulario de búsqueda -->
        <form id="searchForm" class="space-y-4">
            <div>
                <label for="nombreInput" class="block text-sm font-medium text-gray-700">Nombre completo</label>
                <input type="text" id="nombreInput" placeholder="Ej: Juan Pérez" class="mt-1 block w-full px-4 py-2 bg-gray-100 border-gray-300 rounded-lg shadow-sm focus:ring-indigo-500 focus:border-indigo-500">
            </div>
            <div>
                <label for="cedulaInput" class="block text-sm font-medium text-gray-700">Cédula</label>
                <input type="text" id="cedulaInput" placeholder="Ej: 1234567890" class="mt-1 block w-full px-4 py-2 bg-gray-100 border-gray-300 rounded-lg shadow-sm focus:ring-indigo-500 focus:border-indigo-500">
            </div>
            <button type="submit" class="w-full flex justify-center py-3 px-4 border border-transparent rounded-lg shadow-sm text-sm font-semibold text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition duration-150 ease-in-out">
                Buscar
            </button>
        </form>

        <!-- Área para mostrar los resultados -->
        <div id="resultadosDiv" class="mt-6 p-6 bg-gray-50 rounded-lg border-2 border-gray-200 text-center">
            <p class="text-gray-400">La información del participante aparecerá aquí.</p>
        </div>

    </div>

    <script>
        // Datos de los 55 participantes
        const participantes = [
            { nombre: "JOSE LUIS SUAREZ", cedula: "1094911364", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JOSE HERIB SALCEDO", cedula: "19080733", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "FELIPE CONTECHA", cedula: "5880984", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "GUSTAVO JIMENEZ", cedula: "10229696", ciudad: "MANIZALES", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "DANIEL MEJIA", cedula: "19093578", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "FERNANDO MONTOYA", cedula: "10219842", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JHON FABER CARMONA", cedula: "7556478", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "RUBEN VELEZ", cedula: "13254775", ciudad: "B/MANGA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "RAMON MEJIA", cedula: "5946324", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JAIME SARMIENTO", cedula: "11335561", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JOHAN GALVIS", cedula: "9730305", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JOSE WILSON SUAREZ", cedula: "7532331", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "CARLOS FAB MARTINEZ", cedula: "19472741", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "CESAR LOZANO", cedula: "93365816", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "ORLANDO VIVAS", cedula: "3202568", ciudad: "MANIZALES", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "ISMAEL CUARTAS", cedula: "17181874", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "PEDRO FELIPE DAZA", cedula: "19165780", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "ANDRES FELIPE SUAREZ", cedula: "1094900739", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JAIME RIVERO", cedula: "17165980", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "YEZID RODRIGUEZ", cedula: "93364641", ciudad: "MEDELLIN", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JOHNATHAN ARISTIZABAL", cedula: "14138297", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "RUBEN ESTRADA", cedula: "70103436", ciudad: "MANIZALES", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JOHN GIRALDO V", cedula: "7531403", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JAIME ANDRES RIVERO", cedula: "79778397", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JOTA MARIO VALDER", cedula: "98557259", ciudad: "MEDELLIN", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "ROBERTO LASERNA", cedula: "79235615", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "ARLEY DUQUE", cedula: "7540124", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "RICARDO GARCIA", cedula: "14239530", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "URIEL PINILLA", cedula: "14219070", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "ALVARO ROJAS", cedula: "19324907", ciudad: "PEREIRA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "AMADO SALAZAR", cedula: "93373346", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "OSCAR COLONIA", cedula: "71600566", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "BASILIO ALVARADO", cedula: "17051298", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "RAFAEL TORRES", cedula: "19073061", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "LUIS GOMEZ MEJIA", cedula: "4323393", ciudad: "PEREIRA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "CARLOS E. OSPINA", cedula: "93354751", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JOSE LUIS RIVEROS", cedula: "3195380", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "GERSON BELTRAN", cedula: "7302237", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "LEONIDAS TORRES", cedula: "19497104", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "ARGEMIRO AGUIRRE", cedula: "93362586", ciudad: "VENECIA COL.", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "DIEGO PALACIO L.", cedula: "75075816", ciudad: "MANIZALES", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "ELKIN CORREA", cedula: "19351879", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "HERNANDO OVIEDO", cedula: "17162091", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "BELMER PAEZ", cedula: "79412540", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "HUMBERTO BUITRAGO", cedula: "10019527", ciudad: "PEREIRA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "LUIS FDO SALAZAR", cedula: "10240145", ciudad: "PEREIRA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JAMES GOMEZ", cedula: "18463123", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JORGE OSORIO", cedula: "14243360", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "OSMAN OLAYA", cedula: "93357581", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "MAURICIO RIVERA", cedula: "18594552", ciudad: "PEREIRA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "OSCAR RAMIREZ", cedula: "6789647", ciudad: "PEREIRA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "FERNANDO ARANGO", cedula: "98546097", ciudad: "VENECIA COL.", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "HOLMER PUENTES", cedula: "94250412", ciudad: "ARMENIA", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "EMIRO SANCHEZ", cedula: "19338744", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
            { nombre: "JULIO RODRIGUEZ", cedula: "19149998", ciudad: "IBAGUE", horarioDeJuego: "17/8/25 1:00 PM, 18/5/25 4:00 PM, 18/5/25 5:00 PM" },
        ];

        // Obtener elementos del DOM
        const searchForm = document.getElementById('searchForm');
        const nombreInput = document.getElementById('nombreInput');
        const cedulaInput = document.getElementById('cedulaInput');
        const resultadosDiv = document.getElementById('resultadosDiv');

        // Escuchar el evento de envío del formulario
        searchForm.addEventListener('submit', (e) => {
            e.preventDefault(); // Evitar que la página se recargue

            // Limpiar el contenido anterior
            resultadosDiv.innerHTML = '';
            resultadosDiv.classList.add('text-center');

            // Obtener los valores de los campos y convertirlos a minúsculas
            const nombreBusqueda = nombreInput.value.trim().toLowerCase();
            const cedulaBusqueda = cedulaInput.value.trim();

            const resultados = [];

            // Buscar en la lista de participantes y almacenar todos los resultados
            for (const participante of participantes) {
                const nombreParticipante = participante.nombre.trim().toLowerCase();
                const cedulaParticipante = participante.cedula.trim();

                if ((nombreBusqueda && nombreParticipante.includes(nombreBusqueda)) ||
                    (cedulaBusqueda && cedulaParticipante.includes(cedulaBusqueda))) {
                    resultados.push(participante);
                }
            }

            // Mostrar los resultados
            if (resultados.length > 0) {
                resultadosDiv.classList.remove('text-gray-400', 'border-gray-200');
                resultadosDiv.classList.add('text-gray-700', 'space-y-4');
                resultadosDiv.classList.remove('text-center');
                
                let resultadosHTML = '';
                resultados.forEach(participante => {
                    resultadosHTML += `
                        <div class="p-4 bg-white rounded-lg shadow-sm border border-gray-200">
                            <h3 class="text-xl font-bold mb-2">${participante.nombre}</h3>
                            <p class="text-sm"><strong>Cédula:</strong> ${participante.cedula}</p>
                            <p class="text-sm"><strong>Ciudad:</strong> ${participante.ciudad}</p>
                            <p class="text-sm"><strong>Horario de Juego:</strong> ${participante.horarioDeJuego}</p>
                        </div>
                    `;
                });
                resultadosDiv.innerHTML = resultadosHTML;
            } else {
                resultadosDiv.classList.remove('text-gray-700', 'space-y-4');
                resultadosDiv.classList.add('text-gray-400', 'border-gray-200');
                resultadosDiv.classList.add('text-center');
                resultadosDiv.innerHTML = `<p>No se encontró ningún participante con esa información.</p>`;
            }
        });
    </script>
</body>
</html>
