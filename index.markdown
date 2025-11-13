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

<div class="dc-container">
  <div class="page-hero">
    <span class="badge">Mr Albrecht's Parsons Problems · GCSE Computer Science · Dulwich College</span>
    <h1>Parsons Practice</h1>
    <p>Drag code blocks to build working programs. Use <strong>Reset</strong> to reshuffle and <strong>Get Feedback</strong> to check your answer.</p>
  </div>

  <!-- P1 -->
  <div class="parsons-card">
    <h2>1. Basic Reaction Time Game</h2>
    <p class="subtitle">
      Waits a random delay, displays <strong>GO!</strong>, starts a timer, and measures how fast the user presses Enter.
    </p>
    <div class="puzzle-grid">
      <div id="p1-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 1"></div>
      <div id="p1-sortable" class="sortable-code" aria-label="Workspace for puzzle 1"></div>
    </div>
    <div class="parsons-actions">
      <input id="p1-feedbackLink" value="Get Feedback" type="button" />
      <input id="p1-newInstanceLink" value="Reset Problem" type="button" />
      <span id="p1-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback</span>
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

      var p1 = new ParsonsWidget({
        sortableId: "p1-sortable",
        trashId: "p1-sortableTrash",
        max_wrong_lines: 10,
        grader: ParsonsWidget._graders.LineBasedGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        show_feedback: true
      });

      p1.init(initial);
      p1.shuffleLines();
      attachParsonsFeedback("p1", p1);
    })();
    </script>
  </div>

  <!-- P2 -->
  <div class="parsons-card">
    <h2>2. What Should I Wear? (Selection)</h2>
    <p class="subtitle">
      Write <code>advice_for(tempC)</code>: below 10 → “Wear a coat”; 10–14 → “Wear a jumper”; otherwise → “No coat needed”.
    </p>

    <div class="puzzle-grid">
      <div id="p2-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 2"></div>
      <div id="p2-sortable" class="sortable-code" aria-label="Workspace for puzzle 2"></div>
    </div>

    <div class="parsons-actions">
      <input id="p2-feedbackLink" value="Get Feedback" type="button" />
      <input id="p2-newInstanceLink" value="Reset Problem" type="button" />
      <span id="p2-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback</span>
    </div>

    <script type="text/javascript">
    (function(){
      var initial =
        "def advice_for(tempC):\n" +
        "    if tempC < 10:\n" +
        "        return 'Wear a coat'\n" +
        "    elif tempC < 15:\n" +
        "        return 'Wear a jumper'\n" +
        "    else:\n" +
        "        return 'No coat needed'\n" +
        "print(advice_for(8))  # test call #distractor\n";

      var p2 = new ParsonsWidget({
        sortableId: "p2-sortable",
        trashId: "p2-sortableTrash",
        max_wrong_lines: 1,
        grader: ParsonsWidget._graders.LineBasedGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        show_feedback: true
      });

      p2.init(initial);
      p2.shuffleLines();
      attachParsonsFeedback("p2", p2);
    })();
    </script>
  </div>

  <!-- P3 -->
  <div class="parsons-card">
    <h2>3. Exam Grade Classifier (multi-branch selection)</h2>
    <p class="subtitle">
      Task: Ask the user for their exam mark out of 100, then print the grade:<br>
      90 or more → <code>Grade: A</code>; 80–89 → <code>Grade: B</code>; 70–79 → <code>Grade: C</code>; below 70 → <code>Grade: D</code>.
    </p>

    <div class="puzzle-grid">
      <div id="p3-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 3"></div>
      <div id="p3-sortable" class="sortable-code" aria-label="Workspace for puzzle 3"></div>
    </div>

    <div class="parsons-actions">
      <input id="p3-feedbackLink" value="Get Feedback" type="button" />
      <input id="p3-newInstanceLink" value="Reset Problem" type="button" />
      <span id="p3-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback</span>
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

      var p3 = new ParsonsWidget({
        sortableId: "p3-sortable",
        trashId: "p3-sortableTrash",
        max_wrong_lines: 2,
        grader: ParsonsWidget._graders.LineBasedGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        show_feedback: true
      });

      p3.init(initial);
      p3.shuffleLines();
      attachParsonsFeedback("p3", p3);
    })();
    </script>
  </div>

  <!-- P4 -->
  <div class="parsons-card">
    <h2>4. Rollercoaster Ride Check (logical operators + validation)</h2>
    <p class="subtitle">
      Task: A rollercoaster has these rules: rider must be at least 120&nbsp;cm tall and at least 10&nbsp;years old.<br>
      Ask for height (cm) and age (years). If either is less than 0, print <code>Invalid input.</code><br>
      Otherwise, if they meet both conditions, print <code>You can ride the rollercoaster!</code>, else<br>
      <code>Sorry, you are not allowed to ride.</code>
    </p>

    <div class="puzzle-grid">
      <div id="p4-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 4"></div>
      <div id="p4-sortable" class="sortable-code" aria-label="Workspace for puzzle 4"></div>
    </div>

    <div class="parsons-actions">
      <input id="p4-feedbackLink" value="Get Feedback" type="button" />
      <input id="p4-newInstanceLink" value="Reset Problem" type="button" />
      <span id="p4-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback</span>
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
        "height = 0  #distractor\n";

      var p4 = new ParsonsWidget({
        sortableId: "p4-sortable",
        trashId: "p4-sortableTrash",
        max_wrong_lines: 1,
        grader: ParsonsWidget._graders.LineBasedGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        show_feedback: true
      });

      p4.init(initial);
      p4.shuffleLines();
      attachParsonsFeedback("p4", p4);
    })();
    </script>
  </div>

  <!-- P5 -->
  <div class="parsons-card">
    <h2>5. Gaming Performance Feedback (mixed data types + conditions)</h2>
    <p class="subtitle">
      Task: Write a stats screen for an online game. Ask for:
      player name (string), level (1–50), score (≥ 0), accuracy (0–100, float), and VIP status (yes/no, any capitalisation).<br>
      If any values are impossible, print <code>Invalid data entered.</code><br>
      Otherwise:
      VIP + score ≥ 50000 + accuracy ≥ 70 → <code>VIP bonus unlocked for &lt;name&gt;!</code><br>
      Else score ≥ 50000 + accuracy ≥ 70 → <code>Amazing performance, &lt;name&gt;!</code><br>
      Else score ≥ 20000 → <code>Good job, &lt;name&gt;. Keep grinding.</code><br>
      Else → <code>Keep practising, &lt;name&gt;.</code>
    </p>

    <div class="puzzle-grid">
      <div id="p5-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 5"></div>
      <div id="p5-sortable" class="sortable-code" aria-label="Workspace for puzzle 5"></div>
    </div>

    <div class="parsons-actions">
      <input id="p5-feedbackLink" value="Get Feedback" type="button" />
      <input id="p5-newInstanceLink" value="Reset Problem" type="button" />
      <span id="p5-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback</span>
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
        "print('Thanks for playing!')  #distractor\n";

      var p5 = new ParsonsWidget({
        sortableId: "p5-sortable",
        trashId: "p5-sortableTrash",
        max_wrong_lines: 1,
        grader: ParsonsWidget._graders.LineBasedGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        show_feedback: true
      });

      p5.init(initial);
      p5.shuffleLines();
      attachParsonsFeedback("p5", p5);
    })();
    </script>
  </div>
</div>

<!-- Robust feedback helper (shared by all puzzles) -->
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
      wrong += cont.querySelectorAll("li[style*='rgb(255, 221, 221)'], li[style*='#ffdddd']").length;
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
        badge.textContent = "❌ " + count + " issue" + (count > 1 ? "s" : "") + " to fix";
      }
      badge.style.display = "inline-flex";
    }

    function updateBadgeFromResult(result) {
      let wrongCount = 0;
      if (Array.isArray(result)) {
        wrongCount = result.length;
      } else if (result && typeof result === "object") {
        if (Array.isArray(result.errors)) wrongCount = result.errors.length;
        else if (Array.isArray(result.feedback)) wrongCount = result.feedback.length;
        else if (typeof result.errorCount === "number") wrongCount = result.errorCount;
      }
      if (wrongCount > 0) {
        renderBadge(wrongCount);
      } else {
        setTimeout(() => renderBadge(scanWrongInDOM()), 90);
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
