# Scientific-Calculator
I've built a Scientific Calculator using html css and js.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Scientific Calculator</title>
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
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .calculator {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.2);
            max-width: 400px;
            width: 100%;
        }

        .display {
            background: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            text-align: right;
            min-height: 80px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .expression {
            font-size: 14px;
            color: #ccc;
            min-height: 20px;
            word-wrap: break-word;
        }

        .result {
            font-size: 28px;
            font-weight: bold;
            min-height: 35px;
            word-wrap: break-word;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 12px;
        }

        button {
            padding: 15px 8px;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        button:active {
            transform: translateY(0);
        }

        .btn-number {
            background: rgba(255, 255, 255, 0.9);
            color: #333;
        }

        .btn-operator {
            background: rgba(255, 107, 107, 0.9);
            color: white;
        }

        .btn-function {
            background: rgba(74, 144, 226, 0.9);
            color: white;
            font-size: 14px;
        }

        .btn-clear {
            background: rgba(255, 193, 7, 0.9);
            color: #333;
        }

        .btn-equals {
            background: rgba(40, 167, 69, 0.9);
            color: white;
        }

        .btn-wide {
            grid-column: span 2;
        }

        @media (max-width: 480px) {
            .calculator {
                padding: 15px;
            }
            
            button {
                padding: 12px 6px;
                font-size: 14px;
            }
            
            .btn-function {
                font-size: 12px;
            }
            
            .result {
                font-size: 24px;
            }
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display">
            <div class="expression" id="expression"></div>
            <div class="result" id="result">0</div>
        </div>
        
        <div class="buttons">
            <!-- Row 1 -->
            <button class="btn-clear" onclick="clearAll()">C</button>
            <button class="btn-clear" onclick="clearEntry()">CE</button>
            <button class="btn-operator" onclick="appendToExpression('⌫')" title="Backspace">⌫</button>
            <button class="btn-function" onclick="appendToExpression('sin(')" title="Sine">sin</button>
            <button class="btn-function" onclick="appendToExpression('cos(')" title="Cosine">cos</button>
            
            <!-- Row 2 -->
            <button class="btn-function" onclick="appendToExpression('tan(')" title="Tangent">tan</button>
            <button class="btn-function" onclick="appendToExpression('log(')" title="Logarithm base 10">log</button>
            <button class="btn-function" onclick="appendToExpression('ln(')" title="Natural logarithm">ln</button>
            <button class="btn-function" onclick="appendToExpression('sqrt(')" title="Square root">√</button>
            <button class="btn-function" onclick="appendToExpression('^')" title="Power">x^y</button>
            
            <!-- Row 3 -->
            <button class="btn-function" onclick="appendToExpression('π')" title="Pi">π</button>
            <button class="btn-function" onclick="appendToExpression('e')" title="Euler's number">e</button>
            <button class="btn-function" onclick="appendToExpression('(')" title="Left parenthesis">(</button>
            <button class="btn-function" onclick="appendToExpression(')')" title="Right parenthesis">)</button>
            <button class="btn-operator" onclick="appendToExpression('/')" title="Division">÷</button>
            
            <!-- Row 4 -->
            <button class="btn-number" onclick="appendToExpression('7')">7</button>
            <button class="btn-number" onclick="appendToExpression('8')">8</button>
            <button class="btn-number" onclick="appendToExpression('9')">9</button>
            <button class="btn-operator" onclick="appendToExpression('*')" title="Multiplication">×</button>
            <button class="btn-function" onclick="appendToExpression('!')" title="Factorial">x!</button>
            
            <!-- Row 5 -->
            <button class="btn-number" onclick="appendToExpression('4')">4</button>
            <button class="btn-number" onclick="appendToExpression('5')">5</button>
            <button class="btn-number" onclick="appendToExpression('6')">6</button>
            <button class="btn-operator" onclick="appendToExpression('-')" title="Subtraction">−</button>
            <button class="btn-function" onclick="appendToExpression('abs(')" title="Absolute value">|x|</button>
            
            <!-- Row 6 -->
            <button class="btn-number" onclick="appendToExpression('1')">1</button>
            <button class="btn-number" onclick="appendToExpression('2')">2</button>
            <button class="btn-number" onclick="appendToExpression('3')">3</button>
            <button class="btn-operator" onclick="appendToExpression('+')" title="Addition">+</button>
            <button class="btn-function" onclick="toggleSign()" title="Plus/Minus">±</button>
            
            <!-- Row 7 -->
            <button class="btn-number btn-wide" onclick="appendToExpression('0')">0</button>
            <button class="btn-number" onclick="appendToExpression('.')">.</button>
            <button class="btn-equals btn-wide" onclick="calculate()" title="Calculate">=</button>
        </div>
    </div>

    <script>
        let expression = '';
        let result = '0';
        let shouldResetDisplay = false;
        let angleMode = 'DEG'; // DEG or RAD

        function updateDisplay() {
            document.getElementById('expression').textContent = expression;
            document.getElementById('result').textContent = result;
        }

        function appendToExpression(value) {
            if (shouldResetDisplay && !isNaN(value)) {
                expression = '';
                result = '0';
                shouldResetDisplay = false;
            }

            if (value === '⌫') {
                backspace();
                return;
            }

            // Handle special characters
            switch(value) {
                case 'π':
                    expression += 'π';
                    break;
                case 'e':
                    expression += 'e';
                    break;
                case '√':
                    expression += 'sqrt(';
                    break;
                case '^':
                    expression += '^';
                    break;
                case '×':
                    expression += '*';
                    break;
                case '÷':
                    expression += '/';
                    break;
                case '−':
                    expression += '-';
                    break;
                default:
                    expression += value;
            }
            
            updateDisplay();
        }

        function backspace() {
            if (expression.length > 0) {
                expression = expression.slice(0, -1);
                if (expression === '') {
                    result = '0';
                }
                updateDisplay();
            }
        }

        function clearAll() {
            expression = '';
            result = '0';
            shouldResetDisplay = false;
            updateDisplay();
        }

        function clearEntry() {
            result = '0';
            updateDisplay();
        }

        function toggleSign() {
            if (result !== '0') {
                if (result.charAt(0) === '-') {
                    result = result.substring(1);
                } else {
                    result = '-' + result;
                }
                expression = result;
                updateDisplay();
            }
        }

        function factorial(n) {
            if (n < 0) return NaN;
            if (n === 0 || n === 1) return 1;
            let result = 1;
            for (let i = 2; i <= n; i++) {
                result *= i;
            }
            return result;
        }

        function toRadians(degrees) {
            return degrees * (Math.PI / 180);
        }

        function calculate() {
            if (expression === '') return;

            try {
                let expr = expression;
                
                // Replace mathematical constants
                expr = expr.replace(/π/g, Math.PI.toString());
                expr = expr.replace(/e/g, Math.E.toString());
                
                // Handle factorials
                expr = expr.replace(/(\d+(?:\.\d+)?)!/g, (match, num) => {
                    return factorial(parseInt(num)).toString();
                });
                
                // Handle functions
                expr = expr.replace(/sin\(/g, 'Math.sin(');
                expr = expr.replace(/cos\(/g, 'Math.cos(');
                expr = expr.replace(/tan\(/g, 'Math.tan(');
                expr = expr.replace(/log\(/g, 'Math.log10(');
                expr = expr.replace(/ln\(/g, 'Math.log(');
                expr = expr.replace(/sqrt\(/g, 'Math.sqrt(');
                expr = expr.replace(/abs\(/g, 'Math.abs(');
                
                // Handle power operations
                expr = expr.replace(/\^/g, '**');
                
                // Convert trigonometric functions to radians if in degree mode
                if (angleMode === 'DEG') {
                    expr = expr.replace(/Math\.sin\(([^)]+)\)/g, (match, angle) => {
                        return `Math.sin(${angle} * Math.PI / 180)`;
                    });
                    expr = expr.replace(/Math\.cos\(([^)]+)\)/g, (match, angle) => {
                        return `Math.cos(${angle} * Math.PI / 180)`;
                    });
                    expr = expr.replace(/Math\.tan\(([^)]+)\)/g, (match, angle) => {
                        return `Math.tan(${angle} * Math.PI / 180)`;
                    });
                }
                
                // Evaluate the expression
                let calculatedResult = eval(expr);
                
                // Handle special cases
                if (isNaN(calculatedResult)) {
                    result = 'Error';
                } else if (!isFinite(calculatedResult)) {
                    result = 'Infinity';
                } else {
                    // Round to avoid floating point precision issues
                    calculatedResult = Math.round(calculatedResult * 1e12) / 1e12;
                    result = calculatedResult.toString();
                }
                
                shouldResetDisplay = true;
                
            } catch (error) {
                result = 'Error';
                shouldResetDisplay = true;
            }
            
            updateDisplay();
        }

        // Keyboard support
        document.addEventListener('keydown', function(event) {
            const key = event.key;
            
            if (key >= '0' && key <= '9') {
                appendToExpression(key);
            } else if (key === '.') {
                appendToExpression('.');
            } else if (key === '+') {
                appendToExpression('+');
            } else if (key === '-') {
                appendToExpression('-');
            } else if (key === '*') {
                appendToExpression('*');
            } else if (key === '/') {
                appendToExpression('/');
                event.preventDefault(); // Prevent browser search
            } else if (key === '(') {
                appendToExpression('(');
            } else if (key === ')') {
                appendToExpression(')');
            } else if (key === 'Enter' || key === '=') {
                calculate();
                event.preventDefault();
            } else if (key === 'Backspace') {
                backspace();
                event.preventDefault();
            } else if (key === 'Escape') {
                clearAll();
            } else if (key === 'Delete') {
                clearEntry();
            }
        });

        // Initialize display
        updateDisplay();
    </script>
</body>
</html>
