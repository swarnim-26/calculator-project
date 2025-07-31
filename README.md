# calculator-project
calculator
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Calculator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(135deg, #6366f1, #8b5cf6);
            min-height: 100vh;
        }
        .calculator-btn {
            transition: all 0.2s;
        }
        .calculator-btn:hover {
            transform: translateY(-2px);
        }
        .calculator-btn:active {
            transform: translateY(1px);
        }
        .tab-active {
            border-bottom: 3px solid #6366f1;
            color: #6366f1;
            font-weight: 600;
        }
        .converter-icon {
            font-size: 1.5rem;
            margin-bottom: 0.5rem;
        }
        .converter-card {
            transition: all 0.2s;
        }
        .converter-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }
        /* Custom scrollbar for converter grid */
        .converters-grid::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .converters-grid::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }
        .converters-grid::-webkit-scrollbar-thumb {
            background: #c7d2fe;
            border-radius: 10px;
        }
        .converters-grid::-webkit-scrollbar-thumb:hover {
            background: #a5b4fc;
        }
    </style>
</head>
<body class="p-4 flex items-center justify-center">
    <div class="bg-white rounded-2xl shadow-2xl w-full max-w-md overflow-hidden">
        <!-- Calculator Header -->
        <div class="bg-gradient-to-r from-indigo-500 to-purple-600 p-4 text-white">
            <h1 class="text-xl font-bold text-center">Advanced Calculator</h1>
        </div>
        
        <!-- Tab Navigation -->
        <div class="flex border-b">
            <button id="tab-standard" class="tab-active flex-1 py-3 px-4 text-center transition-all">
                <i class="fas fa-calculator mr-1"></i> Standard
            </button>
            <button id="tab-scientific" class="flex-1 py-3 px-4 text-center text-gray-600 transition-all">
                <i class="fas fa-square-root-alt mr-1"></i> Scientific
            </button>
            <button id="tab-converter" class="flex-1 py-3 px-4 text-center text-gray-600 transition-all">
                <i class="fas fa-exchange-alt mr-1"></i> Converter
            </button>
        </div>
        
        <!-- Calculator Display -->
        <div class="p-4 bg-gray-50">
            <div class="bg-white border rounded-lg p-3 mb-2">
                <div id="history" class="text-right text-gray-500 text-sm h-5"></div>
                <div id="display" class="text-right text-2xl font-semibold h-8 overflow-x-auto">0</div>
            </div>
        </div>
        
        <!-- Standard Calculator -->
        <div id="standard-calculator" class="p-4 grid grid-cols-4 gap-2">
            <button class="calculator-btn bg-gray-200 rounded-lg p-3 font-medium" onclick="clearDisplay()">C</button>
            <button class="calculator-btn bg-gray-200 rounded-lg p-3 font-medium" onclick="backspace()">⌫</button>
            <button class="calculator-btn bg-gray-200 rounded-lg p-3 font-medium" onclick="appendToDisplay('%')">%</button>
            <button class="calculator-btn bg-indigo-500 text-white rounded-lg p-3 font-medium" onclick="appendToDisplay('/')">/</button>
            
            <button class="calculator-btn bg-gray-100 rounded-lg p-3 font-medium" onclick="appendToDisplay('7')">7</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-3 font-medium" onclick="appendToDisplay('8')">8</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-3 font-medium" onclick="appendToDisplay('9')">9</button>
            <button class="calculator-btn bg-indigo-500 text-white rounded-lg p-3 font-medium" onclick="appendToDisplay('*')">×</button>
            
            <button class="calculator-btn bg-gray-100 rounded-lg p-3 font-medium" onclick="appendToDisplay('4')">4</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-3 font-medium" onclick="appendToDisplay('5')">5</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-3 font-medium" onclick="appendToDisplay('6')">6</button>
            <button class="calculator-btn bg-indigo-500 text-white rounded-lg p-3 font-medium" onclick="appendToDisplay('-')">-</button>
            
            <button class="calculator-btn bg-gray-100 rounded-lg p-3 font-medium" onclick="appendToDisplay('1')">1</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-3 font-medium" onclick="appendToDisplay('2')">2</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-3 font-medium" onclick="appendToDisplay('3')">3</button>
            <button class="calculator-btn bg-indigo-500 text-white rounded-lg p-3 font-medium" onclick="appendToDisplay('+')">+</button>
            
            <button class="calculator-btn bg-gray-100 rounded-lg p-3 font-medium" onclick="appendToDisplay('0')">0</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-3 font-medium" onclick="appendToDisplay('.')">.</button>
            <button class="calculator-btn bg-indigo-500 text-white rounded-lg p-3 font-medium col-span-2" onclick="calculate()">=</button>
        </div>
        
        <!-- Scientific Calculator -->
        <div id="scientific-calculator" class="p-4 grid grid-cols-5 gap-2 hidden">
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="clearDisplay()">C</button>
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="backspace()">⌫</button>
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="calculateSquareRoot()">√</button>
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="calculatePower()">x^y</button>
            <button class="calculator-btn bg-indigo-500 text-white rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('/')">/</button>
            
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="calculateSin()">sin</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('7')">7</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('8')">8</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('9')">9</button>
            <button class="calculator-btn bg-indigo-500 text-white rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('*')">×</button>
            
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="calculateCos()">cos</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('4')">4</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('5')">5</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('6')">6</button>
            <button class="calculator-btn bg-indigo-500 text-white rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('-')">-</button>
            
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="calculateTan()">tan</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('1')">1</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('2')">2</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('3')">3</button>
            <button class="calculator-btn bg-indigo-500 text-white rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('+')">+</button>
            
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="calculateLog()">log</button>
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('(')">(</button>
            <button class="calculator-btn bg-gray-100 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay('0')">0</button>
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="appendToDisplay(')')">)</button>
            <button class="calculator-btn bg-indigo-500 text-white rounded-lg p-2 text-sm font-medium" onclick="calculate()">=</button>
            
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="calculateFactorial()">n!</button>
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="calculatePi()">π</button>
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="calculateE()">e</button>
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="calculateLn()">ln</button>
            <button class="calculator-btn bg-gray-200 rounded-lg p-2 text-sm font-medium" onclick="calculateMod()">mod</button>
        </div>
        
        <!-- Converter Selection -->
        <div id="converter" class="p-4 hidden">
            <h3 class="text-lg font-medium mb-3 text-gray-700">Select Converter</h3>
            
            <div class="converters-grid grid grid-cols-3 gap-3 max-h-80 overflow-y-auto pb-2">
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('currency')">
                    <i class="fas fa-money-bill-wave converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">Currency</span>
                </div>
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('temperature')">
                    <i class="fas fa-thermometer-half converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">Temperature</span>
                </div>
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('length')">
                    <i class="fas fa-ruler converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">Length</span>
                </div>
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('weight')">
                    <i class="fas fa-weight-hanging converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">Weight</span>
                </div>
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('volume')">
                    <i class="fas fa-flask converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">Volume</span>
                </div>
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('area')">
                    <i class="fas fa-vector-square converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">Area</span>
                </div>
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('data')">
                    <i class="fas fa-database converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">Data</span>
                </div>
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('time')">
                    <i class="fas fa-clock converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">Time</span>
                </div>
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('speed')">
                    <i class="fas fa-tachometer-alt converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">Speed</span>
                </div>
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('bmi')">
                    <i class="fas fa-user converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">BMI</span>
                </div>
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('gst')">
                    <i class="fas fa-receipt converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">GST</span>
                </div>
                <div class="converter-card bg-indigo-50 rounded-lg p-3 flex flex-col items-center cursor-pointer" onclick="showConverterTool('numeral')">
                    <i class="fas fa-sort-numeric-down converter-icon text-indigo-500"></i>
                    <span class="text-sm text-center">Numeral</span>
                </div>
            </div>
        </div>
        
        <!-- Converter Tool -->
        <div id="converter-tool" class="p-4 hidden">
            <div class="flex items-center mb-4">
                <button id="back-to-converters" class="mr-2 bg-gray-200 p-2 rounded-full">
                    <i class="fas fa-arrow-left text-gray-600"></i>
                </button>
                <h3 id="converter-title" class="text-lg font-medium text-gray-700">Currency Converter</h3>
            </div>
            
            <!-- Standard Converter UI -->
            <div id="standard-converter" class="mb-4">
                <div class="grid grid-cols-2 gap-4 mb-3">
                    <div>
                        <input type="number" id="converter-input" class="w-full p-2 border rounded-lg" placeholder="Enter value">
                    </div>
                    <div>
                        <select id="converter-from" class="w-full p-2 border rounded-lg bg-gray-50">
                            <!-- Options will be populated by JavaScript -->
                        </select>
                    </div>
                </div>
                
                <div class="flex justify-center my-3">
                    <button onclick="swapUnits()" class="bg-indigo-100 text-indigo-600 p-2 rounded-full">
                        <i class="fas fa-exchange-alt"></i>
                    </button>
                </div>
                
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <input type="number" id="converter-output" class="w-full p-2 border rounded-lg bg-gray-100" readonly>
                    </div>
                    <div>
                        <select id="converter-to" class="w-full p-2 border rounded-lg bg-gray-50">
                            <!-- Options will be populated by JavaScript -->
                        </select>
                    </div>
                </div>
                
                <button onclick="convert()" class="w-full mt-4 bg-indigo-500 text-white p-3 rounded-lg font-medium hover:bg-indigo-600 transition-colors">Convert</button>
            </div>
            
            <!-- BMI Calculator UI -->
            <div id="bmi-calculator" class="mb-4 hidden">
                <div class="mb-3">
                    <label class="block text-sm font-medium text-gray-700 mb-1">Height</label>
                    <div class="grid grid-cols-2 gap-2">
                        <input type="number" id="bmi-height" class="w-full p-2 border rounded-lg" placeholder="Height">
                        <select id="bmi-height-unit" class="w-full p-2 border rounded-lg bg-gray-50">
                            <option value="cm">Centimeters</option>
                            <option value="m">Meters</option>
                            <option value="ft">Feet</option>
                            <option value="in">Inches</option>
                        </select>
                    </div>
                </div>
                
                <div class="mb-3">
                    <label class="block text-sm font-medium text-gray-700 mb-1">Weight</label>
                    <div class="grid grid-cols-2 gap-2">
                        <input type="number" id="bmi-weight" class="w-full p-2 border rounded-lg" placeholder="Weight">
                        <select id="bmi-weight-unit" class="w-full p-2 border rounded-lg bg-gray-50">
                            <option value="kg">Kilograms</option>
                            <option value="lb">Pounds</option>
                        </select>
                    </div>
                </div>
                
                <button onclick="calculateBMI()" class="w-full mt-2 bg-indigo-500 text-white p-3 rounded-lg font-medium hover:bg-indigo-600 transition-colors">Calculate BMI</button>
                
                <div id="bmi-result" class="mt-4 p-3 bg-gray-100 rounded-lg hidden">
                    <div class="text-center">
                        <div id="bmi-value" class="text-2xl font-bold text-indigo-600">0</div>
                        <div id="bmi-category" class="text-lg font-medium">Normal</div>
                    </div>
                    <div class="mt-2 text-sm text-gray-600">
                        <div><span class="font-medium">Underweight:</span> Less than 18.5</div>
                        <div><span class="font-medium">Normal:</span> 18.5 - 24.9</div>
                        <div><span class="font-medium">Overweight:</span> 25 - 29.9</div>
                        <div><span class="font-medium">Obese:</span> 30 or greater</div>
                    </div>
                </div>
            </div>
            
            <!-- GST Calculator UI -->
            <div id="gst-calculator" class="mb-4 hidden">
                <div class="mb-3">
                    <label class="block text-sm font-medium text-gray-700 mb-1">Amount</label>
                    <input type="number" id="gst-amount" class="w-full p-2 border rounded-lg" placeholder="Enter amount">
                </div>
                
                <div class="mb-3">
                    <label class="block text-sm font-medium text-gray-700 mb-1">GST Rate (%)</label>
                    <select id="gst-rate" class="w-full p-2 border rounded-lg bg-gray-50">
                        <option value="5">5%</option>
                        <option value="12">12%</option>
                        <option value="18" selected>18%</option>
                        <option value="28">28%</option>
                        <option value="custom">Custom</option>
                    </select>
                    <input type="number" id="gst-custom-rate" class="w-full p-2 border rounded-lg mt-2 hidden" placeholder="Enter custom rate">
                </div>
                
                <div class="mb-3">
                    <label class="block text-sm font-medium text-gray-700 mb-1">Calculate</label>
                    <select id="gst-calculation-type" class="w-full p-2 border rounded-lg bg-gray-50">
                        <option value="exclusive">Add GST to amount</option>
                        <option value="inclusive">Extract GST from amount</option>
                    </select>
                </div>
                
                <button onclick="calculateGST()" class="w-full mt-2 bg-indigo-500 text-white p-3 rounded-lg font-medium hover:bg-indigo-600 transition-colors">Calculate</button>
                
                <div id="gst-result" class="mt-4 p-3 bg-gray-100 rounded-lg hidden">
                    <div class="grid grid-cols-2 gap-2">
                        <div class="text-sm font-medium text-gray-700">Original Amount:</div>
                        <div id="gst-original" class="text-right">₹0.00</div>
                        
                        <div class="text-sm font-medium text-gray-700">GST Amount:</div>
                        <div id="gst-tax" class="text-right">₹0.00</div>
                        
                        <div class="text-sm font-medium text-gray-700">Total Amount:</div>
                        <div id="gst-total" class="text-right font-bold">₹0.00</div>
                    </div>
                </div>
            </div>
            
            <!-- Numeral System Converter UI -->
            <div id="numeral-calculator" class="mb-4 hidden">
                <div class="mb-3">
                    <label class="block text-sm font-medium text-gray-700 mb-1">Input Value</label>
                    <input type="text" id="numeral-input" class="w-full p-2 border rounded-lg" placeholder="Enter value">
                </div>
                
                <div class="grid grid-cols-2 gap-4 mb-3">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-1">From</label>
                        <select id="numeral-from" class="w-full p-2 border rounded-lg bg-gray-50">
                            <option value="decimal">Decimal (Base 10)</option>
                            <option value="binary">Binary (Base 2)</option>
                            <option value="octal">Octal (Base 8)</option>
                            <option value="hexadecimal">Hexadecimal (Base 16)</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-1">To</label>
                        <select id="numeral-to" class="w-full p-2 border rounded-lg bg-gray-50">
                            <option value="binary">Binary (Base 2)</option>
                            <option value="octal">Octal (Base 8)</option>
                            <option value="decimal">Decimal (Base 10)</option>
                            <option value="hexadecimal">Hexadecimal (Base 16)</option>
                        </select>
                    </div>
                </div>
                
                <button onclick="convertNumeral()" class="w-full mt-2 bg-indigo-500 text-white p-3 rounded-lg font-medium hover:bg-indigo-600 transition-colors">Convert</button>
                
                <div id="numeral-result" class="mt-4 p-3 bg-gray-100 rounded-lg hidden">
                    <label class="block text-sm font-medium text-gray-700 mb-1">Result</label>
                    <input type="text" id="numeral-output" class="w-full p-2 border rounded-lg bg-white" readonly>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Calculator variables
        let currentInput = '0';
        let calculationHistory = '';
        let currentConverterType = '';
        
        // DOM elements
        const display = document.getElementById('display');
        const history = document.getElementById('history');
        const standardCalc = document.getElementById('standard-calculator');
        const scientificCalc = document.getElementById('scientific-calculator');
        const converter = document.getElementById('converter');
        const converterTool = document.getElementById('converter-tool');
        const converterTitle = document.getElementById('converter-title');
        const standardConverter = document.getElementById('standard-converter');
        const bmiCalculator = document.getElementById('bmi-calculator');
        const gstCalculator = document.getElementById('gst-calculator');
        const numeralCalculator = document.getElementById('numeral-calculator');
        
        // Tab elements
        const tabStandard = document.getElementById('tab-standard');
        const tabScientific = document.getElementById('tab-scientific');
        const tabConverter = document.getElementById('tab-converter');
        
        // Converter elements
        const converterFrom = document.getElementById('converter-from');
        const converterTo = document.getElementById('converter-to');
        const converterInput = document.getElementById('converter-input');
        const converterOutput = document.getElementById('converter-output');
        const backToConverters = document.getElementById('back-to-converters');
        
        // GST elements
        document.getElementById('gst-rate').addEventListener('change', function() {
            const customRateInput = document.getElementById('gst-custom-rate');
            if (this.value === 'custom') {
                customRateInput.classList.remove('hidden');
            } else {
                customRateInput.classList.add('hidden');
            }
        });
        
        // Tab switching
        tabStandard.addEventListener('click', () => {
            standardCalc.classList.remove('hidden');
            scientificCalc.classList.add('hidden');
            converter.classList.add('hidden');
            converterTool.classList.add('hidden');
            
            tabStandard.classList.add('tab-active');
            tabScientific.classList.remove('tab-active');
            tabConverter.classList.remove('tab-active');
        });
        
        tabScientific.addEventListener('click', () => {
            standardCalc.classList.add('hidden');
            scientificCalc.classList.remove('hidden');
            converter.classList.add('hidden');
            converterTool.classList.add('hidden');
            
            tabStandard.classList.remove('tab-active');
            tabScientific.classList.add('tab-active');
            tabConverter.classList.remove('tab-active');
        });
        
        tabConverter.addEventListener('click', () => {
            standardCalc.classList.add('hidden');
            scientificCalc.classList.add('hidden');
            converter.classList.remove('hidden');
            converterTool.classList.add('hidden');
            
            tabStandard.classList.remove('tab-active');
            tabScientific.classList.remove('tab-active');
            tabConverter.classList.add('tab-active');
        });
        
        // Back button for converter tool
        backToConverters.addEventListener('click', () => {
            converter.classList.remove('hidden');
            converterTool.classList.add('hidden');
        });
        
        // Calculator functions
        function updateDisplay() {
            display.textContent = currentInput;
            history.textContent = calculationHistory;
        }
        
        function appendToDisplay(value) {
            if (currentInput === '0' && value !== '.') {
                currentInput = value;
            } else {
                currentInput += value;
            }
            updateDisplay();
        }
        
        function clearDisplay() {
            currentInput = '0';
            calculationHistory = '';
            updateDisplay();
        }
        
        function backspace() {
            if (currentInput.length > 1) {
                currentInput = currentInput.slice(0, -1);
            } else {
                currentInput = '0';
            }
            updateDisplay();
        }
        
        function calculate() {
            try {
                // Replace % with /100*
                let expression = currentInput.replace(/%/g, '/100');
                
                calculationHistory = currentInput + ' =';
                currentInput = eval(expression).toString();
                updateDisplay();
            } catch (error) {
                currentInput = 'Error';
                updateDisplay();
                setTimeout(clearDisplay, 1500);
            }
        }
        
        // Scientific calculator functions
        function calculateSquareRoot() {
            try {
                const value = parseFloat(currentInput);
                if (value >= 0) {
                    calculationHistory = `√(${currentInput})`;
                    currentInput = Math.sqrt(value).toString();
                    updateDisplay();
                } else {
                    currentInput = 'Error';
                    updateDisplay();
                    setTimeout(clearDisplay, 1500);
                }
            } catch (error) {
                currentInput = 'Error';
                updateDisplay();
                setTimeout(clearDisplay, 1500);
            }
        }
        
        function calculatePower() {
            currentInput += '**';
            updateDisplay();
        }
        
        function calculateSin() {
            try {
                const value = parseFloat(currentInput);
                calculationHistory = `sin(${currentInput})`;
                currentInput = Math.sin(value * Math.PI / 180).toString();
                updateDisplay();
            } catch (error) {
                currentInput = 'Error';
                updateDisplay();
                setTimeout(clearDisplay, 1500);
            }
        }
        
        function calculateCos() {
            try {
                const value = parseFloat(currentInput);
                calculationHistory = `cos(${currentInput})`;
                currentInput = Math.cos(value * Math.PI / 180).toString();
                updateDisplay();
            } catch (error) {
                currentInput = 'Error';
                updateDisplay();
                setTimeout(clearDisplay, 1500);
            }
        }
        
        function calculateTan() {
            try {
                const value = parseFloat(currentInput);
                calculationHistory = `tan(${currentInput})`;
                currentInput = Math.tan(value * Math.PI / 180).toString();
                updateDisplay();
            } catch (error) {
                currentInput = 'Error';
                updateDisplay();
                setTimeout(clearDisplay, 1500);
            }
        }
        
        function calculateLog() {
            try {
                const value = parseFloat(currentInput);
                if (value > 0) {
                    calculationHistory = `log(${currentInput})`;
                    currentInput = Math.log10(value).toString();
                    updateDisplay();
                } else {
                    currentInput = 'Error';
                    updateDisplay();
                    setTimeout(clearDisplay, 1500);
                }
            } catch (error) {
                currentInput = 'Error';
                updateDisplay();
                setTimeout(clearDisplay, 1500);
            }
        }
        
        function calculateLn() {
            try {
                const value = parseFloat(currentInput);
                if (value > 0) {
                    calculationHistory = `ln(${currentInput})`;
                    currentInput = Math.log(value).toString();
                    updateDisplay();
                } else {
                    currentInput = 'Error';
                    updateDisplay();
                    setTimeout(clearDisplay, 1500);
                }
            } catch (error) {
                currentInput = 'Error';
                updateDisplay();
                setTimeout(clearDisplay, 1500);
            }
        }
        
        function calculateFactorial() {
            try {
                const num = parseInt(currentInput);
                if (num >= 0 && Number.isInteger(num)) {
                    let result = 1;
                    for (let i = 2; i <= num; i++) {
                        result *= i;
                    }
                    calculationHistory = `${currentInput}!`;
                    currentInput = result.toString();
                    updateDisplay();
                } else {
                    currentInput = 'Error';
                    updateDisplay();
                    setTimeout(clearDisplay, 1500);
                }
            } catch (error) {
                currentInput = 'Error';
                updateDisplay();
                setTimeout(clearDisplay, 1500);
            }
        }
        
        function calculatePi() {
            currentInput = Math.PI.toString();
            updateDisplay();
        }
        
        function calculateE() {
            currentInput = Math.E.toString();
            updateDisplay();
        }
        
        function calculateMod() {
            currentInput += '%';
            updateDisplay();
        }
        
        // Converter data
        const converterData = {
            currency: {
                USD: { name: "US Dollar", rate: 1 },
                EUR: { name: "Euro", rate: 0.85 },
                GBP: { name: "British Pound", rate: 0.73 },
                JPY: { name: "Japanese Yen", rate: 110.14 },
                CAD: { name: "Canadian Dollar", rate: 1.25 },
                AUD: { name: "Australian Dollar", rate: 1.36 },
                INR: { name: "Indian Rupee", rate: 74.5 },
                CNY: { name: "Chinese Yuan", rate: 6.45 },
                SGD: { name: "Singapore Dollar", rate: 1.35 }
            },
            temperature: {
                Celsius: { name: "Celsius", convert: (value, to) => {
                    if (to === "Fahrenheit") return (value * 9/5) + 32;
                    if (to === "Kelvin") return value + 273.15;
                    return value;
                }},
                Fahrenheit: { name: "Fahrenheit", convert: (value, to) => {
                    if (to === "Celsius") return (value - 32) * 5/9;
                    if (to === "Kelvin") return (value - 32) * 5/9 + 273.15;
                    return value;
                }},
                Kelvin: { name: "Kelvin", convert: (value, to) => {
                    if (to === "Celsius") return value - 273.15;
                    if (to === "Fahrenheit") return (value - 273.15) * 9/5 + 32;
                    return value;
                }}
            },
            length: {
                Meter: { name: "Meter", rate: 1 },
                Kilometer: { name: "Kilometer", rate: 0.001 },
                Centimeter: { name: "Centimeter", rate: 100 },
                Millimeter: { name: "Millimeter", rate: 1000 },
                Inch: { name: "Inch", rate: 39.3701 },
                Foot: { name: "Foot", rate: 3.28084 },
                Yard: { name: "Yard", rate: 1.09361 },
                Mile: { name: "Mile", rate: 0.000621371 }
            },
            weight: {
                Kilogram: { name: "Kilogram", rate: 1 },
                Gram: { name: "Gram", rate: 1000 },
                Milligram: { name: "Milligram", rate: 1000000 },
                Pound: { name: "Pound", rate: 2.20462 },
                Ounce: { name: "Ounce", rate: 35.274 },
                Ton: { name: "Metric Ton", rate: 0.001 }
            },
            volume: {
                Liter: { name: "Liter", rate: 1 },
                Milliliter: { name: "Milliliter", rate: 1000 },
                CubicMeter: { name: "Cubic Meter", rate: 0.001 },
                CubicCentimeter: { name: "Cubic Centimeter", rate: 1000 },
                Gallon: { name: "Gallon (US)", rate: 0.264172 },
                Quart: { name: "Quart (US)", rate: 1.05669 },
                Pint: { name: "Pint (US)", rate: 2.11338 },
                FluidOunce: { name: "Fluid Ounce (US)", rate: 33.814 }
            },
            area: {
                SquareMeter: { name: "Square Meter", rate: 1 },
                SquareKilometer: { name: "Square Kilometer", rate: 0.000001 },
                SquareCentimeter: { name: "Square Centimeter", rate: 10000 },
                SquareMillimeter: { name: "Square Millimeter", rate: 1000000 },
                SquareInch: { name: "Square Inch", rate: 1550 },
                SquareFoot: { name: "Square Foot", rate: 10.7639 },
                SquareYard: { name: "Square Yard", rate: 1.19599 },
                Acre: { name: "Acre", rate: 0.000247105 },
                Hectare: { name: "Hectare", rate: 0.0001 }
            },
            data: {
                Byte: { name: "Byte", rate: 1 },
                Kilobyte: { name: "Kilobyte", rate: 0.001 },
                Megabyte: { name: "Megabyte", rate: 0.000001 },
                Gigabyte: { name: "Gigabyte", rate: 1e-9 },
                Terabyte: { name: "Terabyte", rate: 1e-12 },
                Petabyte: { name: "Petabyte", rate: 1e-15 },
                Kibibyte: { name: "Kibibyte", rate: 0.0009765625 },
                Mebibyte: { name: "Mebibyte", rate: 9.5367e-7 },
                Gibibyte: { name: "Gibibyte", rate: 9.3132e-10 },
                Tebibyte: { name: "Tebibyte", rate: 9.0949e-13 }
            },
            time: {
                Second: { name: "Second", rate: 1 },
                Millisecond: { name: "Millisecond", rate: 1000 },
                Minute: { name: "Minute", rate: 1/60 },
                Hour: { name: "Hour", rate: 1/3600 },
                Day: { name: "Day", rate: 1/86400 },
                Week: { name: "Week", rate: 1/604800 },
                Month: { name: "Month (30 days)", rate: 1/2592000 },
                Year: { name: "Year (365 days)", rate: 1/31536000 }
            },
            speed: {
                MeterPerSecond: { name: "Meter/Second", rate: 1 },
                KilometerPerHour: { name: "Kilometer/Hour", rate: 3.6 },
                MilePerHour: { name: "Mile/Hour", rate: 2.23694 },
                Knot: { name: "Knot", rate: 1.94384 },
                FootPerSecond: { name: "Foot/Second", rate: 3.28084 }
            }
        };
        
        // Show converter tool
        function showConverterTool(type) {
            currentConverterType = type;
            converter.classList.add('hidden');
            converterTool.classList.remove('hidden');
            
            // Set title
            let title = type.charAt(0).toUpperCase() + type.slice(1) + " Converter";
            converterTitle.textContent = title;
            
            // Show appropriate converter UI
            standardConverter.classList.add('hidden');
            bmiCalculator.classList.add('hidden');
            gstCalculator.classList.add('hidden');
            numeralCalculator.classList.add('hidden');
            
            if (type === 'bmi') {
                bmiCalculator.classList.remove('hidden');
            } else if (type === 'gst') {
                gstCalculator.classList.remove('hidden');
            } else if (type === 'numeral') {
                numeralCalculator.classList.remove('hidden');
            } else {
                standardConverter.classList.remove('hidden');
                updateConverterOptions(type);
            }
        }
        
        // Update converter options
        function updateConverterOptions(type) {
            converterFrom.innerHTML = '';
            converterTo.innerHTML = '';
            
            if (!converterData[type]) return;
            
            const units = Object.keys(converterData[type]);
            
            units.forEach(unit => {
                const fromOption = document.createElement('option');
                fromOption.value = unit;
                fromOption.textContent = converterData[type][unit].name;
                converterFrom.appendChild(fromOption);
                
                const toOption = document.createElement('option');
                toOption.value = unit;
                toOption.textContent = converterData[type][unit].name;
                converterTo.appendChild(toOption);
            });
            
            // Set default "to" option to be different from "from"
            if (units.length > 1) {
                converterTo.selectedIndex = 1;
            }
        }
        
        // Standard converter
        function convert() {
            const type = currentConverterType;
            const fromUnit = converterFrom.value;
            const toUnit = converterTo.value;
            const inputValue = parseFloat(converterInput.value);
            
            if (isNaN(inputValue)) {
                converterOutput.value = '';
                return;
            }
            
            let result;
            
            if (type === 'temperature') {
                result = converterData[type][fromUnit].convert(inputValue, toUnit);
            } else {
                // For other converters
                const baseValue = inputValue / converterData[type][fromUnit].rate;
                result = baseValue * converterData[type][toUnit].rate;
            }
            
            converterOutput.value = result.toFixed(4);
        }
        
        function swapUnits() {
            const tempIndex = converterFrom.selectedIndex;
            converterFrom.selectedIndex = converterTo.selectedIndex;
            converterTo.selectedIndex = tempIndex;
            
            const tempValue = converterInput.value;
            converterInput.value = converterOutput.value;
            converterOutput.value = tempValue;
        }
        
        // BMI Calculator
        function calculateBMI() {
            const heightInput = parseFloat(document.getElementById('bmi-height').value);
            const weightInput = parseFloat(document.getElementById('bmi-weight').value);
            const heightUnit = document.getElementById('bmi-height-unit').value;
            const weightUnit = document.getElementById('bmi-weight-unit').value;
            
            if (isNaN(heightInput) || isNaN(weightInput) || heightInput <= 0 || weightInput <= 0) {
                alert('Please enter valid height and weight values');
                return;
            }
            
            // Convert height to meters
            let heightInMeters;
            switch (heightUnit) {
                case 'cm':
                    heightInMeters = heightInput / 100;
                    break;
                case 'm':
                    heightInMeters = heightInput;
                    break;
                case 'ft':
                    heightInMeters = heightInput * 0.3048;
                    break;
                case 'in':
                    heightInMeters = heightInput * 0.0254;
                    break;
            }
            
            // Convert weight to kg
            let weightInKg;
            switch (weightUnit) {
                case 'kg':
                    weightInKg = weightInput;
                    break;
                case 'lb':
                    weightInKg = weightInput * 0.453592;
                    break;
            }
            
            // Calculate BMI
            const bmi = weightInKg / (heightInMeters * heightInMeters);
            
            // Determine category
            let category;
            if (bmi < 18.5) {
                category = 'Underweight';
            } else if (bmi < 25) {
                category = 'Normal';
            } else if (bmi < 30) {
                category = 'Overweight';
            } else {
                category = 'Obese';
            }
            
            // Display result
            document.getElementById('bmi-value').textContent = bmi.toFixed(1);
            document.getElementById('bmi-category').textContent = category;
            document.getElementById('bmi-result').classList.remove('hidden');
        }
        
        // GST Calculator
        function calculateGST() {
            const amount = parseFloat(document.getElementById('gst-amount').value);
            let rate;
            
            if (document.getElementById('gst-rate').value === 'custom') {
                rate = parseFloat(document.getElementById('gst-custom-rate').value);
            } else {
                rate = parseFloat(document.getElementById('gst-rate').value);
            }
            
            const calculationType = document.getElementById('gst-calculation-type').value;
            
            if (isNaN(amount) || amount <= 0 || isNaN(rate) || rate < 0) {
                alert('Please enter valid amount and GST rate');
                return;
            }
            
            let originalAmount, gstAmount, totalAmount;
            
            if (calculationType === 'exclusive') {
                // Add GST to amount
                originalAmount = amount;
                gstAmount = amount * (rate / 100);
                totalAmount = originalAmount + gstAmount;
            } else {
                // Extract GST from amount
                originalAmount = amount * (100 / (100 + rate));
                gstAmount = amount - originalAmount;
                totalAmount = amount;
            }
            
            // Display result
            document.getElementById('gst-original').textContent = '₹' + originalAmount.toFixed(2);
            document.getElementById('gst-tax').textContent = '₹' + gstAmount.toFixed(2);
            document.getElementById('gst-total').textContent = '₹' + totalAmount.toFixed(2);
            document.getElementById('gst-result').classList.remove('hidden');
        }
        
        // Numeral System Converter
        function convertNumeral() {
            const input = document.getElementById('numeral-input').value.trim();
            const fromSystem = document.getElementById('numeral-from').value;
            const toSystem = document.getElementById('numeral-to').value;
            
            if (!input) {
                alert('Please enter a value to convert');
                return;
            }
            
            let decimalValue;
            
            // Convert input to decimal
            try {
                switch (fromSystem) {
                    case 'decimal':
                        decimalValue = parseInt(input, 10);
                        break;
                    case 'binary':
                        decimalValue = parseInt(input, 2);
                        break;
                    case 'octal':
                        decimalValue = parseInt(input, 8);
                        break;
                    case 'hexadecimal':
                        decimalValue = parseInt(input, 16);
                        break;
                }
                
                if (isNaN(decimalValue)) {
                    throw new Error('Invalid input for the selected numeral system');
                }
            } catch (error) {
                alert(error.message);
                return;
            }
            
            // Convert decimal to target system
            let result;
            switch (toSystem) {
                case 'decimal':
                    result = decimalValue.toString(10);
                    break;
                case 'binary':
                    result = decimalValue.toString(2);
                    break;
                case 'octal':
                    result = decimalValue.toString(8);
                    break;
                case 'hexadecimal':
                    result = decimalValue.toString(16).toUpperCase();
                    break;
            }
            
            // Display result
            document.getElementById('numeral-output').value = result;
            document.getElementById('numeral-result').classList.remove('hidden');
        }
        
        // Initialize the calculator
        updateDisplay();
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'967e8e44c44f545e',t:'MTc1Mzk4MDIxOC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
