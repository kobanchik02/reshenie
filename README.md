<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tritmaster</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .task {
            margin-bottom: 20px;
        }
        .task h2 {
            margin-bottom: 10px;
        }
        .task-table {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
        }
        .task-table div {
            border: 1px solid black;
            width: 25%;
            padding: 10px;
            box-sizing: border-box;
        }
        .task-table div canvas {
            border: 1px solid black;
        }
        .task-table div input[type="file"] {
            margin-top: 10px;
        }
        .color-picker {
            margin-top: 10px;
        }
        .shape-picker {
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="task">
        <h2>Задача 1: Смена времен года</h2>
        <p>В природе всегда происходит смена времен года: зима, весна, лето, осень. Почему так происходит? Создайте трит-карточку (графическое представление, ментальная модель и блок-схема).</p>
        <button onclick="toggleTable('task1')">Решить</button>
        <div id="task1" class="task-table" style="display: none;">
            <div>
                <h3>Графическое представление</h3>
                <canvas id="graphicCanvas1" width="300" height="300"></canvas>
                <input type="file" id="graphicImageInput1" accept="image/*">
                <input type="color" id="graphicColorPicker1" class="color-picker">
            </div>
            <div>
                <h3>Ментальная модель</h3>
                <canvas id="mentalCanvas1" width="300" height="300"></canvas>
                <input type="file" id="mentalImageInput1" accept="image/*">
                <input type="color" id="mentalColorPicker1" class="color-picker">
            </div>
            <div>
                <h3>Блок-схема</h3>
                <canvas id="blockDiagramCanvas1" width="300" height="300"></canvas>
                <div class="shape-picker">
                    <button onclick="addRectangle('blockDiagramCanvas1')">Квадрат</button>
                    <button onclick="addCircle('blockDiagramCanvas1')">Круг</button>
                    <button onclick="addEllipse('blockDiagramCanvas1')">Овал</button>
                    <button onclick="addParallelogram('blockDiagramCanvas1')">Параллелограмм</button>
                    <button onclick="addTextRectangle('blockDiagramCanvas1')">Квадрат с текстом</button>
                    <button onclick="addDiamond('blockDiagramCanvas1')">Ромб</button>
                    <button onclick="addRectangle('blockDiagramCanvas1')">Прямоугольник</button>
                    <button onclick="addArrow('blockDiagramCanvas1')">Стрелка</button>
                </div>
            </div>
        </div>
    </div>

    <div class="task">
        <h2>Задача 2: Сбор грибов в лесу</h2>
        <p>Создайте трит-карточку "Сбор грибов в лесу".</p>
        <button onclick="toggleTable('task2')">Решить</button>
        <div id="task2" class="task-table" style="display: none;">
            <div>
                <h3>Графическое представление</h3>
                <canvas id="graphicCanvas2" width="300" height="300"></canvas>
                <input type="file" id="graphicImageInput2" accept="image/*">
                <input type="color" id="graphicColorPicker2" class="color-picker">
            </div>
            <div>
                <h3>Ментальная модель</h3>
                <canvas id="mentalCanvas2" width="300" height="300"></canvas>
                <input type="file" id="mentalImageInput2" accept="image/*">
                <input type="color" id="mentalColorPicker2" class="color-picker">
            </div>
            <div>
                <h3>Блок-схема</h3>
                <canvas id="blockDiagramCanvas2" width="300" height="300"></canvas>
                <div class="shape-picker">
                    <button onclick="addRectangle('blockDiagramCanvas2')">Квадрат</button>
                    <button onclick="addCircle('blockDiagramCanvas2')">Круг</button>
                    <button onclick="addEllipse('blockDiagramCanvas2')">Овал</button>
                    <button onclick="addParallelogram('blockDiagramCanvas2')">Параллелограмм</button>
                    <button onclick="addTextRectangle('blockDiagramCanvas2')">Квадрат с текстом</button>
                    <button onclick="addDiamond('blockDiagramCanvas2')">Ромб</button>
                    <button onclick="addRectangle('blockDiagramCanvas2')">Прямоугольник</button>
                    <button onclick="addArrow('blockDiagramCanvas2')">Стрелка</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Добавьте больше задач по аналогии -->

    <script src="https://cdnjs.cloudflare.com/ajax/libs/fabric.js/4.6.0/fabric.min.js"></script>
    <script>
        function toggleTable(id) {
            const table = document.getElementById(id);
            table.style.display = table.style.display === 'none' ? 'flex' : 'none';
        }

        // Инициализация Fabric.js для рисования
        function initFabricCanvas(canvasId, imageInputId, colorPickerId) {
            const canvas = new fabric.Canvas(canvasId);
            const imageInput = document.getElementById(imageInputId);
            const colorPicker = document.getElementById(colorPickerId);

            if (imageInput) {
                imageInput.addEventListener('change', (e) => {
                    const file = e.target.files[0];
                    if (file) {
                        const reader = new FileReader();
                        reader.onload = (event) => {
                            fabric.Image.fromURL(event.target.result, (img) => {
                                img.set({
                                    left: 100,
                                    top: 100,
                                    scaleX: 0.5,
                                    scaleY: 0.5,
                                    selectable: true,
                                    hasControls: true,
                                    hasBorders: true
                                });
                                canvas.add(img);
                            });
                        };
                        reader.readAsDataURL(file);
                    }
                });
            }

            if (colorPicker) {
                colorPicker.addEventListener('change', (e) => {
                    canvas.freeDrawingBrush.color = e.target.value;
                });
            }

            // Добавление инструментов для рисования
            canvas.isDrawingMode = true;
            canvas.freeDrawingBrush.color = 'black';
            canvas.freeDrawingBrush.width = 5;

            // Добавление текста
            canvas.on('mouse:dblclick', (options) => {
                const text = new fabric.IText('Текст', {
                    left: options.e.offsetX,
                    top: options.e.offsetY,
                    fontSize: 20
                });
                canvas.add(text);
            });
        }

        // Функции для добавления фигур
        function addRectangle(canvasId) {
            const canvas = new fabric.Canvas(canvasId);
            const rect = new fabric.Rect({
                left: 100,
                top: 100,
                fill: 'blue',
                width: 100,
                height: 100,
                selectable: true,
                hasControls: true,
                hasBorders: true
            });
            canvas.add(rect);
        }

        function addCircle(canvasId) {
            const canvas = new fabric.Canvas(canvasId);
            const circle = new fabric.Circle({
                left: 100,
                top: 100,
                fill: 'green',
                radius: 50,
                selectable: true,
                hasControls: true,
                hasBorders: true
            });
            canvas.add(circle);
        }

        function addEllipse(canvasId) {
            const canvas = new fabric.Canvas(canvasId);
            const ellipse = new fabric.Ellipse({
                left: 100,
                top: 100,
                fill: 'purple',
                rx: 50,
                ry: 30,
                selectable: true,
                hasControls: true,
                hasBorders: true
            });
            canvas.add(ellipse);
        }

        function addParallelogram(canvasId) {
            const canvas = new fabric.Canvas(canvasId);
            const parallelogram = new fabric.Polygon([
                { x: 0, y: 0 },
                { x: 100, y: 0 },
                { x: 150, y: 50 },
                { x: 50, y: 50 }
            ], {
                left: 100,
                top: 100,
                fill: 'orange',
                selectable: true,
                hasControls: true,
                hasBorders: true
            });
            canvas.add(parallelogram);
        }

        function addTextRectangle(canvasId) {
            const canvas = new fabric.Canvas(canvasId);
            const textRect = new fabric.Rect({
                left: 100,
                top: 100,
                fill: 'yellow',
                width: 100,
                height: 100,
                selectable: true,
                hasControls: true,
                hasBorders: true
            });
            const text = new fabric.IText('Квадрат с текстом', {
                left: 110,
                top: 110,
                fontSize: 14
            });
            canvas.add(textRect, text);
        }

        function addDiamond(canvasId) {
            const canvas = new fabric.Canvas(canvasId);
            const diamond = new fabric.Polygon([
                { x: 50, y: 0 },
                { x: 100, y: 50 },
                { x: 50, y: 100 },
                { x: 0, y: 50 }
            ], {
                left: 100,
                top: 100,
                fill: 'red',
                selectable: true,
                hasControls: true,
                hasBorders: true
            });
            canvas.add(diamond);
        }

        function addArrow(canvasId) {
            const canvas = new fabric.Canvas(canvasId);
            const arrow = new fabric.Path('M 0 0 L 50 50 L 0 100', {
                left: 100,
                top: 100,
                fill: 'transparent',
                stroke: 'black',
                strokeWidth: 2,
                selectable: true,
                hasControls: true,
                hasBorders: true
            });
            canvas.add(arrow);
        }

        // Инициализация всех канв
        initFabricCanvas('graphicCanvas1', 'graphicImageInput1', 'graphicColorPicker1');
        initFabricCanvas('mentalCanvas1', 'mentalImageInput1', 'mentalColorPicker1');
        initFabricCanvas('blockDiagramCanvas1', null, null);

        initFabricCanvas('graphicCanvas2', 'graphicImageInput2', 'graphicColorPicker2');
        initFabricCanvas('mentalCanvas2', 'mentalImageInput2', 'mentalColorPicker2');
        initFabricCanvas('blockDiagramCanvas2', null, null);

        // Добавьте больше инициализаций по аналогии
    </script>
</body>
</html>
