# COTIZADOR-3.0
es una web realizada únicamente para realizar cotizaciones 
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>COTIZACIONES BUFFLANDIA</title>
    <!-- Google Fonts para diseño moderno -->
    <link href="googleapis.com" rel="stylesheet">
    <style>
        :root {
            --bg-gradient: linear-gradient(135deg, #1a0b2e 0%, #0d0614 100%);
            --card-bg: rgba(255, 255, 255, 0.06);
            --primary: #9d4edd;
            --primary-hover: #b5179e;
            --accent: #3f37c9;
            --text: #f8f9fa;
            --text-muted: #b0a8ba;
            --success: #4cc9f0;
            --border: rgba(255, 255, 255, 0.1);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background: var(--bg-gradient);
            color: var(--text);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-x: hidden;
        }

        /* PANTALLA DE BIENVENIDA */
        #welcome-screen {
            text-align: center;
            padding: 2rem;
            max-width: 500px;
            width: 90%;
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 24px;
            backdrop-filter: blur(12px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.5);
        }

        #welcome-screen h1 {
            font-size: 2.5rem;
            color: #fff;
            text-shadow: 0 0 15px var(--primary);
            margin-bottom: 0.5rem;
        }

        #welcome-screen p {
            color: var(--text-muted);
            margin-bottom: 2rem;
        }

        /* BOTONES REALES Y ATRACTIVOS */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            padding: 14px 28px;
            border: none;
            border-radius: 12px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            text-decoration: none;
            box-shadow: 0 6px 20px rgba(157, 78, 221, 0.3);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--primary), var(--accent));
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(157, 78, 221, 0.5);
            filter: brightness(1.1);
        }

        .btn-success {
            background: linear-gradient(135deg, #2a9d8f, #4cc9f0);
            color: #1a0b2e;
        }

        .btn-success:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(76, 201, 240, 0.5);
        }

        .btn-danger {
            background: #e63946;
            color: white;
            padding: 8px 16px;
            font-size: 0.85rem;
        }

        .btn-secondary {
            background: transparent;
            border: 2px solid var(--border);
            color: var(--text);
        }

        .btn-secondary:hover {
            background: rgba(255,255,255,0.05);
        }

        /* INTERFAZ PRINCIPAL */
        #app-screen {
            display: none;
            width: 95%;
            max-width: 1000px;
            margin: 2rem auto;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
        }

        @media (max-width: 768px) {
            #app-screen { grid-template-columns: 1fr; }
        }

        .header-app {
            grid-column: 1 / -1;
            text-align: center;
            margin-bottom: 1rem;
        }

        .header-app h2 {
            font-size: 2.2rem;
            letter-spacing: 2px;
            background: linear-gradient(to right, #fff, var(--primary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .panel {
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 2rem;
            backdrop-filter: blur(10px);
        }

        h3 {
            margin-bottom: 1.5rem;
            border-bottom: 2px solid var(--border);
            padding-bottom: 0.5rem;
            color: var(--success);
        }

        /* FORMULARIOS */
        .form-group {
            margin-bottom: 1.25rem;
        }

        .form-row-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1rem;
        }

        label {
            display: block;
            margin-bottom: 0.5rem;
            font-size: 0.9rem;
            color: var(--text-muted);
        }

        select, input, textarea {
            width: 100%;
            padding: 12px;
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid var(--border);
            border-radius: 10px;
            color: white;
            font-size: 0.95rem;
            transition: all 0.3s;
        }

        select:focus, input:focus, textarea:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 10px rgba(157, 78, 221, 0.3);
        }

        .hidden {
            display: none !important;
        }

        /* LISTA DE ITEMS Y RESUMEN */
        .item-list {
            max-height: 300px;
            overflow-y: auto;
            margin-bottom: 1.5rem;
        }

        .added-item {
            background: rgba(255,255,255,0.03);
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 1rem;
            margin-bottom: 0.75rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .added-item-info p {
            font-size: 0.9rem;
        }

        .added-item-info small {
            color: var(--text-muted);
            display: block;
        }

        .total-box {
            font-size: 1.4rem;
            font-weight: bold;
            text-align: right;
            margin-bottom: 1.5rem;
            color: var(--success);
        }

        #txt-preview {
            background: #000;
            color: #00ffcc;
            font-family: monospace;
            font-size: 0.85rem;
            height: 150px;
            resize: none;
        }

        .actions-block {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-top: 1rem;
        }
    </style>
