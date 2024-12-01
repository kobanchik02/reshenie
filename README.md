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
            width: 100%;
            height: 100%;
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
            </div>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/fabric.js/4.6.0/fabric.min.js"></script>
    <script>
        function toggleTable(id) {
            const table = document.getElementById(id);
            table.style.display = table.style.display === 'none' ? 'flex' : 'none';
        }

        // Инициализация Fabric.js для рисования
        function initFabricCanvas(canvasId, imageInputId) {
            const canvas = new fabric.Canvas(canvasId);
            const imageInput = document.getElementById(imageInputId);

            imageInput.addEventListener('change', (e) => {
                const file = e.target.files[0];
                if (file) {
                    const reader = new FileReader();
                    reader.onload = (event) => {
                        fabric.Image.fromURL(event.target.result, (img) => {
                            img.set({
                                left: 50,
                                top: 50,
                                scaleX: 0.5,
                                scaleY: 0.5,
                                selectable: true,
                                hasControls: true,
                                hasBorders: true
                            });
                            canvas.add(img);
                            canvas.requestRenderAll();
                        });
                    };
                    reader.readAsDataURL(file);
                }
            });
        }

        // Инициализация канвы
        initFabricCanvas('graphicCanvas1', 'graphicImageInput1');
    </script>
</body>
</html>

