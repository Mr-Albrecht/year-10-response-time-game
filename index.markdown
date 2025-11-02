---
layout: default
title: "Multiple Parsons Problems on One Page"
---

# Parsons Practice

## Basic Reaction Time Game

<div id="p1-sortableTrash" class="sortable-code"></div>
<div id="p1-sortable" class="sortable-code"></div>
<div style="clear:both;"></div>
<p>
  <input id="p1-feedbackLink" value="Get Feedback" type="button" />
  <input id="p1-newInstanceLink" value="Reset Problem" type="button" />
</p>

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
                "print(f\"Your reaction time was {reaction_time:.3f} seconds!\")\n";

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


## Parsons 2 (Variable Check Grader)

Construct a program that swaps the values of variables <code>x</code> and <code>y</code> using the helper variable <code>tmp</code>. You can change the names of the variables (<span class="jsparson-toggle"></span>) by clicking them.

<div id="p2-sortableTrash" class="sortable-code"></div>
<div id="p2-sortable" class="sortable-code"></div>
<div style="clear:both;"></div>
<p>
  <input id="p2-feedbackLink" value="Get Feedback" type="button" />
  <input id="p2-newInstanceLink" value="Reset Problem" type="button" />
</p>

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
      {
        message: "Testing with initial variable values x = 3 and y = 4",
        initcode: "x = 3\ny = 4",
        code: "",
        variables: {}
      },
      {
        message: "Testing with initial variable values x = 0 and y = 2",
        initcode: "x = 0\ny = 2",
        code: "",
        variables: {}
      }
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


## Parsons 3 (Unit Test Grader)

Your task is to construct a function which returns the index of the largest element in the array.

<div id="p3-sortableTrash" class="sortable-code"></div>
<div id="p3-sortable" class="sortable-code"></div>
<div style="clear:both;"></div>
<p>
  <input id="p3-feedbackLink" value="Get Feedback" type="button" />
  <input id="p3-newInstanceLink" value="Reset Problem" type="button" />
</p>

<script type="text/javascript">
(function(){
  // Note: includes a couple of distractor lines ("while True:", "pass") by design.
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
    // Keep the original (slightly contrived) unittest string if required by your setup:
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


## Parsons 4 (Language Translation Grader)

Print out "I am a Java program" three times using a for loop.

<div id="p4-sortableTrash" class="sortable-code"></div>
<div id="p4-sortable" class="sortable-code"></div>
<div style="clear:both;"></div>
<p>
  <input id="p4-feedbackLink" value="Get Feedback" type="button" />
  <input id="p4-newInstanceLink" value="Reset Problem" type="button" />
</p>

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
      {
        message: "Testing...",
        initcode: "output = ''",
        code: "",
        variables: {
          "output": "I am a Java program I am a Java program I am a Java program "
        }
      }
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


## Parsons 5 (Turtle Grader)

Construct a program by dragging &amp; dropping and reordering lines. The constructed program should draw a triangle like shown below.

<div id="p5-sortableTrash" class="sortable-code"></div>
<div id="p5-sortable" class="sortable-code"></div>
<div style="clear:both;"></div>
<p>
  <input id="p5-feedbackLink" value="Get Feedback" type="button" />
  <input id="p5-newInstanceLink" value="Reset Problem" type="button" />
</p>

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


### Implementation Notes

When you host multiple Parson's problems on a single markdown page, you need to add a unique prefix. You can easily do this in the Codio generator by typing a unique prefix into the "Prefix" textbox and pressing Enter/Return. Then you can simply copy-paste like normal.

If you want each problem to be its own page, you can use relative p