</head>
<body>

    <!-- PANTALLA DE INICIO -->
    <div id="welcome-screen">
        <h1>BUFFLANDIA</h1>
        <p>Sistema Profesional de Cotizaciones</p>
        <button class="btn btn-primary" onclick="startApp()">COMENZAR</button>
    </div>

    <!-- AMBIENTE DEL APLICATIVO -->
    <div id="app-screen">
        <div class="header-app">
            <h2>COTIZACIONES BUFFLANDIA</h2>
        </div>

        <!-- PANEL DE CONFIGURACIÓN DE PRODUCTO -->
        <div class="panel">
            <h3>Configurar Item</h3>
            
            <div class="form-group">
                <label for="client-name">Nombre del Cliente *</label>
                <input type="text" id="client-name" placeholder="Ej. Juan Pérez">
            </div>

            <div class="form-group">
                <label for="product-select">Producto</label>
                <select id="product-select" onchange="handleProductChange()">
                    <option value="Camiseta">Camiseta</option>
                    <option value="Camiseta niñ@">Camiseta niñ@</option>
                    <option value="Mugs">Mugs</option>
                    <option value="Jarras">Jarras</option>
                    <option value="Caramañola">Caramañola</option>
                    <option value="Buff">Buff</option>
                    <option value="Vinilos">Vinilos</option>
                    <option value="Dtf">Dtf</option>
                    <option value="Diseño">Diseño</option>
                </select>
            </div>

            <!-- Campos Dinámicos según Producto -->
            <div id="type-container" class="form-group">
                <label for="type-select">Tipo</label>
                <select id="type-select" onchange="handleTypeChange()"></select>
            </div>

            <!-- Tallas para Camisetas -->
            <div id="size-container" class="form-group hidden">
                <label for="size-select">Talla de Camiseta</label>
                <select id="size-select">
                    <option value="2-4">2-4</option>
                    <option value="6-8">6-8</option>
                    <option value="10-12">10-12</option>
                    <option value="14-16">14-16</option>
                    <option value="S">S</option>
                    <option value="M">M</option>
                    <option value="L">L</option>
                    <option value="XL">XL</option>
                </select>
            </div>

            <!-- Medidas Dinámicas (Vinilo, DTF, Buff Reflectivo) -->
            <div id="measures-container" class="form-row-2 hidden">
                <div class="form-group">
                    <label for="measure-height">Alto (cm)</label>
                    <input type="number" id="measure-height" value="10" min="1">
                </div>
                <div class="form-group">
                    <label for="measure-width">Ancho (cm)</label>
                    <input type="number" id="measure-width" value="10" min="1">
                </div>
            </div>

            <!-- Tiempo en Minutos Especial para Diseño -->
            <div id="time-container" class="form-group hidden">
                <label for="design-minutes">Tiempo Estimado (Minutos - Mínimo 15)</label>
                <input type="number" id="design-minutes" value="15" min="15">
            </div>

            <!-- Casilla de Estampado -->
            <div id="print-container" class="form-group">
                <label for="print-select">¿Lleva estampado?</label>
                <select id="print-select" onchange="handlePrintChange()">
                    <option value="no">No</option>
                    <option value="si">Si</option>
                </select>
            </div>

            <!-- Detalle de Estampado -->
            <div id="print-detail-container" class="form-group hidden">
                <label for="print-detail-select">Tamaño y Estilo del Estampado</label>
                <select id="print-detail-select"></select>
            </div>

            <!-- Detalle de Buff Reflectivo -->
            <div id="buff-reflective-container" class="form-group hidden">
                <label for="buff-reflective-select">¿Lleva Reflectivo?</label>
                <select id="buff-reflective-select" onchange="handleBuffReflectiveChange()">
                    <option value="no">No</option>
                    <option value="si">Si</option>
                </select>
            </div>

            <!-- Detalle u Observaciones únicas por Item -->
            <div class="form-group">
                <label for="item-observations">Detalles / Observaciones de este ítem</label>
                <textarea id="item-observations" rows="2" placeholder="Especificar color, orientación o notas..."></textarea>
            </div>

            <button class="btn btn-primary" style="width: 100%;" onclick="addItem()">Añadir Producto</button>
        </div>

        <!-- PANEL DE RESUMEN Y EXPORTACIÓN -->
        <div class="panel" style="display: flex; flex-direction: column; justify-content: space-between;">
            <div>
                <h3>Resumen de Cotización</h3>
                <div id="items-container" class="item-list">
                    <!-- Se inyectan dinámicamente -->
                </div>
                <div class="total-box">
                    Total: <span id="total-price">$0 COP</span>
                </div>
            </div>

            <div>
                <label>Vista previa del texto a enviar:</label>
                <textarea id="txt-preview" readonly></textarea>

                <div class="actions-block">
                    <button class="btn btn-secondary" onclick="copyText()">Copiar cotización para enviar</button>
                    <button class="btn btn-success" onclick="sendWhatsApp()">Enviar a WhatsApp</button>
                    <button class="btn btn-secondary" style="border-color: #e63946; color: #e63946;" onclick="resetQuote()">Iniciar Nueva Cotización</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Estructura de Datos de Configuración
        const typesConfig = {
            "Camiseta": ["Piel de durazno", "Algodón 180g", "Algodón 230g", "Mameluco"],
            "Mugs": ["Blanco", "Recuadro", "Color y asa", "Mágico", "Glitter"],
            "Jarras": ["Opalizada blanca", "Fucsia", "Verde neon", "Amarillo neon", "Rojo", "Azul"],
            "Caramañola": ["Blanca", "Plateada", "Mágica"],
            "Buff": ["50cm", "75cm", "1m"],
            "Vinilos": [
                "Vinilo adh colores basicos", "Vinilo adh reflectivo", "Vinilo adh glitter", 
                "Vinilo adh olografico", "Vinilo textil colores básicos", "Vinilo textil reflectivo", 
                "Vinilo textil dorados", "Vinilo textil glitter"
            ],
            "Dtf": ["Dtf 1m a 5 m", "Dtf mas de 5m"],
            "Diseño": ["Fracion menos de 29min", "½ h", "1h"]
        };

        const stampOptions = [
            "DTF Punto corazón de 7 a 9 cm", "DTF Focalizado frente de 22 a 28cm", "DTF Focalizado espalda de 25 a 32 cm",
            "DTF Punto corazón 7 a 9 y espalda 25 a 32", "DTF Focalizado frente y espalda 22 a 28 y 25 a 32",
            "SUBLIMACION Punto corazón de 7 a 9 cm", "SUBLIMACION Focalizado frente de 22 a 28cm", "SUBLIMACION Focalizado espalda de 25 a 32 cm",
            "SUBLIMACION Punto corazón 7 a 9 y espalda 25 a 32", "SUBLIMACION Focalizado frente y espalda 22 a 28 y 25 a 32",
            "VINILO TEXTIL Punto corazón de 7 a 9 cm", "VINILO TEXTIL Focalizado frente de 22 a 28cm", "VINILO TEXTIL Focalizado espalda de 25 a 32 cm",
            "VINILO TEXTIL Punto corazón 7 a 9 y espalda 25 a 32", "VINILO TEXTIL Focalizado frente y espalda 22 a 28 y 25 a 32"
        ];

        // Estado Global del Aplicativo
        let currentQuote = [];
        let clientName = "";

        function startApp() {
            document.getElementById('welcome-screen').style.display = 'none';
            document.getElementById('app-screen').style.display = 'grid';
            handleProductChange();
        }

        // Manejo Dinámico de Interfaz según Producto Seleccionado
        function handleProductChange() {
            const product = document.getElementById('product-select').value;
            const typeSelect = document.getElementById('type-select');
            
            // Poblar Tipos
            typeSelect.innerHTML = "";
            typesConfig[product].forEach(t => {
                let opt = document.createElement('option');
                opt.value = t; opt.textContent = t;
                typeSelect.appendChild(opt);
            });

            // Visibilidad de Campos condicionales
            toggleElement('size-container', product === "Camiseta" || product === "Camiseta niñ@");
            toggleElement('print-container', ["Camiseta", "Camiseta niñ@", "Mugs", "Jarras", "Caramañola", "Buff"].includes(product));
            toggleElement('measures-container', ["Vinilos", "Dtf"].includes(product));
            toggleElement('time-container', product === "Diseño");
            toggleElement('buff-reflective-container', product === "Buff");

            handleTypeChange();
            handlePrintChange();
        }

        function handleTypeChange() {
            const product = document.getElementById('product-select').value;
            const type = document.getElementById('type-select').value;
            // Forzar visualización de tiempo exacto si selecciona fracción en diseño
            if (product === "Diseño") {
                toggleElement('time-container', type === "Fracion menos de 29min");
            }
        }

        function handlePrintChange() {
            const product = document.getElementById('product-select').value;
            const isPrinting = document.getElementById('print-select').value === 'si';
            const detailContainer = document.getElementById('print-detail-container');

            if (isPrinting && ["Camiseta", "Camiseta niñ@"].includes(product)) {
                detailContainer.classList.remove('hidden');
                const pSelect = document.getElementById('print-detail-select');
                pSelect.innerHTML = "";
                stampOptions.forEach(optStr => {
                    let opt = document.createElement('option');
                    opt.value = optStr; opt.textContent = optStr;
                    pSelect.appendChild(opt);
                });
            } else {
                detailContainer.classList.add('hidden');
            }
        }

        function handleBuffReflectiveChange() {
            const isReflective = document.getElementById('buff-reflective-select').value === 'si';
            toggleElement('measures-container', isReflective);
        }

        function toggleElement(id, condition) {
            const el = document.getElementById(id);
            if (condition) el.classList.remove('hidden');
            else el.classList.add('hidden');
        }

        // LÓGICA MATEMÁTICA Y DE COSTOS
        function calculateItemPrice() {
            const product = document.getElementById('product-select').value;
            const type = document.getElementById('type-select').value;
            let finalPrice = 0;

            // 1. Camisetas (Fórmula Margen Real: Costo / 0.7)
            if (product === "Camiseta" || product === "Camiseta niñ@") {
                let cost = 0;
                if (type === "Piel de durazno") cost = 12000;
                else if (type === "Algodón 180g") cost = 15000;
                else if (type === "Algodón 230g") cost = 29000;
                else if (type === "Mameluco") cost = 10000;

                // Sumar valor del Planchazo si aplica
                if (document.getElementById('print-select').value === 'si') {
                    const stamp = document.getElementById('print-detail-select').value;
                    cost += getPlanchazoCost(stamp);
                }
                finalPrice = Math.round(cost / 0.7);
            }
            // 2. Mugs (Precios Finales fijos dados)
            else if (product === "Mugs") {
                if (type === "Blanco") finalPrice = 8500;
                else if (type === "Recuadro") finalPrice = 13700;
                else if (type === "Color y asa") finalPrice = 14000;
                else if (type === "Mágico" || type === "Glitter") finalPrice = 16000;
            }
            // 3. Jarras (Precio final fijo)
            else if (product === "Jarras") {
                finalPrice = 21000; 
            }
            // 4. Caramañolas
            else if (product === "Caramañola") {
                if (type === "Blanca" || type === "Plateada") finalPrice = 18000;
                else if (type === "Mágica") finalPrice = 25000;
            }
            // 5. Buffs
            else if (product === "Buff") {
                if (type === "50cm") finalPrice = 10000;
                else if (type === "75cm") finalPrice = 15000;
                else if (type === "1m") finalPrice = 20000;

                if (document.getElementById('buff-reflective-select').value === 'si') {
                    const h = parseFloat(document.getElementById('measure-height').value) || 0;
                    const w = parseFloat(document.getElementById('measure-width').value) || 0;
                    finalPrice += Math.round(h * w * 22); // Vinilo reflectivo a $22 el cm2
                }
            }
            // 6. Vinilos (Alto x Ancho x Factor)
            else if (product === "Vinilos") {
                const h = parseFloat(document.getElementById('measure-height').value) || 0;
                const w = parseFloat(document.getElementById('measure-width').value) || 0;
                let factor = 7;
                if (type === "Vinilo adh reflectivo") factor = 9;
                else if (type === "Vinilo adh glitter") factor = 11;
                else if (type === "Vinilo adh olografico") factor = 12;
                else if (type === "Vinilo textil colores básicos") factor = 12;
                else if (type === "Vinilo textil reflectivo") factor = 22;
                else if (type === "Vinilo textil dorados") factor = 18;
                else if (type === "Vinilo textil glitter") factor = 22;

                finalPrice = Math.round(h * w * factor);
            }
            // 7. DTF Metraje
            else if (product === "Dtf") {
                const h = parseFloat(document.getElementById('measure-height').value) || 0;
                const w = parseFloat(document.getElementById('measure-width').value) || 0;
                let factor = (type === "Dtf 1m a 5 m") ? 10 : 6;
                finalPrice = Math.round(h * w * factor);
            }
            // 8. Diseño
            else if (product === "Diseño") {
                if (type === "Fracion menos de 29min") {
                    const mins = parseInt(document.getElementById('design-minutes').value) || 15;
                    finalPrice = mins * 500;
                } else if (type === "½ h") {
                    finalPrice = 15000;
                } else if (type === "1h") {
                    finalPrice = 30000;
                }
            }

            return finalPrice;
        }

        function getPlanchazoCost(stampName) {
            if (stampName.includes("DTF")) {
                if (stampName.includes("Focalizado frente y espalda") || stampName.includes("Punto corazón 7 a 9 y espalda")) return 3000;
                if (stampName.includes("Focalizado frente") || stampName.includes("Focalizado espalda")) return 1300;
            }
            if (stampName.includes("SUBLIMACION")) {
                if (stampName.includes("Focalizado frente y espalda") || stampName.includes("Punto corazón 7 a 9 y espalda")) return 3000;
                return 1500;
            }
            if (stampName.includes("VINILO TEXTIL")) {
                if (stampName.includes("Punto corazón de 7 a 9 cm")) return 1300;
                if (stampName.includes("Focalizado frente")) return 1500;
                if (stampName.includes("Focalizado espalda")) return 3000;
                if (stampName.includes("Punto corazón 7 a 9 y espalda")) return 4200;
                if (stampName.includes("Focalizado frente y espalda")) return 5000;
            }
            return 0;
        }

        // GESTIÓN DE LA LISTA DE COTIZACIÓN
        function addItem() {
            const clientInput = document.getElementById('client-name').value.trim();
            if (!clientInput) {
                alert("Por favor ingrese el nombre del cliente primero.");
                return;
            }
            clientName = clientInput;

            const product = document.getElementById('product-select').value;
            const type = document.getElementById('type-select').value;
            const obs = document.getElementById('item-observations').value.trim();
            const value = calculateItemPrice();

            let description = `${product} (${type})`;

            // Agregar Talla si es camiseta
            if (product === "Camiseta" || product === "Camiseta niñ@") {
                const size = document.getElementById('size-select').value;
                description += ` - Talla: ${size}`;
            }

            // Agregar datos complementarios visibles en la especificación
            if (document.getElementById('print-select').value === 'si' && ["Camiseta", "Camiseta niñ@"].includes(product)) {
                description += ` c/ Estampado: ${document.getElementById('print-detail-select').value}`;
            }
            if (product === "Buff" && document.getElementById('buff-reflective-select').value === 'si') {
                description += ` (Con Reflectivo ${document.getElementById('measure-height').value}x${document.getElementById('measure-width').value}cm)`;
            }
            if (["Vinilos", "Dtf"].includes(product)) {
                description += ` [${document.getElementById('measure-height').value}x${document.getElementById('measure-width').value}cm]`;
            }
            if (product === "Diseño" && type === "Fracion menos de 29min") {
                description += ` [${document.getElementById('design-minutes').value} Minutos]`;
            }

            const itemObject = {
                id: Date.now(),
                description: description,
                observations: obs,
                price: value
            };

            currentQuote.push(itemObject);
            document.getElementById('item-observations').value = ""; // Limpiar campo notas individuales
            updateUI();
        }

        function removeItem(id) {
            currentQuote = currentQuote.filter(item => item.id !== id);
            updateUI();
        }

        function updateUI() {
            const container = document.getElementById('items-container');
            container.innerHTML = "";
            let total = 0;

            currentQuote.forEach(item => {
                total += item.price;
                let div = document.createElement('div');
                div.className = "added-item";
                div.innerHTML = `
                    <div class="added-item-info">
                        <p><strong>${item.description}</strong></p>
                        ${item.observations ? `<small>Obs: ${item.observations}</small>` : ''}
                        <small style="color: var(--success); font-weight:bold;">$${item.price.toLocaleString('es-CO')} COP</small>
                    </div>
                    <button class="btn btn-danger" onclick="removeItem(${item.id})">Eliminar</button>
                `;
                container.appendChild(div);
            });

            document.getElementById('total-price').textContent = `$${total.toLocaleString('es-CO')} COP`;
            generateTextPreview(total);
        }

        // GENERACIÓN DE TEXTO CON FORMATO EXCLUSIVO
        function generateTextPreview(totalPrice) {
            if (currentQuote.length === 0) {
                document.getElementById('txt-preview').value = "";
                return;
            }

            const now = new Date();
            const dateStr = now.toLocaleDateString('es-CO');
            const timeStr = now.toLocaleTimeString('es-CO', { hour: '2-digit', minute: '2-digit' });

            let txt = `╔════════════════════════╗\n`;
            txt += `  COTIZACIONES BUFFLANDIA  \n`;
            txt += `╚════════════════════════╝\n\n`;
            txt += `👤 Cliente: ${clientName}\n`;
            txt += `📅 Fecha: ${dateStr}  |  🕒 Hora: ${timeStr}\n`;
            txt += `------------------------------------------\n\n`;

            currentQuote.forEach((item, index) => {
                txt += `${index + 1}. ${item.description}\n`;
                if (item.observations) {
                    txt += `   Nota: ${item.observations}\n`;
                }
                txt += `   Valor: $${item.price.toLocaleString('es-CO')} COP\n`;
                txt += `------------------------------------------\n`;
            });

            txt += `\n💰 VALOR TOTAL: $${totalPrice.toLocaleString('es-CO')} COP\n`;
            txt += `\n¡Gracias por cotizar con nosotros!`;

            document.getElementById('txt-preview').value = txt;
        }

        function copyText() {
            const textarea = document.getElementById('txt-preview');
            if (!textarea.value) return;
            textarea.select();
            document.execCommand('copy');
            alert("¡Cotización copiada al portapapeles exitosamente!");
        }

        function sendWhatsApp() {
            const text = document.getElementById('txt-preview').value;
            if (!text) {
                alert("La cotización está vacía. Añada productos primero.");
                return;
            }
            const encodedText = encodeURIComponent(text);
            const url = `wa.me/573122959905`;
            window.open(url, '_blank');
        }

        function resetQuote() {
            if(confirm("¿Seguro que desea borrar esta cotización e iniciar una nueva?")) {
                currentQuote = [];
                document.getElementById('client-name').value = "";
                document.getElementById('item-observations').value = "";
                updateUI();
            }
        }
    </script>
</body>
</html>
