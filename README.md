html_content = '''<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TecWeek ED — Banco de Prompts Pedagógicos</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        primary: { 50: '#f0f9ff', 100: '#e0f2fe', 500: '#0284c7', 600: '#0369a1', 700: '#0369a1' },
                        primario: '#22c55e',
                        secundario: '#3b82f6',
                        transversal: '#a855f7'
                    }
                }
            }
        }
    </script>
    <style>
        .custom-scrollbar::-webkit-scrollbar { width: 6px; height: 6px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: transparent; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        .dark .custom-scrollbar::-webkit-scrollbar-thumb { background: #475569; }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 dark:bg-slate-900 dark:text-slate-100 min-h-screen flex flex-col transition-colors duration-200">

    <!-- Header Navigation -->
    <header class="sticky top-0 z-40 bg-white/90 dark:bg-slate-800/90 backdrop-blur border-b border-slate-200 dark:border-slate-700 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3 flex flex-wrap justify-between items-center gap-4">
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-sky-500 to-indigo-600 flex items-center justify-center text-white font-bold text-xl shadow-md">
                    ED
                </div>
                <div>
                    <h1 class="text-xl font-bold tracking-tight bg-gradient-to-r from-sky-600 to-indigo-600 dark:from-sky-400 dark:to-indigo-400 bg-clip-text text-transparent">
                        TecWeek ED
                    </h1>
                    <p class="text-xs text-slate-500 dark:text-slate-400">Banco de Prompts Pedagógicos · IA para la Práctica Docente</p>
                </div>
            </div>

            <div class="flex items-center space-x-2 sm:space-x-4">
                <nav class="flex bg-slate-100 dark:bg-slate-700 p-1 rounded-lg text-xs font-semibold text-slate-600 dark:text-slate-300">
                    <button onclick="switchTab('prompts')" id="tab-prompts" class="px-3 py-1.5 rounded-md bg-white dark:bg-slate-800 text-sky-600 dark:text-sky-400 shadow-sm transition">
                        <i class="fa-solid fa-list-check mr-1.5"></i>Prompts
                    </button>
                    <button onclick="switchTab('anatomy')" id="tab-anatomy" class="px-3 py-1.5 rounded-md hover:text-slate-900 dark:hover:text-white transition">
                        <i class="fa-solid fa-graduation-cap mr-1.5"></i>Anatomía
                    </button>
                    <button onclick="switchTab('builder')" id="tab-builder" class="px-3 py-1.5 rounded-md hover:text-slate-900 dark:hover:text-white transition">
                        <i class="fa-solid fa-wand-magic-sparkles mr-1.5"></i>Creador
                    </button>
                    <button onclick="switchTab('ethics')" id="tab-ethics" class="px-3 py-1.5 rounded-md hover:text-slate-900 dark:hover:text-white transition">
                        <i class="fa-solid fa-shield-halved mr-1.5"></i>Ética
                    </button>
                </nav>

                <button onclick="toggleDarkMode()" class="p-2 rounded-lg border border-slate-200 dark:border-slate-700 hover:bg-slate-100 dark:hover:bg-slate-700 text-slate-600 dark:text-slate-300 transition" title="Cambiar Tema">
                    <i class="fa-solid fa-moon dark:hidden"></i>
                    <i class="fa-solid fa-sun hidden dark:block text-amber-400"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex-grow w-full">

        <!-- TAB 1: BANCO DE PROMPTS -->
        <section id="view-prompts" class="space-y-6">
            
            <!-- Banner Instructivo -->
            <div class="bg-gradient-to-r from-sky-500/10 via-indigo-500/10 to-purple-500/10 border border-sky-200 dark:border-sky-800/40 rounded-2xl p-5 flex flex-col md:flex-row gap-4 items-start md:items-center justify-between">
                <div class="space-y-1">
                    <h2 class="text-lg font-semibold text-slate-900 dark:text-slate-100 flex items-center gap-2">
                        <i class="fa-solid fa-lightbulb text-amber-500"></i> ¿Cómo usar este Banco de Prompts?
                    </h2>
                    <p class="text-sm text-slate-600 dark:text-slate-300">
                        Copia cualquier prompt delimitado en las cajas de código e ingrésalo en tu IA de preferencia (<strong class="text-sky-600 dark:text-sky-400">ChatGPT, Gemini, Claude</strong>). Los prompts marcados con <span class="bg-emerald-100 dark:bg-emerald-900/40 text-emerald-700 dark:text-emerald-300 text-xs px-2 py-0.5 rounded font-mono">HTML5/Canvas</span> te entregarán un archivo web interactivo listo para ejecutar localmente en el aula sin internet.
                    </p>
                </div>
            </div>

            <!-- Panel de Filtros & Búsqueda -->
            <div class="bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-2xl p-4 shadow-sm space-y-4">
                <div class="grid grid-cols-1 md:grid-cols-4 gap-3">
                    <!-- Buscador -->
                    <div class="md:col-span-2 relative">
                        <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-3 text-slate-400"></i>
                        <input type="text" id="search-input" oninput="filterPrompts()" placeholder="Buscar por palabra clave, tema, contenido..." class="w-full pl-10 pr-4 py-2 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-sky-500">
                    </div>

                    <!-- Filtro Nivel -->
                    <div>
                        <select id="filter-level" onchange="filterPrompts()" class="w-full px-3 py-2 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-sky-500">
                            <option value="all">Todos los Niveles Educativos</option>
                            <option value="Primario">Nivel Primario</option>
                            <option value="Secundario">Nivel Secundario</option>
                            <option value="Transversal">Transversal / DUA</option>
                        </select>
                    </div>

                    <!-- Filtro Área -->
                    <div>
                        <select id="filter-area" onchange="filterPrompts()" class="w-full px-3 py-2 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-sky-500">
                            <option value="all">Todas las Áreas / Materias</option>
                            <option value="Matemática">Matemática</option>
                            <option value="Lengua">Literatura y Prácticas del Lenguaje</option>
                            <option value="Sociales">Historia y Ciencias Sociales</option>
                            <option value="Biología">Biología y Ciencias Naturales</option>
                            <option value="Física y Química">Física y Química</option>
                            <option value="Tecnología">Tecnología, Robótica y Pensamiento Computacional</option>
                            <option value="Economía">Economía y Ed. Financiera</option>
                            <option value="Filosofía">Filosofía y Pensamiento Crítico</option>
                            <option value="Educación Física">Educación Física y Salud</option>
                            <option value="Ciudadanía">Formación Ética y Ciudadana</option>
                            <option value="Artes Visuales">Artes Visuales</option>
                            <option value="Música">Educación Musical</option>
                            <option value="Inglés">Lenguas Extranjeras (Inglés / ESL)</option>
                            <option value="Geografía">Geografía y Gestión Ambiental</option>
                            <option value="DUA">Inclusión y DUA</option>
                        </select>
                    </div>
                </div>

                <!-- Chips de Acceso Rápido -->
                <div class="flex flex-wrap gap-2 pt-2 border-t border-slate-100 dark:border-slate-700/50 text-xs">
                    <span class="text-slate-400 self-center font-medium">Formatos Rápidos:</span>
                    <button onclick="setFormatFilter('all')" class="format-chip px-2.5 py-1 rounded-lg bg-slate-200 dark:bg-slate-700 font-medium">Todos</button>
                    <button onclick="setFormatFilter('HTML5 / CANVAS')" class="format-chip px-2.5 py-1 rounded-lg bg-emerald-100 dark:bg-emerald-900/30 text-emerald-700 dark:text-emerald-300 font-medium">HTML5 / Canvas</button>
                    <button onclick="setFormatFilter('JUEGO CONVERSACIONAL')" class="format-chip px-2.5 py-1 rounded-lg bg-indigo-100 dark:bg-indigo-900/30 text-indigo-700 dark:text-indigo-300 font-medium">Juego Conversacional</button>
                    <button onclick="setFormatFilter('SIMULADOR WEB')" class="format-chip px-2.5 py-1 rounded-lg bg-purple-100 dark:bg-purple-900/30 text-purple-700 dark:text-purple-300 font-medium">Simulador Web</button>
                </div>
            </div>

            <!-- Lista Dinámica de Prompts -->
            <div id="prompts-grid" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Se poblará vía JavaScript -->
            </div>

            <!-- Estado Vacío -->
            <div id="empty-state" class="hidden text-center py-12 bg-white dark:bg-slate-800 rounded-2xl border border-dashed border-slate-300 dark:border-slate-700">
                <i class="fa-solid fa-folder-open text-4xl text-slate-300 dark:text-slate-600 mb-3"></i>
                <p class="text-slate-500 dark:text-slate-400 font-medium">No se encontraron prompts para los filtros seleccionados.</p>
                <button onclick="resetFilters()" class="mt-3 px-4 py-2 bg-sky-600 text-white rounded-lg text-sm hover:bg-sky-700 transition">Restablecer filtros</button>
            </div>
        </section>

        <!-- TAB 2: ANATOMÍA DE UN PROMPT -->
        <section id="view-anatomy" class="hidden space-y-6">
            <div class="bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-2xl p-6 shadow-sm space-y-6">
                <div>
                    <h2 class="text-2xl font-bold text-slate-900 dark:text-slate-100 mb-2">Anatomía de un Prompt Pedagógico Eficaz</h2>
                    <p class="text-slate-600 dark:text-slate-300 text-sm">
                        Estructurar adecuadamente una consigna permite optimizar la precisión pedagógica y garantizar formatos de salida listos para usar en el aula.
                    </p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="p-4 rounded-xl bg-sky-50 dark:bg-sky-900/20 border border-sky-200 dark:border-sky-800">
                        <span class="text-xs font-bold uppercase tracking-wider text-sky-600 dark:text-sky-400">Paso 1</span>
                        <h3 class="text-lg font-bold text-slate-800 dark:text-slate-200 mt-1 mb-1"><i class="fa-solid fa-user-gear mr-2 text-sky-500"></i>ROL (¿Quién es la IA?)</h3>
                        <p class="text-sm text-slate-600 dark:text-slate-300">Define con precisión la identidad y nivel de experiencia. <br><em class="text-xs text-sky-700 dark:text-sky-300">Ej: "Actúa como diseñador pedagógico experto en ABP..."</em></p>
                    </div>

                    <div class="p-4 rounded-xl bg-indigo-50 dark:bg-indigo-900/20 border border-indigo-200 dark:border-indigo-800">
                        <span class="text-xs font-bold uppercase tracking-wider text-indigo-600 dark:text-indigo-400">Paso 2</span>
                        <h3 class="text-lg font-bold text-slate-800 dark:text-slate-200 mt-1 mb-1"><i class="fa-solid fa-users mr-2 text-indigo-500"></i>CONTEXTO (¿Para quién?)</h3>
                        <p class="text-sm text-slate-600 dark:text-slate-300">Especifica el nivel escolar, edad de los alumnos y marco curricular. <br><em class="text-xs text-indigo-700 dark:text-indigo-300">Ej: "Para estudiantes de 3.° año de secundaria de CABA..."</em></p>
                    </div>

                    <div class="p-4 rounded-xl bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
                        <span class="text-xs font-bold uppercase tracking-wider text-purple-600 dark:text-purple-400">Paso 3</span>
                        <h3 class="text-lg font-bold text-slate-800 dark:text-slate-200 mt-1 mb-1"><i class="fa-solid fa-list-check mr-2 text-purple-500"></i>TAREA / INSTRUCCIÓN</h3>
                        <p class="text-sm text-slate-600 dark:text-slate-300">Detalla los pasos secuenciales y límites claros de contenido. <br><em class="text-xs text-purple-700 dark:text-purple-300">Ej: "Crea 3 problemas con dilemas reales y pistas visuales..."</em></p>
                    </div>

                    <div class="p-4 rounded-xl bg-emerald-50 dark:bg-emerald-900/20 border border-emerald-200 dark:border-emerald-800">
                        <span class="text-xs font-bold uppercase tracking-wider text-emerald-600 dark:text-emerald-400">Paso 4</span>
                        <h3 class="text-lg font-bold text-slate-800 dark:text-slate-200 mt-1 mb-1"><i class="fa-solid fa-file-code mr-2 text-emerald-500"></i>FORMATO DE SALIDA</h3>
                        <p class="text-sm text-slate-600 dark:text-slate-300">Indica la estructura exacta requerida. <br><em class="text-xs text-emerald-700 dark:text-emerald-300">Ej: "En UN ÚNICO ARCHIVO HTML/CSS/JS autocontenido..."</em></p>
                    </div>
                </div>

                <!-- Técnicas Avanzadas -->
                <div class="border-t border-slate-200 dark:border-slate-700 pt-6">
                    <h3 class="text-lg font-bold mb-3 text-slate-900 dark:text-slate-100"><i class="fa-solid fa-bolt text-amber-500 mr-2"></i>Técnicas Avanzadas de Ingeniería de Prompts para Docentes</h3>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-sm">
                        <div class="p-4 bg-slate-50 dark:bg-slate-900 rounded-xl border border-slate-200 dark:border-slate-700">
                            <h4 class="font-bold text-sky-600 dark:text-sky-400 mb-1">Few-Shot Prompting</h4>
                            <p class="text-xs text-slate-600 dark:text-slate-300">Incluye 1 o 2 ejemplos del tipo de respuesta esperada en la consigna para fijar el estilo o la estructura deseada.</p>
                        </div>
                        <div class="p-4 bg-slate-50 dark:bg-slate-900 rounded-xl border border-slate-200 dark:border-slate-700">
                            <h4 class="font-bold text-indigo-600 dark:text-indigo-400 mb-1">Chain-of-Thought (CoT)</h4>
                            <p class="text-xs text-slate-600 dark:text-slate-300">Agrega "Razona paso a paso antes de responder" para mejorar sustancialmente la precisión en problemas matemáticos y biológicos.</p>
                        </div>
                        <div class="p-4 bg-slate-50 dark:bg-slate-900 rounded-xl border border-slate-200 dark:border-slate-700">
                            <h4 class="font-bold text-purple-600 dark:text-purple-400 mb-1">Roleplaying Ficticio</h4>
                            <p class="text-xs text-slate-600 dark:text-slate-300">Pide a la IA: "Simula ser un estudiante de 14 años con dudas sobre la materia y hazme 3 preguntas difíciles" para entrenar explicaciones pedagógicas.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- TAB 3: CREADOR ASISTIDO DE PROMPTS -->
        <section id="view-builder" class="hidden space-y-6">
            <div class="bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-2xl p-6 shadow-sm space-y-6">
                <div>
                    <h2 class="text-2xl font-bold text-slate-900 dark:text-slate-100 mb-1"><i class="fa-solid fa-wand-magic-sparkles text-sky-500 mr-2"></i>Creador Asistido de Prompts</h2>
                    <p class="text-slate-600 dark:text-slate-300 text-sm">Completa el formulario para generar tu prompt pedagógico optimizado listo para copiar.</p>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <!-- Formulario de Construcción -->
                    <div class="space-y-4 text-sm">
                        <div>
                            <label class="block font-semibold text-slate-700 dark:text-slate-300 mb-1">1. Rol de la IA</label>
                            <input type="text" id="build-role" oninput="updateBuiltPrompt()" placeholder="Ej: Diseñador pedagógico experto en biología secundaria" class="w-full px-3 py-2 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl">
                        </div>

                        <div>
                            <label class="block font-semibold text-slate-700 dark:text-slate-300 mb-1">2. Nivel Educativo / Contexto</label>
                            <input type="text" id="build-context" oninput="updateBuiltPrompt()" placeholder="Ej: Para alumnos de 4.° año de secundaria, tema fotosíntesis" class="w-full px-3 py-2 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl">
                        </div>

                        <div>
                            <label class="block font-semibold text-slate-700 dark:text-slate-300 mb-1">3. Tarea / Consigna Pedagógica</label>
                            <textarea id="build-task" oninput="updateBuiltPrompt()" rows="3" placeholder="Ej: Crea una secuencia de 3 actividades con dilemas prácticos reales y preguntas disparadoras..." class="w-full px-3 py-2 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl custom-scrollbar"></textarea>
                        </div>

                        <div>
                            <label class="block font-semibold text-slate-700 dark:text-slate-300 mb-1">4. Formato de Salida Requerido</label>
                            <select id="build-format" onchange="updateBuiltPrompt()" class="w-full px-3 py-2 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl">
                                <option value="En UN ÚNICO ARCHIVO HTML/CSS/JS autocontenido con HTML5 Canvas listo para ejecutar en el navegador.">Aplicación Web Interactiva (HTML/Canvas Autocontenido)</option>
                                <option value="En formato de Secuencia Didáctica estructurada con objetivos, actividades y rúbrica.">Secuencia Didáctica Estructurada</option>
                                <option value="Como motor de Juego Conversacional donde interactúes turno a turno con el estudiante.">Juego Conversacional / Tutor Interactivo</option>
                                <option value="En formato de Tabla Comparativa y Guía de Análisis para coevaluación entre pares.">Tabla Comparativa y Guía de Análisis</option>
                            </select>
                        </div>
                    </div>

                    <!-- Previsualización -->
                    <div class="flex flex-col h-full bg-slate-900 text-slate-100 rounded-2xl p-5 border border-slate-800 shadow-inner">
                        <div class="flex justify-between items-center mb-3">
                            <span class="text-xs font-mono text-slate-400"><i class="fa-solid fa-terminal mr-1.5"></i>Prompt Resultante</span>
                            <button onclick="copyBuiltPrompt()" class="px-3 py-1 bg-sky-600 hover:bg-sky-500 text-white text-xs font-semibold rounded-lg transition flex items-center gap-1.5">
                                <i class="fa-regular fa-copy"></i> Copiar Prompt
                            </button>
                        </div>
                        <div id="built-prompt-output" class="flex-grow font-mono text-xs text-sky-300 bg-slate-950/60 p-4 rounded-xl border border-slate-800 overflow-y-auto whitespace-pre-wrap custom-scrollbar leading-relaxed">
<!-- El código se generará dinámicamente -->
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- TAB 4: DECÁLOGO ÉTICO -->
        <section id="view-ethics" class="hidden space-y-6">
            <div class="bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-2xl p-6 shadow-sm space-y-6">
                <div>
                    <h2 class="text-2xl font-bold text-slate-900 dark:text-slate-100 mb-2"><i class="fa-solid fa-shield-halved text-emerald-500 mr-2"></i>Decálogo de Buenas Prácticas Éticas y Ciudadanía Digital</h2>
                    <p class="text-slate-600 dark:text-slate-300 text-sm">Pautas fundamentales para una integración responsable y crítica de la Inteligencia Artificial en el entorno escolar.</p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                    <div class="p-4 rounded-xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700">
                        <div class="w-8 h-8 rounded-lg bg-sky-100 dark:bg-sky-900/40 text-sky-600 dark:text-sky-400 flex items-center justify-center font-bold mb-3">1</div>
                        <h3 class="font-bold text-slate-800 dark:text-slate-200 mb-1">Criterio Docente Irremplazable</h3>
                        <p class="text-xs text-slate-600 dark:text-slate-400">La IA es un co-piloto didáctico. La supervisión, validación pedagógica y ajuste contextual siempre quedan a cargo del docente.</p>
                    </div>

                    <div class="p-4 rounded-xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700">
                        <div class="w-8 h-8 rounded-lg bg-emerald-100 dark:bg-emerald-900/40 text-emerald-600 dark:text-emerald-400 flex items-center justify-center font-bold mb-3">2</div>
                        <h3 class="font-bold text-slate-800 dark:text-slate-200 mb-1">Protección y Privacidad de Datos</h3>
                        <p class="text-xs text-slate-600 dark:text-slate-400">Nunca ingreses nombres completos, documentos ni datos de identificación personal de los estudiantes en plataformas de IA.</p>
                    </div>

                    <div class="p-4 rounded-xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700">
                        <div class="w-8 h-8 rounded-lg bg-indigo-100 dark:bg-indigo-900/40 text-indigo-600 dark:text-indigo-400 flex items-center justify-center font-bold mb-3">3</div>
                        <h3 class="font-bold text-slate-800 dark:text-slate-200 mb-1">Evaluación Transparente</h3>
                        <p class="text-xs text-slate-600 dark:text-slate-400">Promueve el uso explícito de la IA en los estudiantes, enseñándoles a citar sus consultas y a auditar las respuestas generadas.</p>
                    </div>

                    <div class="p-4 rounded-xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700">
                        <div class="w-8 h-8 rounded-lg bg-purple-100 dark:bg-purple-900/40 text-purple-600 dark:text-purple-400 flex items-center justify-center font-bold mb-3">4</div>
                        <h3 class="font-bold text-slate-800 dark:text-slate-200 mb-1">Mitigación Activa de Sesgos</h3>
                        <p class="text-xs text-slate-600 dark:text-slate-400">Contrasta con fuentes primarias y libros de texto reconocidos cualquier afirmación histórica, social o científica generada por IA.</p>
                    </div>

                    <div class="p-4 rounded-xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700">
                        <div class="w-8 h-8 rounded-lg bg-amber-100 dark:bg-amber-900/40 text-amber-600 dark:text-amber-400 flex items-center justify-center font-bold mb-3">5</div>
                        <h3 class="font-bold text-slate-800 dark:text-slate-200 mb-1">Autocontención e Inclusión Técnica</h3>
                        <p class="text-xs text-slate-600 dark:text-slate-400">Prioriza prompts que generen aplicaciones HTML5/Canvas autocontenidas que puedan ejecutarse sin internet en las compus de la escuela.</p>
                    </div>

                    <div class="p-4 rounded-xl bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700">
                        <div class="w-8 h-8 rounded-lg bg-rose-100 dark:bg-rose-900/40 text-rose-600 dark:text-rose-400 flex items-center justify-center font-bold mb-3">6</div>
                        <h3 class="font-bold text-slate-800 dark:text-slate-200 mb-1">Fomento de la Autonomía Critica</h3>
                        <p class="text-xs text-slate-600 dark:text-slate-400">Enseña a los alumnos que la IA es una herramienta para potenciar la curiosidad y la producción propia, no un sustituto del pensamiento crítico.</p>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- Modal Detalle del Prompt -->
    <div id="modal-backdrop" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-2xl max-w-2xl w-full p-6 shadow-2xl relative space-y-4 max-h-[90vh] overflow-y-auto custom-scrollbar">
            <button onclick="closeModal()" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600 dark:hover:text-slate-200 text-lg p-1">
                <i class="fa-solid fa-xmark"></i>
            </button>

            <div id="modal-content">
                <!-- Se poblará vía JS -->
            </div>
        </div>
    </div>

    <!-- Toast de Notificación -->
    <div id="toast" class="fixed bottom-5 right-5 bg-slate-900 text-white px-4 py-2.5 rounded-xl shadow-xl flex items-center gap-2 text-sm font-medium transition transform translate-y-20 opacity-0 z-50">
        <i class="fa-solid fa-circle-check text-emerald-400"></i>
        <span id="toast-message">Prompt copiado al portapapeles</span>
    </div>

    <!-- Footer -->
    <footer class="bg-white dark:bg-slate-800 border-t border-slate-200 dark:border-slate-700 py-6 mt-12 text-center text-xs text-slate-500 dark:text-slate-400">
        <div class="max-w-7xl mx-auto px-4 space-y-2">
            <p><strong class="text-slate-700 dark:text-slate-300">Banco de Prompts Pedagógicos — TecWeek ED 2026</strong></p>
            <p>Recursos de Inteligencia Artificial para la Práctica Docente · Edición Aulas Dinámicas & Canvas HTML5</p>
        </div>
    </footer>

    <!-- Script de Datos y Lógica -->
    <script>
        const promptsData = [
            {
                id: "p1_1",
                area: "Matemática",
                nivel: "Primario",
                codigo: "Prompt 1.1",
                titulo: "Generador de Desafíos Matemáticos Narrativos",
                formato: "SECUENCIA DIDÁCTICA",
                promptText: "Actúa como diseñador pedagógico de primaria. Diseña una secuencia de 3 problemas matemáticos enmarcados en una narrativa continua de aventura (ej. expedición espacial) para estudiantes de 5.° o 6.° grado.\\nTema: Suma, resta y comparación de fracciones heterogéneas y decimales.\\nRequisitos: 1. Cada problema debe plantear un dilema con contexto práctico real. 2. Incluye una sección de 'Pistas visuales' para estudiantes con dificultades. 3. Añade la solución paso a paso orientada al docente con representaciones concretas sugeridas (recta numérica, barras).",
                recomendacion: "Ideal para iniciar unidades didácticas integrando la narrativa como hilo conductor. Permite trabajar el error como oportunidad de aprendizaje."
            },
            {
                id: "p1_2",
                area: "Matemática",
                nivel: "Primario",
                codigo: "Prompt 1.2",
                titulo: "Aplicación Web Interactiva - 'El Castillo de las Tablas'",
                formato: "HTML5 / CANVAS",
                promptText: "Actúa como desarrollador web educativo. Genera un juego interactivo en UN ÚNICO ARCHIVO HTML/CSS/JS autocontenido de cálculo mental para 3.° y 4.° grado.\\nContenido: Tablas de multiplicar (2 al 12) y divisiones sencillas.\\nMecánica: El estudiante resuelve operaciones para abrir puertas de un castillo con temporizador visual de 15s por pregunta.\\nInterfaz: Contador de puntos, vidas (corazones), retroalimentación en verde/rojo y pantalla final con diplomas ('Caballero Matemático', 'Aprendiz').",
                recomendacion: "Copia la salida en un archivo con extensión .html y ejecútalo directamente en cualquier navegador sin conexión a internet."
            },
            {
                id: "p2_1",
                area: "Matemática",
                nivel: "Secundario",
                codigo: "Prompt 2.1",
                titulo: "Modelización de Situaciones Reales (Funciones)",
                formato: "ABP / SECUENCIA",
                promptText: "Actúa como docente de matemática secundaria. Diseña una unidad de Aprendizaje Basado en Problemas (ABP) sobre Funciones Lineales y Cuadráticas.\\nEstructura: 1. Caso real: Análisis financiero juvenil (emprendimiento o plan de datos móviles). 2. Guía de trabajo: 4 preguntas progresivas para tabular datos, deducir la fórmula analítica f(x), graficar e interpretar vértices/puntos de equilibrio. 3. Rúbrica: Criterios de Formulación analítica, Interpretación gráfica y Argumentación.",
                recomendacion: "Conecta conceptos abstractos algebraicos con situaciones económicas reales vividas por los adolescentes."
            },
            {
                id: "p2_2",
                area: "Matemática",
                nivel: "Secundario",
                codigo: "Prompt 2.2",
                titulo: "Simulador Web Interactivo de Estadística y Probabilidad",
                formato: "SIMULADOR WEB",
                promptText: "Desarrolla en un ÚNICO ARCHIVO HTML/CSS/JS un Simulador de Laboratorio Estadístico.\\nFuncionalidades: 1. Generador interactivo de datos (lanzamiento virtual de dados con N = 10, 100, 1000 repeticiones). 2. Cálculo automático en tiempo real de Media, Mediana, Moda y Desvío Estándar. 3. Gráfico dinámico en HTML Canvas comparando frecuencia relativa acumulada vs. probabilidad teórica.",
                recomendacion: "Excelente para demostrar empíricamente la Ley de los Grandes Números directamente en la pantalla."
            },
            {
                id: "p3_1",
                area: "Lengua",
                nivel: "Secundario",
                codigo: "Prompt 3.1",
                titulo: "Juego de Rol Textual e Historia Interactiva",
                formato: "JUEGO CONVERSACIONAL",
                promptText: "Actúa como motor de aventura conversacional estilo 'Elige tu propia aventura' ambientado en la obra 'El Lazarillo de Tormes' (o 'El Martín Fierro').\\nMecánica para el aula: Presenta la escena inicial tomando el rol del protagonista e interpelando al estudiante. 2. Da 3 opciones de decisión coherentes con la obra y 1 opción de texto libre. 3. Evalúa la respuesta del alumno: si es coherente con el contexto de la época, avanza la trama; si hay anacronismos, explica el marco histórico y sugiere reintentar.",
                recomendacion: "Permite trabajar la empatía lectora y la comprensión del contexto sociocultural de las obras literarias."
            },
            {
                id: "p3_2",
                area: "Lengua",
                nivel: "Secundario",
                codigo: "Prompt 3.2",
                titulo: "Taller de Análisis y Creación Poética Comparada",
                formato: "ESCRITURA CREATIVA",
                promptText: "Diseña una guía de taller de escritura y análisis poético para ciclo superior de secundaria sobre Vanguardias del Siglo XX (Ultraísmo, Surrealismo, Creacionismo).\\nEstructura: 1. Cuadro comparativo: Métrica, verso libre y metáforas en 3 autores clave. 2. Consigna de creación asistida: Guía paso a paso para elaborar un caligrama o un poema surrealista mediante técnica de 'cadáver exquisito'. 3. Lista de cotejo: 4 indicadores para coevaluación entre pares.",
                recomendacion: "Fomenta la creatividad combinatoria y la apreciación formal de los movimientos estéticos del siglo XX."
            },
            {
                id: "p4_1",
                area: "Sociales",
                nivel: "Secundario",
                codigo: "Prompt 4.1",
                titulo: "Conferencia de Prensa Histórica (Simulación de Roles)",
                formato: "JUEGO DE ROLES",
                promptText: "Actúa como facilitador de simulaciones históricas. Prepara el guion y dinámica para una 'Conferencia de Prensa Histórica' sobre la Revolución Industrial (o Revolución de Mayo).\\nEntregables: 1. Tarjetas de rol: 4 personajes contrapuestos (empresario burgués, obrero ludita, trabajadora infantil, político higienista). 2. Preguntas detonantes: 3 preguntas incisivas para el rol de periodistas. 3. Glosario obligatorio: Términos que cada rol debe defender (capital, plusvalía, condiciones laborales).",
                recomendacion: "Entrena el debate argumentativo y la capacidad de sostener posturas contrapuestas con rigor histórico."
            },
            {
                id: "p4_2",
                area: "Sociales",
                nivel: "Secundario",
                codigo: "Prompt 4.2",
                titulo: "Línea de Tiempo Interactiva y Análisis Multicausal",
                formato: "HTML5 / CANVAS",
                promptText: "Desarrolla en un ÚNICO ARCHIVO HTML/CSS/JS una Línea de Tiempo Interactiva sobre la Primera Guerra Mundial (o la Guerra Fría).\\nCaracterísticas: 1. Botones de filtrado multidimensional: Económica, Política, Militar y Social. 2. Al hacer clic en un hito, se despliega un modal con: Fuente primaria (cita histórica), causas directas e indirectas, y un micro-quiz interactivo para validar lectura.",
                recomendacion: "El filtrado dimensional ayuda a desarmar explicaciones unicausales simples de procesos históricos complejos."
            },
            {
                id: "p5_1",
                area: "Biología",
                nivel: "Secundario",
                codigo: "Prompt 5.1",
                titulo: "Laboratorio de Genética y Cuadros de Punnett",
                formato: "SIMULADOR WEB",
                promptText: "Crea en un ÚNICO ARCHIVO HTML/CSS/JS un simulador interactivo de Leyes de Mendel y Herencia Genética para Biología.\\nFunciones: 1. Selección de genotipos parentales (homocigota dominante, recesivo, heterocigota) para caracteres fenotípicos visibles. 2. Generación automática del Cuadro de Punnett con proporciones genotípicas y fenotípicas calculadas. 3. Modo 'Desafío de Diagnóstico': dado el fenotipo de los descendientes, el estudiante debe deducir el genotipo parental.",
                recomendacion: "Visualiza de forma inmediata los cruzamientos genéticos abstractos en cuadros tabulares interactivos."
            },
            {
                id: "p5_2",
                area: "Biología",
                nivel: "Secundario",
                codigo: "Prompt 5.2",
                titulo: "Simulador Interactivo de ADN a Proteína",
                formato: "HTML5 / CANVAS",
                promptText: "Actúa como desarrollador web experto en simulación científica escolar. Crea un único archivo HTML (con CSS y JS) que sea un Simulador Interactivo de ADN a Proteína.\\nPaso 1 (ADN): Ingreso de secuencia corta o generación aleatoria.\\nPaso 2 (Transcripción): Botón 'Transcribir a ARNm' que genere la hebra complementaria (Uracilo por Timina).\\nPaso 3 (Traducción): Botón 'Traducir a Cadena de Aminoácidos' leyendo codones de 3 en 3 con los aminoácidos resultantes e imagen del código genético.",
                recomendacion: "Permite vivenciar la expresión génica paso a paso, comprendiendo el rol del Uracilo y la lectura por tripletes."
            },
            {
                id: "p6_1",
                area: "Física y Química",
                nivel: "Secundario",
                codigo: "Prompt 6.1",
                titulo: "Simulador de Cinemática (MRU y MRUA)",
                formato: "HTML5 / CANVAS",
                promptText: "Actúa como desarrollador web educativo y profesor de física. Genera una app en UN ÚNICO ARCHIVO HTML/CSS/JS con HTML5 Canvas que simule el movimiento de un vehículo en MRU y MRUA.\\nRequisitos: Sliders para ajustar velocidad inicial (v0) y aceleración (a). Gráficos dinámicos en tiempo real de Posición vs. Tiempo x(t) y Velocidad vs. Tiempo v(t). Opción de activar obstáculos en la pista para calcular distancia de frenado de emergencia.",
                recomendacion: "Facilita la vinculación entre los gráficos cartesianos de movimiento y el comportamiento físico real del objeto."
            },
            {
                id: "p7_1",
                area: "Tecnología",
                nivel: "Transversal",
                codigo: "Prompt 7.1",
                titulo: "Intérprete y Visualizador de Diagramas de Flujo",
                formato: "HTML5 / CANVAS",
                promptText: "Actúa como diseñador instruccional en tecnología escolar. Crea una app web en HTML/CSS/JS autocontenido que permita a estudiantes de 6.° de primaria a 2.° de secundaria armar diagramas de flujo mediante bloques (Inicio, Decisión, Acción, Fin).\\nMecánica: El alumno arma la lógica para resolver un problema cotidiano (ej: 'Aprender a cruzar la calle' o 'Hacer andar un robot') y presiona 'Ejecutar' para ver la animación paso a paso de su algoritmo.",
                recomendacion: "Fomenta el pensamiento algorítmico y la descomposición lógica de problemas antes de codificar."
            },
            {
                id: "p8_1",
                area: "Economía",
                nivel: "Secundario",
                codigo: "Prompt 8.1",
                titulo: "Simulador de Presupuesto y Emprendimiento Escolar",
                formato: "SIMULADOR WEB",
                promptText: "Actúa como desarrollador web y mentor de proyectos escolares. Crea una aplicación interactiva en HTML/CSS/JS para simular un microemprendimiento estudiantil (ej: venta de cuadernos artesanales o stand de comida).\\nCaracterísticas: Calculadora de Costos Fijos vs. Variables, Punto de Equilibrio interactivo con gráfico Canvas, y un slider de 'Precio de Venta' que calcula margen de ganancia e impacto en la demanda esperada.",
                recomendacion: "Excelente para proyectos interdisciplinarios de economía, matemática aplicada y emprendedurismo."
            },
            {
                id: "p9_1",
                area: "Filosofía",
                nivel: "Secundario",
                codigo: "Prompt 9.1",
                titulo: "El Ágora Socrática: Debate de Paradojas Éticas",
                formato: "JUEGO CONVERSACIONAL",
                promptText: "Actúa como tutor filosófico socrático. Elige un dilema filosófico clásico (ej: El mito de la caverna de Platón o El barco de Teseo). Entabla un diálogo participativo con el alumno formulando preguntas contundentes sobre sus respuestas, sin dar una 'verdad única', guiándolo a cuestionar sus propios supuestos y citando a autores clave del tema.",
                recomendacion: "Promueve la alfabetización filosófica y la construcción de respuestas argumentadas basadas en la duda metódica."
            },
            {
                id: "p10_1",
                area: "Educación Física",
                nivel: "Transversal",
                codigo: "Prompt 10.1",
                titulo: "Diseñador de Circuitos Motores Inclusivos (DUA)",
                formato: "SECUENCIA DIDÁCTICA",
                promptText: "Actúa como especialista en Educación Física y Diseño Universal para el Aprendizaje (DUA). Diseña un plan de 4 estaciones para desarrollar capacidades coordinativas (equilibrio, lateralidad, salto) en 3.° y 4.° grado.\\nRequisitos: Incluye adaptaciones específicas para estudiantes con movilidad reducida o baja visión, criterios de seguridad y una lista de verificación de autoevaluación motriz para los alumnos.",
                recomendacion: "Garantiza la participación efectiva de la totalidad del alumnado en las clases de educación física."
            },
            {
                id: "p12_1",
                area: "Artes Visuales",
                nivel: "Transversal",
                codigo: "Prompt 12.1",
                titulo: "Sintetizador Visual y Mezclador Cromático Canvas",
                formato: "HTML5 / CANVAS",
                promptText: "Crea una app web en UN ÚNICO ARCHIVO HTML/CSS/JS con HTML5 Canvas para Artes Visuales y Física de la Luz.\\nFuncionalidades: 1. Círculo cromático interactivo renderizado en Canvas que permite mezclar colores aditivos (RGB) y substractivos (RYB/CMYK). 2. Generador de paletas armónicas (Análogas, Complementarias, Tríadas). 3. Lienzo Canvas interactivo donde el alumno aplica la paleta creada sobre bosquejos de movimientos artísticos (Impresionismo, Cubismo, Pop Art) analizando el impacto expresivo.",
                recomendacion: "Integra conceptos plásticos con la teoría física de la luz de manera experimental e intuitiva."
            },
            {
                id: "p13_1",
                area: "Música",
                nivel: "Transversal",
                codigo: "Prompt 13.1",
                titulo: "Secuenciador Rítmico y Laboratorio de Parámetros Sonoros",
                formato: "HTML5 / CANVAS",
                promptText: "Actúa como programador y educador musical. Genera una app web interactiva en UN ÚNICO ARCHIVO HTML/CSS/JS con Web Audio API y Canvas.\\nFunciones: 1. Secuenciador rítmico matricial de 8 pasos para componer patrones de percusión. 2. Visualizador de onda sonora (osciloscopio Canvas) para manipular Altura, Duración, Intensidad y Timbre. 3. Minijuego de entrenamiento auditivo con retroalimentación sonora visual.",
                recomendacion: "Utiliza la Web Audio API nativa del navegador para producir sonido real en tiempo real sin requerir librerías externas."
            },
            {
                id: "p14_1",
                area: "Inglés",
                nivel: "Secundario",
                codigo: "Prompt 14.1",
                titulo: "Tutor Conversacional Cotidiano Adaptativo (ESL)",
                formato: "JUEGO CONVERSACIONAL",
                promptText: "Actúa como tutor interactivo de idioma inglés (ESL) para nivel A2/B1 en un juego de rol conversacional.\\nSimula un escenario real (ej. pedir comida en un restaurante, check-in en aeropuerto o entrevista de trabajo).\\nEn cada turno habla en inglés natural y añade al final de su mensaje una casilla estructurada [Feedback Pedagógico] con: 1. Correcciones gramaticales breves. 2. Vocabulario alternativo más natural. 3. Traducción al español si el estudiante tuvo dudas. Adapta el nivel de complejidad según la fluidez observada.",
                recomendacion: "Garantiza una práctica inmersiva en idioma extranjero reduciendo la ansiedad mediante retroalimentación constructiva."
            },
            {
                id: "p15_1",
                area: "Geografía",
                nivel: "Secundario",
                codigo: "Prompt 15.1",
                titulo: "CartoLab: Tectónica de Placas y Riesgo Ambiental",
                formato: "HTML5 / CANVAS",
                promptText: "Desarrolla en UN ÚNICO ARCHIVO HTML/CSS/JS una App Geográfica interactiva con HTML5 Canvas.\\nMódulos: 1. Laboratorio de Tectónica: Animación en Canvas de bordes de placas (Convergente, Divergente, Transformante) mostrando orogénesis, fosas y epicentros sísmicos. 2. Triángulo de Riesgo Socioambiental: Simulador interactivo que permite modificar variables de Amenaza, Vulnerabilidad y Exposición para visualizar el impacto de un desastre natural en un mapa Canvas.",
                recomendacion: "Permite comprender la diferencia crítica entre un fenómeno natural, la vulnerabilidad social y un desastre socioambiental."
            },
            {
                id: "p16_1",
                area: "DUA",
                nivel: "Transversal",
                codigo: "Prompt 16.1",
                titulo: "Adaptador Universal Multimodal de Contenidos",
                formato: "ESTRATEGIA DUA",
                promptText: "Actúa como especialista en Diseño Universal para el Aprendizaje (DUA) y Educación Inclusiva.\\nTome el siguiente texto o contenido curricular: [insertar texto] y genere 3 versiones complementarias:\\n1. Versión Lectura Fácil: Estructura directa, oraciones breves y glosario explicativo para dificultades de lectura.\\n2. Versión Esquemática Visual: Mapa conceptual en formato texto/Markdown estructurado con jerarquías e íconos.\\n3. Guía de Evaluación Diversificada: 3 opciones alternativas para evaluar el objetivo sin escritura tradicional (audio-respuesta, dibujo técnico guiado, representación de rol).",
                recomendacion: "Herramienta imprescindible para diversificar guías de estudio y garantizar accesibilidad cognitiva pedagógica."
            }
        ];

        let currentActiveTab = 'prompts';
        let currentFormatFilter = 'all';

        function init() {
            renderPrompts(promptsData);
            updateBuiltPrompt();
        }

        function switchTab(tabId) {
            ['prompts', 'anatomy', 'builder', 'ethics'].forEach(tab => {
                const viewEl = document.getElementById('view-' + tab);
                const tabBtn = document.getElementById('tab-' + tab);
                if (tab === tabId) {
                    viewEl.classList.remove('hidden');
                    tabBtn.classList.add('bg-white', 'dark:bg-slate-800', 'text-sky-600', 'dark:text-sky-400', 'shadow-sm');
                } else {
                    viewEl.classList.add('hidden');
                    tabBtn.classList.remove('bg-white', 'dark:bg-slate-800', 'text-sky-600', 'dark:text-sky-400', 'shadow-sm');
                }
            });
            currentActiveTab = tabId;
        }

        function toggleDarkMode() {
            document.documentElement.classList.toggle('dark');
        }

        function renderPrompts(data) {
            const grid = document.getElementById('prompts-grid');
            const emptyState = document.getElementById('empty-state');
            grid.innerHTML = '';

            if (data.length === 0) {
                emptyState.classList.remove('hidden');
                return;
            } else {
                emptyState.classList.add('hidden');
            }

            data.forEach(item => {
                let badgeLevelClass = 'bg-blue-100 text-blue-800 dark:bg-blue-900/40 dark:text-blue-300';
                if (item.nivel === 'Primario') badgeLevelClass = 'bg-emerald-100 text-emerald-800 dark:bg-emerald-900/40 dark:text-emerald-300';
                if (item.nivel === 'Transversal') badgeLevelClass = 'bg-purple-100 text-purple-800 dark:bg-purple-900/40 dark:text-purple-300';

                const card = document.createElement('div');
                card.className = 'bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-2xl p-5 shadow-sm hover:shadow-md transition flex flex-col justify-between space-y-4';

                card.innerHTML = `
                    <div class="space-y-3">
                        <div class="flex flex-wrap items-center justify-between gap-2">
                            <span class="text-xs font-mono font-bold text-slate-400">${item.codigo}</span>
                            <div class="flex flex-wrap gap-1.5">
                                <span class="px-2 py-0.5 rounded-md text-xs font-medium ${badgeLevelClass}">${item.nivel}</span>
                                <span class="px-2 py-0.5 rounded-md text-xs font-medium bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300">${item.area}</span>
                            </div>
                        </div>

                        <h3 class="text-base font-bold text-slate-900 dark:text-slate-100">${item.titulo}</h3>

                        <div class="relative bg-slate-900 rounded-xl p-3 font-mono text-xs text-sky-300 border border-slate-800">
                            <div class="max-h-28 overflow-y-auto custom-scrollbar pr-2 leading-relaxed">
                                ${escapeHtml(item.promptText)}
                            </div>
                            <button onclick="copyText('${escapeJsString(item.promptText)}')" class="absolute top-2 right-2 bg-slate-800 hover:bg-slate-700 text-slate-200 p-1.5 rounded-md transition text-xs" title="Copiar Prompt">
                                <i class="fa-regular fa-copy"></i>
                            </button>
                        </div>
                    </div>

                    <div class="pt-2 border-t border-slate-100 dark:border-slate-700/60 flex items-center justify-between text-xs">
                        <span class="font-mono text-emerald-600 dark:text-emerald-400 font-semibold">[${item.formato}]</span>
                        <button onclick="openModal('${item.id}')" class="text-sky-600 dark:text-sky-400 hover:underline font-semibold flex items-center gap-1">
                            Ver Orientación <i class="fa-solid fa-arrow-right text-[10px]"></i>
                        </button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function filterPrompts() {
            const searchValue = document.getElementById('search-input').value.toLowerCase();
            const levelValue = document.getElementById('filter-level').value;
            const areaValue = document.getElementById('filter-area').value;

            const filtered = promptsData.filter(item => {
                const matchesSearch = item.titulo.toLowerCase().includes(searchValue) || 
                                      item.promptText.toLowerCase().includes(searchValue) ||
                                      item.area.toLowerCase().includes(searchValue);
                const matchesLevel = levelValue === 'all' || item.nivel === levelValue;
                const matchesArea = areaValue === 'all' || item.area === areaValue;
                const matchesFormat = currentFormatFilter === 'all' || item.formato === currentFormatFilter;

                return matchesSearch && matchesLevel && matchesArea && matchesFormat;
            });

            renderPrompts(filtered);
        }

        function setFormatFilter(format) {
            currentFormatFilter = format;
            filterPrompts();
        }

        function resetFilters() {
            document.getElementById('search-input').value = '';
            document.getElementById('filter-level').value = 'all';
            document.getElementById('filter-area').value = 'all';
            currentFormatFilter = 'all';
            filterPrompts();
        }

        function openModal(id) {
            const item = promptsData.find(p => p.id === id);
            if (!item) return;

            const container = document.getElementById('modal-content');
            container.innerHTML = `
                <div class="space-y-4">
                    <div class="flex items-center gap-2">
                        <span class="px-2.5 py-0.5 rounded-md text-xs font-bold bg-sky-100 text-sky-800 dark:bg-sky-900/40 dark:text-sky-300">${item.codigo}</span>
                        <span class="text-xs font-semibold text-slate-500 dark:text-slate-400">${item.area} · ${item.nivel}</span>
                    </div>

                    <h2 class="text-xl font-bold text-slate-900 dark:text-slate-100">${item.titulo}</h2>

                    <div class="space-y-1">
                        <span class="text-xs font-bold uppercase tracking-wider text-slate-400">Prompt Completo</span>
                        <div class="bg-slate-900 text-sky-300 font-mono text-xs p-4 rounded-xl border border-slate-800 whitespace-pre-wrap leading-relaxed max-h-60 overflow-y-auto custom-scrollbar">
                            ${escapeHtml(item.promptText)}
                        </div>
                    </div>

                    <div class="bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 rounded-xl p-4 text-xs text-amber-900 dark:text-amber-200 space-y-1">
                        <div class="font-bold flex items-center gap-1.5"><i class="fa-solid fa-chalkboard-user"></i> Orientación Pedagógica de Aula</div>
                        <p>${item.recomendacion}</p>
                    </div>

                    <div class="flex justify-end gap-2 pt-2">
                        <button onclick="copyText('${escapeJsString(item.promptText)}')" class="px-4 py-2 bg-sky-600 hover:bg-sky-500 text-white font-semibold text-xs rounded-xl transition flex items-center gap-1.5">
                            <i class="fa-regular fa-copy"></i> Copiar Prompt
                        </button>
                    </div>
                </div>
            `;

            document.getElementById('modal-backdrop').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('modal-backdrop').classList.add('hidden');
        }

        function updateBuiltPrompt() {
            const role = document.getElementById('build-role').value || '[Definir Rol]';
            const context = document.getElementById('build-context').value || '[Definir Nivel y Contexto]';
            const task = document.getElementById('build-task').value || '[Definir Tarea o Consigna]';
            const format = document.getElementById('build-format').value;

            const prompt = `Actúa como ${role}.\n\nContexto: Para ${context}.\n\nTarea: ${task}\n\nFormato de Salida: ${format}`;
            document.getElementById('built-prompt-output').textContent = prompt;
        }

        function copyBuiltPrompt() {
            const text = document.getElementById('built-prompt-output').textContent;
            copyText(text);
        }

        function copyText(text) {
            navigator.clipboard.writeText(text).then(() => {
                showToast('Prompt copiado al portapapeles');
            });
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-message').textContent = msg;
            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 2500);
        }

        function escapeHtml(str) {
            return str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
        }

        function escapeJsString(str) {
            return str.replace(/\\/g, '\\\\').replace(/'/g, "\\'").replace(/\n/g, '\\n');
        }

        window.onload = init;
    </script>
</body>
</html>
'''

with open("TecWeek_ED_Banco_de_Prompts.html", "w", encoding="utf-8") as f:
    f.write(html_content)

print("Archivo generado exitosamente.")
