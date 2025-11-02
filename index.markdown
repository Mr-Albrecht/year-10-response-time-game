---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Multiple Parson's Problems on One Page
---
# Parsons Practice

## Basic Reaction Time Game

<div id="Mr Albrecht's Basic Reaction Time Game-sortableTrash" class="sortable-code"></div> 
<div id="Mr Albrecht's Basic Reaction Time Game-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="Mr Albrecht's Basic Reaction Time Game-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="Mr Albrecht's Basic Reaction Time Game-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<script type="text/javascript"> 
(function(){
  var initial = "import time
\n" +
    "import random
\n" +
    "
\n" +
    "# Reaction time game
\n" +
    "print(&quot;Welcome to the Reaction Time Game!&quot;)
\n" +
    "print(&quot;When you see &#039;GO!&#039;, press Enter as fast as you can.&quot;)
\n" +
    "input(&quot;Press Enter to start...&quot;)
\n" +
    "
\n" +
    "wait_time = random.uniform(2, 5) # Wait for a random time between 2 and 5 seconds
\n" +
    "print(&quot;Get ready...&quot;)
\n" +
    "time.sleep(wait_time) # Pauses the program for the wait time
\n" +
    "
\n" +
    "# Start the timer
\n" +
    "print(&quot;GO!&quot;)
\n" +
    "start_time = time.time()
\n" +
    "
\n" +
    "# Wait for user to react
\n" +
    "input()
\n" +
    "end_time = time.time()
\n" +
    "
\n" +
    "# Calculate and display reaction time
\n" +
    "reaction_time = end_time - start_time
\n" +
    "print(f&quot;Your reaction time was {reaction_time:.3f} seconds!&quot;) #the f allows us to use variables in the print function
\n" +
    "";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "Mr Albrecht's Basic Reaction Time Game-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.shuffleLines();
  $("#Mr Albrecht's Basic Reaction Time Game-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#Mr Albrecht's Basic Reaction Time Game-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.getFeedback(); 
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
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p2-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.VariableCheckGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "trashId": "p2-sortableTrash",
    "vartests": [
        {
            "message": "Testing with initial variable values x = 3 and y = 4",
            "initcode": "x = 3\ny = 4",
            "code": "",
            "variables": {}
        },
        {
            "message": "Testing with initial variable values x = 0 and y = 2",
            "initcode": "x = 0\ny = 2",
            "code": "",
            "variables": {}
        }
    ]
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.shuffleLines();
  $("#p2-newInstanceLink").click(function(event){
      event.preventDefault();
      parsonsPuzzle.shuffleLines();
  });
  $("#p2-feedbackLink").click(function(event){
      event.preventDefault();
      parsonsPuzzle.getFeedback();
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
  var initial = "def maxindex(arg):\n" +
    " ans = 0\n" +
    " for i in range(len(arg)):\n" +
    " if arg[i] > arg[ans]:\n" +
    " ans = i\n" +
    " while True:\n" +
    "pass\n" +
    " return ans";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p3-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.UnitTestGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "trashId": "p3-sortableTrash",
    "unittests": "import unittestparson\nclass myTests(unittestparson.unittest):\n  def test_0(self):\n    self.assertEqual(,,)\n_test_result = myTests().main()"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.shuffleLines();
  $("#p3-newInstanceLink").click(function(event){
      event.preventDefault();
      parsonsPuzzle.shuffleLines();
  });
  $("#p3-feedbackLink").click(function(event){
      event.preventDefault();
      parsonsPuzzle.getFeedback();
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
  var initial = "for (int i=0;i<3;i++) {\n" +
    "System.out.print(\\\"I \\\");\n" +
    "System.out.print(\\\"am \\\");\n" +
    "System.out.print(\\\"a Java program \\\");\n" +
    "}";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p4-sortable",
    "max_wrong_lines": 1,
    "grader": ParsonsWidget._graders.LanguageTranslationGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "executable_code": "for x in range(3):\n    output += 'I '\n    output += 'am '\n    output += 'a Java program '\npass",
    "programmingLang": "java",
    "vartests": [
        {
            "message": "Testing...",
            "initcode": "output = ''",
            "code": "",
            "variables": {
                "output": "I am a Java program I am a Java program I am a Java program "
            }
        }
    ]
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.shuffleLines();
  $("#p4-newInstanceLink").click(function(event){
      event.preventDefault();
      parsonsPuzzle.shuffleLines();
  });
  $("#p4-feedbackLink").click(function(event){
      event.preventDefault();
      parsonsPuzzle.getFeedback();
   });
})();
</script>


## Parsons 5 (Turtle Grader)
Construct a program by dragging&amp;dropping and reordering lines. The constructed program should draw a triangle like shown below.

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
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p5-sortable",
    "max_wrong_lines": 1,
    "grader": ParsonsWidget._graders.TurtleGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "trashId": "p5-sortableTrash",
    "executable_code": "for i in range(0,3):\nmyTurtle.forward(100)\nmyTurtle.left(120)\npass",
    "programmingLang": "pseudo",
    "turtleModelCode": "modelTurtle.forward(100)\nmodelTurtle.left(120)\nmodelTurtle.forward(100)\nmodelTurtle.left(120)\nmodelTurtle.forward(100)\nmodelTurtle.left(120)",
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.shuffleLines();
  $("#p5-newInstanceLink").click(function(event){
      event.preventDefault();
      parsonsPuzzle.shuffleLines();
  });
  $("#p5-feedbackLink").click(function(event){
      event.preventDefault();
      parsonsPuzzle.getFeedback();
  });
})();
</script>

### Implementation Notes

When you host multiple Parson's problems on a single markdown page, you need to add a unique prefix. You can easily do this in the Codio generator by typing a unique prefix into the "Prefix" textbox and pressing Enter/Return. Then you can simply copy-paste like normal.

If want each problem to be it's own page, you can use relative path links at the bottom of each of your markdown pages as seen below. If you want students to be able to return to previous problems in this format, consider adding previous links or link to a table of contents like page.

### Example Next Link
[Next](./parsons/example1.html)
