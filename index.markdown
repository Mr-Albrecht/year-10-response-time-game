---
layout: default
title: "Multiple Parsons Problems on One Page"
---

<!-- Roboto font -->
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">

<style>
  :root{
    --dc-bg: #0b1f3a;
    --dc-accent: #0ea5a5;
    --dc-accent-2: #7c9aff;
    --dc-muted: #f6f8fb;
    --dc-text: #1f2937;
    --dc-border: #e5e7eb;
    --radius: 16px;
    --shadow: 0 8px 24px rgba(16,24,40,.08);
  }

  html, body {
    font-family: "Roboto", system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial, "Noto Sans", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", sans-serif;
    color: var(--dc-text);
    background: var(--dc-muted);
    line-height: 1.65;
  }

  .dc-container { max-width: 1000px; margin: 40px auto 80px; padding: 0 20px; }

  .page-hero{
    background: linear-gradient(135deg, var(--dc-bg), #142a4f 60%, var(--dc-accent-2));
    color: #fff;
    border-radius: var(--radius);
    padding: 28px 28px 24px;
    box-shadow: var(--shadow);
    margin: 12px 0 28px;
    position: relative;
    overflow: hidden;
  }
  .page-hero:after{
    content: "";
    position: absolute;
    inset: -40px -40px auto auto;
    width: 240px; height: 240px;
    background: radial-gradient(closest-side, rgba(255,255,255,.18), transparent 70%);
    transform: rotate(12deg);
    pointer-events: none;
  }
  .page-hero h1{ margin: 0 0 6px 0; font-weight: 700; letter-spacing: .3px; }
  .page-hero p{ margin: 6px 0 0 0; opacity: .95; }
  .badge{
    display: inline-block; background: rgba(255,255,255,.16); color: #fff;
    border: 1px solid rgba(255,255,255,.22); padding: 6px 10px; font-size: 12px;
    border-radius: 999px; margin-bottom: 10px; letter-spacing: .3px;
  }

  h2{ font-size: 1.25rem; margin: 28px 0 8px; color: var(--dc-bg); letter-spacing: .2px; }
  .subtitle{ margin: 4px 0 12px; color: #475569; }

  .parsons-card{
    background: #fff; border: 1px solid var(--dc-border); border-radius: var(--radius);
    padding: 18px 18px 14px; margin: 14px 0 28px; box-shadow: var(--shadow);
  }
  .parsons-actions{ margin-top: 10px; display: flex; gap: 10px; flex-wrap: wrap; align-items: center; }

  input[type="button"]{
    appearance: none; border: 1px solid #cbd5e1; background: #fff; padding: 8px 14px;
    border-radius: 10px; cursor: pointer; font-weight: 500;
    transition: transform .05s ease, box-shadow .2s ease, border-color .2s ease, background .2s ease;
    box-shadow: 0 1px 0 rgba(0,0,0,.02);
  }
  input[type="button"]:hover{ border-color: var(--dc-accent); background: #f7fbfb; }
  input[type="button"]:active{ transform: translateY(1px); }
  .parsons-actions input[type="button"]:first-child{
    background: var(--dc-accent); color: #08343b; border-color: rgba(8,52,59,.2);
  }

  .sortable-code{
    background: #fafcff; border: 1px dashed #cbd5e1; border-radius: 12px;
    min-height: 120px; padding: 10px; margin-bottom: 10px;
  }
  .sortable-code li{
    background: #fff; border: 1px solid #e5e7eb; border-radius: 10px !important;
    padding: 8px 10px !important; margin: 6px 0 !important;
    box-shadow: 0 2px 8px rgba(17,24,39,.05);
    font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
    font-size: 14px;
  }

  .puzzle-grid{ display: grid; gap: 12px; }
  @media (min-width: 720px){
    .puzzle-grid{ grid-template-columns: 1fr 1fr; align-items: start; }
  }

  /* Clear, colour-coded feedback pills */
  .fb-pill{
    display:inline-flex; align-items:center; gap:8px; padding:6px 10px; border-radius:999px; font-size:12px; font-weight:600;
    border:1px solid;
  }
  .fb-ok{ background:#ecfdf5; color:#065f46; border-color:#a7f3d0; }
  .fb-bad{ background:#fef2f2; color:#991b1b; border-color:#fecaca; }
  .fb-neutral{ background:#eef2ff; color:#3730a3; border-color:#c7d2fe; }

  /* highlight wrong lines (common classes across js-parsons builds) */
  .sortable-code li.incorrect,
  .sortable-code li.ui-state-error,
  .sortable-code li.highlight-error,
  .sortable-code li.line-error,
  .sortable-code li.parsons-error{
    border-color:#ef4444 !important;
    box-shadow: 0 0 0 2px rgba(239,68,68,.15), 0 2px 8px rgba(17,24,39,.05);
  }
</style>

<!-- Shared feedback helper: MUST be defined before puzzles use it -->
<script>
  function attachParsonsFeedback(prefix, widget) {
    const sortableId = prefix + "-sortable";
    const badgeId    = prefix + "-feedbackBadge";
    const resetId    = prefix + "-newInstanceLink";
    const btnId      = prefix + "-feedbackLink";

    function scanWrongInDOM() {
      const cont = document.getElementById(sortableId);
      if (!cont) return 0;
      let wrong = 0;
      wrong += cont.querySelectorAll(
        "li.incorrect, li.ui-state-error, li.highlight-error, li.line-error, li.parsons-error"
      ).length;
      wrong += cont.querySelectorAll("li[title*='incorrect' i]").length;
      wrong += cont.querySelectorAll(
        "li[style*='rgb(255, 221, 221)'], li[style*='#ffdddd']"
      ).length;
      return wrong;
    }

    function renderBadge(count) {
      const badge = document.getElementById(badgeId);
      if (!badge) return;
      if (count === 0) {
        badge.className = "fb-pill fb-ok";
        badge.textContent = "✅ All correct!";
      } else {
        badge.className = "fb-pill fb-bad";
        badge.textContent =
          "❌ " + count + " issue" + (count > 1 ? "s" : "") + " to fix";
      }
      badge.style.display = "inline-flex";
    }

    const resetBtn = document.getElementById(resetId);
    if (resetBtn) {
      resetBtn.addEventListener("click", (e) => {
        e.preventDefault();
        widget.shuffleLines();
        const badge = document.getElementById(badgeId);
        if (badge) badge.style.display = "none";
      });
    }

    const fbBtn = document.getElementById(btnId);
    if (fbBtn) {
      fbBtn.addEventListener("click", (e) => {
        e.preventDefault();
        widget.getFeedback();            // let js-parsons mark lines
        setTimeout(() => {               // then we count them
          const wrong = scanWrongInDOM();
          renderBadge(wrong);
        }, 60);
      });
    }
  }

    function renderBadge(count) {
      const badge = document.getElementById(badgeId);
      if (!badge) return;
      if (count === 0) {
        badge.className = "fb-pill fb-ok";
        badge.textContent = "✅ All correct!";
      } else {
        badge.className = "fb-pill fb-bad";
        badge.textContent = "❌ " + count + " issue" + (count > 1 ? "s" : "") + " to fix";
      }
      badge.style.display = "inline-flex";
    }

    function updateBadgeFromResult(result) {
      let wrongCount = 0;

      if (Array.isArray(result)) {
        wrongCount = result.length;
      } else if (result && typeof result === "object") {
        if (Array.isArray(result.errors))       wrongCount = result.errors.length;
        else if (Array.isArray(result.feedback)) wrongCount = result.feedback.length;
        else if (typeof result.errorCount === "number") wrongCount = result.errorCount;
      } else if (typeof result === "string") {
        // crude heuristic: if result mentions "correct", assume 0; if "incorrect", assume some errors
        if (/incorrect/i.test(result)) wrongCount = 1;
        else wrongCount = 0;
      }

      // Fallback: if we still think there are 0 errors, check DOM highlights
      if (wrongCount === 0) {
        setTimeout(() => renderBadge(scanWrongInDOM()), 80);
      } else {
        renderBadge(wrongCount);
      }
    }

    const resetBtn = document.getElementById(resetId);
    if (resetBtn) {
      resetBtn.addEventListener("click", (e) => {
        e.preventDefault();
        widget.shuffleLines();
        const badge = document.getElementById(badgeId);
        if (badge) badge.style.display = "none";
      });
    }

    const fbBtn = document.getElementById(btnId);
    if (fbBtn) {
      fbBtn.addEventListener("click", (e) => {
        e.preventDefault();
        const result = widget.getFeedback();
        updateBadgeFromResult(result);
      });
    }
  }
</script>

<div class="dc-container">
  <div class="page-hero">
    <span class="badge">Mr Albrecht's Parsons Problems · GCSE Computer Science · Dulwich College</span>
    <h1>Parsons Practice</h1>
    <p>Drag code blocks to build working programs. Use <strong>Reset</strong> to reshuffle and <strong>Get Feedback</strong> to check your answer.</p>
  </div>

  <!-- 1. Reaction Time -->
  <div class="parsons-card">
    <h2>1. Basic Reaction Time Game</h2>
    <p class="subtitle">
      Waits a random delay, displays <strong>GO!</strong>, starts a timer, and measures how fast the user presses Enter.
    </p>
    <div class="puzzle-grid">
      <div id="ReactionGame-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 1"></div>
      <div id="ReactionGame-sortable" class="sortable-code" aria-label="Workspace for puzzle 1"></div>
    </div>
    <div class="parsons-actions">
      <input id="ReactionGame-feedbackLink" value="Get Feedback" type="button" />
      <input id="ReactionGame-newInstanceLink" value="Reset Problem" type="button" />
      <span id="ReactionGame-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback</span>
    </div>

    <script type="text/javascript">
    (function(){
      var initial =
        "import time\n" +
        "import random\n" +
        "print(\"Welcome to the Reaction Time Game!\")\n" +
        "print(\"When you see 'GO!', press Enter as fast as you can.\")\n" +
        "input(\"Press Enter to start...\")\n" +
        "wait_time = random.uniform(2, 5)\n" +
        "print(\"Get ready...\")\n" +
        "time.sleep(wait_time)\n" +
        "print(\"GO!\")\n" +
        "start_time = time.time()\n" +
        "input()\n" +
        "end_time = time.time()\n" +
        "reaction_time = end_time - start_time\n" +
        "print(f\\\"Your reaction time was {reaction_time:.3f} seconds!\\\")\n";

      var widget = new ParsonsWidget({
        sortableId: "ReactionGame-sortable",
        trashId: "ReactionGame-sortableTrash",
        max_wrong_lines: 10,
        grader: ParsonsWidget._graders.LineBasedGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        show_feedback: true
      });

      widget.init(initial);
      widget.shuffleLines();
      attachParsonsFeedback("ReactionGame", widget);
    })();
    </script>
  </div>

  <!-- 2. Temp Calculator -->
  <div class="parsons-card">
    <h2>2. Temperature Calculator (input + arithmetic)</h2>
    <p class="subtitle">
      Ask for a temperature in °C, convert it to °F, and print a simple message:
      freezing (≤ 0 °C), boiling (≥ 100 °C), or normal.
    </p>

    <div class="puzzle-grid">
      <div id="TempCalculator-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 2"></div>
      <div id="TempCalculator-sortable" class="sortable-code" aria-label="Workspace for puzzle 2"></div>
    </div>

    <div class="parsons-actions">
      <input id="TempCalculator-feedbackLink" value="Get Feedback" type="button" />
      <input id="TempCalculator-newInstanceLink" value="Reset Problem" type="button" />
      <span id="TempCalculator-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback</span>
    </div>

    <script type="text/javascript">
    (function(){
      var initial =
        "temp_c = float(input('Enter the temperature in °C: '))\n" +
        "temp_f = temp_c * 9 / 5 + 32\n" +
        "print('Temperature in Fahrenheit:', temp_f)\n" +
        "if temp_c <= 0:\n" +
        "    print('It is freezing.')\n" +
        "elif temp_c >= 100:\n" +
        "    print('It is boiling.')\n" +
        "else:\n" +
        "    print('It is a normal temperature.')\n" +
        "temp_k = temp_c + 273.15  #distractor\n";

      var widget = new ParsonsWidget({
        sortableId: "TempCalculator-sortable",
        trashId: "TempCalculator-sortableTrash",
        max_wrong_lines: 1,
        grader: ParsonsWidget._graders.LineBasedGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        show_feedback: true
      });

      widget.init(initial);
      widget.shuffleLines();
      attachParsonsFeedback("TempCalculator", widget);
    })();
    </script>
  </div>

  <!-- 3. Exam Grade -->
  <div class="parsons-card">
    <h2>3. Exam Grade Classifier (multi-branch selection)</h2>
    <p class="subtitle">
      Ask the user for their exam mark out of 100, then print the grade:<br>
      90 or more → <code>Grade: A</code>, 80–89 → <code>Grade: B</code>, 70–79 → <code>Grade: C</code>, below 70 → <code>Grade: D</code>.
    </p>

    <div class="puzzle-grid">
      <div id="ExamGrade-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 3"></div>
      <div id="ExamGrade-sortable" class="sortable-code" aria-label="Workspace for puzzle 3"></div>
    </div>

    <div class="parsons-actions">
      <input id="ExamGrade-feedbackLink" value="Get Feedback" type="button" />
      <input id="ExamGrade-newInstanceLink" value="Reset Problem" type="button" />
      <span id="ExamGrade-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback</span>
    </div>

    <script type="text/javascript">
    (function(){
      var initial =
        "mark = int(input('Enter your exam mark out of 100: '))\n" +
        "\n" +
        "if mark >= 90:\n" +
        "    print('Grade: A')\n" +
        "elif mark >= 80:\n" +
        "    print('Grade: B')\n" +
        "elif mark >= 70:\n" +
        "    print('Grade: C')\n" +
        "else:\n" +
        "    print('Grade: D')\n" +
        "elif mark > 75:  #distractor\n" +
        "elif mark >= 80  #distractor\n";

      var widget = new ParsonsWidget({
        sortableId: "ExamGrade-sortable",
        trashId: "ExamGrade-sortableTrash",
        max_wrong_lines: 2,
        grader: ParsonsWidget._graders.LineBasedGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        show_feedback: true
      });

      widget.init(initial);
      widget.shuffleLines();
      attachParsonsFeedback("ExamGrade", widget);
    })();
    </script>
  </div>

  <!-- 4. Rollercoaster -->
  <div class="parsons-card">
    <h2>4. Rollercoaster Ride Check (logical operators + validation)</h2>
    <p class="subtitle">
      Ask for height (cm) and age (years). If either is less than 0, print <code>Invalid input.</code><br>
      Otherwise, if height ≥ 120 and age ≥ 10, print <code>You can ride the rollercoaster!</code>, else<br>
      <code>Sorry, you are not allowed to ride.</code>
    </p>

    <div class="puzzle-grid">
      <div id="RollercoasterRide-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 4"></div>
      <div id="RollercoasterRide-sortable" class="sortable-code" aria-label="Workspace for puzzle 4"></div>
    </div>

    <div class="parsons-actions">
      <input id="RollercoasterRide-feedbackLink" value="Get Feedback" type="button" />
      <input id="RollercoasterRide-newInstanceLink" value="Reset Problem" type="button" />
      <span id="RollercoasterRide-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback</span>
    </div>

    <script type="text/javascript">
    (function(){
      var initial =
        "height = int(input('Enter your height in cm: '))\n" +
        "age = int(input('Enter your age in years: '))\n" +
        "\n" +
        "if height < 0 or age < 0:\n" +
        "    print('Invalid input.')\n" +
        "elif height >= 120 and age >= 10:\n" +
        "    print('You can ride the rollercoaster!')\n" +
        "else:\n" +
        "    print('Sorry, you are not allowed to ride.')\n" +
        "height = 0  #distractor\n" +
        "age = 0  #distractor\n" +
        "print('Welcome!')  #distractor\n";

      var widget = new ParsonsWidget({
        sortableId: "RollercoasterRide-sortable",
        trashId: "RollercoasterRide-sortableTrash",
        max_wrong_lines: 3,
        grader: ParsonsWidget._graders.LineBasedGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        show_feedback: true
      });

      widget.init(initial);
      widget.shuffleLines();
      attachParsonsFeedback("RollercoasterRide", widget);
    })();
    </script>
  </div>

  <!-- 5. Gaming Feedback -->
  <div class="parsons-card">
    <h2>5. Gaming Performance Feedback (mixed data types + conditions)</h2>
    <p class="subtitle">
      Ask for: player name, level (1–50), score (≥ 0), accuracy (0–100), and VIP (yes/no).<br>
      If any value impossible → <code>Invalid data entered.</code><br>
      Otherwise:
      VIP + score ≥ 50000 + accuracy ≥ 70 → <code>VIP bonus unlocked for &lt;name&gt;!</code><br>
      Else score ≥ 50000 + accuracy ≥ 70 → <code>Amazing performance, &lt;name&gt;!</code><br>
      Else score ≥ 20000 → <code>Good job, &lt;name&gt;. Keep grinding.</code><br>
      Else → <code>Keep practising, &lt;name&gt;.</code>
    </p>

    <div class="puzzle-grid">
      <div id="GamingFeedback-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 5"></div>
      <div id="GamingFeedback-sortable" class="sortable-code" aria-label="Workspace for puzzle 5"></div>
    </div>

    <div class="parsons-actions">
      <input id="GamingFeedback-feedbackLink" value="Get Feedback" type="button" />
      <input id="GamingFeedback-newInstanceLink" value="Reset Problem" type="button" />
      <span id="GamingFeedback-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback</span>
    </div>

    <script type="text/javascript">
    (function(){
      var initial =
        "name = input('Enter your player name: ')\n" +
        "level = int(input('Enter your level (1-50): '))\n" +
        "score = int(input('Enter your score: '))\n" +
        "accuracy = float(input('Enter your accuracy (0-100): '))\n" +
        "vip = input('Are you a VIP player? (yes/no): ')\n" +
        "vip = vip.lower()\n" +
        "\n" +
        "if level < 1 or level > 50 or score < 0 or accuracy < 0 or accuracy > 100:\n" +
        "    print('Invalid data entered.')\n" +
        "elif score >= 50000 and accuracy >= 70 and vip == 'yes':\n" +
        "    print('VIP bonus unlocked for ' + name + '!')\n" +
        "elif score >= 50000 and accuracy >= 70:\n" +
        "    print('Amazing performance, ' + name + '!')\n" +
        "elif score >= 20000:\n" +
        "    print('Good job, ' + name + '. Keep grinding.')\n" +
        "else:\n" +
        "    print('Keep practising, ' + name + '.')\n" +
        "print('Thanks for playing!')  #distractor\n" +
        "score = 0  #distractor\n" +
        "vip = 'yes'  #distractor\n";

      var widget = new ParsonsWidget({
        sortableId: "GamingFeedback-sortable",
        trashId: "GamingFeedback-sortableTrash",
        max_wrong_lines: 3,
        grader: ParsonsWidget._graders.LineBasedGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        show_feedback: true
      });

      widget.init(initial);
      widget.shuffleLines();
      attachParsonsFeedback("GamingFeedback", widget);
    })();
    </script>
  </div>
</div>
