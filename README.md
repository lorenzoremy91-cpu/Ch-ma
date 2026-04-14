<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulateur d'Impact - Subventions Vertes</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
            background: #f8fafc;
            color: #1e293b;
            margin: 0;
            padding: 0;
        }

        .slider-thumb::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 28px;
            height: 28px;
            background: #16a34a;
            cursor: pointer;
            border-radius: 50%;
            border: 4px solid white;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }

        .card {
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .metric-bar {
            transition: width 0.8s cubic-bezier(0.34, 1.56, 0.64, 1);
        }
    </style>
</head>
<body class="p-2 md:p-6 min-h-screen flex items-center justify-center">

    <div class="w-full max-w-4xl bg-white rounded-[1.5rem] md:rounded-[2.5rem] shadow-2xl overflow-hidden border border-slate-100">
        <!-- Header Simplifié pour Canva -->
        <div class="bg-green-600 p-6 text-white text-center">
            <h1 class="text-2xl md:text-3xl font-extrabold mb-1">Simulateur de Politique Verte</h1>
            <p class="text-green-100 text-sm opacity-90">Effet de levier des subventions sur l'économie</p>
        </div>

        <!-- Controller Section -->
        <div class="p-6 border-b border-slate-100 bg-slate-50/50">
            <div class="flex flex-col items-center">
                <label for="subsidy-slider" class="text-[10px] font-bold text-slate-400 uppercase tracking-[0.2em] mb-4">Niveau d'investissement public</label>
                <div class="flex items-center w-full gap-4 max-w-xl">
                    <span class="text-slate-400 text-xs font-bold">0%</span>
                    <input type="range" id="subsidy-slider" min="0" max="100" value="20" 
                           class="slider-thumb w-full h-2 bg-slate-200 rounded-lg appearance-none cursor-pointer accent-green-600">
                    <span class="text-green-600 text-xs font-bold">100%</span>
                </div>
                <div id="subsidy-label" class="mt-4 text-5xl font-black text-green-600 tracking-tighter">20%</div>
            </div>
        </div>

        <!-- Results Grid -->
        <div class="p-6 grid grid-cols-1 sm:grid-cols-2 gap-4">
            
            <!-- R&D Card -->
            <div class="card p-5 rounded-2xl bg-white border border-slate-100 shadow-sm hover:shadow-md">
                <div class="flex justify-between items-center mb-3">
                    <div class="p-2 bg-blue-50 rounded-lg text-blue-600 text-xl">🔬</div>
                    <div id="rd-status" class="text-[10px] font-bold px-2 py-1 rounded bg-slate-100 text-slate-500 uppercase">Faible</div>
                </div>
                <h3 class="font-bold text-slate-800 text-sm mb-1">Recherche & Innovation</h3>
                <p class="text-xs text-slate-500 mb-4 h-8" id="rd-desc">Investissement minimal en nouvelles technologies.</p>
                <div class="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                    <div id="rd-bar" class="metric-bar h-full bg-blue-500" style="width: 20%"></div>
                </div>
            </div>

            <!-- Costs Card -->
            <div class="card p-5 rounded-2xl bg-white border border-slate-100 shadow-sm hover:shadow-md">
                <div class="flex justify-between items-center mb-3">
                    <div class="p-2 bg-amber-50 rounded-lg text-amber-600 text-xl">🏭</div>
                    <div id="costs-status" class="text-[10px] font-bold px-2 py-1 rounded bg-slate-100 text-slate-500 uppercase">Élevé</div>
                </div>
                <h3 class="font-bold text-slate-800 text-sm mb-1">Coût de Production</h3>
                <p class="text-xs text-slate-500 mb-4 h-8" id="costs-desc">Production artisanale à coût unitaire élevé.</p>
                <div class="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                    <div id="costs-bar" class="metric-bar h-full bg-amber-500" style="width: 80%"></div>
                </div>
            </div>

            <!-- Price Card -->
            <div class="card p-5 rounded-2xl bg-white border border-slate-100 shadow-sm hover:shadow-md">
                <div class="flex justify-between items-center mb-3">
                    <div class="p-2 bg-emerald-50 rounded-lg text-emerald-600 text-xl">🏷️</div>
                    <div id="price-status" class="text-[10px] font-bold px-2 py-1 rounded bg-slate-100 text-slate-500 uppercase">Cher</div>
                </div>
                <h3 class="font-bold text-slate-800 text-sm mb-1">Prix Consommateur</h3>
                <p class="text-xs text-slate-500 mb-4 h-8" id="price-desc">Produit de niche réservé aux hauts revenus.</p>
                <div class="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                    <div id="price-bar" class="metric-bar h-full bg-emerald-500" style="width: 90%"></div>
                </div>
            </div>

            <!-- Adoption Card -->
            <div class="card p-5 rounded-2xl bg-white border border-slate-100 shadow-sm hover:shadow-md">
                <div class="flex justify-between items-center mb-3">
                    <div class="p-2 bg-green-50 rounded-lg text-green-600 text-xl">🌍</div>
                    <div id="adoption-status" class="text-[10px] font-bold px-2 py-1 rounded bg-slate-100 text-slate-500 uppercase">Limitée</div>
                </div>
                <h3 class="font-bold text-slate-800 text-sm mb-1">Impact Climat</h3>
                <p class="text-xs text-slate-500 mb-4 h-8" id="adoption-desc">Impact négligeable sur les émissions.</p>
                <div class="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                    <div id="adoption-bar" class="metric-bar h-full bg-green-500" style="width: 5%"></div>
                </div>
            </div>

        </div>

        <!-- Synthesis Box -->
        <div id="synthesis" class="mx-6 mb-6 p-4 rounded-xl bg-green-50 border border-green-100 text-green-800 italic text-center text-xs">
            "Bougez le curseur pour voir l'impact."
        </div>
    </div>

    <script>
        const slider = document.getElementById('subsidy-slider');
        const labels = {
            subsidy: document.getElementById('subsidy-label'),
            rdStatus: document.getElementById('rd-status'),
            rdDesc: document.getElementById('rd-desc'),
            costsStatus: document.getElementById('costs-status'),
            costsDesc: document.getElementById('costs-desc'),
            priceStatus: document.getElementById('price-status'),
            priceDesc: document.getElementById('price-desc'),
            adoptionStatus: document.getElementById('adoption-status'),
            adoptionDesc: document.getElementById('adoption-desc'),
            synthesis: document.getElementById('synthesis')
        };

        const bars = {
            rd: document.getElementById('rd-bar'),
            costs: document.getElementById('costs-bar'),
            price: document.getElementById('price-bar'),
            adoption: document.getElementById('adoption-bar')
        };

        function updateSimulation(val) {
            const v = parseInt(val);
            labels.subsidy.innerText = v + "%";

            // Logic Simulation
            const rdVal = Math.min(100, v * 1.2);
            bars.rd.style.width = rdVal + "%";
            if(v < 30) {
                labels.rdStatus.innerText = "Faible";
                labels.rdDesc.innerText = "Recherche limitée.";
            } else if(v < 70) {
                labels.rdStatus.innerText = "Active";
                labels.rdDesc.innerText = "Nombreux brevets déposés.";
            } else {
                labels.rdStatus.innerText = "Disruptive";
                labels.rdDesc.innerText = "Sauts technologiques majeurs.";
            }

            const costsVal = Math.max(15, 100 - (v * 0.85));
            bars.costs.style.width = costsVal + "%";
            if(v < 30) { labels.costsStatus.innerText = "Élevé"; labels.costsDesc.innerText = "Production manuelle."; }
            else if(v < 70) { labels.costsStatus.innerText = "En baisse"; labels.costsDesc.innerText = "Automatisation en cours."; }
            else { labels.costsStatus.innerText = "Optimisé"; labels.costsDesc.innerText = "Économies d'échelle massives."; }

            const priceVal = Math.max(10, 95 - (v * 0.9));
            bars.price.style.width = priceVal + "%";
            if(v < 40) { labels.priceStatus.innerText = "Cher"; labels.priceDesc.innerText = "Inaccessible pour la majorité."; }
            else if(v < 80) { labels.priceStatus.innerText = "Compétitif"; labels.priceDesc.innerText = "Equivalent au fossile."; }
            else { labels.priceStatus.innerText = "Moins cher"; labels.priceDesc.innerText = "L'option verte domine le marché."; }

            const adoptionVal = v < 20 ? v/2 : Math.min(100, Math.pow(v/10, 2));
            bars.adoption.style.width = adoptionVal + "%";
            if(v < 30) { labels.adoptionStatus.innerText = "Faible"; labels.adoptionDesc.innerText = "Moins de 1% du marché."; }
            else if(v < 75) { labels.adoptionStatus.innerText = "Transition"; labels.adoptionDesc.innerText = "Adoption rapide par les foyers."; }
            else { labels.adoptionStatus.innerText = "Standard"; labels.adoptionDesc.innerText = "Remplacement total du thermique."; }

            // Synthesis
            if(v === 0) labels.synthesis.innerText = "Stagnation : Sans aide, le fossile reste roi.";
            else if(v < 40) labels.synthesis.innerText = "Phase d'amorçage : L'État prend le risque initial.";
            else if(v < 80) labels.synthesis.innerText = "Accélération : Le marché devient autonome.";
            else labels.synthesis.innerText = "Victoire : La technologie est propre et rentable.";
        }

        slider.addEventListener('input', (e) => updateSimulation(e.target.value));
        updateSimulation(20);
    </script>
</body>
</html>
