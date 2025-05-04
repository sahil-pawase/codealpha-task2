<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <style>
        .calculator {
            width: 300px;
            margin: 50px auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        #display {
            width: 100%;
            height: 40px;
            margin-bottom: 10px;
            text-align: right;
            padding: 5px;
            font-size: 20px;
        }
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 5px;
        }
        button {
            padding: 10px;
            font-size: 18px;
            border: 1px solid #999;
            border-radius: 3px;
            cursor: pointer;
        }
        button:hover {
            background-color:blue;
        }
        .toggle {
            background-color: gray;
            color: white;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <input type="text" id="display" readonly>
        <div class="buttons" >
            <button onclick="clearDisplay()">C</button>
            <button onclick="deleteDisplay()">AC</button>
            <button onclick="appendToDisplay('/')">/</button>
            <button onclick="appendToDisplay('*')">*</button>
            <button onclick="appendToDisplay('7')">7</button>
            <button onclick="appendToDisplay('8')">8</button>
            <button onclick="appendToDisplay('9')">9</button>
            <button onclick="appendToDisplay('-')">-</button>
            <button onclick="appendToDisplay('4')">4</button>
            <button onclick="appendToDisplay('5')">5</button>
            <button onclick="appendToDisplay('6')">6</button>
            <button onclick="appendToDisplay('+')">+</button>
            <button onclick="appendToDisplay('1')">1</button>
            <button onclick="appendToDisplay('2')">2</button>
            <button onclick="appendToDisplay('3')">3</button>
            <button onclick="appendToDisplay('%')">%</button>
            <button class="toggle" onclick="toggleCalculator()">Off</button>
            <button onclick="appendToDisplay('0')">0</button>
            <button onclick="appendToDisplay('.')">.</button>
            <button onclick="calculate()">=</button>
        </div>
    </div>

    <script>
        function appendToDisplay(value) {
            document.getElementById('display').value += value;
        }

        function clearDisplay() {
            document.getElementById('display').value = '';
        }

        function deleteDisplay() {
            let display = document.getElementById('display').value;
            document.getElementById('display').value = display.slice(0, -1);
        }

        function calculate() {
            let display = document.getElementById('display').value;
            if (display.includes('%')) {
                let parts = display.split('%');
                if (parts.length === 2 && parts[1] === '') {
                    document.getElementById('display').value = parseFloat(parts[0]) / 100;
                } else if (parts.length === 2) {
                    document.getElementById('display').value = (parseFloat(parts[0]) * parseFloat(parts[1])) / 100;
                } else {
                    document.getElementById('display').value = 'Error';
                }
            } else {
                try {
                    document.getElementById('display').value = eval(display);
                } catch (e) {
                    document.getElementById('display').value = 'Error';
                }
            }
        }

        function toggleCalculator() {
            let display = document.getElementById('display');
            let buttons = document.querySelectorAll('.buttons button');
            let toggleButton = document.querySelector('.toggle');
            if (toggleButton.textContent === 'Off') {
                display.value = '';
                buttons.forEach(button => {
                    if (!button.classList.contains('toggle')) {
                        button.disabled = true;
                    }
                });
                toggleButton.textContent = 'On';
            } else {
                buttons.forEach(button => {
                    button.disabled = false;
                });
                toggleButton.textContent = 'Off';
            }
        }
    </script>
    <script src="/calculator/index.js"></script>
</body>
</html>
