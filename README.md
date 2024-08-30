# CALCULATOR
create a basic calculator using CSS, HTML, and JavaScript,
//Basic HTML Layout
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Basic Calculator</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="calculator">
        <div class="display" id="display"></div>
        <div class="buttons">
            <button class="btn" data-value="7">7</button>
            <button class="btn" data-value="8">8</button>
            <button class="btn" data-value="9">9</button>
            <button class="btn operator" data-value="/">/</button>

            <button class="btn" data-value="4">4</button>
            <button class="btn" data-value="5">5</button>
            <button class="btn" data-value="6">6</button>
            <button class="btn operator" data-value="*">*</button>

            <button class="btn" data-value="1">1</button>
            <button class="btn" data-value="2">2</button>
            <button class="btn" data-value="3">3</button>
            <button class="btn operator" data-value="-">-</button>

            <button class="btn" data-value="0">0</button>
            <button class="btn" data-value=".">.</button>
            <button class="btn clear">C</button>
            <button class="btn operator" data-value="+">+</button>

            <button class="btn equal" id="equal">=</button>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>


//Basic CSS Styles



body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-color: #f0f0f0;
}

.calculator {
    display: grid;
    grid-template-rows: auto 1fr;
    gap: 10px;
    width: 220px;
}

.display {
    background-color: #333;
    color: #fff;
    text-align: right;
    padding: 10px;
    font-size: 2em;
    border-radius: 5px;
}

.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
}

.btn {
    background-color: #fff;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 1.5em;
    padding: 20px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.btn:hover {
    background-color: #f0f0f0;
}

.btn.operator {
    background-color: #f9a825;
    color: #fff;
}

.btn.operator:hover {
    background-color: #f57f17;
}

.btn.equal {
    background-color: #4caf50;
    color: #fff;
    grid-column: span 4;
}

.btn.equal:hover {
    background-color: #388e3c;
}

.btn.clear {
    background-color: #e53935;
    color: #fff;
    grid-column: span 4;
}

.btn.clear:hover {
    background-color: #d32f2f;
}



//Basic JavaScript



document.addEventListener('DOMContentLoaded', () => {
    const display = document.getElementById('display');
    let currentInput = '';
    let operator = '';
    let previousInput = '';
    
    // Handle button clicks
    document.querySelectorAll('.btn').forEach(button => {
        button.addEventListener('click', (e) => {
            const value = e.target.dataset.value;

            if (e.target.classList.contains('clear')) {
                currentInput = '';
                previousInput = '';
                operator = '';
                display.textContent = '';
            } else if (e.target.classList.contains('operator')) {
                operator = value;
                previousInput = currentInput;
                currentInput = '';
            } else if (e.target.classList.contains('equal')) {
                if (previousInput && operator && currentInput) {
                    display.textContent = calculate(previousInput, operator, currentInput);
                    currentInput = display.textContent;
                    previousInput = '';
                    operator = '';
                }
            } else {
                currentInput += value;
                display.textContent = currentInput;
            }
        });
    });

    // Perform calculation
    function calculate(num1, op, num2) {
        const n1 = parseFloat(num1);
        const n2 = parseFloat(num2);
        
        switch (op) {
            case '+': return n1 + n2;
            case '-': return n1 - n2;
            case '*': return n1 * n2;
            case '/': return n1 / n2;
            default: return '';
        }
    }
});

