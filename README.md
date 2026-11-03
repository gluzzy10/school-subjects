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
            --text: #fff;
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
        header { margin-bottom: 35px; text-align: center; }
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
        .subtitle { margin-top: 10px; color: var(--text-muted); font-size: 1.1rem; }
        .subject-nav {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 12px;
            margin-bottom: 30px;
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
        .nav-btn:hover, .nav-btn.active {
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
        .task-text { margin-bottom: 25px; font-size: 1.2rem; line-height: 1.7; }
        .options-grid { display: flex; flex-direction: column; gap: 12px; margin-bottom: 25px; }
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
        .option-item:hover { transform: translateX(5px); border-color: #444477; background: #1c1c3d; }
        .option-item.selected { border-color: var(--accent); background: rgba(0, 242, 254, 0.08); }
        .radio-circle { position: relative; flex: 0 0 20px; width: 20px; height: 20px; border: 2px solid #666688; border-radius: 50%; }
        .option-item.selected .radio-circle { border-color: var(--accent); }
        .option-item.selected .radio-circle::after {
            position: absolute;
            top: 50%; left: 50%;
            width: 10px; height: 10px;
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
        }
        .result-panel { display: none; margin-top: 25px; padding: 22px; border-radius: 16px; }
        .result-panel.success { border: 1px solid var(--success); background: rgba(0, 255, 135, 0.1); color: #d1ffd6; }
        .result-panel.error { border: 1px solid var(--error); background: rgba(254, 8, 81, 0.1); color: #ffcbd7; }
        .result-panel h3 { margin-top: 0; }
        .explanation { margin-top: 15px; padding-top: 15px; border-top: 1px solid rgba(255,255,255,.12); color: #d0d0e0; font-size: 1rem; line-height: 1.6; }
        @media (max-width: 520px) {
            .task-header { flex-direction: column; }
            .nav-btn { padding: 11px 15px; }
            .btn-check { width: 100%; }
        }
        @media (prefers-reduced-motion: reduce) {
            *, *::before, *::after { scroll-behavior: auto !important; animation-duration: .01ms !important; animation-iteration-count: 1 !important; transition-duration: .01ms !important; }
        }
    </style>
</head>
<body>
    <header>
        <h1>SciTech PRO</h1>
        <div class="subtitle">Задания максимального олимпиадного уровня по шести школьным предметам</div>
    </header>
    <nav class="subject-nav" aria-label="Выбор школьного предмета">
        <button class="nav-btn active" type="button" data-subject="math">Математика</button>
        <button class="nav-btn" type="button" data-subject="physics">Физика</button>
        <button class="nav-btn" type="button" data-subject="chemistry">Химия</button>
        <button class="nav-btn" type="button" data-subject="biology">Биология</button>
        <button class="nav-btn" type="button" data-subject="geography">География</button>
        <button class="nav-btn" type="button" data-subject="history">История</button>
    </nav>
    <main class="main-box" id="game-container" aria-live="polite"></main>
    <script>
        const tasks = {
            math: {
                level: "Уровень: олимпиадный максимум",
                topic: "Алгебра / логарифмы и параметр",
                text: `Найдите количество целых значений параметра <b>a</b>, при которых уравнение<br><b>log₃(x⁴ − 4x² + a) = log₃(2x² − 2x)</b><br>имеет ровно три различных вещественных корня.`,
                options: ["1 значение", "2 значения", "3 значения", "Таких значений нет"],
                correct: 0,
                explain: `Область определения: 2x² − 2x &gt; 0, то есть x &lt; 0 или x &gt; 1. При равных основаниях аргументы равны, откуда a = f(x) = −x⁴ + 6x² − 2x. На x &lt; 0 функция сначала возрастает, затем убывает к f(0)=0; её максимум больше 3. Поэтому при a=3 есть два корня на x&lt;0. На x&gt;1 функция начинается со значения f(1)=3 (точка x=1 исключена), сначала возрастает выше 3, затем убывает до −∞; при a=3 имеется ровно один корень x&gt;1. Итого при a=3 ровно три корня. При целых a&lt;3 суммарно не набирается три корня, а при a&gt;3 число корней не равно трём. Подходит только одно целое значение: a=3.`
            },
            physics: {
                level: "Уровень: олимпиадный максимум",
                topic: "Термодинамика / первый закон",
                text: `Одноатомный идеальный газ медленно нагревают в цилиндре с теплоизолированными стенками под поршнем без трения. Внешнее давление постоянно, а поршень не меняет массу. Какая доля переданного газу количества теплоты Q идёт на работу расширения?`,
                options: ["Всё тепло", "2/3 от Q", "2/5 от Q", "1/4 от Q"],
                correct: 2,
                explain: `Давление газа постоянно, поэтому процесс изобарный. Для одноатомного идеального газа ΔU=(3/2)nRΔT, а работа A=nRΔT. По первому закону Q=ΔU+A=(5/2)nRΔT, следовательно A/Q=2/5.`
            },
            chemistry: {
                level: "Уровень: олимпиадный максимум",
                topic: "Неорганическая химия / стехиометрия",
                text: `Смесь нитратов магния и серебра полностью разложили при нагревании. Объём выделившихся газов оказался в 11/9 раза больше, чем при разложении такого же общего количества вещества (в молях) чистого нитрата серебра. Каково молярное соотношение Mg(NO₃)₂ : AgNO₃ в исходной смеси?`,
                options: ["1 : 1", "1 : 2", "2 : 3", "3 : 1"],
                correct: 1,
                explain: `Уравнения: 2Mg(NO₃)₂ → 2MgO + 4NO₂ + O₂ и 2AgNO₃ → 2Ag + 2NO₂ + O₂. Один моль Mg(NO₃)₂ даёт 2,5 моль газа, один моль AgNO₃ — 1,5 моль. Пусть в смеси x и y моль соответственно. Тогда (2,5x+1,5y)/(1,5(x+y))=11/9. После сокращения: 15x+9y=11x+11y, поэтому 4x=2y и x:y=1:2.`
            },
            biology: {
                level: "Уровень: олимпиадный максимум",
                topic: "Генетика / анализ сцепления генов",
                text: `Проведено анализирующее скрещивание особи с генотипом <b>ABC/abc</b> с тройным рецессивным тестером. Среди 1000 потомков получены классы: ABC — 360, abc — 340, Abc — 80, aBC — 70, ABc — 60, abC — 50, AbC — 20, aBc — 20. Определите порядок генов, расстояния между соседними генами и интерференцию.`,
                options: ["A–B–C; 19 и 15 сМ; интерференция −0,40", "A–C–B; 15 и 19 сМ; интерференция 0,30", "B–A–C; 19 и 15 сМ; интерференция 0,40", "A–B–C; 15 и 19 сМ; интерференция −0,40"],
                correct: 0,
                explain: `Наиболее частые классы ABC и abc — родительские, наименее частые AbC и aBc — двойные кроссоверы. Сравнение показывает, что средний ген — B, то есть порядок A–B–C. Для участка A–B рекомбинантны Abc, aBC и оба класса двойного кроссовера: (80+70+20+20)/1000=0,19, или 19 сМ. Для B–C: (60+50+20+20)/1000=0,15, или 15 сМ. Ожидаемая доля двойных кроссоверов при независимости равна 0,19×0,15=0,0285, то есть 28,5. Наблюдается 40. Коэффициент совпадения 40/28,5≈1,40; интерференция I=1−1,40≈−0,40.`
            },
            geography: {
                level: "Уровень: олимпиадный максимум",
                topic: "Физическая география / водный баланс",
                text: `Площадь речного бассейна — 45 000 км². За год выпадает 820 мм осадков, фактическое испарение равно 470 мм, запас воды в бассейне увеличивается на 30 мм, а подземный сток за пределы бассейна эквивалентен слою 40 мм. Считая год равным 365 суткам, найдите средний годовой расход реки. Округлите до целых м³/с.`,
                options: ["300 м³/с", "400 м³/с", "440 м³/с", "520 м³/с"],
                correct: 1,
                explain: `По водному балансу слой речного стока равен 820−470−30−40=280 мм=0,28 м. Объём стока: 0,28×45 000 км²=0,28×45×10⁹ м²=12,6×10⁹ м³. В году 31 536 000 секунд, поэтому средний расход Q=12,6×10⁹/31 536 000≈399,5 м³/с, то есть 400 м³/с.`
            },
            history: {
                level: "Уровень: олимпиадный максимум",
                topic: "История России / реформы 1905–1906 гг.",
                text: `Какое утверждение наиболее точно описывает соотношение Манифеста 17 октября 1905 года и Основных государственных законов Российской империи, изданных 23 апреля 1906 года?`,
                options: [
                    "Манифест ввёл парламентский суверенитет, а Основные законы закрепили ответственность правительства перед Думой.",
                    "Манифест провозгласил гражданские свободы и участие Думы в законодательстве; Основные законы закрепили эти положения, сохранив значительные полномочия императора.",
                    "Основные законы отменили Государственную думу и полностью восстановили порядок управления, существовавший до 1905 года.",
                    "Манифест передал законодательную власть Государственному совету, а Основные законы сделали Думу исключительно совещательным органом."
                ],
                correct: 1,
                explain: `Манифест 17 октября обещал гражданские свободы и установил, что законы не должны приниматься без одобрения Государственной думы. Основные государственные законы не установили парламентское верховенство и ответственность министров перед Думой: император сохранял исполнительную власть, право назначать министров, созывать и распускать Думу, а также право вето. Законодательная процедура включала Думу, Государственный совет и утверждение императором. Поэтому верен второй вариант.`
            }
        };

        let activeSubject = "math";
        let selectedIndex = null;
        const gameContainer = document.getElementById("game-container");

        document.querySelectorAll(".nav-btn").forEach((button) => {
            button.addEventListener("click", () => {
                activeSubject = button.dataset.subject;
                selectedIndex = null;
                document.querySelectorAll(".nav-btn").forEach((item) => item.classList.toggle("active", item === button));
                renderCard();
            });
        });

        function renderCard() {
            const data = tasks[activeSubject];
            const optionsHTML = data.options.map((option, index) => `
                <button class="option-item" type="button" aria-pressed="false" data-option="${index}">
                    <span class="radio-circle" aria-hidden="true"></span><span>${option}</span>
                </button>
            `).join("");
            gameContainer.innerHTML = `
                <div class="task-header"><span>${data.topic}</span><span>${data.level}</span></div>
                <div class="task-text">${data.text}</div>
                <div class="options-grid">${optionsHTML}</div>
                <button class="btn-check" type="button">Проверить ответ</button>
                <div class="result-panel" role="status" aria-live="polite"></div>
            `;
            gameContainer.querySelectorAll(".option-item").forEach((button) => {
                button.addEventListener("click", () => chooseOption(Number(button.dataset.option)));
            });
            gameContainer.querySelector(".btn-check").addEventListener("click", checkAnswer);
        }

        function chooseOption(index) {
            selectedIndex = index;
            gameContainer.querySelectorAll(".option-item").forEach((item, itemIndex) => {
                const isSelected = itemIndex === index;
                item.classList.toggle("selected", isSelected);
                item.setAttribute("aria-pressed", String(isSelected));
            });
        }

        function checkAnswer() {
            if (selectedIndex === null) {
                window.alert("Сначала выберите вариант ответа.");
                return;
            }
            const data = tasks[activeSubject];
            const panel = gameContainer.querySelector(".result-panel");
            const isCorrect = selectedIndex === data.correct;
            panel.className = `result-panel ${isCorrect ? "success" : "error"}`;
            panel.innerHTML = `
                <h3>${isCorrect ? "🔥 Отлично! Ответ верный" : "❌ Ответ неверный"}</h3>
                ${isCorrect ? "<p>Задача максимального уровня сложности решена.</p>" : `<p>Правильный ответ: <b>${data.options[data.correct]}</b></p>`}
                <div class="explanation"><b>Разбор:</b><br>${data.explain}</div>
            `;
            panel.style.display = "block";
        }

        renderCard();
    </script>
</body>
</html>
