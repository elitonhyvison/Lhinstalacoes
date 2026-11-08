# Lhinstalacoes
```html
<!DOCTYPE html>
<html lang="pt-BR" class="h-full bg-slate-50">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LH Instalações e Serviços - Precificação Rápida</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#fffbe6',
                            100: '#fef3c7',
                            400: '#fbbf24',
                            500: '#f59e0b',
                            600: '#d97706',
                            700: '#b45309',
                        },
                        lhblack: {
                            800: '#18181b',
                            900: '#09090b',
                            full: '#000000',
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
    <!-- FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body { font-family: 'Inter', sans-serif; }
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: #f5f5f4; }
        ::-webkit-scrollbar-thumb { background: #d6d3d1; border-radius: 9999px; }
        ::-webkit-scrollbar-thumb:hover { background: #a8a29e; }
    </style>
</head>
<body class="min-h-full flex flex-col text-slate-800 antialiased bg-stone-50 pb-36 sm:pb-28">

    <!-- Header com Identidade Visual LH -->
    <header class="bg-lhblack-full text-white border-b-4 border-brand-500 sticky top-0 z-30 shadow-md">
        <div class="max-w-4xl mx-auto px-4 h-16 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <!-- Escudo/Logo LH -->
                <div class="w-10 h-11 bg-brand-500 rounded-b-xl rounded-t-sm flex flex-col items-center justify-center font-black text-lhblack-full shadow-lg border border-brand-400 relative overflow-hidden">
                    <span class="text-xs leading-none tracking-tighter font-extrabold -mb-0.5">LH</span>
                    <i class="fa-solid fa-wrench text-[9px] text-lhblack-full opacity-80"></i>
                </div>
                <div>
                    <h1 class="font-black text-white tracking-wider text-base sm:text-lg leading-none uppercase">LH</h1>
                    <p class="text-[9px] sm:text-[10px] text-brand-400 font-bold tracking-widest uppercase">Instalações e Serviços</p>
                </div>
            </div>

            <div class="flex items-center gap-2">
                <button onclick="openItemModal()" class="text-xs bg-brand-500 hover:bg-brand-400 text-lhblack-full font-bold px-3 py-2 rounded-lg transition flex items-center gap-1.5 shadow-md">
                    <i class="fa-solid fa-plus text-lhblack-full"></i> <span class="hidden sm:inline">Novo Móvel</span>
                </button>
                <button onclick="clearCurrentProposal()" class="text-xs bg-stone-800 hover:bg-stone-700 text-stone-300 font-semibold px-3 py-2 rounded-lg transition flex items-center gap-1 border border-stone-700" title="Limpar Orçamento">
                    <i class="fa-solid fa-rotate-left"></i> <span class="hidden sm:inline">Limpar</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Conteúdo Principal -->
    <main class="max-w-4xl mx-auto px-4 py-6 w-full flex-grow space-y-6">

        <!-- Dados Rápidos do Cliente -->
        <section class="bg-white rounded-2xl p-4 sm:p-5 border border-stone-200/80 shadow-sm space-y-4">
            <h2 class="text-xs font-bold uppercase tracking-wider text-stone-400 flex items-center gap-2">
                <i class="fa-solid fa-user text-brand-500"></i> Cliente & Local
            </h2>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                <input type="text" id="client-name" placeholder="Nome do Cliente (ex: Maria)" class="w-full bg-stone-50 border border-stone-200 rounded-xl px-3.5 py-2.5 text-sm font-medium text-stone-800 placeholder:text-stone-400 focus:outline-none focus:border-brand-500 focus:bg-white transition">
                <input type="text" id="client-address" placeholder="Bairro / Região (ex: Centro)" class="w-full bg-stone-50 border border-stone-200 rounded-xl px-3.5 py-2.5 text-sm font-medium text-stone-800 placeholder:text-stone-400 focus:outline-none focus:border-brand-500 focus:bg-white transition">
            </div>
        </section>

        <!-- Seleção de Móveis em Abas de Categoria -->
        <section class="bg-white rounded-2xl p-4 sm:p-5 border border-stone-200/80 shadow-sm space-y-4">
            <div class="flex items-center justify-between">
                <h2 class="text-xs font-bold uppercase tracking-wider text-stone-400 flex items-center gap-2">
                    <i class="fa-solid fa-list-check text-brand-500"></i> Catálogo de Móveis
                </h2>
                <span class="text-xs font-bold text-lhblack-full bg-brand-100 border border-brand-400 px-2.5 py-1 rounded-full" id="selected-count-badge">0 itens selecionados</span>
            </div>

            <!-- Filtros de Categoria -->
            <div class="flex gap-2 overflow-x-auto pb-2 scrollbar-none" id="category-tabs">
                <!-- Inserido dinamicamente -->
            </div>

            <!-- Grid de Cards de Móveis -->
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3" id="furniture-grid">
                <!-- Cards renderizados dinamicamente -->
            </div>
        </section>

        <!-- Adicionais e Taxas (Toggles) -->
        <section class="bg-white rounded-2xl p-4 sm:p-5 border border-stone-200/80 shadow-sm space-y-4">
            <h2 class="text-xs font-bold uppercase tracking-wider text-stone-400 flex items-center gap-2">
                <i class="fa-solid fa-sliders text-brand-500"></i> Taxas & Adicionais
            </h2>

            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                
                <!-- Taxa de Fixação na Parede -->
                <div class="p-3.5 rounded-xl border border-stone-200 bg-stone-50/50 flex flex-col justify-between space-y-3">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center gap-2.5">
                            <div class="w-8 h-8 rounded-lg bg-lhblack-full text-brand-400 flex items-center justify-center text-sm font-bold shadow-sm">
                                <i class="fa-solid fa-screwdriver"></i>
                            </div>
                            <div>
                                <p class="text-xs font-bold text-stone-800">Fixação na Parede</p>
                                <p class="text-[11px] text-stone-500">Bucha, parafuso e nível</p>
                            </div>
                        </div>
                        <label class="relative inline-flex items-center cursor-pointer">
                            <input type="checkbox" id="toggle-wall" onchange="calculateTotal()" class="sr-only peer">
                            <div class="w-11 h-6 bg-stone-300 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-stone-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-brand-500"></div>
                        </label>
                    </div>
                    <div class="flex items-center justify-between pt-2 border-t border-stone-200/60">
                        <span class="text-xs text-stone-500 font-medium">Valor Adicional:</span>
                        <div class="relative w-28">
                            <span class="absolute left-2.5 top-1.5 text-xs text-stone-400 font-bold">R$</span>
                            <input type="number" id="wall-price" value="20" min="0" step="5" oninput="calculateTotal()" class="w-full bg-white border border-stone-200 rounded-lg pl-7 pr-2 py-1 text-xs font-bold text-right text-stone-800 focus:outline-none focus:border-brand-500">
                        </div>
                    </div>
                </div>

                <!-- Taxa de Deslocamento -->
                <div class="p-3.5 rounded-xl border border-stone-200 bg-stone-50/50 flex flex-col justify-between space-y-3">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center gap-2.5">
                            <div class="w-8 h-8 rounded-lg bg-lhblack-full text-brand-400 flex items-center justify-center text-sm font-bold shadow-sm">
                                <i class="fa-solid fa-truck-fast"></i>
                            </div>
                            <div>
                                <p class="text-xs font-bold text-stone-800">Taxa de Deslocamento</p>
                                <p class="text-[11px] text-stone-500">Combustível / Visita</p>
                            </div>
                        </div>
                        <label class="relative inline-flex items-center cursor-pointer">
                            <input type="checkbox" id="toggle-travel" onchange="calculateTotal()" class="sr-only peer">
                            <div class="w-11 h-6 bg-stone-300 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-stone-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-brand-500"></div>
                        </label>
                    </div>
                    <div class="flex items-center justify-between pt-2 border-t border-stone-200/60">
                        <span class="text-xs text-stone-500 font-medium">Valor Taxa:</span>
                        <div class="relative w-28">
                            <span class="absolute left-2.5 top-1.5 text-xs text-stone-400 font-bold">R$</span>
                            <input type="number" id="travel-price" value="20" min="0" step="5" oninput="calculateTotal()" class="w-full bg-white border border-stone-200 rounded-lg pl-7 pr-2 py-1 text-xs font-bold text-right text-stone-800 focus:outline-none focus:border-brand-500">
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <!-- Itens Selecionados no Orçamento -->
        <section class="bg-white rounded-2xl p-4 sm:p-5 border border-stone-200/80 shadow-sm space-y-3">
            <h2 class="text-xs font-bold uppercase tracking-wider text-stone-400 flex items-center gap-2">
                <i class="fa-solid fa-receipt text-brand-500"></i> Resumo dos Itens Selecionados
            </h2>
            <div id="selected-summary-list" class="space-y-2">
                <!-- Lista de Itens Adicionados -->
            </div>
            <div id="empty-summary-msg" class="text-center py-6 text-stone-400 text-xs">
                Nenhum móvel selecionado até o momento. Selecione no catálogo acima.
            </div>
        </section>

    </main>

    <!-- BARRA FIXA INFERIOR DE TOTAL E BOTÃO WHATSAPP -->
    <div class="fixed bottom-0 left-0 right-0 bg-lhblack-full border-t-2 border-brand-500 shadow-2xl p-4 z-40">
        <div class="max-w-4xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-3">
            
            <div class="flex items-center justify-between w-full sm:w-auto gap-4">
                <div>
                    <p class="text-[10px] font-bold text-stone-400 uppercase tracking-widest">Valor Total do Serviço</p>
                    <h3 id="total-final-display" class="text-2xl sm:text-3xl font-black text-brand-400 tracking-tight">R$ 0,00</h3>
                </div>
                <div class="text-right sm:text-left border-l border-stone-800 pl-4">
                    <p class="text-[11px] text-stone-400">Móveis: <span id="subtotal-display" class="font-bold text-stone-200">R$ 0,00</span></p>
                    <p class="text-[11px] text-stone-400">Extras: <span id="extras-display" class="font-bold text-stone-200">R$ 0,00</span></p>
                </div>
            </div>

            <div class="flex items-center gap-2 w-full sm:w-auto">
                <button onclick="copyToWhatsApp()" class="w-full sm:w-auto flex-1 bg-emerald-600 hover:bg-emerald-500 active:bg-emerald-700 text-white font-black py-3.5 px-6 rounded-xl shadow-lg shadow-emerald-950/40 transition flex items-center justify-center gap-2 text-xs sm:text-sm uppercase tracking-wider">
                    <i class="fa-brands fa-whatsapp text-lg"></i> Copiar para WhatsApp
                </button>
            </div>

        </div>
    </div>

    <!-- MODAL (CRIAR / EDITAR MÓVEL) -->
    <div id="item-modal" class="fixed inset-0 bg-lhblack-full/70 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-5 shadow-2xl space-y-4 border border-stone-200">
            <div class="flex justify-between items-center border-b border-stone-100 pb-3">
                <h3 id="modal-title" class="font-bold text-lhblack-full text-base flex items-center gap-2">
                    <i class="fa-solid fa-pen-to-square text-brand-500"></i> Editar Móvel
                </h3>
                <button onclick="closeItemModal()" class="text-stone-400 hover:text-stone-600 p-1">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>

            <input type="hidden" id="modal-item-id">

            <div class="space-y-3">
                <div>
                    <label class="block text-xs font-semibold text-stone-600 mb-1">Nome do Móvel</label>
                    <input type="text" id="modal-item-name" placeholder="Ex: Cômoda 4 Gavetas" class="w-full bg-stone-50 border border-stone-200 rounded-xl px-3.5 py-2 text-sm text-stone-800 focus:outline-none focus:border-brand-500">
                </div>

                <div>
                    <label class="block text-xs font-semibold text-stone-600 mb-1">Categoria</label>
                    <select id="modal-item-category" class="w-full bg-stone-50 border border-stone-200 rounded-xl px-3.5 py-2 text-sm text-stone-800 focus:outline-none focus:border-brand-500">
                        <option value="Quarto">Quarto</option>
                        <option value="Sala">Sala</option>
                        <option value="Cozinha">Cozinha</option>
                        <option value="Escritório">Escritório</option>
                        <option value="Geral">Geral</option>
                    </select>
                </div>

                <div>
                    <label class="block text-xs font-semibold text-stone-600 mb-1">Valor Base de Montagem (R$)</label>
                    <input type="number" id="modal-item-price" placeholder="60" min="0" step="5" class="w-full bg-stone-50 border border-stone-200 rounded-xl px-3.5 py-2 text-sm text-stone-800 focus:outline-none focus:border-brand-500">
                </div>
            </div>

            <div class="flex justify-end gap-2 pt-3 border-t border-stone-100">
                <button onclick="closeItemModal()" class="px-4 py-2 rounded-xl text-xs font-semibold text-stone-500 hover:bg-stone-100">Cancelar</button>
                <button onclick="saveFurnitureItem()" class="px-5 py-2 rounded-xl text-xs font-black text-lhblack-full bg-brand-500 hover:bg-brand-400 shadow-md uppercase tracking-wider">Salvar</button>
            </div>
        </div>
    </div>

    <!-- TOAST DE NOTIFICAÇÃO -->
    <div id="toast" class="fixed top-5 right-5 bg-lhblack-full text-white text-xs font-semibold px-4 py-3 rounded-xl shadow-2xl transition-all transform translate-y-[-100px] opacity-0 z-50 flex items-center gap-2 border border-brand-500">
        <i class="fa-solid fa-circle-check text-brand-400"></i> <span id="toast-msg">Mensagem</span>
    </div>

    <script>
        // Catálogo Padrão Inicial
        const defaultCatalog = [
            { id: '1', name: 'Cômoda até 4 gavetas', category: 'Quarto', price: 60 },
            { id: '2', name: 'Guarda-roupa Casal', category: 'Quarto', price: 180 },
            { id: '3', name: 'Guarda-roupa Solteiro', category: 'Quarto', price: 120 },
            { id: '4', name: 'Cama Casal / Box', category: 'Quarto', price: 60 },
            { id: '5', name: 'Aparador Simples', category: 'Sala', price: 40 },
            { id: '6', name: 'Painel de TV', category: 'Sala', price: 90 },
            { id: '7', name: 'Rack para Sala', category: 'Sala', price: 75 },
            { id: '8', name: 'Mesa c/ 4 Cadeiras', category: 'Sala', price: 80 },
            { id: '9', name: 'Mesa c/ 6 Cadeiras', category: 'Sala', price: 110 },
            { id: '10', name: 'Armário Aéreo Cozinha', category: 'Cozinha', price: 70 },
            { id: '11', name: 'Balcão de Cozinha', category: 'Cozinha', price: 80 },
            { id: '12', name: 'Escrivaninha / Gamer', category: 'Escritório', price: 65 },
        ];

        let catalog = [];
        let selectedCategory = 'Todos';
        let selections = {}; // { idItem: quantidade }

        window.onload = function() {
            loadCatalog();
            renderCategoryTabs();
            renderGrid();
            calculateTotal();
        };

        function loadCatalog() {
            const saved = localStorage.getItem('lh_furniture_catalog');
            if (saved) {
                try { catalog = JSON.parse(saved); } catch(e) { catalog = [...defaultCatalog]; }
            } else {
                catalog = [...defaultCatalog];
            }
        }

        function saveCatalog() {
            localStorage.setItem('lh_furniture_catalog', JSON.stringify(catalog));
        }

        function renderCategoryTabs() {
            const categories = ['Todos', ...new Set(catalog.map(c => c.category))];
            const container = document.getElementById('category-tabs');
            container.innerHTML = '';

            categories.forEach(cat => {
                const active = cat === selectedCategory;
                const btn = document.createElement('button');
                btn.className = `px-3.5 py-1.5 rounded-full text-xs font-bold whitespace-nowrap transition-all border ${
                    active ? 'bg-lhblack-full text-brand-400 border-lhblack-full shadow-sm' : 'bg-stone-100 text-stone-600 border-stone-200 hover:bg-stone-200'
                }`;
                btn.innerText = cat;
                btn.onclick = () => {
                    selectedCategory = cat;
                    renderCategoryTabs();
                    renderGrid();
                };
                container.appendChild(btn);
            });
        }

        function renderGrid() {
            const container = document.getElementById('furniture-grid');
            container.innerHTML = '';

            const filtered = selectedCategory === 'Todos' ? catalog : catalog.filter(i => i.category === selectedCategory);

            filtered.forEach(item => {
                const qty = selections[item.id] || 0;
                const card = document.createElement('div');
                card.className = `p-3.5 rounded-xl border transition-all flex flex-col justify-between space-y-3 cursor-pointer ${
                    qty > 0 ? 'bg-brand-50/70 border-brand-500 shadow-sm' : 'bg-white border-stone-200 hover:border-stone-300'
                }`;
                
                card.onclick = (e) => {
                    if (!e.target.closest('.action-btn')) {
                        toggleSelection(item.id);
                    }
                };

                card.innerHTML = `
                    <div class="flex items-start justify-between gap-2">
                        <div>
                            <span class="text-[10px] font-bold uppercase tracking-wider text-stone-400">${item.category}</span>
                            <h4 class="font-bold text-stone-900 text-sm leading-tight">${item.name}</h4>
                        </div>
                        <div class="flex flex-col items-end gap-1">
                            <span class="text-xs font-black text-lhblack-full bg-brand-400 px-2 py-0.5 rounded-md shadow-sm">
                                R$ ${item.price}
                            </span>
                            <!-- Botões de Ação (Editar / Excluir) -->
                            <div class="flex items-center gap-1.5 pt-1">
                                <button onclick="openItemModal('${item.id}')" class="action-btn text-stone-400 hover:text-stone-800 p-1 text-xs" title="Editar">
                                    <i class="fa-solid fa-pen"></i>
                                </button>
                                <button onclick="deleteFurnitureItem('${item.id}')" class="action-btn text-stone-400 hover:text-red-600 p-1 text-xs" title="Excluir">
                                    <i class="fa-solid fa-trash-can"></i>
                                </button>
                            </div>
                        </div>
                    </div>

                    <div class="flex items-center justify-between pt-1 border-t border-stone-200/60">
                        <span class="text-[11px] font-semibold text-stone-500">${qty > 0 ? 'Adicionado' : 'Clique p/ adicionar'}</span>
                        
                        <div class="flex items-center gap-1.5">
                            ${qty > 0 ? `
                                <button onclick="changeQty('${item.id}', -1)" class="action-btn w-7 h-7 rounded-lg bg-white border border-stone-300 text-stone-800 hover:bg-stone-100 flex items-center justify-center text-xs font-bold shadow-sm">
                                    <i class="fa-solid fa-minus"></i>
                                </button>
                                <span class="text-xs font-extrabold text-stone-900 w-5 text-center">${qty}</span>
                                <button onclick="changeQty('${item.id}', 1)" class="action-btn w-7 h-7 rounded-lg bg-lhblack-full text-brand-400 flex items-center justify-center text-xs font-bold shadow-sm hover:bg-stone-800">
                                    <i class="fa-solid fa-plus"></i>
                                </button>
                            ` : `
                                <button onclick="changeQty('${item.id}', 1)" class="action-btn w-7 h-7 rounded-lg bg-stone-100 text-stone-700 flex items-center justify-center text-xs font-bold hover:bg-lhblack-full hover:text-brand-400 transition">
                                    <i class="fa-solid fa-plus"></i>
                                </button>
                            `}
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function changeQty(id, delta) {
            const current = selections[id] || 0;
            const updated = current + delta;

            if (updated <= 0) {
                delete selections[id];
            } else {
                selections[id] = updated;
            }

            renderGrid();
            calculateTotal();
        }

        function toggleSelection(id) {
            if (selections[id]) {
                delete selections[id];
            } else {
                selections[id] = 1;
            }
            renderGrid();
            calculateTotal();
        }

        function calculateTotal() {
            let subtotal = 0;
            let totalItemsCount = 0;
            const summaryList = document.getElementById('selected-summary-list');
            const emptyMsg = document.getElementById('empty-summary-msg');
            summaryList.innerHTML = '';

            const selectedIds = Object.keys(selections);

            if (selectedIds.length === 0) {
                emptyMsg.classList.remove('hidden');
            } else {
                emptyMsg.classList.add('hidden');
            }

            selectedIds.forEach(id => {
                const item = catalog.find(i => i.id === id);
                if (!item) return;

                const qty = selections[id];
                const itemTotal = item.price * qty;
                subtotal += itemTotal;
                totalItemsCount += qty;

                const row = document.createElement('div');
                row.className = 'flex items-center justify-between p-2.5 rounded-xl bg-stone-50 border border-stone-200/80 text-xs';
                row.innerHTML = `
                    <div class="flex items-center gap-2">
                        <span class="w-5 h-5 rounded-md bg-lhblack-full text-brand-400 font-bold text-[10px] flex items-center justify-center">${qty}x</span>
                        <span class="font-bold text-stone-800">${item.name}</span>
                    </div>
                    <div class="flex items-center gap-3">
                        <span class="font-extrabold text-stone-900">R$ ${itemTotal.toFixed(2)}</span>
                        <button onclick="changeQty('${item.id}', -${qty})" class="text-stone-400 hover:text-red-500">
                            <i class="fa-solid fa-xmark"></i>
                        </button>
                    </div>
                `;
                summaryList.appendChild(row);
            });

            let extras = 0;
            const wallActive = document.getElementById('toggle-wall').checked;
            const travelActive = document.getElementById('toggle-travel').checked;

            if (wallActive) {
                extras += parseFloat(document.getElementById('wall-price').value) || 0;
            }
            if (travelActive) {
                extras += parseFloat(document.getElementById('travel-price').value) || 0;
            }

            const totalFinal = subtotal + extras;

            document.getElementById('selected-count-badge').innerText = `${totalItemsCount} item(ns)`;
            document.getElementById('subtotal-display').innerText = `R$ ${subtotal.toFixed(2)}`;
            document.getElementById('extras-display').innerText = `R$ ${extras.toFixed(2)}`;
            document.getElementById('total-final-display').innerText = `R$ ${totalFinal.toFixed(2)}`;
        }

        function copyToWhatsApp() {
            const selectedIds = Object.keys(selections);
            if (selectedIds.length === 0) {
                showToast('Selecione ao menos um móvel para enviar!');
                return;
            }

            const client = document.getElementById('client-name').value.trim();
            const address = document.getElementById('client-address').value.trim();
            
            let message = `🛠️ *LH INSTALAÇÕES E SERVIÇOS*\n`;
            message += ` Orçamento de Montagem de Móveis\n`;
            message += `-----------------------------------\n`;
            if (client) message += `👤 *Cliente:* ${client}\n`;
            if (address) message += `📍 *Local:* ${address}\n`;
            message += `\n📋 *Móveis a serem montados:*\n`;

            let subtotal = 0;
            selectedIds.forEach(id => {
                const item = catalog.find(i => i.id === id);
                if (item) {
                    const qty = selections[id];
                    const itemTotal = item.price * qty;
                    subtotal += itemTotal;
                    message += `• ${qty}x ${item.name} (R$ ${itemTotal.toFixed(2)})\n`;
                }
            });

            let extras = 0;
            const wallActive = document.getElementById('toggle-wall').checked;
            const travelActive = document.getElementById('toggle-travel').checked;

            if (wallActive || travelActive) {
                message += `\n⚙️ *Adicionais / Serviços Extras:*\n`;
                if (wallActive) {
                    const val = parseFloat(document.getElementById('wall-price').value) || 0;
                    extras += val;
                    message += `• Fixação na parede (bucha/parafuso): R$ ${val.toFixed(2)}\n`;
                }
                if (travelActive) {
                    const val = parseFloat(document.getElementById('travel-price').value) || 0;
                    extras += val;
                    message += `• Taxa de Deslocamento / Visita: R$ ${val.toFixed(2)}\n`;
                }
            }

            const totalFinal = subtotal + extras;
            message += `-----------------------------------\n`;
            message += `💰 *VALOR TOTAL: R$ ${totalFinal.toFixed(2)}*\n`;
            message += `💳 *Formas de Pagamento:* PIX ou Dinheiro\n\n`;
            message += `Podemos agendar o serviço para quando? Fico no aguardo! 😊`;

            const tempTextArea = document.createElement('textarea');
            tempTextArea.value = message;
            document.body.appendChild(tempTextArea);
            tempTextArea.select();
            document.execCommand('copy');
            document.body.removeChild(tempTextArea);

            showToast('Orçamento LH copiado para o WhatsApp!');
        }

        function clearCurrentProposal() {
            selections = {};
            document.getElementById('client-name').value = '';
            document.getElementById('client-address').value = '';
            document.getElementById('toggle-wall').checked = false;
            document.getElementById('toggle-travel').checked = false;
            renderGrid();
            calculateTotal();
            showToast('Orçamento limpo.');
        }

        // --- GERENCIAMENTO DE MÓVEIS (CRIAR / EDITAR / EXCLUIR) ---

        function openItemModal(id = null) {
            const modal = document.getElementById('item-modal');
            const modalTitle = document.getElementById('modal-title');

            if (id) {
                const item = catalog.find(i => i.id === id);
                if (!item) return;
                modalTitle.innerHTML = `<i class="fa-solid fa-pen-to-square text-brand-500"></i> Editar Móvel`;
                document.getElementById('modal-item-id').value = item.id;
                document.getElementById('modal-item-name').value = item.name;
                document.getElementById('modal-item-category').value = item.category;
                document.getElementById('modal-item-price').value = item.price;
            } else {
                modalTitle.innerHTML = `<i class="fa-solid fa-plus text-brand-500"></i> Cadastrar Novo Móvel`;
                document.getElementById('modal-item-id').value = '';
                document.getElementById('modal-item-name').value = '';
                document.getElementById('modal-item-category').value = 'Quarto';
                document.getElementById('modal-item-price').value = '';
            }

            modal.classList.remove('hidden');
        }

        function closeItemModal() {
            document.getElementById('item-modal').classList.add('hidden');
        }

        function saveFurnitureItem() {
            const id = document.getElementById('modal-item-id').value;
            const name = document.getElementById('modal-item-name').value.trim();
            const category = document.getElementById('modal-item-category').value;
            const price = parseFloat(document.getElementById('modal-item-price').value) || 0;

            if (!name || price <= 0) {
                showToast('Preencha o nome e um valor válido!');
                return;
            }

            if (id) {
                // Editar existente
                const index = catalog.findIndex(i => i.id === id);
                if (index !== -1) {
                    catalog[index] = { id, name, category, price };
                    showToast('Móvel atualizado com sucesso!');
                }
            } else {
                // Criar novo
                const newItem = {
                    id: Date.now().toString(),
                    name,
                    category,
                    price
                };
                catalog.push(newItem);
                showToast('Novo móvel cadastrado!');
            }

            saveCatalog();
            renderCategoryTabs();
            renderGrid();
            calculateTotal();
            closeItemModal();
        }

        function deleteFurnitureItem(id) {
            const item = catalog.find(i => i.id === id);
            if (!item) return;

            if (confirm(`Deseja realmente remover "${item.name}" do catálogo?`)) {
                catalog = catalog.filter(i => i.id !== id);
                delete selections[id];
                saveCatalog();
                renderCategoryTabs();
                renderGrid();
                calculateTotal();
                showToast('Móvel removido!');
            }
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = msg;
            toast.classList.remove('translate-y-[-100px]', 'opacity-0');

            setTimeout(() => {
                toast.classList.add('translate-y-[-100px]', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
```
