<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi Colección Digimon TCG</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            margin-bottom: 30px;
            text-align: center;
        }

        h1 {
            color: #667eea;
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        .stats {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 15px;
            flex-wrap: wrap;
        }

        .stat {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 10px 20px;
            border-radius: 10px;
            font-weight: bold;
        }

        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
        }

        .tab-btn {
            flex: 1;
            padding: 15px;
            background: white;
            color: #333;
            border: 2px solid #667eea;
            border-radius: 10px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 16px rgba(0,0,0,0.1);
        }

        .tab-btn:hover {
            background: #f5f5ff;
        }

        .tab-btn.active {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
            border-color: #667eea;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .controls {
            background: white;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            margin-bottom: 30px;
        }

        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 15px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
        }

        label {
            font-weight: bold;
            margin-bottom: 5px;
            color: #333;
        }

        input, select, textarea {
            padding: 10px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 14px;
            transition: border-color 0.3s;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: #667eea;
        }

        textarea {
            resize: vertical;
            min-height: 60px;
        }

        button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        button:active {
            transform: translateY(0);
        }

        .filters {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-bottom: 15px;
        }

        .filter-section {
            margin-bottom: 20px;
        }

        .filter-section h3 {
            margin-bottom: 10px;
            color: #333;
        }

        .filter-btn {
            padding: 8px 16px;
            background: white;
            color: #333;
            border: 2px solid #667eea;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 14px;
            font-weight: 600;
        }

        .filter-btn:hover {
            background: #f5f5ff;
        }

        .filter-btn.active {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-color: #667eea;
        }

        .search-box {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            margin-bottom: 15px;
        }

        .cards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
        }

        .card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 48px rgba(0,0,0,0.15);
        }

        .card-image-container {
            width: 100%;
            height: 380px;
            overflow: hidden;
            background: linear-gradient(135deg, #f0f0f0 0%, #e0e0e0 100%);
        }

        .card-image {
            width: 100%;
            height: 100%;
            object-fit: contain;
            background: #f9f9f9;
        }

        .card-image-placeholder {
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #999;
            font-size: 5em;
        }

        .card-content {
            padding: 20px;
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: start;
            margin-bottom: 15px;
        }

        .card-name {
            font-size: 1.3em;
            font-weight: bold;
            color: #333;
        }

        .card-number {
            background: #667eea;
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 0.9em;
        }

        .card-info {
            margin: 10px 0;
        }

        .card-label {
            font-weight: bold;
            color: #666;
            font-size: 0.9em;
        }

        .card-value {
            color: #333;
            margin-top: 3px;
        }

        .card-color, .card-rarity, .card-trait {
            display: inline-block;
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 0.85em;
            font-weight: bold;
            margin-top: 5px;
            margin-right: 5px;
        }

        .card-trait {
            background: #9C27B0;
            color: white;
        }

        .quantity {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-top: 10px;
            padding-top: 10px;
            border-top: 2px solid #f0f0f0;
        }

        .quantity-badge {
            background: #4caf50;
            color: white;
            padding: 8px 15px;
            border-radius: 20px;
            font-weight: bold;
        }

        .card-actions {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }

        .btn-small {
            flex: 1;
            padding: 8px;
            font-size: 0.9em;
            background: #f44336;
        }

        .btn-small:hover {
            background: #d32f2f;
        }

        .btn-edit {
            background: #2196F3;
        }

        .btn-edit:hover {
            background: #1976D2;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: white;
            border-radius: 15px;
            padding: 30px;
            max-width: 800px;
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-header h2 {
            color: #667eea;
            margin: 0;
        }

        .close-btn {
            background: #f44336;
            color: white;
            border: none;
            width: 35px;
            height: 35px;
            border-radius: 50%;
            font-size: 20px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 0;
        }

        .close-btn:hover {
            background: #d32f2f;
        }

        .empty-state {
            text-align: center;
            padding: 60px 20px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
        }

        .empty-state h2 {
            color: #667eea;
            margin-bottom: 10px;
        }

        .empty-state p {
            color: #666;
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 1.8em;
            }

            .stats {
                gap: 15px;
            }

            .cards-grid {
                grid-template-columns: 1fr;
            }

            .tabs {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🎴 Mi Colección Digimon TCG</h1>
            <div class="stats">
                <div class="stat">Total: <span id="totalCards">0</span> cartas</div>
                <div class="stat">Diferentes: <span id="uniqueCards">0</span></div>
            </div>
        </header>

        <div class="tabs">
            <button class="tab-btn active" onclick="switchTab('collection')">📚 Mi Colección</button>
            <button class="tab-btn" onclick="switchTab('add')">➕ Agregar Cartas</button>
            <button class="tab-btn" onclick="switchTab('share')">📤 Compartir</button>
        </div>

        <div id="collectionTab" class="tab-content active">
            <div class="controls">
                <h2 style="margin-bottom: 15px;">🔍 Filtrar Colección</h2>
                <input type="text" class="search-box" id="searchBox" placeholder="Buscar por nombre o número...">
                
                <div class="filter-section">
                    <h3>Color</h3>
                    <div class="filters" id="colorFilters">
                        <button class="filter-btn active" data-filter="all" data-type="color">Todos</button>
                        <button class="filter-btn" data-filter="Rojo" data-type="color">Rojo</button>
                        <button class="filter-btn" data-filter="Azul" data-type="color">Azul</button>
                        <button class="filter-btn" data-filter="Amarillo" data-type="color">Amarillo</button>
                        <button class="filter-btn" data-filter="Verde" data-type="color">Verde</button>
                        <button class="filter-btn" data-filter="Negro" data-type="color">Negro</button>
                        <button class="filter-btn" data-filter="Morado" data-type="color">Morado</button>
                        <button class="filter-btn" data-filter="Blanco" data-type="color">Blanco</button>
                    </div>
                </div>

                <div class="filter-section">
                    <h3>Trait</h3>
                    <div class="filters" id="traitFilters">
                        <button class="filter-btn active" data-filter="all" data-type="trait">Todos</button>
                    </div>
                </div>
            </div>

            <div id="cardsContainer" class="cards-grid"></div>
        </div>

        <!-- Modal para editar -->
        <div id="editModal" class="modal">
            <div class="modal-content">
                <div class="modal-header">
                    <h2>✏️ Editar Carta</h2>
                    <button class="close-btn" onclick="closeEditModal()">✕</button>
                </div>
                <form id="editCardForm">
                    <input type="hidden" id="editCardId">
                    <div class="form-row">
                        <div class="form-group">
                            <label for="editCardName">Nombre *</label>
                            <input type="text" id="editCardName" required placeholder="Ej: Agumon">
                        </div>
                        <div class="form-group">
                            <label for="editCardNumber">Número *</label>
                            <input type="text" id="editCardNumber" required placeholder="Ej: BT1-010">
                        </div>
                        <div class="form-group">
                            <label for="editCardColor">Color *</label>
                            <select id="editCardColor" required>
                                <option value="">Selecciona...</option>
                                <option value="Rojo">Rojo</option>
                                <option value="Azul">Azul</option>
                                <option value="Amarillo">Amarillo</option>
                                <option value="Verde">Verde</option>
                                <option value="Negro">Negro</option>
                                <option value="Morado">Morado</option>
                                <option value="Blanco">Blanco</option>
                                <option value="Multicolor">Multicolor</option>
                                <option value="SinColor">SinColor</option>
                            </select>
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="editCardImage">URL de Imagen (opcional)</label>
                        <input type="url" id="editCardImage" placeholder="https://ejemplo.com/imagen-carta.jpg">
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="editCardType">Tipo *</label>
                            <select id="editCardType" required>
                                <option value="">Selecciona...</option>
                                <option value="Digimon">Digimon</option>
                                <option value="Tamer">Tamer</option>
                                <option value="Opción">Opción</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="editCardTrait">Trait *</label>
                            <input type="text" id="editCardTrait" required placeholder="Ej: Reptile, Dragon, Vaccine">
                        </div>
                        <div class="form-group">
                            <label for="editCardRarity">Rareza *</label>
                            <select id="editCardRarity" required>
                                <option value="">Selecciona...</option>
                                <option value="Common">Common (C)</option>
                                <option value="Uncommon">Uncommon (U)</option>
                                <option value="Rare">Rare (R)</option>
                                <option value="Super Rare">Super Rare (SR)</option>
                                <option value="Secret Rare">Secret Rare (SEC)</option>
                                <option value="Promo">Promo (P)</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="editCardQuantity">Cantidad *</label>
                            <div style="display: flex; gap: 10px; align-items: center;">
                                <button type="button" onclick="changeQuantity(-1)" style="width: 40px; padding: 10px;">-</button>
                                <input type="number" id="editCardQuantity" value="1" min="1" required style="text-align: center;">
                                <button type="button" onclick="changeQuantity(1)" style="width: 40px; padding: 10px;">+</button>
                            </div>
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="editCardNotes">Notas (opcional)</label>
                        <textarea id="editCardNotes" placeholder="Ej: Para intercambio, condición mint, etc."></textarea>
                    </div>
                    <button type="submit">💾 Guardar Cambios</button>
                </form>
            </div>
        </div>

        <div id="addTab" class="tab-content">
            <div class="controls">
                <h2 style="margin-bottom: 15px;">➕ Agregar Nueva Carta</h2>
                <form id="addCardForm">
                    <div class="form-row">
                        <div class="form-group">
                            <label for="cardName">Nombre *</label>
                            <input type="text" id="cardName" required placeholder="Ej: Agumon">
                        </div>
                        <div class="form-group">
                            <label for="cardNumber">Número *</label>
                            <input type="text" id="cardNumber" required placeholder="Ej: BT1-010">
                        </div>
                        <div class="form-group">
                            <label for="cardColor">Color *</label>
                            <select id="cardColor" required>
                                <option value="">Selecciona...</option>
                                <option value="Rojo">Rojo</option>
                                <option value="Azul">Azul</option>
                                <option value="Amarillo">Amarillo</option>
                                <option value="Verde">Verde</option>
                                <option value="Negro">Negro</option>
                                <option value="Morado">Morado</option>
                                <option value="Blanco">Blanco</option>
                                <option value="Multicolor">Multicolor</option>
                                <option value="SinColor">SinColor</option>
                            </select>
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="cardImage">URL de Imagen (opcional)</label>
                        <input type="url" id="cardImage" placeholder="https://ejemplo.com/imagen-carta.jpg">
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="cardType">Tipo *</label>
                            <select id="cardType" required>
                                <option value="">Selecciona...</option>
                                <option value="Digimon">Digimon</option>
                                <option value="Tamer">Tamer</option>
                                <option value="Opción">Opción</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="cardTrait">Trait *</label>
                            <input type="text" id="cardTrait" required placeholder="Ej: Reptile, Dragon, Vaccine">
                        </div>
                        <div class="form-group">
                            <label for="cardRarity">Rareza *</label>
                            <select id="cardRarity" required>
                                <option value="">Selecciona...</option>
                                <option value="Common">Common (C)</option>
                                <option value="Uncommon">Uncommon (U)</option>
                                <option value="Rare">Rare (R)</option>
                                <option value="Super Rare">Super Rare (SR)</option>
                                <option value="Secret Rare">Secret Rare (SEC)</option>
                                <option value="Promo">Promo (P)</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="cardQuantity">Cantidad *</label>
                            <input type="number" id="cardQuantity" value="1" min="1" required>
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="cardNotes">Notas (opcional)</label>
                        <textarea id="cardNotes" placeholder="Ej: Para intercambio, condición mint, etc."></textarea>
                    </div>
                    <button type="submit">Agregar Carta</button>
                </form>
            </div>
        </div>

        <div id="shareTab" class="tab-content">
            <div class="controls">
                <h2 style="margin-bottom: 15px;">📤 Exportar / Importar Colección</h2>
                
                <div style="margin-bottom: 30px;">
                    <h3 style="margin-bottom: 10px;">💾 Exportar tu colección</h3>
                    <p style="color: #666; margin-bottom: 15px;">Descarga un archivo JSON con todas tus cartas para hacer respaldo o transferir a otro dispositivo.</p>
                    <button onclick="exportCollection()">📥 Descargar Colección (JSON)</button>
                </div>

                <div style="margin-bottom: 30px; padding-top: 30px; border-top: 2px solid #e0e0e0;">
                    <h3 style="margin-bottom: 10px;">📂 Importar colección</h3>
                    <p style="color: #666; margin-bottom: 15px;">Carga un archivo JSON previamente exportado. Esto reemplazará tu colección actual.</p>
                    <input type="file" id="importFile" accept=".json" style="margin-bottom: 10px;">
                    <button onclick="importCollection()">📤 Cargar Colección</button>
                </div>

                <div style="padding-top: 30px; border-top: 2px solid #e0e0e0;">
                    <h3 style="margin-bottom: 10px;">📱 Generar código QR</h3>
                    <p style="color: #666; margin-bottom: 15px;">Genera un código QR que otros pueden escanear para ver tu colección (requiere que subas este HTML a internet).</p>
                    <div class="form-group">
                        <label for="urlInput">URL de tu colección online:</label>
                        <input type="url" id="urlInput" placeholder="https://tu-sitio.com/mi-coleccion.html">
                    </div>
                    <button onclick="generateQR()" style="margin-bottom: 20px;">🔲 Generar QR</button>
                    
                    <div id="qrContainer" style="display: none; text-align: center; background: white; padding: 20px; border-radius: 10px; box-shadow: 0 4px 16px rgba(0,0,0,0.1);">
                        <canvas id="qrCanvas"></canvas>
                        <p style="margin-top: 15px; color: #666;">Escanea este código para ver la colección</p>
                        <button onclick="downloadQR()" style="margin-top: 10px;">💾 Descargar QR</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <script>
        let cards = [];
        let currentColorFilter = 'all';
        let currentTraitFilter = 'all';
        let searchTerm = '';

        // Cargar cartas desde memoria
        function loadCards() {
            const saved = localStorage.getItem('digimonCards');
            if (saved) {
                cards = JSON.parse(saved);
                updateTraitFilters();
                renderCards();
            }
        }

        // Guardar cartas
        function saveCards() {
            localStorage.setItem('digimonCards', JSON.stringify(cards));
        }

        // Cambiar pestañas
        function switchTab(tab) {
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
            
            if (tab === 'collection') {
                document.querySelector('[onclick="switchTab(\'collection\')"]').classList.add('active');
                document.getElementById('collectionTab').classList.add('active');
            } else if (tab === 'add') {
                document.querySelector('[onclick="switchTab(\'add\')"]').classList.add('active');
                document.getElementById('addTab').classList.add('active');
            } else if (tab === 'share') {
                document.querySelector('[onclick="switchTab(\'share\')"]').classList.add('active');
                document.getElementById('shareTab').classList.add('active');
            }
        }

        // Actualizar filtros de traits
        function updateTraitFilters() {
            const traits = new Set();
            cards.forEach(card => {
                if (card.trait) {
                    card.trait.split(',').forEach(t => traits.add(t.trim()));
                }
            });

            const traitFilters = document.getElementById('traitFilters');
            const allBtn = traitFilters.querySelector('[data-filter="all"]');
            traitFilters.innerHTML = '';
            traitFilters.appendChild(allBtn);

            Array.from(traits).sort().forEach(trait => {
                const btn = document.createElement('button');
                btn.className = 'filter-btn';
                btn.setAttribute('data-filter', trait);
                btn.setAttribute('data-type', 'trait');
                btn.textContent = trait;
                btn.onclick = () => {
                    document.querySelectorAll('[data-type="trait"]').forEach(b => b.classList.remove('active'));
                    btn.classList.add('active');
                    currentTraitFilter = trait;
                    renderCards();
                };
                traitFilters.appendChild(btn);
            });
        }

        // Agregar carta
        document.getElementById('addCardForm').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const card = {
                id: Date.now(),
                name: document.getElementById('cardName').value,
                number: document.getElementById('cardNumber').value,
                color: document.getElementById('cardColor').value,
                type: document.getElementById('cardType').value,
                trait: document.getElementById('cardTrait').value,
                rarity: document.getElementById('cardRarity').value,
                quantity: parseInt(document.getElementById('cardQuantity').value),
                notes: document.getElementById('cardNotes').value,
                imageUrl: document.getElementById('cardImage').value
            };

            cards.push(card);
            saveCards();
            updateTraitFilters();
            renderCards();
            e.target.reset();
            switchTab('collection');
        });

        // Eliminar carta
        function deleteCard(id) {
            if (confirm('¿Eliminar esta carta?')) {
                cards = cards.filter(c => c.id !== id);
                saveCards();
                updateTraitFilters();
                renderCards();
            }
        }

        // Abrir modal de edición
        function editCard(id) {
            const card = cards.find(c => c.id === id);
            if (!card) return;

            document.getElementById('editCardId').value = card.id;
            document.getElementById('editCardName').value = card.name;
            document.getElementById('editCardNumber').value = card.number;
            document.getElementById('editCardColor').value = card.color;
            document.getElementById('editCardImage').value = card.imageUrl || '';
            document.getElementById('editCardType').value = card.type;
            document.getElementById('editCardTrait').value = card.trait;
            document.getElementById('editCardRarity').value = card.rarity;
            document.getElementById('editCardQuantity').value = card.quantity;
            document.getElementById('editCardNotes').value = card.notes || '';

            document.getElementById('editModal').classList.add('active');
        }

        // Cerrar modal de edición
        function closeEditModal() {
            document.getElementById('editModal').classList.remove('active');
        }

        // Cambiar cantidad con botones +/-
        function changeQuantity(delta) {
            const input = document.getElementById('editCardQuantity');
            const newValue = parseInt(input.value) + delta;
            if (newValue >= 1) {
                input.value = newValue;
            }
        }

        // Guardar edición
        document.getElementById('editCardForm').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const id = parseInt(document.getElementById('editCardId').value);
            const cardIndex = cards.findIndex(c => c.id === id);
            
            if (cardIndex !== -1) {
                cards[cardIndex] = {
                    id: id,
                    name: document.getElementById('editCardName').value,
                    number: document.getElementById('editCardNumber').value,
                    color: document.getElementById('editCardColor').value,
                    type: document.getElementById('editCardType').value,
                    trait: document.getElementById('editCardTrait').value,
                    rarity: document.getElementById('editCardRarity').value,
                    quantity: parseInt(document.getElementById('editCardQuantity').value),
                    notes: document.getElementById('editCardNotes').value,
                    imageUrl: document.getElementById('editCardImage').value
                };

                saveCards();
                updateTraitFilters();
                renderCards();
                closeEditModal();
            }
        });

        // Cerrar modal al hacer clic fuera
        document.getElementById('editModal').addEventListener('click', (e) => {
            if (e.target.id === 'editModal') {
                closeEditModal();
            }
        });

        // Exportar colección
        function exportCollection() {
            if (cards.length === 0) {
                alert('No tienes cartas para exportar');
                return;
            }

            const dataStr = JSON.stringify(cards, null, 2);
            const dataBlob = new Blob([dataStr], { type: 'application/json' });
            const url = URL.createObjectURL(dataBlob);
            const link = document.createElement('a');
            link.href = url;
            link.download = `digimon-collection-${new Date().toISOString().split('T')[0]}.json`;
            link.click();
            URL.revokeObjectURL(url);
        }

        // Importar colección
        function importCollection() {
            const fileInput = document.getElementById('importFile');
            const file = fileInput.files[0];

            if (!file) {
                alert('Por favor selecciona un archivo');
                return;
            }

            const reader = new FileReader();
            reader.onload = (e) => {
                try {
                    const importedCards = JSON.parse(e.target.result);
                    
                    if (!Array.isArray(importedCards)) {
                        alert('Archivo inválido');
                        return;
                    }

                    if (confirm(`¿Importar ${importedCards.length} cartas? Esto reemplazará tu colección actual.`)) {
                        cards = importedCards;
                        saveCards();
                        updateTraitFilters();
                        renderCards();
                        switchTab('collection');
                        alert('Colección importada exitosamente!');
                    }
                } catch (error) {
                    alert('Error al leer el archivo. Asegúrate de que sea un JSON válido.');
                }
            };
            reader.readAsText(file);
        }

        // Generar código QR
        let qrCodeInstance = null;
        function generateQR() {
            const url = document.getElementById('urlInput').value;
            
            if (!url) {
                alert('Por favor ingresa la URL de tu colección');
                return;
            }

            const qrContainer = document.getElementById('qrContainer');
            const qrCanvas = document.getElementById('qrCanvas');
            
            // Limpiar QR anterior
            qrCanvas.innerHTML = '';
            if (qrCodeInstance) {
                qrCodeInstance.clear();
            }

            // Generar nuevo QR
            qrCodeInstance = new QRCode(qrCanvas, {
                text: url,
                width: 256,
                height: 256,
                colorDark: '#667eea',
                colorLight: '#ffffff',
                correctLevel: QRCode.CorrectLevel.H
            });

            qrContainer.style.display = 'block';
        }

        // Descargar QR
        function downloadQR() {
            const canvas = document.querySelector('#qrCanvas canvas');
            if (!canvas) {
                alert('Primero genera el código QR');
                return;
            }

            canvas.toBlob((blob) => {
                const url = URL.createObjectURL(blob);
                const link = document.createElement('a');
                link.href = url;
                link.download = 'qr-digimon-collection.png';
                link.click();
                URL.revokeObjectURL(url);
            });
        }

        // Obtener color para etiqueta
        function getColorStyle(color) {
            const colors = {
                'Rojo': 'background: #f44336; color: white;',
                'Azul': 'background: #2196F3; color: white;',
                'Amarillo': 'background: #FFC107; color: black;',
                'Verde': 'background: #4CAF50; color: white;',
                'Negro': 'background: #333; color: white;',
                'Morado': 'background: #9C27B0; color: white;',
                'Blanco': 'background: #f5f5f5; color: black; border: 2px solid #ddd;',
                'Multicolor': 'background: linear-gradient(135deg, #f44336, #2196F3, #4CAF50); color: white;',
                'Sincolor': 'background: linear-gradient(135deg, #f44336, #2196F3, #4CAF50); color: white;'
            };
            return colors[color] || '';
        }

        // Renderizar cartas
        function renderCards() {
            const container = document.getElementById('cardsContainer');
            
            // Filtrar cartas
            let filtered = cards.filter(card => {
                const matchesColor = currentColorFilter === 'all' || card.color === currentColorFilter;
                const matchesTrait = currentTraitFilter === 'all' || (card.trait && card.trait.includes(currentTraitFilter));
                const matchesSearch = card.name.toLowerCase().includes(searchTerm.toLowerCase()) || 
                                     card.number.toLowerCase().includes(searchTerm.toLowerCase());
                return matchesColor && matchesTrait && matchesSearch;
            });

            // Actualizar estadísticas
            document.getElementById('totalCards').textContent = cards.reduce((sum, c) => sum + c.quantity, 0);
            document.getElementById('uniqueCards').textContent = cards.length;

            if (filtered.length === 0) {
                container.innerHTML = `
                    <div class="empty-state">
                        <h2>No hay cartas aquí</h2>
                        <p>Agrega tu primera carta usando la pestaña "Agregar Cartas"</p>
                    </div>
                `;
                return;
            }

            container.innerHTML = filtered.map(card => `
                <div class="card">
                    <div class="card-image-container">
                        ${card.imageUrl ? 
                            `<img src="${card.imageUrl}" alt="${card.name}" class="card-image" onerror="this.style.display='none'; this.parentElement.innerHTML='<div class=\\'card-image-placeholder\\'>🎴</div>';">` 
                            : 
                            `<div class="card-image-placeholder">🎴</div>`
                        }
                    </div>
                    
                    <div class="card-content">
                        <div class="card-header">
                            <div class="card-name">${card.name}</div>
                            <div class="card-number">${card.number}</div>
                        </div>
                        
                        <div class="card-info">
                            <div class="card-label">Tipo</div>
                            <div class="card-value">${card.type}</div>
                        </div>

                        <div>
                            <div class="card-color" style="${getColorStyle(card.color)}">${card.color}</div>
                            <div class="card-rarity" style="background: #FF9800; color: white;">${card.rarity}</div>
                        </div>

                        ${card.trait ? `
                            <div class="card-info" style="margin-top: 10px;">
                                <div class="card-label">Traits</div>
                                <div>
                                    ${card.trait.split(',').map(t => `<span class="card-trait">${t.trim()}</span>`).join('')}
                                </div>
                            </div>
                        ` : ''}

                        ${card.notes ? `
                            <div class="card-info" style="margin-top: 10px;">
                                <div class="card-label">Notas</div>
                                <div class="card-value">${card.notes}</div>
                            </div>
                        ` : ''}

                        <div class="quantity">
                            <span class="card-label">Cantidad:</span>
                            <span class="quantity-badge">${card.quantity}x</span>
                        </div>

                        <div class="card-actions">
                            <button class="btn-small btn-edit" onclick="editCard(${card.id})">✏️ Editar</button>
                            <button class="btn-small" onclick="deleteCard(${card.id})">🗑️ Eliminar</button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        // Filtros de color
        document.querySelectorAll('[data-type="color"]').forEach(btn => {
            btn.addEventListener('click', () => {
                document.querySelectorAll('[data-type="color"]').forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                currentColorFilter = btn.dataset.filter;
                renderCards();
            });
        });

        // Filtros de trait
        document.querySelectorAll('[data-type="trait"]').forEach(btn => {
            btn.addEventListener('click', () => {
                document.querySelectorAll('[data-type="trait"]').forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                currentTraitFilter = btn.dataset.filter;
                renderCards();
            });
        });

        // Búsqueda
        document.getElementById('searchBox').addEventListener('input', (e) => {
            searchTerm = e.target.value;
            renderCards();
        });

        // Inicializar
        loadCards();
    </script>
</body>
</html>
