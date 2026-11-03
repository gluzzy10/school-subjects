# school-subjects
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SciTech PRO — школьный тренажёр</title>
    <style>
        :root {
            --bg: #0a0a12;
            --panel: #121224;
            --accent: #00f2fe;
            --accent-glow: rgba(0, 242, 254, 0.25);
            --text: #ffffff;
            --text-muted: #a0a0b8;
            --success: #00ff87;
            --error: #fe0851;
        }

        * { box-sizing: border-box; }

        body {
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            overflow-x: hidden;
            background: var(--bg);
            color: var(--text);
            font-family: "Segoe UI", system-ui, sans-serif;
        }

        header {
            margin-bottom: 35px;
            text-align: center;
            animation: fadeInDown 0.8s ease both;
        }

        h1 {
            margin: 0;
            font-size: clamp(2rem, 7vw, 3rem);
            letter-spacing: 2px;
            text-transform: uppercase;
            background: linear-gradient(45deg, #00f2fe, #4facfe);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            filter: drop-shadow(0 0 15px var(--accent-glow));
        }

        .subtitle {
            margin-top: 10px;
            color: var(--text-muted);
            font-size: 1.1rem;
        }

        .subject-nav {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 12px;
            margin-bottom: 30px;
            animation: fadeIn 1s ease both;
        }

        .nav-btn {
            padding: 13px 22px;
            border: 1px solid #222244;
            border-radius: 12px;
            background: var(--panel);
            color: var(--text);
            font: inherit;
            font-weight: 600;
            cursor: pointer;
            transition: 0.25s ease;
        }

        .nav-btn:hover,
        .nav-btn.active {
            transform: translateY(-3px);
            border-color: var(--accent);
            background: rgba(0, 242, 254, 0.05);
            box-shadow: 0 0 20px var(--accent-glow);
            color: var(--accent);
        }

        .main-box {
            width: min(100%, 800px);
            padding: clamp(22px, 5vw, 40px);
            border: 1px solid #1e1e38;
            border-radius: 24px;
            background: var(--panel);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4);
            animation: fadeInUp 0.6s ease both;
        }

        .task-header {
            display: flex;
            justify-content: space-between;
            gap: 12px;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #1e1e38;
            color: var(--text-muted);
            font-size: 0.85rem;
            letter-spacing: 1px;
            text-transform: uppercase;
        }

        .task-text {
            margin-bottom: 25px;
            font-size: 1.2rem;
            line-height: 1.7;
        }

        .options-grid {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 25px;
        }

        .option-item {
            display: flex;
            align-items: center;
            gap: 15px;
            width: 100%;
            padding: 16px 20px;
            border: 2px solid #222244;
            border-radius: 14px;
            background: #161630;
            color: var(--text);
            font: inherit;
            font-size: 1.05rem;
            text-align: left;
            cursor: pointer;
            transition: 0.2s ease;
        }

        .option-item:hover {
            transform: translateX(5px);
            border-color: #444477;
            background: #1c1c3d;
        }

        .option-item.selected {
            border-color: var(--accent);
            background: rgba(0, 242, 254, 0.08);
            box-shadow: 0 0 15px rgba(0, 242, 254, 0.15);
        }

        .radio-circle {
            position: relative;
            flex: 0 0 20px;
            width: 20px;
            height: 20px;
            border: 2px solid #666688;
            border-radius: 50%;
        }

        .option-item.selected .radio-circle { border-color: var(--accent); }

        .option-item.selected .radio-circle::after {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: var(--accent);
            content: "";
            transform: translate(-50%, -50%);
        }

        .btn-check {
            padding: 15px 32px;
            border: 0;
            border-radius: 12px;
            background: linear-gradient(135deg, #00f2fe, #4facfe);
            color: #000;
            font: inherit;
            font-size: 1.05rem;
            font-weight: 700;
            cursor: pointer;
            transition: 0.25s ease;
        }

        .btn-check:hover {
            transform: scale(1.02);
            box-shadow: 0 0 25px var(--accent-glow);
        }

        .result-panel {
            display: none;
            margin-top: 25px;
            padding: 22px;
            border-radius: 16px;
            animation: slideIn 0.4s ease both;
        }

        .result-panel.success {
            border: 1px solid var(--success);
            background: rgba(0, 255, 135, 0.1);
            color: #d1ffd6;
        }

        .result-panel.error {
            border: 1px solid var(--error);
            background: rgba(254, 8, 81, 0.1);
            color: #ffcbd7;
        }

        .result-panel h3 { margin-top: 0; }

        .explanation {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid rgba(255, 255, 255, 0.12);
            color: #d0d0e0;
            font-size: 1rem;
            line-height: 1.6;
        }

        @keyframes fadeInDown {
            from { opacity: 0; transform: translateY(-25px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(15px) scale(0.98); }
            to { opacity: 1; transform: translateY(0) scale(1); }
        }

        @media (max-width: 520px) {
            .task-header { flex-direction: column; }
            .nav-btn { padding: 11px 15px; }
            .btn-check { width: 100%; }
        }

        @media (prefers-reduced-motion: reduce) {
            *,
            *::before,
            *::after {
                scroll-behavior: auto !important;
                animation-duration: 0.01ms !important;
                animation-iteration-count: 1 !important;
                transition-duration: 0.01ms !important;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>SciTech PRO</h1>
        <div class="subtitle">
            Интерактивные задания олимпиадного уровня по шести школьным предметам
        </div>
    </header>

    <nav class="subject-nav" aria-label="Выбор школьного предмета">
        <button class="nav-btn active" type="button" onclick="selectSubject('math', this)">Математика</button>
        <button class="nav-btn" type="button" onclick="selectSubject('physics', this)">Физика</button>
        <button class="nav-btn" type="button" onclick="selectSubject('chemistry', this)">Химия</button>
        <button class="nav-btn" type="button" onclick="selectSubject('biology', this)">Биология</button>
        <button class="nav-btn" type="button" onclick="selectSubject('geography', this)">География</button>
        <button class="nav-btn" type="button" onclick="selectSubject('history', this)">История</button>
    </nav>

    <main class="main-box" id="game-container" aria-live="polite"></main>

    <script>
        const tasks = {
            math: {
                level: "Уровень: профильный",
                topic: "Алгебра / логарифмы",
                text: `
                    Укажите количество целых значений параметра <b>a</b>,
                    при которых уравнение<br>
                    <b>log₃(x⁴ − 4x² + a) = log₃(2x² − 2x)</b><br>
                    имеет ровно три различных вещественных корня.
                `,
                options: ["1 значение", "2 значения", "3 значения", "Таких значений нет"],
                correct: 2,
                explain: `
                    Область определения требует 2x² − 2x &gt; 0, то есть
                    x &lt; 0 или x &gt; 1. Так как логарифмы имеют одинаковое
                    основание, их аргументы равны. Получаем
                    a = −x⁴ + 6x² − 2x. На промежутке x &lt; 0 функция
                    достигает максимума примерно 12,6; на x &gt; 1 её максимум
                    примерно 5,7. Подсчёт пересечений на этих промежутках
                    показывает, что ровно три корня получаются при
                    a = 1, 2 и 3. Значит, подходят три целых значения.
                `
            },
            physics: {
                level: "Уровень: олимпиадный",
                topic: "Термодинамика",
                text: `
                    В вертикальном цилиндре с теплоизолированными стенками
                    находится одноатомный идеальный газ под подвижным поршнем.
                    Поршень движется без трения, а внешнее давление постоянно.
                    Газ медленно нагревают, сообщая ему количество теплоты Q.
                    Какая часть теплоты переходит в работу газа?
                `,
                options: ["Всё тепло", "2/3 от Q", "2/5 от Q", "1/4 от Q"],
                correct: 2,
                explain: `
                    Постоянное внешнее давление означает изобарный процесс.
                    Для одноатомного идеального газа изменение внутренней энергии
                    равно ΔU = (3/2)nRΔT, а работа газа — A = nRΔT.
                    По первому закону термодинамики Q = ΔU + A = (5/2)nRΔT.
                    Поэтому A/Q = 2/5.
                `
            },
            chemistry: {
                level: "Уровень: олимпиадный",
                topic: "Неорганическая химия / стехиометрия",
                text: `
                    Смесь нитрата магния и нитрата серебра полностью разложили
                    при нагревании. Объём выделившихся газов оказался в 11/9 раза
                    больше, чем при разложении такого же общего количества
                    вещества (в молях) чистого нитрата серебра.
                    Каково молярное соотношение нитрата магния и нитрата серебра
                    в исходной смеси?
                `,
                options: ["1 : 1", "1 : 2", "2 : 3", "3 : 1"],
                correct: 1,
                explain: `
                    Уравнения разложения:
                    2Mg(NO₃)₂ → 2MgO + 4NO₂ + O₂,
                    2AgNO₃ → 2Ag + 2NO₂ + O₂.
                    Один моль Mg(NO₃)₂ даёт 2,5 моль газа,
                    а один моль AgNO₃ — 1,5 моль газа.
                    Пусть в смеси x моль нитрата магния и y моль нитрата серебра.
                    Тогда отношение объёмов к газу от такого же количества
                    чистого AgNO₃ равно (2,5x + 1,5y) / (1,5(x + y)).
                    При x : y = 1 : 2 это отношение равно 11/9.
                `
            },
            biology: {
                level: "Уровень: олимпиадный максимум",
                topic: "Генетика / анализ сцепления генов",
                text: `
                    Проведено анализирующее скрещивание особи с генотипом
                    <b>ABC/abc</b> с тройным рецессивным тестером. Среди 1000
                    потомков обнаружено: ABC — 360, abc — 340, Abc — 80,
                    aBC — 70, ABc — 60, abC — 50, AbC — 20, aBc — 20.
                    Считая, что двойные кроссоверы учтены в частотах обеих
                    соседних пар, определите порядок генов, расстояния между
                    соседними генами и интерференцию.
                `,
                options: [
                    "A–B–C; 19 и 15 сМ; интерференция −0,40",
                    "A–C–B; 15 и 19 сМ; интерференция 0,30",
                    "B–A–C; 19 и 15 сМ; интерференция 0,40",
                    "A–B–C; 15 и 19 сМ; интерференция −0,40"
                ],
                correct: 0,
                explain: `
                    Наиболее частые классы ABC и abc — родительские, наименее
                    частые AbC и aBc — двойные кроссоверы. Сопоставление этих
                    классов показывает, что средний ген — B, поэтому порядок
                    A–B–C. Для участка A–B рекомбинантны Abc, aBC и оба класса
                    двойного кроссовера: (80 + 70 + 20 + 20)/1000 = 0,19,
                    то есть 19 сМ. Для B–C частота равна
                    (60 + 50 + 20 + 20)/1000 = 0,15, то есть 15 сМ.
                    Ожидаемая доля двойных кроссоверов при независимости
                    событий: 0,19 × 0,15 = 0,0285, или 28,5 особи.
                    Коэффициент совпадения = 40/28,5 ≈ 1,40; интерференция
                    I = 1 − 1,40 ≈ −0,40 (отрицательная интерференция).
                `
            },
            geography: {
                level: "Уровень: олимпиадный максимум",
                topic: "Физическая география / водный баланс",
                text: `
                    Площадь речного бассейна составляет 45 000 км². За год
                    выпадает 820 мм осадков, фактическое испарение равно 470 мм,
                    а запас воды в бассейне увеличивается на 30 мм. Кроме того,
                    за пределы бассейна подземным стоком уходит объём воды,
                    эквивалентный слою 40 мм. Считая год равным 365 суткам,
                    найдите средний годовой расход реки. Округлите до целых м³/с.
                `,
                options: ["300 м³/с", "400 м³/с", "440 м³/с", "520 м³/с"],
                correct: 1,
                explain: `
                    По уравнению водного баланса слой речного стока равен
                    820 − 470 − 30 − 40 = 280 мм = 0,28 м. Объём стока:
                    0,28 × 45 000 км² = 0,28 × 45 × 10⁹ м² = 12,6 × 10⁹ м³.
                    В году 31 536 000 секунд, поэтому средний расход
                    Q = 12,6 × 10⁹ / 31 536 000 ≈ 399,5 м³/с,
                    то есть 400 м³/с.
                `
            },
            history: {
                level: "Уровень: олимпиадный максимум",
                topic: "История России / политические реформы 1905–1906 гг.",
                text: `
                    Какое утверждение наиболее точно описывает соотношение
                    Манифеста 17 октября 1905 года и Основных государственных
                    законов Российской империи, изданных 23 апреля 1906 года?
                `,
                options: [
                    "Манифест ввёл парламентский суверенитет, а Основные законы лишь закрепили ответственное перед Думой правительство.",
                    "Манифест провозгласил гражданские свободы и участие Думы в законодательстве; Основные законы закрепили новые представительные процедуры, сохранив за императором широкие прерогативы.",
                    "Основные законы отменили Государственную думу и вернули порядок управления, существовавший до революции 1905 года.",
                    "Манифест передал законодательную власть Государственному совету, а Основные законы сделали Думу исключительно совещательным органом."
                ],
                correct: 1,
                explain: `
                    Манифест 17 октября обещал гражданские свободы и установил,
                    что законы не должны приниматься без одобрения Думы. Однако
                    Основные государственные законы не превращали Россию в
                    парламентскую монархию с верховенством парламента: император
                    сохранял исполнительную власть, право назначать министров,
                    созывать и распускать Думу, а также право вето. Законодательная
                    процедура включала Государственную думу, Государственный совет
                    и утверждение императором. Поэтому верен второй вариант.
                `
            }
        };

        let activeSubject = "math";
        let selectedIndex = null;

        function selectSubject(subject, button) {
            activeSubject = subject;
            selectedIndex = null;

            document.querySelectorAll(".nav-btn").forEach((item) => {
                item.classList.remove("active");
            });

            button.classList.add("active");
            renderCard();
        }

        function renderCard() {
            const data = tasks[activeSubject];
            const box = document.getElementById("game-container");

            const optionsHTML = data.options.map((option, index) => `
                <button
                    class="option-item"
                    type="button"
                    aria-pressed="false"
                    onclick="chooseOption(${index})"
                >
                    <span class="radio-circle" aria-hidden="true"></span>
                    <span>${option}</span>
                </button>
            `).join("");

            box.innerHTML = `
                <div class="task-header">
                    <span>${data.topic}</span>
                    <span>${data.level}</span>
                </div>
                <div class="task-text">${data.text}</div>
                <div class="options-grid" id="options-block">${optionsHTML}</div>
                <button class="btn-check" type="button" onclick="checkAnswer()">
                    Проверить ответ
                </button>
                <div class="result-panel" id="res-panel" role="status"></div>
            `;
        }

        function chooseOption(index) {
            selectedIndex = index;

            document.querySelectorAll(".option-item").forEach((item, itemIndex) => {
                const isSelected = itemIndex === index;
                item.classList.toggle("selected", isSelected);
                item.setAttribute("aria-pressed", String(isSelected));
            });
        }

        function checkAnswer() {
            if (selectedIndex === null) {
                alert("Сначала выберите вариант ответа.");
                return;
            }

            const data = tasks[activeSubject];
            const panel = document.getElementById("res-panel");
            const isCorrect = selectedIndex === data.correct;

            panel.className = `result-panel ${isCorrect ? "success" : "error"}`;

            if (isCorrect) {
                panel.innerHTML = `
                    <h3>🔥 Отлично! Ответ верный</h3>
                    <p>Вы решили задачу максимального уровня сложности.</p>
                    <div class="explanation">
                        <b>Разбор:</b><br>${data.explain}
                    </div>
                `;
            } else {
                panel.innerHTML = `
                    <h3>❌ Ответ неверный</h3>
                    <p>Посмотрите правильный ответ и разбор решения.</p>
                    <div class="explanation">
                        <b>Правильный ответ:</b> ${data.options[data.correct]}
                        <br><br>
                        <b>Разбор:</b><br>${data.explain}
                    </div>
                `;
            }

            panel.style.display = "block";
        }

        renderCard();
    </script>
</body>
</html>
