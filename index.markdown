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

  /* Clear, colour-coded feedback */
  .fb-pill{
    display:inline-flex; align-items:center; gap:8px; padding:6px 10px; border-radius:999px; font-size:12px; font-weight:600;
    border:1px solid;
  }
  .fb-ok{ background:#ecfdf5; color:#065f46; border-color:#a7f3d0; }
  .fb-bad{ background:#fef2f2; color:#991b1b; border-color:#fecaca; }
  .fb-neutral{ background:#eef2ff; color:#3730a3; border-color:#c7d2fe; }

  /* Highlight wrong lines after feedback (covers common js-parsons classes) */
  .sortable-code li.incorrect,
  .sortable-code li.ui-state-error,
  .sortable-code li.highlight-error{
    border-color:#ef4444 !important;
    box-shadow: 0 0 0 2px rgba(239,68,68,.15), 0 2px 8px rgba(17,24,39,.05);
  }

  .puzzle-grid{ display: grid; gap: 12px; }
  @media (min-width: 720px){
    .puzzle-grid{ grid-template-columns: 1fr 1fr; align-items: start; }
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
    <h2>Basic Reaction Time Game</h2>
    <p class="subtitle">
      This program waits for a random delay, shows <strong>GO!</strong>, starts a timer, and measures how quickly the user presses Enter. Build it from the shuffled lines.
    </p>
    <div class="puzzle-grid">
      <div id="p1-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 1"></div>
      <div id="p1-sortable" class="sortable-code" aria-label="Workspace for puzzle 1"></div>
    </div>
    <div class="parsons-actions">
      <input id="p1-feedbackLink" value="Get Feedback" type="button" />
      <input id="p1-newInstanceLink" value="Reset Problem" type="button" />
      <span id="p1-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback ready</span>
    </div>

    <script type="text/javascript">
    (function(){
      var initial = "import time\n" +
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

      function showBadge(widget, containerId, badgeId){
        // Count common error-marking classes after getFeedback()
        var cont = document.getElementById(containerId);
        var wrong = cont.querySelectorAll('li.incorrect, li.ui-state-error, li.highlight-error').length;
        var badge = document.getElementById(badgeId);
        if(!badge) return;
        if(wrong === 0){
          badge.className = "fb-pill fb-ok";
          badge.textContent = "✅ All correct!";
        }else{
          badge.className = "fb-pill fb-bad";
          badge.textContent = "❌ " + wrong + " issue" + (wrong>1? "s":"") + " to fix";
        }
        badge.style.display = "inline-flex";
      }

      p1.init(initial);
      p1.shuffleLines();

      document.getElementById("p1-newInstanceLink").addEventListener("click", function(e){
        e.preventDefault();
        p1.shuffleLines();
        var b = document.getElementById("p1-feedbackBadge");
        if(b){ b.style.display = "none"; }
      });

      document.getElementById("p1-feedbackLink").addEventListener("click", function(e){
        e.preventDefault();
        p1.getFeedback();
        showBadge(p1, "p1-sortable", "p1-feedbackBadge");
      });
    })();
    </script>
  </div>

  <!-- P2 -->
  <div class="parsons-card">
    <h2>Parsons 2 — Coat or No Coat? (Selection)</h2>
    <p class="subtitle">Set <code>advice</code> based on <code>tempC</code>: below 10 → “Wear a coat”, otherwise → “No coat needed”.</p>

    <div class="puzzle-grid">
      <div id="p2-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 2"></div>
      <div id="p2-sortable" class="sortable-code" aria-label="Workspace for puzzle 2"></div>
    </div>

    <div class="parsons-actions">
      <input id="p2-feedbackLink" value="Get Feedback" type="button" />
      <input id="p2-newInstanceLink" value="Reset Problem" type="button" />
      <span id="p2-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback ready</span>
    </div>

    <script type="text/javascript">
    (function(){
      var initial =
        "if tempC < 10:\n" +
        "    advice = \"Wear a coat\"\n" +
        "else:\n" +
        "    advice = \"No coat needed\"\n";

      var p2 = new ParsonsWidget({
        sortableId: "p2-sortable",
        trashId: "p2-sortableTrash",
        max_wrong_lines: 10,
        grader: ParsonsWidget._graders.VariableCheckGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        vartests: [
          { message: "Testing with tempC = 5",  initcode: "tempC = 5",  code: "", variables: { "advice": "Wear a coat" } },
          { message: "Testing with tempC = 15", initcode: "tempC = 15", code: "", variables: { "advice": "No coat needed" } }
        ]
      });

      function showBadge(containerId, badgeId){
        var cont = document.getElementById(containerId);
        var wrong = cont.querySelectorAll('li.incorrect, li.ui-state-error, li.highlight-error').length;
        var badge = document.getElementById(badgeId);
        if(!badge) return;
        if(wrong === 0){ badge.className = "fb-pill fb-ok";  badge.textContent = "✅ All correct!"; }
        else{            badge.className = "fb-pill fb-bad"; badge.textContent = "❌ " + wrong + " issue" + (wrong>1? "s":"") + " to fix"; }
        badge.style.display = "inline-flex";
      }

      p2.init(initial);
      p2.shuffleLines();

      document.getElementById("p2-newInstanceLink").addEventListener("click", function(e){
        e.preventDefault();
        p2.shuffleLines();
        var b = document.getElementById("p2-feedbackBadge");
        if(b){ b.style.display = "none"; }
      });

      document.getElementById("p2-feedbackLink").addEventListener("click", function(e){
        e.preventDefault();
        p2.getFeedback();
        showBadge("p2-sortable", "p2-feedbackBadge");
      });
    })();
    </script>
  </div>

  <!-- P3 -->
  <div class="parsons-card">
    <h2>Parsons 3 — Max of Two (Selection + Functions)</h2>
    <p class="subtitle">Create <code>max_of_two(a, b)</code> that returns the larger number using <code>if/else</code>.</p>

    <div class="puzzle-grid">
      <div id="p3-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 3"></div>
      <div id="p3-sortable" class="sortable-code" aria-label="Workspace for puzzle 3"></div>
    </div>

    <div class="parsons-actions">
      <input id="p3-feedbackLink" value="Get Feedback" type="button" />
      <input id="p3-newInstanceLink" value="Reset Problem" type="button" />
      <span id="p3-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback ready</span>
    </div>

    <script type="text/javascript">
    (function(){
      var initial =
        "def max_of_two(a, b):\n" +
        "    if a > b:\n" +
        "        return a\n" +
        "    else:\n" +
        "        return b\n" +
        "    while True:\n" +
        "        pass\n";

      var tests = "import unittestparson\n" +
                  "class myTests(unittestparson.unittest):\n" +
                  "  def test_0(self):\n" +
                  "    self.assertEqual(max_of_two(3,5), 5)\n" +
                  "  def test_1(self):\n" +
                  "    self.assertEqual(max_of_two(-2,-7), -2)\n" +
                  "  def test_2(self):\n" +
                  "    self.assertEqual(max_of_two(10,10), 10)\n" +
                  "_test_result = myTests().main()";

      var p3 = new ParsonsWidget({
        sortableId: "p3-sortable",
        trashId: "p3-sortableTrash",
        max_wrong_lines: 10,
        grader: ParsonsWidget._graders.UnitTestGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        unittests: tests
      });

      function showBadge(containerId, badgeId){
        var cont = document.getElementById(containerId);
        var wrong = cont.querySelectorAll('li.incorrect, li.ui-state-error, li.highlight-error').length;
        var badge = document.getElementById(badgeId);
        if(!badge) return;
        if(wrong === 0){ badge.className = "fb-pill fb-ok";  badge.textContent = "✅ All correct!"; }
        else{            badge.className = "fb-pill fb-bad"; badge.textContent = "❌ " + wrong + " issue" + (wrong>1? "s":"") + " to fix"; }
        badge.style.display = "inline-flex";
      }

      p3.init(initial);
      p3.shuffleLines();

      document.getElementById("p3-newInstanceLink").addEventListener("click", function(e){
        e.preventDefault();
        p3.shuffleLines();
        var b = document.getElementById("p3-feedbackBadge");
        if(b){ b.style.display = "none"; }
      });

      document.getElementById("p3-feedbackLink").addEventListener("click", function(e){
        e.preventDefault();
        p3.getFeedback();
        showBadge("p3-sortable", "p3-feedbackBadge");
      });
    })();
    </script>
  </div>

  <!-- P4 -->
  <div class="parsons-card">
    <h2>Parsons 4 — Pass/Merit/Distinction (Java Selection)</h2>
    <p class="subtitle">For a given <code>score</code>: Distinction (≥75), Merit (≥60), else Pass. Build the <code>if / else if / else</code> chain.</p>

    <div class="puzzle-grid">
      <div id="p4-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 4"></div>
      <div id="p4-sortable" class="sortable-code" aria-label="Workspace for puzzle 4"></div>
    </div>

    <div class="parsons-actions">
      <input id="p4-feedbackLink" value="Get Feedback" type="button" />
      <input id="p4-newInstanceLink" value="Reset Problem" type="button" />
      <span id="p4-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback ready</span>
    </div>

    <script type="text/javascript">
    (function(){
      var initial =
        "if (score >= 75) {\n" +
        "  System.out.print(\\\"Distinction\\\");\n" +
        "} else if (score >= 60) {\n" +
        "  System.out.print(\\\"Merit\\\");\n" +
        "} else {\n" +
        "  System.out.print(\\\"Pass\\\");\n" +
        "}";

      var p4 = new ParsonsWidget({
        sortableId: "p4-sortable",
        trashId: "p4-sortableTrash",
        max_wrong_lines: 2,
        grader: ParsonsWidget._graders.LanguageTranslationGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        programmingLang: "java",
        executable_code:
          "def emit(score):\n" +
          "    global output\n" +
          "    if score >= 75:\n" +
          "        output += 'Distinction'\n" +
          "    elif score >= 60:\n" +
          "        output += 'Merit'\n" +
          "    else:\n" +
          "        output += 'Pass'\n" +
          "emit(test_score)\n" +
          "pass",
        vartests: [
          { message: "Testing score = 82", initcode: "output = ''\ntest_score = 82", code: "", variables: { "output": "Distinction" } },
          { message: "Testing score = 67", initcode: "output = ''\ntest_score = 67", code: "", variables: { "output": "Merit" } },
          { message: "Testing score = 41", initcode: "output = ''\ntest_score = 41", code: "", variables: { "output": "Pass" } }
        ]
      });

      function showBadge(containerId, badgeId){
        var cont = document.getElementById(containerId);
        var wrong = cont.querySelectorAll('li.incorrect, li.ui-state-error, li.highlight-error').length;
        var badge = document.getElementById(badgeId);
        if(!badge) return;
        if(wrong === 0){ badge.className = "fb-pill fb-ok";  badge.textContent = "✅ All correct!"; }
        else{            badge.className = "fb-pill fb-bad"; badge.textContent = "❌ " + wrong + " issue" + (wrong>1? "s":"") + " to fix"; }
        badge.style.display = "inline-flex";
      }

      p4.init(initial);
      p4.shuffleLines();

      document.getElementById("p4-newInstanceLink").addEventListener("click", function(e){
        e.preventDefault();
        p4.shuffleLines();
        var b = document.getElementById("p4-feedbackBadge");
        if(b){ b.style.display = "none"; }
      });

      document.getElementById("p4-feedbackLink").addEventListener("click", function(e){
        e.preventDefault();
        p4.getFeedback();
        showBadge("p4-sortable", "p4-feedbackBadge");
      });
    })();
    </script>
  </div>

  <!-- P5 -->
  <div class="parsons-card">
    <h2>Parsons 5 — Triangle Classifier (Selection + Validation)</h2>
    <p class="subtitle">Write <code>triangle_type(a, b, c)</code> → one of <code>equilateral</code>, <code>isosceles</code>, <code>scalene</code>, or <code>invalid</code>. Return <code>invalid</code> if any side ≤ 0 or triangle inequality fails.</p>

    <div class="puzzle-grid">
      <div id="p5-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 5"></div>
      <div id="p5-sortable" class="sortable-code" aria-label="Workspace for puzzle 5"></div>
    </div>

    <div class="parsons-actions">
      <input id="p5-feedbackLink" value="Get Feedback" type="button" />
      <input id="p5-newInstanceLink" value="Reset Problem" type="button" />
      <span id="p5-feedbackBadge" class="fb-pill fb-neutral" style="display:none;">Feedback ready</span>
    </div>

    <script type="text/javascript">
    (function(){
      var initial =
        "def triangle_type(a, b, c):\n" +
        "    if a <= 0 or b <= 0 or c <= 0:\n" +
        "        return \"invalid\"\n" +
        "    if a + b <= c or a + c <= b or b + c <= a:\n" +
        "        return \"invalid\"\n" +
        "    if a == b == c:\n" +
        "        return \"equilateral\"\n" +
        "    elif a == b or a == c or b == c:\n" +
        "        return \"isosceles\"\n" +
        "    else:\n" +
        "        return \"scalene\"\n" +
        "    while True:\n" +
        "        pass\n";

      var tests =
        "import unittestparson\n" +
        "class myTests(unittestparson.unittest):\n" +
        "  def test_equilateral(self):\n" +
        "    self.assertEqual(triangle_type(5,5,5), 'equilateral')\n" +
        "  def test_isosceles(self):\n" +
        "    self.assertEqual(triangle_type(4,4,3), 'isosceles')\n" +
        "  def test_scalene(self):\n" +
        "    self.assertEqual(triangle_type(3,4,5), 'scalene')\n" +
        "  def test_invalid_zero(self):\n" +
        "    self.assertEqual(triangle_type(0,4,5), 'invalid')\n" +
        "  def test_invalid_ineq(self):\n" +
        "    self.assertEqual(triangle_type(1,2,8), 'invalid')\n" +
        "_test_result = myTests().main()";

      var p5 = new ParsonsWidget({
        sortableId: "p5-sortable",
        trashId: "p5-sortableTrash",
        max_wrong_lines: 10,
        grader: ParsonsWidget._graders.UnitTestGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        unittests: tests
      });

      function showBadge(containerId, badgeId){
        var cont = document.getElementById(containerId);
        var wrong = cont.querySelectorAll('li.incorrect, li.ui-state-error, li.highlight-error').length;
        var badge = document.getElementById(badgeId);
        if(!badge) return;
        if(wrong === 0){ badge.className = "fb-pill fb-ok";  badge.textContent = "✅ All correct!"; }
        else{            badge.className = "fb-pill fb-bad"; badge.textContent = "❌ " + wrong + " issue" + (wrong>1? "s":"") + " to fix"; }
        badge.style.display = "inline-flex";
      }

      p5.init(initial);
      p5.shuffleLines();

      document.getElementById("p5-newInstanceLink").addEventListener("click", function(e){
        e.preventDefault();
        p5.shuffleLines();
        var b = document.getElementById("p5-feedbackBadge");
        if(b){ b.style.display = "none"; }
      });

      document.getElementById("p5-feedbackLink").addEventListener("click", function(e){
        e.preventDefault();
        p5.getFeedback();
        showBadge("p5-sortable", "p5-feedbackBadge");
      });
    })();
    </script>
  </div>
</div>
