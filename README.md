# rlnut
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Calculadora Nutricional Completa</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    .tab-content {
      display: none;
    }
    .tab-content.active {
      display: block;
      animation: fadeIn 0.3s ease;
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
    .input-highlight {
      transition: all 0.3s ease;
    }
    .input-highlight:focus {
      border-color: #4f46e5;
      box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.2);
    }
    .result-box {
      transition: all 0.3s ease;
    }
    .result-box:hover {
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(0,0,0,0.1);
    }
  </style>
</head>
<body class="bg-gray-50 min-h-screen">
  <div class="container mx-auto px-4 py-8 max-w-4xl">
    <header class="text-center mb-8">
      <h1 class="text-3xl font-bold text-indigo-700 mb-2">
        <i class="fas fa-calculator mr-2"></i>Calculadora Nutricional Completa
      </h1>
      <p class="text-gray-600">Avaliação nutricional completa com recomendações personalizadas</p>
    </header>

    <div class="bg-white rounded-xl shadow-lg overflow-hidden mb-8">
      <div class="flex border-b border-gray-200 overflow-x-auto">
        <button class="tab-btn py-3 px-4 font-medium text-indigo-600 border-b-2 border-indigo-600 whitespace-nowrap" data-tab="dados">
          <i class="fas fa-user-circle mr-2"></i>Dados Básicos
        </button>
        <button class="tab-btn py-3 px-4 font-medium text-gray-500 hover:text-indigo-600 whitespace-nowrap" data-tab="resultados">
          <i class="fas fa-chart-bar mr-2"></i>Resultados
        </button>
        <button class="tab-btn py-3 px-4 font-medium text-gray-500 hover:text-indigo-600 whitespace-nowrap" data-tab="semiologia">
          <i class="fas fa-stethoscope mr-2"></i>Semiologia
        </button>
        <button class="tab-btn py-3 px-4 font-medium text-gray-500 hover:text-indigo-600 whitespace-nowrap" data-tab="recomendacoes">
          <i class="fas fa-clipboard-list mr-2"></i>Recomendações
        </button>
      </div>

      <!-- Dados Básicos Tab -->
      <div id="dados" class="tab-content active p-6">
        <h2 class="text-xl font-semibold text-gray-800 mb-4">
          <i class="fas fa-user-edit mr-2 text-indigo-600"></i>Informações do Paciente
        </h2>
        
        <div class="grid md:grid-cols-2 gap-6">
          <div class="space-y-4">
            <div>
              <label for="peso" class="block text-gray-700 font-medium mb-1">Peso Atual (kg)</label>
              <input type="number" id="peso" step="0.1" class="w-full px-4 py-2 border rounded-lg input-highlight" placeholder="Ex: 68.5">
            </div>
            
            <div>
              <label for="pesoUsual" class="block text-gray-700 font-medium mb-1">Peso Usual (kg)</label>
              <input type="number" id="pesoUsual" step="0.1" class="w-full px-4 py-2 border rounded-lg input-highlight" placeholder="Ex: 72.0">
            </div>
            
            <div>
              <label for="pesoEdema" class="block text-gray-700 font-medium mb-1">Peso estimado do edema (kg)</label>
              <input type="number" id="pesoEdema" step="0.1" value="0" class="w-full px-4 py-2 border rounded-lg input-highlight">
            </div>
            
            <div>
              <label for="altura" class="block text-gray-700 font-medium mb-1">Altura (cm)</label>
              <input type="number" id="altura" step="0.1" class="w-full px-4 py-2 border rounded-lg input-highlight" placeholder="Ex: 170.0">
            </div>
          </div>
          
          <div class="space-y-4">
            <div>
              <label for="idade" class="block text-gray-700 font-medium mb-1">Idade (anos)</label>
              <input type="number" id="idade" class="w-full px-4 py-2 border rounded-lg input-highlight" placeholder="Ex: 45">
            </div>
            
            <div>
              <label for="sexo" class="block text-gray-700 font-medium mb-1">Sexo</label>
              <select id="sexo" class="w-full px-4 py-2 border rounded-lg input-highlight">
                <option value="masculino">Masculino</option>
                <option value="feminino">Feminino</option>
              </select>
            </div>
            
            <div>
              <label for="etnia" class="block text-gray-700 font-medium mb-1">Etnia</label>
              <select id="etnia" class="w-full px-4 py-2 border rounded-lg input-highlight">
                <option value="branco">Branco</option>
                <option value="negro">Negro</option>
              </select>
            </div>
            
            <div>
              <label for="faseCritico" class="block text-gray-700 font-medium mb-1">Fase do paciente crítico</label>
              <select id="faseCritico" class="w-full px-4 py-2 border rounded-lg input-highlight">
                <option value="estavel">Estável</option>
                <option value="critico1">Crítico - Dias 1 a 3</option>
                <option value="critico2">Crítico - Dias 4 a 7</option>
                <option value="critico3">Crítico - Após 7 dias</option>
              </select>
            </div>
          </div>
        </div>
        
        <h2 class="text-xl font-semibold text-gray-800 mt-8 mb-4">
          <i class="fas fa-ruler-combined mr-2 text-indigo-600"></i>Medidas Antropométricas
        </h2>
        
        <div class="grid md:grid-cols-2 gap-6">
          <div>
            <label for="aj" class="block text-gray-700 font-medium mb-1">Altura do joelho (cm)</label>
            <input type="number" id="aj" step="0.1" class="w-full px-4 py-2 border rounded-lg input-highlight" placeholder="Ex: 52.5">
          </div>
          
          <div>
            <label for="cb" class="block text-gray-700 font-medium mb-1">Circunferência do braço (cm)</label>
            <input type="number" id="cb" step="0.1" class="w-full px-4 py-2 border rounded-lg input-highlight" placeholder="Ex: 28.0">
          </div>
        </div>
        
        <h2 class="text-xl font-semibold text-gray-800 mt-8 mb-4">
          <i class="fas fa-sliders-h mr-2 text-indigo-600"></i>Personalização de Metas
        </h2>
        
        <div class="grid md:grid-cols-3 gap-6">
          <div>
            <label for="caloriaManual" class="block text-gray-700 font-medium mb-1">Meta calórica (kcal/kg)</label>
            <input type="number" id="caloriaManual" step="0.1" class="w-full px-4 py-2 border rounded-lg input-highlight" placeholder="Opcional">
          </div>
          
          <div>
            <label for="proteinaManual" class="block text-gray-700 font-medium mb-1">Meta proteica (g/kg)</label>
            <input type="number" id="proteinaManual" step="0.1" class="w-full px-4 py-2 border rounded-lg input-highlight" placeholder="Opcional">
          </div>
          
          <div>
            <label for="hidratacaoManual" class="block text-gray-700 font-medium mb-1">Hidratação (ml/kg)</label>
            <input type="number" id="hidratacaoManual" step="1" class="w-full px-4 py-2 border rounded-lg input-highlight" placeholder="Ex: 30">
          </div>
        </div>
        
        <button onclick="calcular()" class="w-full mt-8 bg-indigo-600 text-white py-3 px-4 rounded-lg hover:bg-indigo-700 transition duration-300 font-medium">
          <i class="fas fa-calculator mr-2"></i>Calcular Avaliação Nutricional
        </button>
      </div>

      <!-- Resultados Tab -->
      <div id="resultados" class="tab-content p-6">
        <h2 class="text-xl font-semibold text-gray-800 mb-6">
          <i class="fas fa-chart-pie mr-2 text-indigo-600"></i>Resultados da Avaliação
        </h2>
        
        <div id="resultado" class="space-y-4">
          <div class="text-center py-12 text-gray-400">
            <i class="fas fa-calculator text-4xl mb-2"></i>
            <p>Preencha os dados na aba "Dados Básicos" e clique em calcular para ver os resultados</p>
          </div>
        </div>
      </div>

      <!-- Semiologia Tab -->
      <div id="semiologia" class="tab-content p-6">
        <h2 class="text-xl font-semibold text-gray-800 mb-6">
          <i class="fas fa-stethoscope mr-2 text-indigo-600"></i>Semiologia Nutricional
        </h2>
        
        <div class="grid md:grid-cols-2 gap-6">
          <div class="bg-gray-50 p-5 rounded-lg">
            <h3 class="font-semibold text-indigo-700 mb-3">
              <i class="fas fa-user-circle mr-2"></i>Avaliação Física
            </h3>
            <ul class="space-y-3 text-gray-700">
              <li class="flex items-start">
                <i class="fas fa-scissors text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Cabelo:</strong> ressecamento, queda, alopecia – possível deficiência de proteína, zinco, biotina.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-user text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Face:</strong> palidez, edema, descamação – deficiência de ferro, niacina, vitamina B2.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-tooth text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Gengivas:</strong> sangramento, edema – deficiência de vitamina C.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-lips text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Lábios:</strong> rachaduras, queilite angular – deficiência de riboflavina, ferro, niacina.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-smile text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Língua:</strong> avermelhada, lisa, dolorosa – deficiência de B12, ácido fólico, ferro, niacina.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-eye text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Olhos:</strong> cegueira noturna, xeroftalmia – deficiência de vitamina A.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-skin text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Pele:</strong> descamação, dermatite, hiperpigmentação – deficiência de zinco, vitamina A, B3.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-hand-paper text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Unhas:</strong> quebradiças, côncavas (coiloniquia) – deficiência de ferro, proteínas.</span>
              </li>
            </ul>
          </div>
          
          <div class="bg-gray-50 p-5 rounded-lg">
            <h3 class="font-semibold text-indigo-700 mb-3">
              <i class="fas fa-clipboard-check mr-2"></i>Exame Físico Nutricional
            </h3>
            <ul class="space-y-3 text-gray-700">
              <li class="flex items-start">
                <i class="fas fa-stethoscope text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Abdome:</strong> distendido, com ascite – pode indicar desnutrição proteico-calórica.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-mouth text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Boca:</strong> alterações em mucosas e dentes – possíveis deficiências de vitamina C, B-complexo.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-circle text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Bola de gordura de Bichat:</strong> afundamento indica depleção de gordura subcutânea.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-bolt text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Face aguda:</strong> expressão alerta, típica de desnutrição aguda.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-hourglass-half text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Face crônica:</strong> expressão abatida, típica de desnutrição crônica.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-user-injured text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Fúrcula esternal/pescoço:</strong> proeminente = perda de musculatura peitoral.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-walking text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Membros inferiores:</strong> redução de massa muscular = atrofia, deficiência proteica.</span>
              </li>
              <li class="flex items-start">
                <i class="fas fa-dumbbell text-indigo-500 mt-1 mr-2"></i>
                <span><strong>Membros superiores:</strong> afundamento da têmpora = atrofia muscular, deficiência energética/proteica.</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Recomendações Tab -->
      <div id="recomendacoes" class="tab-content p-6">
        <h2 class="text-xl font-semibold text-gray-800 mb-6">
          <i class="fas fa-clipboard-list mr-2 text-indigo-600"></i>Recomendações Nutricionais
        </h2>
        
        <div class="grid md:grid-cols-2 gap-6">
          <div class="bg-indigo-50 p-5 rounded-lg">
            <h3 class="font-semibold text-indigo-700 mb-3">
              <i class="fas fa-fire-alt mr-2"></i>Recomendações Calóricas
            </h3>
            <ul class="space-y-3 text-gray-700">
              <li>
                <strong>Paciente estável com desnutrição ou risco nutricional:</strong>
                <p class="text-sm text-gray-600 mt-1">30 a 35 kcal/kg/dia</p>
              </li>
              <li>
                <strong>Paciente crítico:</strong>
                <ul class="text-sm text-gray-600 mt-1 ml-4 space-y-1">
                  <li>1º ao 3º dia: 15 a 20 kcal/kg/dia</li>
                  <li>4º ao 7º dia: 25 a 30 kcal/kg/dia</li>
                  <li>Após 7 dias: 30 kcal/kg/dia</li>
                </ul>
              </li>
              <li>
                <strong>Paciente obeso:</strong>
                <ul class="text-sm text-gray-600 mt-1 ml-4 space-y-1">
                  <li>IMC 30–50 kg/m²: 11 a 14 kcal/kg/dia (peso atual)</li>
                  <li>IMC > 50 kg/m²: 22 a 25 kcal/kg/dia (peso ideal ou ajustado)</li>
                </ul>
              </li>
            </ul>
          </div>
          
          <div class="bg-indigo-50 p-5 rounded-lg">
            <h3 class="font-semibold text-indigo-700 mb-3">
              <i class="fas fa-drumstick-bite mr-2"></i>Recomendações Proteicas
            </h3>
            <ul class="space-y-3 text-gray-700">
              <li>
                <strong>Paciente crítico:</strong>
                <p class="text-sm text-gray-600 mt-1">1,2 a 2,0 g/kg/dia</p>
              </li>
              <li>
                <strong>Paciente com sepse, trauma ou queimadura:</strong>
                <p class="text-sm text-gray-600 mt-1">Até 2,5 g/kg/dia, conforme tolerância</p>
              </li>
              <li>
                <strong>Paciente obeso crítico:</strong>
                <ul class="text-sm text-gray-600 mt-1 ml-4 space-y-1">
                  <li>IMC 30–40 kg/m²: 2,0 g/kg de peso ideal</li>
                  <li>IMC > 40 kg/m²: até 2,5 g/kg de peso ideal</li>
                </ul>
              </li>
            </ul>
          </div>
        </div>
        
        <div class="mt-6 bg-gray-50 p-4 rounded-lg">
          <p class="text-sm text-gray-600">
            <i class="fas fa-info-circle text-indigo-500 mr-1"></i>
            <strong>Fontes:</strong> BRASPEN 2024, ESPEN 2024, ASPEN Guidelines 2024
          </p>
        </div>
      </div>
    </div>
    
    <footer class="mt-8 text-center text-gray-600 text-sm">
      <p>© 2024 Calculadora Nutricional Completa - Todos os direitos reservados</p>
    </footer>
  </div>

  <script>
    // Tab functionality
    const tabButtons = document.querySelectorAll('.tab-btn');
    const tabContents = document.querySelectorAll('.tab-content');

    tabButtons.forEach(button => {
      button.addEventListener('click', () => {
        const tabId = button.getAttribute('data-tab');
        
        // Remove active class from all buttons and contents
        tabButtons.forEach(btn => {
          btn.classList.remove('border-indigo-600', 'text-indigo-600');
          btn.classList.add('text-gray-500');
        });
        
        tabContents.forEach(content => {
          content.classList.remove('active');
        });
        
        // Add active class to clicked button and corresponding content
        button.classList.add('border-indigo-600', 'text-indigo-600');
        button.classList.remove('text-gray-500');
        document.getElementById(tabId).classList.add('active');
      });
    });

    function calcular() {
      const peso = parseFloat(document.getElementById('peso').value);
      const pesoUsual = parseFloat(document.getElementById('pesoUsual').value);
      const pesoEdema = parseFloat(document.getElementById('pesoEdema').value);
      const altura_cm = parseFloat(document.getElementById('altura').value);
      const altura_m = altura_cm / 100;
      const idade = parseInt(document.getElementById('idade').value);
      const sexo = document.getElementById('sexo').value;
      const etnia = document.getElementById('etnia').value;
      const aj = parseFloat(document.getElementById('aj').value);
      const cb = parseFloat(document.getElementById('cb').value);

      const imc = peso / (altura_m ** 2);

      // Peso estimado
      let pesoEstimado, alturaEstimada;
      if (sexo === 'masculino' && etnia === 'branco') {
        pesoEstimado = (1.19 * aj) + (3.21 * cb) - 86.82;
        alturaEstimada = 71.85 + (1.88 * aj);
      } else if (sexo === 'masculino') {
        pesoEstimado = (1.09 * aj) + (3.14 * cb) - 83.72;
        alturaEstimada = 73.42 + (1.79 * aj);
      } else if (sexo === 'feminino' && etnia === 'branco') {
        pesoEstimado = (1.01 * aj) + (2.81 * cb) - 60.04;
        alturaEstimada = 70.25 + (1.87 * aj) - (0.06 * idade);
      } else {
        pesoEstimado = (1.24 * aj) + (2.97 * cb) - 82.48;
        alturaEstimada = 68.10 + (1.87 * aj) - (0.06 * idade);
      }

      // Classificação IMC
      let classificacaoIMC = '';
      let imcClass = '';
      if (imc < 16) {
        classificacaoIMC = 'Magreza grau III';
        imcClass = 'text-red-600 font-semibold';
      } else if (imc < 17) {
        classificacaoIMC = 'Magreza grau II';
        imcClass = 'text-red-500 font-semibold';
      } else if (imc < 18.5) {
        classificacaoIMC = 'Magreza grau I';
        imcClass = 'text-orange-500 font-semibold';
      } else if (imc < 25) {
        classificacaoIMC = 'Eutrofia';
        imcClass = 'text-green-600 font-semibold';
      } else if (imc < 30) {
        classificacaoIMC = 'Sobrepeso';
        imcClass = 'text-yellow-600 font-semibold';
      } else if (imc < 35) {
        classificacaoIMC = 'Obesidade grau I';
        imcClass = 'text-red-500 font-semibold';
      } else if (imc < 40) {
        classificacaoIMC = 'Obesidade grau II';
        imcClass = 'text-red-600 font-semibold';
      } else {
        classificacaoIMC = 'Obesidade grau III';
        imcClass = 'text-red-700 font-semibold';
      }

      // Peso ideal baseado no IMC médio
      let imcRef;
      if (idade >= 60) {
        imcRef = 24.5; // Idosos
      } else if (sexo === 'masculino') {
        imcRef = 22.0; // Homens adultos
      } else {
        imcRef = 20.8; // Mulheres adultas
      }
      
      let pesoIdeal = (altura_m ** 2) * imcRef;

      // Peso corrigido
      let pesoCorrigido = peso - pesoEdema;

      // Peso ajustado
      let pesoAjustado;
      if (imc > 30) {
        pesoAjustado = (peso - pesoIdeal) * 0.25 + pesoIdeal;
      } else if (imc < 18) {
        pesoAjustado = (pesoIdeal - peso) * 0.25 + peso;
      } else {
        pesoAjustado = peso;
      }

      // Percentual de perda de peso
      let percentualPerda = ((pesoUsual - peso) / pesoUsual) * 100;
      let perdaClass = '';
      if (percentualPerda > 10) {
        perdaClass = 'text-red-600 font-semibold';
      } else if (percentualPerda > 5) {
        perdaClass = 'text-orange-500 font-semibold';
      } else {
        perdaClass = 'text-green-600 font-semibold';
      }

      // Adequação do peso
      let adequacaoPeso = (peso / pesoIdeal) * 100;
      let adequacaoClass = '';
      if (adequacaoPeso < 70) {
        adequacaoClass = 'text-red-600 font-semibold';
      } else if (adequacaoPeso < 80) {
        adequacaoClass = 'text-orange-500 font-semibold';
      } else if (adequacaoPeso < 90) {
        adequacaoClass = 'text-yellow-600 font-semibold';
      } else {
        adequacaoClass = 'text-green-600 font-semibold';
      }

      let calorias;
      const fase = document.getElementById('faseCritico').value;
      if (imc >= 30 && imc <= 50) {
        calorias = peso * 12.5;
      } else if (imc > 50) {
        calorias = pesoIdeal * 23.5;
      } else {
        if (fase === 'critico1') calorias = peso * 17.5;
        else if (fase === 'critico2') calorias = peso * 27.5;
        else calorias = peso * 32.5;
      }
      
      const caloriaManual = parseFloat(document.getElementById('caloriaManual').value);
      const proteinaManual = parseFloat(document.getElementById('proteinaManual').value);
      const hidratacaoManual = parseFloat(document.getElementById('hidratacaoManual').value);

      if (!isNaN(caloriaManual)) {
        calorias = imc > 50 ? pesoIdeal * caloriaManual : peso * caloriaManual;
      }
      
      const proteinas = !isNaN(proteinaManual)
        ? (imc >= 30 ? pesoIdeal * proteinaManual : peso * proteinaManual)
        : (imc >= 30 ? pesoIdeal * 2.0 : peso * 1.5);

      const hidratacao = !isNaN(hidratacaoManual) ? peso * hidratacaoManual : null;

      let calTxt = `<strong>Calorias estimadas:</strong> ${calorias.toFixed(2)} kcal/dia`;
      let protTxt = `<strong>Proteínas estimadas:</strong> ${proteinas.toFixed(2)} g/dia`;
      let hidrTxt = hidratacao ? `<strong>Hidratação estimada:</strong> ${hidratacao.toFixed(0)} ml/dia` : '';

      if (!isNaN(caloriaManual)) calTxt = `<span class="bg-yellow-100 px-2 py-1 rounded">${calTxt} (personalizado)</span>`;
      if (!isNaN(proteinaManual)) protTxt = `<span class="bg-yellow-100 px-2 py-1 rounded">${protTxt} (personalizado)</span>`;
      if (!isNaN(hidratacaoManual)) hidrTxt = `<span class="bg-yellow-100 px-2 py-1 rounded">${hidrTxt} (personalizado)</span>`;

      // Format results with icons and better styling
      const resultadoHTML = `
        <div class="grid md:grid-cols-2 gap-4">
          <div class="result-box bg-white p-4 rounded-lg border border-gray-200">
            <h3 class="font-semibold text-indigo-700 mb-3 border-b pb-2">
              <i class="fas fa-weight mr-2"></i>Dados Antropométricos
            </h3>
            <ul class="space-y-2">
              <li class="flex justify-between">
                <span><i class="fas fa-weight-scale mr-2 text-gray-500"></i>IMC:</span>
                <span class="${imcClass}">${imc.toFixed(2)} (${classificacaoIMC})</span>
              </li>
              <li class="flex justify-between">
                <span><i class="fas fa-ruler-vertical mr-2 text-gray-500"></i>Peso Estimado:</span>
                <span>${pesoEstimado.toFixed(2)} kg</span>
              </li>
              <li class="flex justify-between">
                <span><i class="fas fa-ruler mr-2 text-gray-500"></i>Altura Estimada:</span>
                <span>${alturaEstimada.toFixed(2)} cm</span>
              </li>
              <li class="flex justify-between">
                <span><i class="fas fa-bullseye mr-2 text-gray-500"></i>Peso Ideal (IMC ${imcRef}):</span>
                <span>${pesoIdeal.toFixed(2)} kg</span>
              </li>
            </ul>
          </div>
          
          <div class="result-box bg-white p-4 rounded-lg border border-gray-200">
            <h3 class="font-semibold text-indigo-700 mb-3 border-b pb-2">
              <i class="fas fa-chart-line mr-2"></i>Avaliação Nutricional
            </h3>
            <ul class="space-y-2">
              <li class="flex justify-between">
                <span><i class="fas fa-adjust mr-2 text-gray-500"></i>Peso Corrigido:</span>
                <span>${pesoCorrigido.toFixed(2)} kg</span>
              </li>
              <li class="flex justify-between">
                <span><i class="fas fa-balance-scale mr-2 text-gray-500"></i>Peso Ajustado:</span>
                <span>${pesoAjustado.toFixed(2)} kg</span>
              </li>
              <li class="flex justify-between">
                <span><i class="fas fa-percentage mr-2 text-gray-500"></i>Perda de Peso:</span>
                <span class="${perdaClass}">${percentualPerda.toFixed(2)}%</span>
              </li>
              <li class="flex justify-between">
                <span><i class="fas fa-check-circle mr-2 text-gray-500"></i>Adequação do Peso:</span>
                <span class="${adequacaoClass}">${adequacaoPeso.toFixed(2)}%</span>
              </li>
            </ul>
          </div>
          
          <div class="result-box bg-white p-4 rounded-lg border border-gray-200 md:col-span-2">
            <h3 class="font-semibold text-indigo-700 mb-3 border-b pb-2">
              <i class="fas fa-utensils mr-2"></i>Recomendações Nutricionais
            </h3>
            <div class="grid md:grid-cols-3 gap-4">
              <div class="bg-indigo-50 p-3 rounded">
                ${calTxt}
              </div>
              <div class="bg-indigo-50 p-3 rounded">
                ${protTxt}
              </div>
              ${hidrTxt ? `<div class="bg-indigo-50 p-3 rounded">${hidrTxt}</div>` : ''}
            </div>
          </div>
        </div>
      `;

      document.getElementById('resultado').innerHTML = resultadoHTML;
      
      // Switch to results tab after calculation
      document.querySelector('[data-tab="resultados"]').click();
    }
  </script>
</body>
</html>
