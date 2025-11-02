---
layout: default
title: "Multiple Parsons Problems on One Page"
---

<!-- Roboto font -->
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">

<style>
  :root{
    --dc-bg: #0b1f3a;         /* deep navy accent */
    --dc-accent: #0ea5a5;     /* teal accent */
    --dc-accent-2: #7c9aff;   /* soft indigo hint */
    --dc-muted: #f6f8fb;      /* page background */
    --dc-text: #1f2937;       /* body text */
    --dc-border: #e5e7eb;     /* borders */
    --radius: 16px;
    --shadow: 0 8px 24px rgba(16,24,40,.08);
  }

  html, body {
    font-family: "Roboto", system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial, "Noto Sans", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", sans-serif;
    color: var(--dc-text);
    background: var(--dc-muted);
    line-height: 1.65;
  }

  .dc-container {
    max-width: 1000px;
    margin: 40px auto 80px;
    padding: 0 20px;
  }

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
  .page-hero h1{
    margin: 0 0 6px 0;
    font-weight: 700;
    letter-spacing: .3px;
  }
  .page-hero p{
    margin: 6px 0 0 0;
    opacity: .95;
  }
  .badge{
    display: inline-block;
    background: rgba(255,255,255,.16);
    color: #fff;
    border: 1px solid rgba(255,255,255,.22);
    padding: 6px 10px;
    font-size: 12px;
    border-radius: 999px;
    margin-bottom: 10px;
    letter-spacing: .3px;
  }

  h2{
    font-size: 1.25rem;
    margin: 28px 0 12px;
    color: var(--dc-bg);
    letter-spacing: .2px;
  }
  h3{ margin-top: 18px; }

  .parsons-card{
    background: #fff;
    border: 1px solid var(--dc-border);
    border-radius: var(--radius);
    padding: 18px 18px 14px;
    margin: 14px 0 28px;
    box-shadow: var(--shadow);
  }
  .parsons-actions{
    margin-top: 10px;
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
  }

  input[type="button"]{
    appearance: none;
    border: 1px solid #cbd5e1;
    background: #fff;
    padding: 8px 14px;
    border-radius: 10px;
    cursor: pointer;
    font-weight: 500;
    transition: transform .05s ease, box-shadow .2s ease, border-color .2s ease, background .2s ease;
    box-shadow: 0 1px 0 rgba(0,0,0,.02);
  }
  input[type="button"]:hover{
    border-color: var(--dc-accent);
    background: #f7fbfb;
  }
  input[type="button"]:active{
    transform: translateY(1px);
  }
  .parsons-actions input[type="button"]:first-child{
    background: var(--dc-accent);
    color: #08343b;
    border-color: rgba(8,52,59,.2);
  }
  .parsons-actions input[type="button"]:first-child:hover{
    filter: brightness(1.03);
  }

  .sortable-code{
    background: #fafcff;
    border: 1px dashed #cbd5e1;
    border-radius: 12px;
    min-height: 120px;
    padding: 10px;
    margin-bottom: 10px;
  }
  .sortable-code li{
    background: #fff;
    border: 1px solid #e5e7eb;
    border-radius: 10px !important;
    padding: 8px 10px !important;
    margin: 6px 0 !important;
    box-shadow: 0 2px 8px rgba(17,24,39,.05);
    font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
    font-size: 14px;
  }

  .puzzle-grid{
    display: grid;
    gap: 12px;
  }
  @media (min-width: 720px){
    .puzzle-grid{
      grid-template-columns: 1fr 1fr;
      align-items: start;
    }
  }

  .notes{
    background: #fff;
    border: 1px solid var(--dc-border);
    border-radius: var(--radius);
    padding: 16px 18px;
    box-shadow: var(--shadow);
  }
  .notes strong{ color: var(--dc-bg); }
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
    <div class="puzzle-grid">
      <div id="p1-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 1"></div>
      <div id="p1-sortable" class="sortable-code" aria-label="Workspace for puzzle 1"></div>
    </div>
    <div class="parsons-actions">
      <input id="p1-feedbackLink" value="Get Feedback" type="button" />
      <input id="p1-newInstanceLink" value="Reset Problem" type="button" />
    </div>

    <script type="text/javascript">
    (function(){
      var initial = "import time\n" +
                    "import random\n" +
                    "\n" +
                    "# Reaction time game\n" +
                    "print(\"Welcome to the Reaction Time Game!\")\n" +
                    "print(\"When you see 'GO!', press Enter as fast as you can.\")\n" +
                    "input(\"Press Enter to start...\")\n" +
                    "\n" +
                    "wait_time = random.uniform(2, 5)  # Wait for a random time between 2 and 5 seconds\n" +
                    "print(\"Get ready...\")\n" +
                    "time.sleep(wait_time)  # Pauses the program for the wait time\n" +
                    "\n" +
                    "# Start the timer\n" +
                    "print(\"GO!\")\n" +
                    "start_time = time.time()\n" +
                    "\n" +
                    "# Wait for user to react\n" +
                    "input()\n" +
                    "end_time = time.time()\n" +
                    "\n" +
                    "# Calculate and display reaction time\n" +
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

      $("#p1-newInstanceLink").on("click", function(e){
        e.preventDefault();
        p1.shuffleLines();
      });

      $("#p1-feedbackLink").on("click", function(e){
        e.preventDefault();
        p1.getFeedback();
      });
    })();
    </script>
  </div>

  <!-- P2 -->
  <div class="parsons-card">
    <h2>Parsons 2 (Variable Check Grader)</h2>
    <p>Swap the values of <code>x</code> and <code>y</code> using helper variable <code>tmp</code>. Click variable names (<span class="jsparson-toggle"></span>) to toggle them.</p>

    <div class="puzzle-grid">
      <div id="p2-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 2"></div>
      <div id="p2-sortable" class="sortable-code" aria-label="Workspace for puzzle 2"></div>
    </div>

    <div class="parsons-actions">
      <input id="p2-feedbackLink" value="Get Feedback" type="button" />
      <input id="p2-newInstanceLink" value="Reset Problem" type="button" />
    </div>

    <script type="text/javascript">
    (function(){
      var initial = "$$toggle::x::y::tmp$$ = $$toggle::x::y::tmp$$\n" +
                    "$$toggle::x::y::tmp$$ = $$toggle::x::y::tmp$$\n" +
                    "$$toggle::x::y::tmp$$ = $$toggle::x::y::tmp$$";

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
          { message: "Testing with initial variable values x = 3 and y = 4", initcode: "x = 3\ny = 4", code: "", variables: {} },
          { message: "Testing with initial variable values x = 0 and y = 2", initcode: "x = 0\ny = 2", code: "", variables: {} }
        ]
      });

      p2.init(initial);
      p2.shuffleLines();

      $("#p2-newInstanceLink").on("click", function(e){
        e.preventDefault();
        p2.shuffleLines();
      });

      $("#p2-feedbackLink").on("click", function(e){
        e.preventDefault();
        p2.getFeedback();
      });
    })();
    </script>
  </div>

  <!-- P3 -->
  <div class="parsons-card">
    <h2>Parsons 3 (Unit Test Grader)</h2>
    <p>Build a function that returns the index of the largest element in the array.</p>

    <div class="puzzle-grid">
      <div id="p3-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 3"></div>
      <div id="p3-sortable" class="sortable-code" aria-label="Workspace for puzzle 3"></div>
    </div>

    <div class="parsons-actions">
      <input id="p3-feedbackLink" value="Get Feedback" type="button" />
      <input id="p3-newInstanceLink" value="Reset Problem" type="button" />
    </div>

    <script type="text/javascript">
    (function(){
      var initial = "def maxindex(arg):\n" +
                    "    ans = 0\n" +
                    "    for i in range(len(arg)):\n" +
                    "        if arg[i] > arg[ans]:\n" +
                    "            ans = i\n" +
                    "    while True:\n" +
                    "        pass\n" +
                    "    return ans\n";

      var p3 = new ParsonsWidget({
        sortableId: "p3-sortable",
        trashId: "p3-sortableTrash",
        max_wrong_lines: 10,
        grader: ParsonsWidget._graders.UnitTestGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        unittests: "import unittestparson\nclass myTests(unittestparson.unittest):\n  def test_0(self):\n    self.assertEqual(,,)\n_test_result = myTests().main()"
      });

      p3.init(initial);
      p3.shuffleLines();

      $("#p3-newInstanceLink").on("click", function(e){
        e.preventDefault();
        p3.shuffleLines();
      });

      $("#p3-feedbackLink").on("click", function(e){
        e.preventDefault();
        p3.getFeedback();
      });
    })();
    </script>
  </div>

  <!-- P4 -->
  <div class="parsons-card">
    <h2>Parsons 4 (Language Translation Grader)</h2>
    <p>Print <code>"I am a Java program"</code> three times using a <code>for</code> loop.</p>

    <div class="puzzle-grid">
      <div id="p4-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 4"></div>
      <div id="p4-sortable" class="sortable-code" aria-label="Workspace for puzzle 4"></div>
    </div>

    <div class="parsons-actions">
      <input id="p4-feedbackLink" value="Get Feedback" type="button" />
      <input id="p4-newInstanceLink" value="Reset Problem" type="button" />
    </div>

    <script type="text/javascript">
    (function(){
      var initial = "for (int i = 0; i < 3; i++) {\n" +
                    "  System.out.print(\\\"I \\\");\n" +
                    "  System.out.print(\\\"am \\\");\n" +
                    "  System.out.print(\\\"a Java program \\\");\n" +
                    "}";

      var p4 = new ParsonsWidget({
        sortableId: "p4-sortable",
        trashId: "p4-sortableTrash",
        max_wrong_lines: 1,
        grader: ParsonsWidget._graders.LanguageTranslationGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        programmingLang: "java",
        executable_code: "for x in range(3):\n    output += 'I '\n    output += 'am '\n    output += 'a Java program '\npass",
        vartests: [
          { message: "Testing...", initcode: "output = ''", code: "", variables: { "output": "I am a Java program I am a Java program I am a Java program " } }
        ]
      });

      p4.init(initial);
      p4.shuffleLines();

      $("#p4-newInstanceLink").on("click", function(e){
        e.preventDefault();
        p4.shuffleLines();
      });

      $("#p4-feedbackLink").on("click", function(e){
        e.preventDefault();
        p4.getFeedback();
      });
    })();
    </script>
  </div>

  <!-- P5 -->
  <div class="parsons-card">
    <h2>Parsons 5 (Turtle Grader)</h2>
    <p>Construct a program that draws an equilateral triangle.</p>

    <div class="puzzle-grid">
      <div id="p5-sortableTrash" class="sortable-code" aria-label="Trash area for puzzle 5"></div>
      <div id="p5-sortable" class="sortable-code" aria-label="Workspace for puzzle 5"></div>
    </div>

    <div class="parsons-actions">
      <input id="p5-feedbackLink" value="Get Feedback" type="button" />
      <input id="p5-newInstanceLink" value="Reset Problem" type="button" />
    </div>

    <script type="text/javascript">
    (function(){
      var initial = "REPEAT 3 TIMES\n" +
                    "  forward(100)\n" +
                    "  left(120)\n" +
                    "ENDREPEAT";

      var p5 = new ParsonsWidget({
        sortableId: "p5-sortable",
        trashId: "p5-sortableTrash",
        max_wrong_lines: 1,
        grader: ParsonsWidget._graders.TurtleGrader,
        exec_limit: 2500,
        can_indent: true,
        x_indent: 50,
        lang: "en",
        programmingLang: "pseudo",
        executable_code: "for i in range(0,3):\nmyTurtle.forward(100)\nmyTurtle.left(120)\npass",
        turtleModelCode: "modelTurtle.forward(100)\nmodelTurtle.left(120)\nmodelTurtle.forward(100)\nmodelTurtle.left(120)\nmodelTurtle.forward(100)\nmodelTurtle.left(120)\n"
      });

      p5.init(initial);
      p5.shuffleLines();

      $("#p5-newInstanceLink").on("click", function(e){
        e.preventDefault();
        p5.shuffleLines();
      });

      $("#p5-feedbackLink").on("click", function(e){
        e.preventDefault();
        p5.getFeedback();
      });
    })();
    </script>
  </div>

  <div class="notes">
    <strong>Implementation notes</strong><br>
    If you host multiple Parsons problems on one page, ensure each has a unique prefix (<code>p1</code>, <code>p2</code>, …). If you prefer one problem per page, add <em>Next</em> links below.
    <br><br>
    <a href="./parsons/example1.html">Next</a>
  </div>
</div>
