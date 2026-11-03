# school-subjects
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>SciTech PRO — школьный тренажёр</title>
    <style>
        :root {
            --bg: #070b14;
            --bg-2: #101828;
            --panel: rgba(18, 24, 41, 0.82);
            --panel-strong: rgba(12, 18, 30, 0.92);
            --accent: #5ee7ff;
            --accent-2: #7c6cff;
            --success: #54f3a7;
            --error: #ff5f7a;
            --text: #edf6ff;
            --text-muted: #a7b2c8;
            --border: rgba(255,255,255,0.08);
            --shadow: rgba(94, 231, 255, 0.22);
        }

        * { box-sizing: border-box; }

        html { scroll-behavior: smooth; }

        body {
            position: relative;
            min-height: 100vh;
            margin: 0;
            padding: 26px 18px 50px;
            display: flex;
            flex-direction: column;
            align-items: center;
            background:
                radial-gradient(circle at top left, rgba(124,108,255,0.18), transparent 26%),
                radial-gradient(circle at bottom right, rgba(94,231,255,0.15), transparent 28%),
                linear-gradient(135deg, var(--bg), var(--bg-2));
            color: var(--text);
            font-family: "Segoe UI", system-ui, -apple-system, sans-serif;
            overflow-x: hidden;
        }

        body::before,
        body::after {
            content: "";
            position: fixed;
            inset: auto;
            width: 520px;
            height: 520px;
            border-radius: 50%;
            filter: blur(70px);
            opacity: 0.25;
            pointer-events: none;
            z-index: 0;
        }

        body::before {
            top: -140px;
            left: -120px;
            background: rgba(124, 108, 255, 0.7);
            animation: drift 16s ease-in-out infinite alternate;
        }

        body::after {
            right: -150px;
            bottom: -180px;
            background: rgba(94, 231, 255, 0.7);
            animation: drift 19s ease-in-out infinite alternate-reverse;
        }

        @keyframes drift {
            0%   { transform: translate(0, 0) scale(1); }
            100% { transform: translate(40px, 30px) scale(1.2); }
        }

        header,
        .subject-nav,
        .main-box {
            position: relative;
            z-index: 1;
        }

        header {
            margin-bottom: 28px;
            text-align: center;
            animation: fadeDown 0.9s cubic-bezier(.2,.8,.2,1) both;
        }

        h1 {
            margin: 0;
            font-size: clamp(2.1rem, 6vw, 3.5rem);
            letter-spacing: 2px;
            text-transform: uppercase;
            background: linear-gradient(90deg, #5ee7ff, #7c6cff, #8ef0d1);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 0 22px rgba(94, 231, 255, 0.35);
        }

        .subtitle {
            margin-top: 10px;
            color: var(--text-muted);
            font-size: 1.08rem;
            letter-spacing: 0.04em;
        }

        .subject-nav {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 12px;
            margin-bottom: 26px;
            animation: fadeIn 1s ease both;
        }

        .nav-btn {
            position: relative;
            padding: 13px 22px;
            border: 1px solid rgba(255,255,255,0.08);
            border-radius: 14px;
            background: rgba(19, 25, 38, 0.8);
            color: var(--text);
            font: inherit;
            font-weight: 700;
            letter-spacing: 0.02em;
            cursor: pointer;
            transition: transform 0.25s ease, box-shadow 0.25s ease, border-color 0.25s ease, background 0.25s ease;
            box-shadow: inset 0 0 0 1px rgba(255,255,255,0.03);
        }

        .nav-btn:hover,
        .nav-btn.active {
            transform: translateY(-3px) scale(1.02);
            border-color: rgba(94, 231, 255, 0.7);
            background: rgba(22, 35, 52, 0.9);
            box-shadow: 0 10px 24px rgba(94, 231, 255, 0.12), 0 0 20px rgba(94, 231, 255, 0.18);
            color: var(--accent);
        }

        .main-box {
            width: min(100%, 840px);
            padding: clamp(22px, 4vw, 40px);
            border: 1px solid var(--border);
            border-radius: 28px;
            background: linear-gradient(180deg, rgba(17, 24, 39, 0.9), rgba(12, 18, 30, 0.95));
            box-shadow: 0 24px 70px rgba(2, 6, 15, 0.72), inset 0 0 0 1px rgba(255,255,255,0.02);
            backdrop-filter: blur(10px);
            animation: riseIn 0.7s cubic-bezier(.2,.8,.2,1) both;
        }

        @keyframes riseIn {
            from { opacity: 0; transform: translateY(18px) scale(0.985); }
            to { opacity: 1; transform: translateY(0) scale(1); }
        }

        @keyframes fadeDown {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .task-header {
            display: flex;
            justify-content: space-between;
            gap: 14px;
            margin-bottom: 18px;
            padding-bottom: 16px;
            border-bottom: 1px solid rgba(255,255,255,0.08);
            color: var(--text-muted);
            font-size: 0.82rem;
            letter-spacing: 0.12em;
            text-transform: uppercase;
        }

        .task-text {
            margin-bottom: 24px;
            font-size: clamp(1.08rem, 2vw, 1.3rem);
            line-height: 1.75;
            color: var(--text);
        }

        .options-grid {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 24px;
        }

        .option-item {
            display: flex;
            align-items: center;
            gap: 14px;
            width: 100%;
            padding: 16px 18px;
            border: 1px solid rgba(255,255,255,0.08);
            border-radius: 16px;
            background: rgba(255,255,255,0.02);
            color: var(--text);
            font: inherit;
            font-size: 1.03rem;
            text-align: left;
            cursor: pointer;
            transition: transform 0.2s ease, border-color 0.2s ease, background 0.2s ease, box-shadow 0.2s ease;
        }

        .option-item:hover {
            transform: translateX(4px);
            border-color: rgba(255,255,255,0.15);
            background: rgba(255,255,255,0.04);
        }

        .option-item.selected {
            border-color: rgba(94, 231, 255, 0.9);
            background: rgba(94, 231, 255, 0.08);
            box-shadow: 0 0 0 1px rgba(94, 231, 255, 0.18), 0 12px 24px rgba(94, 231, 255, 0.08);
            animation: pulseSelect 0.35s ease;
        }

        @keyframes pulseSelect {
            0% { transform: scale(0.99); }
            50% { transform: scale(1.01); }
            100% { transform: scale(1); }
        }

        .radio-circle {
            position: relative;
            flex: 0 0 20px;
            width: 20px;
            height: 20px;
            border: 2px solid rgba(255,255,255,0.4);
            border-radius: 50%;
            background: transparent;
        }

        .option-item.selected .radio-circle {
            border-color: var(--accent);
            box-shadow: 0 0 14px rgba(94, 231, 255, 0.25);
        }

        .option-item.selected .radio-circle::after {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--accent), var(--accent-2));
            content: "";
            transform: translate(-50%, -50%);
        }

        .btn-check {
            padding: 15px 32px;
            border: none;
            border-radius: 14px;
            background: linear-gradient(135deg, var(--accent), var(--accent-2));
            color: #081018;
            font: inherit;
            font-size: 1.03rem;
            font-weight: 800;
            letter-spacing: 0.02em;
            cursor: pointer;
            box-shadow: 0 12px 30px rgba(124, 108, 255, 0.28);
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }

        .btn-check:hover {
            transform: translateY(-2px) scale(1.01);
            box-shadow: 0 18px 36px rgba(94, 231, 255, 0.25);
        }

        .result-panel {
            display: none;
            margin-top: 24px;
            padding: 22px 20px;
            border-radius: 18px;
            border: 1px solid rgba(255,255,255,0.08);
            background: rgba(255,255,255,0.02);
            animation: panelSlide 0.35s ease both;
        }

        @keyframes panelSlide {
            from { opacity: 0; transform: translateY(12px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .result-panel.success {
            border-color: rgba(84, 243, 167, 0.5);
            background: rgba(84, 243, 167, 0.08);
            color: #dffef1;
        }

        .result-panel.error {
            border-color: rgba(255, 95, 122, 0.5);
            background: rgba(255, 95, 122, 0.08);
            color: #ffe3ea;
        }

        .result-panel h3 {
            margin: 0 0 8px;
            font-size: 1.2rem;
        }

        .result-panel p {
            margin: 0 0 10px;
            color: inherit;
        }

        .explanation {
            margin-top: 12px;
            padding-top: 12px;
            border-top: 1px solid rgba(255,255,255,0.1);
            line-height: 1.7;
            color: inherit;
        }

        @media (max-width: 520px) {
            body { padding-top: 18px; }
            .task-header { flex-direction: column; }
            .nav-btn { padding: 11px 16px; }
            .btn-check { width: 100%; }
        }

        @media (prefers-reduced-motion: reduce) {
            *, *::before, *::after {
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
        <div class="subtitle">Интерактивные задания максимального уровня по шести школьным предметам</div>
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
                text: `
                    Найдите количество целых значений параметра <b>a</b>,
                    при которых уравнение<br>
                    <b>log₃(x⁴ − 4x² + a) = log₃(2x² − 2x)</b><br>
                    имеет ровно три различных вещественных корня.
                `,
                options: ["1 значение", "2 значения", "3 значения", "Таких значений нет"],
                correct: 2,
                explain: `
                    Область определения: <b>2x² − 2x &gt; 0</b>, то есть <b>x &lt; 0</b> или <b>x &gt; 1</b>.
                    При равных основаниях логарифмов аргументы равны:
                    <b>x⁴ − 4x² + a = 2x² − 2x</b>, следовательно <b>a = −x⁴ + 6x² − 2x</b>.
                    Функция <b>f(x) = −x⁴ + 6x² − 2x</b> на промежутках <b>x &lt; 0</b> и <b>x &gt; 1</b>
                    имеет максимум, равный 3, и только при <b>a = 3</b> число пересечений с прямой <b>y = a</b>
                    даёт ровно три корня. Для остальных целых значений число корней не равно трём.
                    Значит, подходит ровно <b>3</b> целых значения параметра.
                `
            },
            physics: {
                level: "Уровень: олимпиадный максимум",
                topic: "Термодинамика / первый закон",
                text: `
                    Одноатомный идеальный газ медленно нагревают в цилиндре
                    с теплоизолированными стенками под поршнем без трения.
                    Внешнее давление постоянно. Какая доля переданного газу тепла Q
                    идёт на работу расширения?
                `,
                options: ["Всё тепло", "2/3 от Q", "2/5 от Q", "1/4 от Q"],
                correct: 2,
                explain: `
                    При постоянном внешнем давлении процесс изобарный.
                    Для одноатомного идеального газа изменение внутренней энергии:
                    <b>ΔU = (3/2)nRΔT</b>, работа газа: <b>A = nRΔT</b>.
                    По первому закону термодинамики:
                    <b>Q = ΔU + A = (5/2)nRΔT</b>.
                    Следовательно, <b>A/Q = 2/5</b>.
                `
            },
            chemistry: {
                level: "Уровень: олимпиадный максимум",
                topic: "Неорганическая химия / стехиометрия",
                text: `
                    Смесь нитратов магния и серебра полностью разложили при нагревании.
                    Объём выделившихся газов оказался в <b>11/9</b> раза больше,
                    чем при разложении такого же общего количества вещества (в молях)
                    чистого нитрата серебра. Каково молярное соотношение
                    <b>Mg(NO₃)₂ : AgNO₃</b> в исходной смеси?
                `,
                options: ["1 : 1", "1 : 2", "2 : 3", "3 : 1"],
                correct: 1,
                explain: `
                    Уравнения разложения:
                    <b>2Mg(NO₃)₂ → 2MgO + 4NO₂ + O₂</b>,
                    <b>2AgNO₃ → 2Ag + 2NO₂ + O₂</b>.
                    Один моль <b>Mg(NO₃)₂</b> даёт <b>2,5</b> моль газа,
                    а один моль <b>AgNO₃</b> — <b>1,5</b> моль газа.
                    Пусть в смеси <b>x</b> моль Mg(NO₃)₂ и <b>y</b> моль AgNO₃.
                    Тогда
                    <b>(2,5x + 1,5y) / (1,5(x + y)) = 11/9</b>.
                    Это даёт <b>15x + 9y = 11x + 11y</b>, то есть
                    <b>4x = 2y</b>, следовательно <b>x : y = 1 : 2</b>.
                `
            },
            biology: {
                level: "Уровень: олимпиадный максимум",
                topic: "Генетика / анализ сцепления генов",
                text: `
                    Проведено анализирующее скрещивание особи с генотипом
                    <b>ABC/abc</b> с тройным рецессивным тестером.
                    Среди 1000 потомков получены классы:
                    ABC — 360, abc — 340, Abc — 80,
                    aBC — 70, ABc — 60, abC — 50,
                    AbC — 20, aBc — 20.
                    Определите порядок генов, расстояния между соседними генами
                    и коэффициент интерференции.
                `,
                options: [
                    "A–B–C; 19 и 15 сМ; интерференция −0,40",
                    "A–C–B; 15 и 19 сМ; интерференция 0,30",
                    "B–A–C; 19 и 15 сМ; интерференция 0,40",
                    "A–B–C; 15 и 19 сМ; интерференция −0,40"
                ],
                correct: 0,
                explain: `
                    Наиболее частые классы <b>ABC</b> и <b>abc</b> — родительские.
                    Наименее частые <b>AbC</b> и <b>aBc</b> — двойные кроссоверы.
                    Сравнение показывает, что средний ген — <b>B</b>, поэтому порядок генов:
                    <b>A–B–C</b>.
                    Для участка A–B рекомбинантны классы Abc, aBC и оба класса двойного кроссовера:
                    <b>(80 + 70 + 20 + 20)/1000 = 0,19</b>, то есть <b>19 сМ</b>.
                    Для участка B–C:
                    <b>(60 + 50 + 20 + 20)/1000 = 0,15</b>, то есть <b>15 сМ</b>.
                    Ожидаемая доля двойных кроссоверов при независимости:
                    <b>0,19 × 0,15 = 0,0285</b>.
                    Наблюдаемая доля: <b>40/1000 = 0,04</b>.
                    Коэффициент совпадения:
                    <b>0,04 / 0,0285 ≈ 1,40</b>.
                    Интерференция: <b>I = 1 − 1,40 = −0,40</b>.
                `
            },
            geography: {
                level: "Уровень: олимпиадный максимум",
                topic: "Физическая география / водный баланс",
                text: `
                    Площадь речного бассейна составляет <b>45 000 км²</b>.
                    За год выпадает <b>820 мм</b> осадков, фактическое испарение равно <b>470 мм</b>,
                    запас воды в бассейне увеличивается на <b>30 мм</b>, а подземный сток
                    за пределы бассейна эквивалентен слою <b>40 мм</b>.
                    Считая год равным <b>365</b> суткам, найдите средний годовой расход реки.
                    Округлите до целых <b>м³/с</b>.
                `,
                options: ["300 м³/с", "400 м³/с", "440 м³/с", "520 м³/с"],
                correct: 1,
                explain: `
                    По уравнению водного баланса слой речного стока равен:
                    <b>820 − 470 − 30 − 40 = 280 мм = 0,28 м</b>.
                    Объём стока:
                    <b>0,28 × 45 000 км² = 0,28 × 45 × 10⁹ = 12,6 × 10⁹ м³</b>.
                    В году:
                    <b>365 × 24 × 3600 = 31 536 000 с</b>.
                    Средний расход:
                    <b>Q = 12,6 × 10⁹ / 31 536 000 ≈ 399,5 м³/с</b>.
                    Округление даёт <b>400 м³/с</b>.
                `
            },
            history: {
                level: "Уровень: олимпиадный максимум",
                topic: "История России / реформы 1905–1906 гг.",
                text: `
                    Какое утверждение наиболее точно описывает соотношение
                    Манифеста 17 октября 1905 года и Основных государственных законов
                    Российской империи, изданных 23 апреля 1906 года?
                `,
                options: [
                    "Манифест ввёл парламентский суверенитет, а Основные законы закрепили ответственность правительства перед Думой.",
                    "Манифест провозгласил гражданские свободы и участие Думы в законодательстве; Основные законы закрепили эти положения, сохранив значительные полномочия императора.",
                    "Основные законы отменили Государственную думу и полностью восстановили порядок управления, существовавший до 1905 года.",
                    "Манифест передал законодательную власть Государственному совету, а Основные законы сделали Думу исключительно совещательным органом."
                ],
                correct: 1,
                explain: `
                    Манифест 17 октября обещал гражданские свободы и установил,
                    что законы не должны приниматься без одобрения Государственной думы.
                    Однако Основные государственные законы не создавали парламентскую монархию
                    в современном смысле: император сохранял исполнительную власть,
                    право назначать министров, созывать и распускать Думу,
                    а также право вето. Законодательная процедура включала Государственную думу,
                    Государственный совет и утверждение императором.
                    Поэтому верен именно второй вариант.
                `
            }
        };

        let activeSubject = "math";
        let selectedIndex = null;
        const gameContainer = document.getElementById("game-container");

        document.querySelectorAll(".nav-btn").forEach((button) => {
            button.addEventListener("click", () => {
                activeSubject = button.dataset.subject;
                selectedIndex = null;
                document.querySelectorAll(".nav-btn").forEach((item) => {
                    item.classList.toggle("active", item === button);
                });
                renderCard();
            });
        });

        function renderCard() {
            const data = tasks[activeSubject];
            const optionsHTML = data.options.map((option, index) => `
                <button class="option-item" type="button" aria-pressed="false" data-option="${index}">
                    <span class="radio-circle" aria-hidden="true"></span>
                    <span>${option}</span>
                </button>
            `).join("");

            gameContainer.innerHTML = `
                <div class="task-header">
                    <span>${data.topic}</span>
                    <span>${data.level}</span>
                </div>
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
                ${isCorrect ? "<p>Вы решили задачу на максимальном уровне сложности.</p>" : `<p>Правильный ответ: <b>${data.options[data.correct]}</b></p>`}
                <div class="explanation"><b>Разбор:</b><br>${data.explain}</div>
            `;
            panel.style.display = "block";
        }

        renderCard();
    </script>
</body>
</html>
