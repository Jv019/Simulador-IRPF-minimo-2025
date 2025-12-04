<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Deloitte | Simulador IRPF Mínimo 2025</title>
    
    <!-- Bibliotecas Externas (CDN) -->
    <!-- Tailwind para estilização rápida e responsiva -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Lucide Icons para interface visual limpa -->
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <!-- Chart.js para visualização de dados (Dashboard) -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        /* Fonte corporativa Open Sans (Padrão Deloitte) */
        @import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;600;700;800&display=swap');
        
        /* Variáveis de Branding */
        :root {
            --deloitte-green: #86BC25;
            --deloitte-black: #000000;
            --deloitte-white: #FFFFFF;
            --deloitte-gray: #D0D0CE;
        }

        body { font-family: 'Open Sans', sans-serif; background-color: #f4f4f4; color: #000000; }
        
        /* Tipografia da Marca */
        .brand-logo { font-weight: 800; letter-spacing: -0.02em; font-size: 1.5rem; color: #000000; }
        .brand-dot { color: #86BC25; display: inline-block; width: 0.5em; }

        /* Otimização para Impressão (Geração de Papéis de Trabalho em PDF) */
        @media print {
            body { background-color: white; -webkit-print-color-adjust: exact; }
            .no-print { display: none !important; }
            .print-only { display: block !important; }
            .card { box-shadow: none; border: 1px solid #ccc; break-inside: avoid; }
            #main-container { max-width: 100%; margin: 0; padding: 0; }
            header { border: none !important; }
            /* Remove fundos escuros para economizar tinta e melhorar legibilidade */
            .bg-black { background-color: white !important; color: black !important; border: 1px solid black; }
        }
        .print-only { display: none; }
    </style>
</head>
<body class="text-black selection:bg-[#86BC25] selection:text-white">

    <!-- MODAL DE DOCUMENTAÇÃO (Base Legal) -->
    <div id="modal-docs" class="fixed inset-0 bg-black/60 z-50 hidden flex items-center justify-center p-4 backdrop-blur-sm no-print">
        <div class="bg-white w-full max-w-3xl max-h-[90vh] overflow-y-auto border-t-[6px] border-[#86BC25] shadow-2xl">
            <div class="p-8 border-b sticky top-0 bg-white z-10 flex justify-between items-center">
                <div>
                    <h2 class="text-2xl font-bold text-black mb-1">Metodologia Legal</h2>
                    <p class="text-sm text-gray-500">Base: Lei nº 15.270 de 26/11/2025</p>
                </div>
                <button onclick="app.toggleDocs()" class="p-2 hover:bg-gray-100 rounded-full transition"><i data-lucide="x" class="w-6 h-6"></i></button>
            </div>
            
            <div class="p-8 space-y-6 text-sm text-gray-800 leading-relaxed">
                <!-- Seção 1: Art 6-A -->
                <section>
                    <h3 class="font-bold text-lg text-black mb-2 flex items-center gap-2">
                        <span class="w-2 h-2 bg-[#86BC25] rounded-full"></span> 
                        1. Retenção na Fonte (Art. 6º-A)
                    </h3>
                    <p class="text-gray-600 mb-2">
                        A partir de janeiro/2026, lucros e dividendos pagos por uma mesma PJ a uma PF residente no Brasil em montante superior a <strong>R$ 50.000,00 mensais</strong> sujeitam-se à retenção de 10%.
                    </p>
                </section>

                <!-- Seção 2: Art 16-A -->
                <section>
                    <h3 class="font-bold text-lg text-black mb-2 flex items-center gap-2">
                        <span class="w-2 h-2 bg-[#86BC25] rounded-full"></span>
                        2. IRPF Mínimo Anual (Art. 16-A)
                    </h3>
                    <p class="text-gray-600 mb-2">Aplicável para renda total anual superior a R$ 600.000,00.</p>
                    <ul class="list-disc pl-5 space-y-1 text-gray-600">
                        <li><strong>Base de Cálculo (§ 1º):</strong> Soma de todos os rendimentos (tributáveis, exclusivos, isentos), deduzindo apenas exceções taxativas (Poupança, LCI/LCA/LCD, Agro, etc).</li>
                        <li><strong>Alíquota (§ 2º):</strong>
                            <ul class="pl-4 mt-1 border-l border-gray-300">
                                <li>Até R$ 600k: 0%</li>
                                <li>R$ 600k a R$ 1.2M: Fórmula <code>(REND/60.000) - 10</code></li>
                                <li>Acima de R$ 1.2M: 10%</li>
                            </ul>
                        </li>
                    </ul>
                </section>

                <!-- Seção 3: Art 16-B -->
                <section>
                    <h3 class="font-bold text-lg text-black mb-2 flex items-center gap-2">
                        <span class="w-2 h-2 bg-[#86BC25] rounded-full"></span>
                        3. Redutor de Dividendos (Art. 16-B)
                    </h3>
                    <p class="text-gray-600">
                        Crédito concedido se (Carga PJ + Carga PF) > Limite Nominal (34%, 40% ou 45%). Evita tributação excessiva sobre o lucro distribuído.
                    </p>
                </section>
            </div>
            
            <div class="p-6 border-t bg-gray-50 flex justify-end">
                <button onclick="app.toggleDocs()" class="px-8 py-3 bg-black text-white font-bold hover:bg-[#86BC25] transition duration-300">Compreendido</button>
            </div>
        </div>
    </div>

    <!-- MAIN CONTAINER -->
    <div id="main-container" class="max-w-7xl mx-auto p-4 md:p-8 space-y-8">
        
        <!-- HEADER -->
        <header class="bg-white p-6 shadow-sm border-t-[6px] border-[#86BC25] flex flex-col md:flex-row justify-between items-center gap-6 print:border-0 print:shadow-none">
            <div class="flex flex-col items-start">
                <div class="brand-logo mb-2">
                    Deloitte<span class="text-[#86BC25]">.</span>
                </div>
                <h1 class="text-2xl font-bold text-black tracking-tight">Simulador de Tributação Mínima</h1>
                <div class="flex items-center gap-2 text-sm font-medium text-gray-500 mt-1">
                    <span class="bg-black text-white px-2 py-0.5 text-xs font-bold uppercase">Lei 15.270/2025</span>
                    <span>Compliance & Tax Calculation</span>
                </div>
            </div>
            
            <!-- Botões de Ação (Topo) -->
            <div class="flex gap-3 no-print">
                <!-- Botão Demo removido para aspecto profissional -->
                <button onclick="app.toggleDocs()" class="px-5 py-2 text-sm font-bold text-black bg-white border-2 border-gray-200 hover:border-[#86BC25] hover:text-[#86BC25] transition flex items-center gap-2">
                    <i data-lucide="scale" class="w-4 h-4"></i>
                    Base Legal
                </button>
                <button onclick="window.print()" class="px-5 py-2 text-sm font-bold text-white bg-black hover:bg-[#86BC25] transition flex items-center gap-2 shadow-lg">
                    <i data-lucide="printer" class="w-4 h-4"></i>
                    Relatório / PDF
                </button>
            </div>
        </header>

        <!-- HEADER IMPRESSÃO (Apenas visível no PDF) -->
        <div class="print-only border-b-2 border-black pb-6 mb-8">
            <div class="flex justify-between items-end">
                <div>
                    <div class="brand-logo text-2xl mb-4">Deloitte<span class="text-[#86BC25]">.</span></div>
                    <h2 class="text-xl font-bold uppercase text-black">Papel de Trabalho: Apuração IRPF Mínimo</h2>
                    <p class="text-sm text-gray-600 mt-1">Referência: Lei nº 15.270, de 26 de Novembro de 2025</p>
                </div>
                <div class="text-right text-sm">
                    <div><strong>Data Emissão:</strong> <span id="print-date"></span></div>
                    <div><strong>Responsável:</strong> Consultoria Tax</div>
                </div>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
            
            <!-- COLUNA ESQUERDA: INPUTS -->
            <div class="lg:col-span-7 space-y-6">
                
                <div class="bg-white shadow-md border border-gray-200 card">
                    <div class="p-5 border-b border-gray-200 bg-gray-50 flex justify-between items-center no-print">
                        <div>
                            <h2 class="font-bold text-black text-lg flex items-center gap-2">
                                <i data-lucide="layers" class="w-5 h-5 text-[#86BC25]"></i>
                                Fontes de Renda
                            </h2>
                            <p class="text-xs text-gray-500 mt-1">Informe os rendimentos anuais brutos</p>
                        </div>
                        <button onclick="app.addIncome()" class="text-white bg-black hover:bg-[#86BC25] text-xs font-bold uppercase tracking-wide px-4 py-2 transition shadow-lg flex items-center gap-2">
                            <i data-lucide="plus" class="w-3 h-3"></i> Adicionar
                        </button>
                    </div>

                    <div id="incomes-list" class="p-5 space-y-6">
                        <!-- Lista renderizada via JS -->
                    </div>
                    
                    <div id="empty-state" class="hidden text-center py-16 bg-gray-50/50">
                        <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-white shadow-sm mb-4">
                            <i data-lucide="folder-plus" class="w-8 h-8 text-[#86BC25]"></i>
                        </div>
                        <h3 class="text-black font-bold">Nenhuma fonte lançada</h3>
                        <p class="text-gray-500 text-sm mt-1">Clique em "Adicionar" para inserir os rendimentos do cliente.</p>
                    </div>
                </div>

                <!-- Audit Log -->
                <div class="bg-white shadow-md border border-gray-200 card">
                    <div class="p-4 border-b border-gray-200 bg-black flex justify-between items-center">
                        <h3 class="font-bold text-white text-xs uppercase tracking-widest flex items-center gap-2">
                            <i data-lucide="file-code" class="w-4 h-4 text-[#86BC25]"></i>
                            Audit Trail (Memória de Cálculo)
                        </h3>
                    </div>
                    <div class="p-4 bg-gray-50 font-mono text-xs h-64 overflow-y-auto leading-relaxed border-l-4 border-black text-gray-700" id="audit-log">
                        <!-- Logs gerados pelo algoritmo -->
                    </div>
                </div>
            </div>

            <!-- COLUNA DIREITA: RESULTADOS -->
            <div class="lg:col-span-5 space-y-6">
                
                <!-- Card Principal -->
                <div class="bg-white p-8 shadow-xl border-t-4 border-black card relative">
                    
                    <h2 class="text-xl font-bold text-black mb-6 flex items-center gap-2">
                        <i data-lucide="calculator" class="w-5 h-5 text-[#86BC25]"></i>
                        Demonstrativo Consolidado
                    </h2>

                    <div class="space-y-5">
                        <div class="flex justify-between text-sm border-b border-gray-100 pb-2">
                            <span class="text-gray-600">Total de Rendimentos</span>
                            <span class="font-bold text-black" id="res-total">R$ 0,00</span>
                        </div>
                        
                        <!-- Barra de Progresso da Base -->
                        <div>
                            <div class="flex justify-between text-sm mb-1">
                                <span class="text-gray-600">Base IRPF Mínimo (Art. 16-A)</span>
                                <span class="font-bold text-black" id="res-base">R$ 0,00</span>
                            </div>
                            <div class="w-full bg-gray-200 h-1.5 overflow-hidden">
                                <div id="progress-bar-base" class="h-full bg-[#86BC25] w-0 transition-all duration-700"></div>
                            </div>
                            <div class="flex justify-between text-[10px] text-gray-400 mt-1 uppercase tracking-wide">
                                <span>Isenção: R$ 600k</span>
                                <span>Teto: R$ 1.2M</span>
                            </div>
                        </div>

                        <!-- Detalhes do Cálculo -->
                        <div class="bg-gray-50 p-4 border border-gray-100">
                            <div class="flex justify-between items-center mb-2">
                                <span class="text-xs font-bold text-gray-500 uppercase">Alíquota Efetiva</span>
                                <span id="res-rate" class="text-sm font-bold bg-black text-[#86BC25] px-2 py-0.5 font-mono">0.00%</span>
                            </div>
                            <div class="flex justify-between text-sm text-gray-800">
                                <span>Imposto Mínimo Bruto</span>
                                <span class="font-bold" id="res-gross">R$ 0,00</span>
                            </div>
                        </div>

                        <!-- Redutor Visual -->
                        <div id="row-reducer" class="hidden flex justify-between text-sm text-[#86BC25] bg-green-50/50 p-3 border-l-2 border-[#86BC25]">
                            <span class="flex items-center gap-1 font-bold"><i data-lucide="arrow-down-circle" class="w-3 h-3"></i> Crédito Redutor (Art. 16-B)</span>
                            <span class="font-bold" id="res-reducer">-R$ 0,00</span>
                        </div>

                        <!-- Saldo Final -->
                        <div class="pt-2">
                            <div class="flex justify-between items-end mb-1">
                                <span class="text-sm font-bold text-black">IRPF Mínimo Devido</span>
                                <span class="text-xl font-bold text-black" id="res-net">R$ 0,00</span>
                            </div>
                            <div class="flex justify-between text-xs text-gray-500">
                                <span title="IRRF (Art. 6-A) + Outros Pagamentos">(-) Antecipação/Retenções</span>
                                <span id="res-paid">-R$ 0,00</span>
                            </div>
                        </div>

                        <!-- Caixa de Status -->
                        <div id="status-box" class="mt-6 p-6 text-center transition-all bg-gray-50 border border-gray-200">
                            <span id="status-label" class="text-xs font-bold uppercase tracking-widest mb-2 block text-gray-400">Resultado da Apuração</span>
                            <span id="status-value" class="text-3xl font-extrabold block text-black tracking-tight">R$ 0,00</span>
                            <p id="status-desc" class="text-xs mt-3 text-gray-500">Aguardando dados para cálculo.</p>
                        </div>
                    </div>
                </div>

                <!-- Gráfico -->
                <div class="bg-white p-6 shadow-md border border-gray-200 card no-print">
                    <h3 class="text-xs font-bold text-black uppercase tracking-widest mb-4 border-b pb-2">Composição Tributária</h3>
                    <div class="h-48">
                        <canvas id="taxChart"></canvas>
                    </div>
                </div>

                <!-- Disclaimer Oficial -->
                <div class="print-only text-[10px] text-justify text-gray-500 mt-8 border-t border-black pt-4 font-serif leading-tight">
                    <p><strong>Disclaimer:</strong> Este documento constitui um papel de trabalho auxiliar e não substitui a declaração oficial. O cálculo observa estritamente os Arts. 6º-A, 16-A e 16-B da Lei nº 15.270/2025. A responsabilidade pela veracidade dos dados (especialmente a carga efetiva da PJ para fins de redutor) é do usuário.</p>
                </div>

            </div>
        </div>

        <!-- TEMPLATE DO ITEM DE RENDA (DOM Injection) -->
        <template id="income-template">
            <div class="group relative bg-white p-5 border border-gray-200 hover:border-[#86BC25] hover:shadow-md transition-all duration-300 card mb-4">
                <button class="btn-remove absolute top-4 right-4 text-gray-300 hover:text-black transition no-print">
                    <i data-lucide="trash" class="w-4 h-4"></i>
                </button>

                <!-- Linha 1: Descrição e CNPJ -->
                <div class="grid grid-cols-1 md:grid-cols-12 gap-5 mb-4">
                    <div class="md:col-span-8">
                        <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5">Fonte Pagadora</label>
                        <input type="text" class="inp-desc w-full p-2.5 bg-gray-50 border-b-2 border-gray-200 focus:border-[#86BC25] focus:bg-white outline-none transition text-sm font-semibold text-black placeholder-gray-400" placeholder="Ex: Cia ABC Participações">
                    </div>
                    <div class="md:col-span-4">
                        <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5">CNPJ</label>
                        <input type="text" class="inp-cnpj w-full p-2.5 bg-gray-50 border-b-2 border-gray-200 focus:border-[#86BC25] focus:bg-white outline-none transition text-sm text-black placeholder-gray-400" placeholder="00.000.000/0000-00">
                    </div>
                </div>

                <!-- Linha 2: Valores e Tipo -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-5">
                    <!-- Tipo -->
                    <div>
                        <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5">Natureza</label>
                        <div class="relative">
                            <select class="inp-type w-full p-2.5 bg-white border border-gray-200 text-sm font-medium appearance-none pr-8 cursor-pointer focus:border-[#86BC25] outline-none text-black hover:bg-gray-50 transition">
                                <option value="salary">Salário / Pró-Labore</option>
                                <option value="dividend">Lucros e Dividendos (Art. 6-A/16-B)</option>
                                <option value="capital_gain">Ganho de Capital</option>
                                <option value="savings">Isento (Lei Art. 16-A §1º)</option>
                            </select>
                            <i data-lucide="chevron-down" class="w-4 h-4 absolute right-3 top-3 text-gray-400 pointer-events-none"></i>
                        </div>
                    </div>
                    
                    <!-- Valor -->
                    <div>
                        <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5">Rendimento Anual</label>
                        <div class="relative">
                            <span class="absolute left-3 top-2.5 text-gray-400 text-sm font-medium">R$</span>
                            <input type="number" class="inp-val w-full p-2.5 pl-9 border border-gray-200 focus:border-[#86BC25] outline-none text-sm font-mono font-bold text-black placeholder-gray-300" placeholder="0,00">
                        </div>
                    </div>

                    <!-- Imposto -->
                    <div>
                        <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5 flex items-center justify-between">
                            <span>IR Pago/Retido</span>
                            <i data-lucide="info" class="w-3 h-3 text-gray-300 cursor-help" title="Incluir antecipação de 10% (Art. 6-A) se houver"></i>
                        </label>
                        <div class="relative">
                            <span class="absolute left-3 top-2.5 text-gray-400 text-sm font-medium">R$</span>
                            <input type="number" class="inp-tax w-full p-2.5 pl-9 border border-gray-200 focus:border-[#86BC25] outline-none text-sm font-mono font-bold text-black placeholder-gray-300" placeholder="0,00">
                        </div>
                    </div>
                </div>

                <!-- Alertas Dinâmicos (Art 6-A) -->
                <div class="alert-container mt-3">
                    <div class="alert-50k hidden flex items-start gap-2 bg-yellow-50 p-2 border border-yellow-200 text-[11px] text-yellow-800 mt-2">
                        <i data-lucide="alert-triangle" class="w-4 h-4 mt-0.5 shrink-0"></i>
                        <span><strong>Compliance (Art. 6º-A):</strong> A média mensal excede R$ 50.000,00. Verificar retenção de 10% na fonte.</span>
                    </div>
                </div>

                <!-- Painel do Redutor (Art 16-B) -->
                <div class="area-redutor hidden mt-4 pt-4 border-t border-gray-100 bg-gray-50/50 -mx-5 -mb-5 p-5">
                    <div class="flex items-center gap-2 mb-3">
                        <span class="bg-[#86BC25] text-white text-[10px] font-bold px-2 py-0.5 rounded-full uppercase">Art. 16-B</span>
                        <span class="text-xs font-bold text-black">Parâmetros para Cálculo do Crédito</span>
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-[10px] text-gray-500 mb-1">Alíquota Efetiva PJ (Decimal)</label>
                            <input type="number" step="0.0001" class="inp-corp-rate w-full p-2 border border-gray-300 text-xs text-center text-black font-mono focus:border-[#86BC25] outline-none" value="0.34">
                        </div>
                        <div>
                            <label class="block text-[10px] text-gray-500 mb-1">Teto Setorial (§1º)</label>
                            <select class="inp-corp-limit w-full p-2 border border-gray-300 text-xs bg-white text-black focus:border-[#86BC25] outline-none">
                                <option value="0.34">34% (Geral)</option>
                                <option value="0.40">40% (Seguros)</option>
                                <option value="0.45">45% (Bancos)</option>
                            </select>
                        </div>
                    </div>
                </div>
            </div>
        </template>
    </div>

    <!-- LOGIC CORE -->
    <script>
        /**
         * Parâmetros Globais conforme Lei 15.270/2025
         * Manter alinhado com publicação oficial do DOU.
         */
        const TAX_RULES = {
            MIN_THRESHOLD: 600000,   // Limite de isenção Art. 16-A
            MAX_THRESHOLD: 1200000,  // Teto da progressividade
            MAX_RATE: 0.10,          // Alíquota máxima 10%
            DIVIDEND_RETENTION_MONTHLY_LIMIT: 50000 // Limite mensal Art. 6-A
        };

        const INCOME_CONFIG = {
            'salary': { label: 'Rendimento Tributável', include: true, isDividend: false },
            'dividend': { label: 'Lucros e Dividendos', include: true, isDividend: true },
            'capital_gain': { label: 'Ganho de Capital', include: true, isDividend: false },
            'savings': { label: 'Excluído (Isento)', include: false, isDividend: false }
        };

        const app = {
            data: [],
            chart: null,

            // Inicialização do App
            init() {
                this.updateDate();
                lucide.createIcons();
                this.initChart();
                // Verifica estado inicial vazio
                this.renderList();
            },

            updateDate() {
                const date = new Date().toLocaleDateString('pt-BR');
                const el = document.getElementById('print-date');
                if(el) el.textContent = date;
            },

            addIncome(defaults = {}) {
                const id = Date.now();
                this.data.push({
                    id,
                    desc: defaults.desc || '',
                    cnpj: '',
                    type: defaults.type || 'salary',
                    val: defaults.val || 0,
                    tax: defaults.tax || 0,
                    corpRate: 0.34,
                    corpLimit: 0.34,
                    showRedutor: false
                });
                this.renderList();
            },

            removeIncome(id) {
                this.data = this.data.filter(item => item.id !== id);
                this.renderList();
            },

            updateItem(id, field, value) {
                const idx = this.data.findIndex(i => i.id === id);
                if (idx === -1) return;
                
                // Parsing de valores numéricos para evitar erros de cálculo
                if (['val', 'tax', 'corpRate', 'corpLimit'].includes(field)) {
                    value = parseFloat(value) || 0;
                    if(value < 0) value = 0; // Proteção contra negativos
                }
                
                this.data[idx][field] = value;
                
                // Ajuste de UI baseado no tipo de renda
                if (field === 'type') {
                    this.data[idx].showRedutor = INCOME_CONFIG[value].isDividend;
                }

                // Recalcula totais
                this.calculate();
                
                // Validações visuais (sem re-render completo para manter foco no input)
                this.validateItemVisuals(id);
            },

            validateItemVisuals(id) {
                const item = this.data.find(i => i.id === id);
                const elItem = document.querySelector(`[data-id="${id}"]`);
                if(!elItem) return;

                const alert50k = elItem.querySelector('.alert-50k');
                const areaRed = elItem.querySelector('.area-redutor');
                
                // Validação de Compliance Art. 6-A (Retenção 50k mensal)
                // Usamos uma média simples anualizada para o alerta
                if (item.type === 'dividend' && item.val > (TAX_RULES.DIVIDEND_RETENTION_MONTHLY_LIMIT * 12)) {
                    alert50k.classList.remove('hidden');
                } else {
                    alert50k.classList.add('hidden');
                }

                // Toggle área do Redutor
                if (item.type === 'dividend') {
                    areaRed.classList.remove('hidden');
                } else {
                    areaRed.classList.add('hidden');
                }
            },

            renderList() {
                const container = document.getElementById('incomes-list');
                const template = document.getElementById('income-template');
                container.innerHTML = '';

                if (this.data.length === 0) {
                    document.getElementById('empty-state').classList.remove('hidden');
                } else {
                    document.getElementById('empty-state').classList.add('hidden');
                    
                    this.data.forEach(item => {
                        const clone = template.content.cloneNode(true);
                        const root = clone.querySelector('.card');
                        root.setAttribute('data-id', item.id);

                        // Helper para bind de eventos
                        const bind = (selector, field, event = 'input') => {
                            const el = clone.querySelector(selector);
                            el.value = item[field];
                            el.addEventListener(event, (e) => this.updateItem(item.id, field, e.target.value));
                        };

                        bind('.inp-desc', 'desc');
                        bind('.inp-cnpj', 'cnpj');
                        
                        const elType = clone.querySelector('.inp-type');
                        elType.value = item.type;
                        elType.addEventListener('change', (e) => {
                            this.updateItem(item.id, 'type', e.target.value);
                            this.renderList(); // Re-render necessário se mudar estrutura
                        });

                        bind('.inp-val', 'val');
                        bind('.inp-tax', 'tax');
                        bind('.inp-corp-rate', 'corpRate');
                        
                        const elCorpLim = clone.querySelector('.inp-corp-limit');
                        elCorpLim.value = item.corpLimit;
                        elCorpLim.addEventListener('change', (e) => this.updateItem(item.id, 'corpLimit', e.target.value));

                        clone.querySelector('.btn-remove').onclick = () => this.removeIncome(item.id);

                        container.appendChild(clone);
                        setTimeout(() => this.validateItemVisuals(item.id), 0);
                    });
                }
                
                lucide.createIcons();
                this.calculate();
            },

            // --- CORE ENGINE DE CÁLCULO ---
            calculate() {
                let logs = [];
                let totalIncome = 0;
                let minBase = 0;
                let paidTax = 0;
                
                const now = new Date().toLocaleTimeString();
                logs.push(`[${now}] INICIANDO APURAÇÃO...`);

                // PASSO 1: Classificação e Soma (Art. 16-A § 1º)
                this.data.forEach(item => {
                    const config = INCOME_CONFIG[item.type];
                    totalIncome += item.val;
                    paidTax += item.tax;
                    
                    if (config.include) {
                        minBase += item.val;
                        logs.push(`[BASE] R$ ${item.val.toLocaleString('pt-BR')} - ${item.desc} (${config.label})`);
                    } else {
                        logs.push(`[EXCLUÍDO] R$ ${item.val.toLocaleString('pt-BR')} - ${item.desc} (Isento/Excluído)`);
                    }
                });

                // PASSO 2: Aplicação da Alíquota Progressiva (Art 16-A § 2º)
                let rate = 0;
                if (minBase <= TAX_RULES.MIN_THRESHOLD) {
                    rate = 0;
                    logs.push(`> FAIXA ISENTA: Base <= R$ 600k`);
                } else if (minBase >= TAX_RULES.MAX_THRESHOLD) {
                    rate = TAX_RULES.MAX_RATE;
                    logs.push(`> FAIXA TETO: Base >= R$ 1.2M. Alíquota Fixa 10%`);
                } else {
                    // Cálculo da Fórmula: Alíquota = (REND / 60.000) - 10
                    const formulaValue = (minBase / 60000) - 10;
                    rate = formulaValue / 100; // Converte percentual para decimal
                    logs.push(`> PROGRESSIVIDADE: Aplicação da Fórmula Art. 16-A §2º II`);
                    logs.push(`> (${minBase.toLocaleString('pt-BR')} / 60.000) - 10 = ${formulaValue.toFixed(4)}%`);
                }

                const grossTax = minBase * rate;

                // PASSO 3: Cálculo do Redutor de Dividendos (Art 16-B)
                let totalReducer = 0;
                this.data.forEach(item => {
                    if (INCOME_CONFIG[item.type].isDividend && rate > 0) {
                        const effectiveTotalLoad = item.corpRate + rate;
                        if (effectiveTotalLoad > item.corpLimit) {
                            const creditRate = effectiveTotalLoad - item.corpLimit;
                            const creditVal = item.val * creditRate;
                            totalReducer += creditVal;
                            logs.push(`> REDUTOR APLICADO (${item.desc}): Carga Efetiva ${(effectiveTotalLoad*100).toFixed(2)}% excedeu teto de ${item.corpLimit*100}%. Crédito: R$ ${creditVal.toFixed(2)}`);
                        }
                    }
                });

                // PASSO 4: Consolidação Final (Netting)
                const netMinTax = Math.max(0, grossTax - totalReducer);
                const finalDue = netMinTax - paidTax;

                // --- Atualização da Interface (DOM) ---
                const fmt = (v) => v.toLocaleString('pt-BR', {style:'currency', currency:'BRL'});
                
                document.getElementById('res-total').textContent = fmt(totalIncome);
                document.getElementById('res-base').textContent = fmt(minBase);
                document.getElementById('res-rate').textContent = (rate * 100).toFixed(4) + '%';
                
                // Atualiza Barra de Progresso Visual
                const pct = Math.min(100, Math.max(0, ((minBase - 600000) / 600000) * 100));
                document.getElementById('progress-bar-base').style.width = minBase < 600000 ? '0%' : `${pct}%`;

                document.getElementById('res-gross').textContent = fmt(grossTax);
                
                // Exibe Redutor apenas se houver valor relevante
                const elRed = document.getElementById('row-reducer');
                if (totalReducer > 0.01) {
                    elRed.classList.remove('hidden');
                    document.getElementById('res-reducer').textContent = '-' + fmt(totalReducer);
                } else {
                    elRed.classList.add('hidden');
                }

                document.getElementById('res-net').textContent = fmt(netMinTax);
                document.getElementById('res-paid').textContent = '-' + fmt(paidTax);

                // Lógica de Status Final
                const box = document.getElementById('status-box');
                const lbl = document.getElementById('status-label');
                const val = document.getElementById('status-value');
                const dsc = document.getElementById('status-desc');

                if (finalDue > 0.01) {
                    // Cenário: Saldo a Pagar
                    box.className = "mt-6 p-6 text-center transition-all bg-white border-2 border-black";
                    lbl.textContent = "Saldo a Recolher (Art. 16-A §6º)";
                    lbl.className = "text-xs font-bold uppercase tracking-widest mb-2 block text-black";
                    val.textContent = fmt(finalDue);
                    val.className = "text-3xl font-extrabold block text-black tracking-tight";
                    dsc.textContent = "Valor deve ser adicionado ao Ajuste Anual.";
                } else {
                    // Cenário: Conformidade
                    box.className = "mt-6 p-6 text-center transition-all bg-[#86BC25] border-2 border-[#86BC25]";
                    lbl.textContent = "Conformidade Fiscal Verificada";
                    lbl.className = "text-xs font-bold uppercase tracking-widest mb-2 block text-white/90";
                    val.textContent = "R$ 0,00";
                    val.className = "text-3xl font-extrabold block text-white tracking-tight";
                    dsc.textContent = "Retenções na fonte cobrem a exigência mínima da lei.";
                    dsc.className = "text-xs mt-3 text-white/90";
                }

                // Renderiza Logs
                const logContainer = document.getElementById('audit-log');
                logContainer.innerHTML = logs.map(l => `<div class="border-b border-gray-200 py-1.5 hover:bg-white px-2 transition">${l}</div>`).join('');

                this.updateChart(paidTax, finalDue > 0 ? finalDue : 0, totalReducer);
            },

            // --- VISUALIZAÇÃO ---
            initChart() {
                const ctx = document.getElementById('taxChart').getContext('2d');
                Chart.defaults.font.family = "'Open Sans', sans-serif";
                this.chart = new Chart(ctx, {
                    type: 'doughnut',
                    data: {
                        labels: ['Retido na Fonte', 'Saldo a Pagar', 'Crédito Redutor'],
                        datasets: [{
                            data: [0, 0, 0],
                            backgroundColor: ['#D0D0CE', '#000000', '#86BC25'], // Cores Deloitte
                            borderWidth: 0,
                            hoverOffset: 4
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: { 
                            legend: { position: 'right', labels: { font: { size: 11 }, usePointStyle: true, boxWidth: 8 } }
                        },
                        cutout: '70%'
                    }
                });
            },

            updateChart(paid, due, reducer) {
                if(this.chart) {
                    this.chart.data.datasets[0].data = [paid, due, reducer];
                    this.chart.update();
                }
            },

            toggleDocs() {
                const m = document.getElementById('modal-docs');
                m.classList.toggle('hidden');
            }
        };

        // Bootstrap da Aplicação
        window.onload = () => app.init();
    </script>
</body>
</html>
