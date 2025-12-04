<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Deloitte | Simulador IRPF Mínimo 2025</title>
    
    <!-- Bibliotecas Externas (CDN) -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        @import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;600;700;800&display=swap');
        
        :root {
            --deloitte-green: #86BC25;
            --deloitte-black: #000000;
            --deloitte-white: #FFFFFF;
            --deloitte-gray: #D0D0CE;
        }

        body { font-family: 'Open Sans', sans-serif; background-color: #f4f4f4; color: #000000; }
        
        .brand-logo { font-weight: 800; letter-spacing: -0.02em; font-size: 1.5rem; color: #000000; }
        .brand-dot { color: #86BC25; display: inline-block; width: 0.5em; }

        @media print {
            body { background-color: white; -webkit-print-color-adjust: exact; }
            .no-print { display: none !important; }
            .print-only { display: block !important; }
            .card { box-shadow: none; border: 1px solid #ccc; break-inside: avoid; }
            #main-container { max-width: 100%; margin: 0; padding: 0; }
            header { border: none !important; }
            .bg-black { background-color: white !important; color: black !important; border: 1px solid black; }
        }
        .print-only { display: none; }
    </style>
</head>
<body class="text-black selection:bg-[#86BC25] selection:text-white">

    <!-- MODAL DE DOCUMENTAÇÃO -->
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
                <section>
                    <h3 class="font-bold text-lg text-black mb-2 flex items-center gap-2">
                        <span class="w-2 h-2 bg-[#86BC25] rounded-full"></span> 
                        1. Base de Cálculo Anual (Art. 16-A)
                    </h3>
                    <p class="text-gray-600 mb-2">A tributação mínima considera a <strong>soma anual</strong> de todos os rendimentos. Caso tenha renda variável (ex: 60k num mês, 40k no outro), insira o <strong>Total Anual</strong>.</p>
                    <ul class="list-disc pl-5 space-y-1 text-gray-600">
                        <li>Até R$ 600k/ano: <strong>Isento (0%)</strong></li>
                        <li>R$ 600k a R$ 1.2M/ano: <strong>Fórmula (Renda / 60.000) - 10</strong></li>
                        <li>Acima de R$ 1.2M/ano: <strong>Fixa em 10%</strong></li>
                    </ul>
                </section>
                <section>
                    <h3 class="font-bold text-lg text-black mb-2 flex items-center gap-2">
                        <span class="w-2 h-2 bg-[#86BC25] rounded-full"></span> 
                        2. Retenção Mensal (Art. 6-A)
                    </h3>
                    <p class="text-gray-600">A retenção de 10% é devida apenas nos meses onde o pagamento de dividendos superar R$ 50.000,00. O IRPF Mínimo (anual) desconta o que foi retido.</p>
                </section>
            </div>
            <div class="p-6 border-t bg-gray-50 flex justify-end">
                <button onclick="app.toggleDocs()" class="px-8 py-3 bg-black text-white font-bold hover:bg-[#86BC25] transition duration-300">Entendi</button>
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
                    <span>Cálculo Mensal e Anual</span>
                </div>
            </div>
            
            <div class="flex gap-3 no-print">
                <button onclick="app.toggleDocs()" class="px-5 py-2 text-sm font-bold text-black bg-white border-2 border-gray-200 hover:border-[#86BC25] hover:text-[#86BC25] transition flex items-center gap-2">
                    <i data-lucide="scale" class="w-4 h-4"></i>
                    Regras
                </button>
                <button onclick="window.print()" class="px-5 py-2 text-sm font-bold text-white bg-black hover:bg-[#86BC25] transition flex items-center gap-2 shadow-lg">
                    <i data-lucide="printer" class="w-4 h-4"></i>
                    Imprimir Relatório
                </button>
            </div>
        </header>

        <!-- HEADER IMPRESSÃO -->
        <div class="print-only border-b-2 border-black pb-6 mb-8">
            <div class="flex justify-between items-end">
                <div>
                    <div class="brand-logo text-2xl mb-4">Deloitte<span class="text-[#86BC25]">.</span></div>
                    <h2 class="text-xl font-bold uppercase text-black">Relatório de Apuração IRPF Mínimo</h2>
                </div>
                <div class="text-right text-sm">
                    <div class="mb-1"><strong>Contribuinte:</strong> <span id="print-taxpayer-name">N/A</span></div>
                    <div><strong>Data:</strong> <span id="print-date"></span></div>
                </div>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
            
            <!-- ESQUERDA: INPUTS -->
            <div class="lg:col-span-7 space-y-6">
                
                <!-- Identificação -->
                <div class="bg-white shadow-md border border-gray-200 card">
                    <div class="p-5 border-b border-gray-200 bg-gray-50 flex justify-between items-center no-print">
                        <h2 class="font-bold text-black text-lg flex items-center gap-2">
                            <i data-lucide="user" class="w-5 h-5 text-[#86BC25]"></i>
                            Identificação
                        </h2>
                    </div>
                    <div class="p-5 grid grid-cols-1 md:grid-cols-2 gap-5">
                        <div>
                            <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5">Nome do Contribuinte</label>
                            <input type="text" id="input-taxpayer-name" oninput="app.updateTaxpayerInfo()" class="w-full p-2.5 bg-white border border-gray-300 focus:border-[#86BC25] outline-none transition text-sm text-black" placeholder="Nome Completo">
                        </div>
                        <div>
                            <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5">CPF</label>
                            <input type="text" id="input-taxpayer-cpf" oninput="app.updateTaxpayerInfo()" class="w-full p-2.5 bg-white border border-gray-300 focus:border-[#86BC25] outline-none transition text-sm text-black" placeholder="000.000.000-00">
                        </div>
                    </div>
                </div>

                <!-- Fontes de Renda -->
                <div class="bg-white shadow-md border border-gray-200 card">
                    <div class="p-5 border-b border-gray-200 bg-gray-50 flex justify-between items-center no-print">
                        <div>
                            <h2 class="font-bold text-black text-lg flex items-center gap-2">
                                <i data-lucide="layers" class="w-5 h-5 text-[#86BC25]"></i>
                                Fontes de Renda
                            </h2>
                            <p class="text-xs text-gray-500 mt-1">Utilize "Mensal" para projeções ou "Anual" para valores fechados.</p>
                        </div>
                        <button onclick="app.addIncome()" class="text-white bg-black hover:bg-[#86BC25] text-xs font-bold uppercase tracking-wide px-4 py-2 transition shadow-lg flex items-center gap-2">
                            <i data-lucide="plus" class="w-3 h-3"></i> Adicionar
                        </button>
                    </div>

                    <div id="incomes-list" class="p-5 space-y-6">
                        <!-- Lista Dinâmica -->
                    </div>
                    
                    <div id="empty-state" class="hidden text-center py-16 bg-gray-50/50">
                        <h3 class="text-black font-bold">Nenhuma fonte lançada</h3>
                        <p class="text-gray-500 text-sm mt-1">Clique em "Adicionar" para iniciar.</p>
                    </div>
                </div>
            </div>

            <!-- DIREITA: RESULTADOS -->
            <div class="lg:col-span-5 space-y-6">
                
                <!-- Resultado Consolidado -->
                <div class="bg-white p-8 shadow-xl border-t-4 border-black card relative">
                    
                    <div class="flex justify-between items-start mb-6">
                        <h2 class="text-xl font-bold text-black flex items-center gap-2">
                            <i data-lucide="calculator" class="w-5 h-5 text-[#86BC25]"></i>
                            Resultado Consolidado
                        </h2>
                        <span class="text-[10px] font-bold uppercase bg-gray-100 px-2 py-1 rounded text-gray-500">Ano-Calendário 2026</span>
                    </div>

                    <!-- Tabela de Valores -->
                    <div class="space-y-0 text-sm border border-gray-200 rounded-sm overflow-hidden">
                        
                        <!-- Cabeçalho da Tabela -->
                        <div class="grid grid-cols-3 bg-gray-50 border-b border-gray-200 p-2 font-bold text-[10px] uppercase tracking-wide text-gray-500">
                            <div class="col-span-1">Item</div>
                            <div class="col-span-1 text-right">Média Mensal</div>
                            <div class="col-span-1 text-right">Total Anual</div>
                        </div>

                        <!-- Linha 1: Renda Total -->
                        <div class="grid grid-cols-3 border-b border-gray-100 p-3 hover:bg-gray-50 transition">
                            <div class="col-span-1 font-semibold text-gray-700">Renda Total</div>
                            <div class="col-span-1 text-right text-gray-500" id="res-total-month">R$ 0,00</div>
                            <div class="col-span-1 text-right font-bold text-black" id="res-total-year">R$ 0,00</div>
                        </div>

                        <!-- Linha 2: Base de Cálculo -->
                        <div class="grid grid-cols-3 border-b border-gray-100 p-3 hover:bg-gray-50 transition">
                            <div class="col-span-1 font-semibold text-gray-700">Base IRPF Mín.</div>
                            <div class="col-span-1 text-right text-gray-500" id="res-base-month">R$ 0,00</div>
                            <div class="col-span-1 text-right font-bold text-black" id="res-base-year">R$ 0,00</div>
                        </div>

                        <!-- Linha 3: Imposto Devido (Calculado) -->
                        <div class="grid grid-cols-3 border-b border-gray-100 p-3 bg-gray-50/50">
                            <div class="col-span-1 font-bold text-black flex flex-col">
                                <span>Imposto Devido</span>
                                <span class="text-[10px] font-normal text-gray-500">Alíquota: <span id="res-rate">0.00%</span></span>
                            </div>
                            <div class="col-span-1 text-right text-gray-500 font-medium" id="res-due-month">R$ 0,00</div>
                            <div class="col-span-1 text-right font-bold text-black" id="res-due-year">R$ 0,00</div>
                        </div>

                        <!-- Linha 4: Imposto Pago (Input) -->
                        <div class="grid grid-cols-3 p-3">
                            <div class="col-span-1 font-semibold text-gray-600">(-) Imposto Pago</div>
                            <div class="col-span-1 text-right text-gray-400" id="res-paid-month">-R$ 0,00</div>
                            <div class="col-span-1 text-right font-medium text-gray-600" id="res-paid-year">-R$ 0,00</div>
                        </div>
                    </div>

                    <!-- Caixa de Status Final -->
                    <div id="status-box" class="mt-6 p-6 text-center transition-all bg-gray-50 border border-gray-200">
                        <span id="status-label" class="text-xs font-bold uppercase tracking-widest mb-2 block text-gray-400">Resultado Final</span>
                        <span id="status-value" class="text-3xl font-extrabold block text-black tracking-tight">R$ 0,00</span>
                        <p id="status-desc" class="text-xs mt-3 text-gray-500">Preencha os valores para calcular.</p>
                    </div>
                </div>

                <!-- Gráfico -->
                <div class="bg-white p-6 shadow-md border border-gray-200 card no-print">
                    <h3 class="text-xs font-bold text-black uppercase tracking-widest mb-4 border-b pb-2">Comparativo: Devido vs Pago</h3>
                    <div class="h-48">
                        <canvas id="taxChart"></canvas>
                    </div>
                </div>
            </div>
        </div>

        <!-- TEMPLATE ITEM -->
        <template id="income-template">
            <div class="group relative bg-white p-5 border border-gray-200 hover:border-[#86BC25] hover:shadow-md transition-all duration-300 card mb-4">
                <button class="btn-remove absolute top-4 right-4 text-gray-300 hover:text-black transition no-print">
                    <i data-lucide="trash" class="w-4 h-4"></i>
                </button>

                <!-- Linha 1: Fonte, CNPJ e Natureza -->
                <div class="grid grid-cols-1 md:grid-cols-12 gap-5 mb-4">
                    <div class="md:col-span-5">
                        <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5">Fonte Pagadora</label>
                        <input type="text" class="inp-desc w-full p-2.5 bg-gray-50 border-b-2 border-gray-200 focus:border-[#86BC25] focus:bg-white outline-none transition text-sm font-semibold text-black placeholder-gray-400" placeholder="Empresa">
                    </div>
                    <div class="md:col-span-3">
                        <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5">CNPJ</label>
                        <input type="text" class="inp-cnpj w-full p-2.5 bg-gray-50 border-b-2 border-gray-200 focus:border-[#86BC25] focus:bg-white outline-none transition text-sm text-black placeholder-gray-400" placeholder="00.000/0000-00">
                    </div>
                    <div class="md:col-span-4">
                        <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5">Natureza</label>
                        <div class="relative">
                            <select class="inp-type w-full p-2.5 bg-white border border-gray-200 text-sm font-medium appearance-none pr-8 cursor-pointer focus:border-[#86BC25] outline-none text-black hover:bg-gray-50 transition">
                                <option value="salary">Salário / Pró-Labore</option>
                                <option value="dividend">Lucros e Dividendos</option>
                                <option value="capital_gain">Ganho de Capital</option>
                                <option value="savings">Isento (Poupança/LCI)</option>
                            </select>
                            <i data-lucide="chevron-down" class="w-4 h-4 absolute right-3 top-3 text-gray-400 pointer-events-none"></i>
                        </div>
                    </div>
                </div>

                <!-- Linha 2: Valores e Frequência -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
                    <div>
                        <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5">Rendimento Bruto</label>
                        <div class="flex gap-2">
                            <div class="relative w-full">
                                <span class="absolute left-3 top-2.5 text-gray-400 text-sm font-medium">R$</span>
                                <input type="number" class="inp-val w-full p-2.5 pl-9 border border-gray-200 focus:border-[#86BC25] outline-none text-sm font-mono font-bold text-black placeholder-gray-300" placeholder="0,00">
                            </div>
                            <select class="inp-freq w-24 bg-gray-50 border border-gray-200 text-xs font-bold text-gray-700 focus:border-[#86BC25] outline-none cursor-pointer">
                                <option value="annual">Anual</option>
                                <option value="monthly">Mensal</option>
                            </select>
                        </div>
                        <div class="text-[10px] text-gray-400 mt-1 text-right monthly-preview">Média: R$ 0,00/mês</div>
                    </div>

                    <div>
                        <label class="block text-[10px] font-bold text-gray-400 uppercase tracking-wide mb-1.5">Imposto Pago / Retido</label>
                        <div class="relative">
                            <span class="absolute left-3 top-2.5 text-gray-400 text-sm font-medium">R$</span>
                            <input type="number" class="inp-tax w-full p-2.5 pl-9 border border-gray-200 focus:border-[#86BC25] outline-none text-sm font-mono font-bold text-black placeholder-gray-300" placeholder="0,00">
                        </div>
                        <div class="text-[10px] text-gray-300 mt-1 text-right">*Na mesma frequência</div>
                    </div>
                </div>

                <div class="alert-container mt-3">
                    <div class="alert-50k hidden flex items-start gap-2 bg-yellow-50 p-2 border border-yellow-200 text-[11px] text-yellow-800 mt-2">
                        <i data-lucide="alert-triangle" class="w-4 h-4 mt-0.5 shrink-0"></i>
                        <span><strong>Compliance (Art. 6º-A):</strong> Média mensal excede R$ 50.000,00. Verificar retenção de 10%.</span>
                    </div>
                </div>

                <!-- Redutor com Calculadora Auxiliar -->
                <div class="area-redutor hidden mt-4 pt-4 border-t border-gray-100 bg-gray-50/50 -mx-5 -mb-5 p-5">
                    <div class="flex items-center justify-between mb-3">
                        <div class="flex items-center gap-2">
                            <span class="bg-[#86BC25] text-white text-[10px] font-bold px-2 py-0.5 rounded-full uppercase">Art. 16-B</span>
                            <span class="text-xs font-bold text-black">Redutor de Dividendos</span>
                        </div>
                        <button type="button" class="btn-calc-helper text-[10px] text-indigo-600 hover:underline flex items-center gap-1 font-bold">
                            <i data-lucide="calculator" class="w-3 h-3"></i> Calcular Alíquota
                        </button>
                    </div>
                    
                    <!-- Calculadora Helper (Toggle) -->
                    <div class="calc-helper hidden bg-white border border-indigo-100 p-3 mb-3 rounded shadow-sm">
                        <p class="text-[10px] font-bold text-gray-500 mb-2 uppercase">Calculadora de Alíquota Efetiva</p>
                        <div class="grid grid-cols-3 gap-2 mb-2">
                            <div><label class="text-[9px]">Lucro Contábil</label><input type="number" class="hlp-profit w-full border p-1 text-xs"></div>
                            <div><label class="text-[9px]">IRPJ Devido</label><input type="number" class="hlp-irpj w-full border p-1 text-xs"></div>
                            <div><label class="text-[9px]">CSLL Devida</label><input type="number" class="hlp-csll w-full border p-1 text-xs"></div>
                        </div>
                        <button type="button" class="btn-apply-rate w-full bg-indigo-600 text-white text-[10px] py-1 font-bold hover:bg-indigo-700">Aplicar Resultado</button>
                    </div>

                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-[10px] text-gray-500 mb-1">Carga Efetiva PJ (Decimal)</label>
                            <input type="number" step="0.0001" class="inp-corp-rate w-full p-2 border border-gray-300 text-xs text-center text-black font-mono focus:border-[#86BC25] outline-none" value="0.34">
                        </div>
                        <div>
                            <label class="block text-[10px] text-gray-500 mb-1">Limite Setorial</label>
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

    <script>
        const TAX_RULES = { MIN_THRESHOLD: 600000, MAX_THRESHOLD: 1200000, MAX_RATE: 0.10, DIVIDEND_RETENTION_MONTHLY_LIMIT: 50000 };
        const INCOME_CONFIG = {
            'salary': { include: true, isDividend: false },
            'dividend': { include: true, isDividend: true },
            'capital_gain': { include: true, isDividend: false },
            'savings': { include: false, isDividend: false }
        };

        const app = {
            data: [],
            chart: null,

            init() {
                this.updateDate();
                lucide.createIcons();
                this.initChart();
                this.renderList();
            },

            updateDate() {
                const date = new Date().toLocaleDateString('pt-BR');
                const el = document.getElementById('print-date');
                if(el) el.textContent = date;
            },

            updateTaxpayerInfo() {
                const name = document.getElementById('input-taxpayer-name').value;
                document.getElementById('print-taxpayer-name').textContent = name || 'N/A';
            },

            addIncome() {
                const id = Date.now();
                this.data.push({ id, desc: '', cnpj: '', type: 'salary', val: 0, tax: 0, frequency: 'annual', corpRate: 0.34, corpLimit: 0.34, showRedutor: false });
                this.renderList();
            },

            removeIncome(id) {
                this.data = this.data.filter(item => item.id !== id);
                this.renderList();
            },

            updateItem(id, field, value) {
                const idx = this.data.findIndex(i => i.id === id);
                if (idx === -1) return;
                
                if (['val', 'tax', 'corpRate', 'corpLimit'].includes(field)) {
                    value = parseFloat(value) || 0;
                    if(value < 0) value = 0;
                }
                
                this.data[idx][field] = value;
                if (field === 'type') this.data[idx].showRedutor = INCOME_CONFIG[value].isDividend;

                if (field === 'val' || field === 'frequency') {
                    const item = this.data[idx];
                    const el = document.querySelector(`[data-id="${id}"] .monthly-preview`);
                    if(el) {
                        if (item.frequency === 'annual') {
                            el.textContent = `Média: ${(item.val/12).toLocaleString('pt-BR', {style:'currency', currency:'BRL'})}/mês`;
                        } else {
                            el.textContent = `Projeção Anual: ${(item.val*12).toLocaleString('pt-BR', {style:'currency', currency:'BRL'})}`;
                        }
                    }
                }

                this.calculate();
                this.updateVisuals(id);
            },

            updateVisuals(id) {
                const item = this.data.find(i => i.id === id);
                const elItem = document.querySelector(`[data-id="${id}"]`);
                if(!elItem) return;
                
                const areaRed = elItem.querySelector('.area-redutor');
                const alert50k = elItem.querySelector('.alert-50k');
                
                // Redutor visível apenas para dividendos
                if (item.type === 'dividend') areaRed.classList.remove('hidden');
                else areaRed.classList.add('hidden');

                // Alerta 50k
                const annualVal = item.frequency === 'monthly' ? item.val * 12 : item.val;
                if (item.type === 'dividend' && annualVal > (TAX_RULES.DIVIDEND_RETENTION_MONTHLY_LIMIT * 12)) {
                    alert50k.classList.remove('hidden');
                } else {
                    alert50k.classList.add('hidden');
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

                        const bind = (sel, field) => {
                            const el = clone.querySelector(sel);
                            if (!el) return;
                            el.value = item[field];
                            el.addEventListener('input', (e) => this.updateItem(item.id, field, e.target.value));
                        };

                        bind('.inp-desc', 'desc');
                        bind('.inp-cnpj', 'cnpj');
                        bind('.inp-val', 'val');
                        bind('.inp-tax', 'tax');
                        bind('.inp-corp-rate', 'corpRate');
                        
                        const elType = clone.querySelector('.inp-type');
                        if (elType) {
                            elType.value = item.type;
                            elType.addEventListener('change', (e) => this.updateItem(item.id, 'type', e.target.value));
                        }

                        const elFreq = clone.querySelector('.inp-freq');
                        if (elFreq) {
                            elFreq.value = item.frequency;
                            elFreq.addEventListener('change', (e) => this.updateItem(item.id, 'frequency', e.target.value));
                        }

                        const elLimit = clone.querySelector('.inp-corp-limit');
                        if (elLimit) {
                            elLimit.value = item.corpLimit;
                            elLimit.addEventListener('change', (e) => this.updateItem(item.id, 'corpLimit', e.target.value));
                        }

                        const btnRemove = clone.querySelector('.btn-remove');
                        if (btnRemove) btnRemove.onclick = () => this.removeIncome(item.id);

                        // --- Lógica da Calculadora Auxiliar ---
                        const btnHelper = clone.querySelector('.btn-calc-helper');
                        const calcHelper = clone.querySelector('.calc-helper');
                        const btnApply = clone.querySelector('.btn-apply-rate');
                        
                        if(btnHelper) {
                            btnHelper.onclick = () => calcHelper.classList.toggle('hidden');
                        }
                        
                        if(btnApply) {
                            btnApply.onclick = () => {
                                const profit = parseFloat(clone.querySelector('.hlp-profit').value) || 0;
                                const irpj = parseFloat(clone.querySelector('.hlp-irpj').value) || 0;
                                const csll = parseFloat(clone.querySelector('.hlp-csll').value) || 0;
                                if(profit > 0) {
                                    const effective = (irpj + csll) / profit;
                                    // Atualiza input principal e modelo de dados
                                    const inputRate = root.querySelector('.inp-corp-rate');
                                    inputRate.value = effective.toFixed(4);
                                    this.updateItem(item.id, 'corpRate', effective);
                                    calcHelper.classList.add('hidden'); // Fecha helper
                                } else {
                                    alert("Lucro deve ser maior que zero.");
                                }
                            };
                        }

                        // Inicializa texto de prévia
                        const elPrev = clone.querySelector('.monthly-preview');
                        if(elPrev) {
                            if (item.frequency === 'annual') {
                                elPrev.textContent = `Média: ${(item.val/12).toLocaleString('pt-BR', {style:'currency', currency:'BRL'})}/mês`;
                            } else {
                                elPrev.textContent = `Projeção Anual: ${(item.val*12).toLocaleString('pt-BR', {style:'currency', currency:'BRL'})}`;
                            }
                        }

                        container.appendChild(clone);
                        setTimeout(() => this.updateVisuals(item.id), 0);
                    });
                }
                
                lucide.createIcons();
                this.calculate();
            },

            calculate() {
                let totalIncome = 0;
                let minBase = 0;
                let paidTax = 0;

                this.data.forEach(item => {
                    const config = INCOME_CONFIG[item.type];
                    const multiplier = item.frequency === 'monthly' ? 12 : 1;
                    const annualVal = item.val * multiplier;
                    const annualTax = item.tax * multiplier;

                    totalIncome += annualVal;
                    paidTax += annualTax;
                    
                    if (config.include) minBase += annualVal;
                });

                let rate = 0;
                if (minBase >= TAX_RULES.MAX_THRESHOLD) rate = TAX_RULES.MAX_RATE;
                else if (minBase > TAX_RULES.MIN_THRESHOLD) {
                    rate = ((minBase / 60000) - 10) / 100;
                }

                const grossTax = minBase * rate;
                
                let totalReducer = 0;
                this.data.forEach(item => {
                    if (INCOME_CONFIG[item.type].isDividend && rate > 0) {
                        const multiplier = item.frequency === 'monthly' ? 12 : 1;
                        const annualVal = item.val * multiplier;
                        
                        const load = item.corpRate + rate;
                        if (load > item.corpLimit) totalReducer += annualVal * (load - item.corpLimit);
                    }
                });

                const taxDue = Math.max(0, grossTax - totalReducer);
                const balance = taxDue - paidTax;

                const fmt = (v) => v.toLocaleString('pt-BR', {style:'currency', currency:'BRL'});
                
                document.getElementById('res-total-year').textContent = fmt(totalIncome);
                document.getElementById('res-total-month').textContent = fmt(totalIncome/12);
                
                document.getElementById('res-base-year').textContent = fmt(minBase);
                document.getElementById('res-base-month').textContent = fmt(minBase/12);
                
                document.getElementById('res-rate').textContent = (rate * 100).toFixed(2) + '%';
                
                document.getElementById('res-due-year').textContent = fmt(taxDue);
                document.getElementById('res-due-month').textContent = fmt(taxDue/12);
                
                document.getElementById('res-paid-year').textContent = '-' + fmt(paidTax);
                document.getElementById('res-paid-month').textContent = '-' + fmt(paidTax/12);

                const box = document.getElementById('status-box');
                const lbl = document.getElementById('status-label');
                const val = document.getElementById('status-value');
                const dsc = document.getElementById('status-desc');

                if (balance > 0.01) {
                    box.className = "mt-6 p-6 text-center bg-white border-2 border-black";
                    lbl.textContent = "Complemento a Pagar";
                    lbl.className = "text-xs font-bold uppercase tracking-widest mb-2 block text-black";
                    val.textContent = fmt(balance);
                    val.className = "text-3xl font-extrabold block text-black tracking-tight";
                    dsc.textContent = "Imposto devido é superior ao retido.";
                } else if (balance < -0.01) {
                    box.className = "mt-6 p-6 text-center bg-[#86BC25] border-2 border-[#86BC25]";
                    lbl.textContent = "Imposto Pago a Maior";
                    lbl.className = "text-xs font-bold uppercase tracking-widest mb-2 block text-white/90";
                    val.textContent = fmt(Math.abs(balance));
                    val.className = "text-3xl font-extrabold block text-white tracking-tight";
                    dsc.textContent = "Valor excedente passível de restituição.";
                    dsc.className = "text-xs mt-3 text-white/90";
                } else {
                    box.className = "mt-6 p-6 text-center bg-gray-50 border border-gray-200";
                    lbl.textContent = "Situação Regular";
                    lbl.className = "text-xs font-bold uppercase tracking-widest mb-2 block text-gray-400";
                    val.textContent = "R$ 0,00";
                    val.className = "text-3xl font-extrabold block text-gray-300";
                    dsc.textContent = "Imposto pago é exatamente igual ao devido.";
                }

                this.updateChart(paidTax, Math.max(0, balance), Math.abs(Math.min(0, balance)));
            },

            initChart() {
                const ctx = document.getElementById('taxChart').getContext('2d');
                Chart.defaults.font.family = "'Open Sans', sans-serif";
                this.chart = new Chart(ctx, {
                    type: 'doughnut',
                    data: {
                        labels: ['Pago/Retido', 'A Pagar', 'Excedente'],
                        datasets: [{
                            data: [0, 0, 0],
                            backgroundColor: ['#D0D0CE', '#000000', '#86BC25'],
                            borderWidth: 0,
                            hoverOffset: 4
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: { legend: { position: 'right', labels: { usePointStyle: true, boxWidth: 8 } } },
                        cutout: '75%'
                    }
                });
            },

            updateChart(paid, due, surplus) {
                if(this.chart) {
                    this.chart.data.datasets[0].data = [paid, due, surplus];
                    this.chart.update();
                }
            },

            toggleDocs() {
                const m = document.getElementById('modal-docs');
                m.classList.toggle('hidden');
            }
        };

        window.onload = () => app.init();
    </script>
</body>
</html>
