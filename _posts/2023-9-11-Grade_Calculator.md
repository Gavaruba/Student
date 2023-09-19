---
toc: false
comments: false
layout: post
title: Score Calculator
description:
type: Project
---

%%html


<html>
<head>
    <title>Score Calculator</title>
</head>
<body>
    <!-- Help Message -->
    <h3>Input scores, press tab to add each new number.</h3>
    <!-- Table for Scores -->
    <table border="2">
        <thead>
            <tr>
                <th>#</th>
                <th>Score</th>
            </tr>
        </thead>
        <tbody id="scoreTableBody">
            <!-- Table rows will be added here -->
        </tbody>
    </table>
    <!-- Totals -->
    <ul>
        <li>
            Total : <span id="total">0.0</span>
            Count : <span id="count">0.0</span>
            Average : <span id="average">0.0</span>
        </li>
    </ul>
    <!-- Rows added using scores ID -->
    <div id="scores">
        <!-- JavaScript-generated inputs -->
    </div>
     <!-- Clear Button -->
    <button onclick="clearScores()">Clear</button>
    <script>
        // Execute on input event and calculate totals
        function calculator(event) {
            var key = event.key;
            // Check if the pressed key is the "Tab" key (key code 9) or "Enter" key (key code 13)
            if (key === "Tab" || key === "Enter") {
                event.preventDefault(); // Prevent default behavior (tabbing to the next element)
                var array = document.getElementsByName('score'); // Setup array of scores
                var total = 0; // Running total
                var count = 0; // Count of input elements with valid values
                // Clear the table body before adding new rows
                var tableBody = document.getElementById('scoreTableBody');
                tableBody.innerHTML = '';
                for (var i = 0; i < array.length; i++) {
                    var value = array[i].value;
                    if (parseFloat(value)) {
                        var parsedValue = parseFloat(value);
                        total += parsedValue; // Add to running total
                        count++;
                        // Add a new row to the table
                        var newRow = tableBody.insertRow(-1);
                        var cell1 = newRow.insertCell(0);
                        var cell2 = newRow.insertCell(1);
                        cell1.innerHTML = count;
                        cell2.innerHTML = parsedValue.toFixed(3);
                    }
                }
                // Update totals
                document.getElementById('total').innerHTML = total.toFixed(3);
                document.getElementById('count').innerHTML = count;
                if (count > 0) {
                    document.getElementById('average').innerHTML = (total / count).toFixed(3);
                } else {
                    document.getElementById('average').innerHTML = "0.0";
                }
                // Adds a new input line only if all array values satisfy parseFloat
                if (count === document.getElementsByName('score').length) {
                    newInputLine(count); // Make a new input line
                }
            }
        }
        // Creates a new input box
        function newInputLine(index) {
            // Add a label for each score element
            var title = document.createElement('label');
            title.htmlFor = index;
            title.innerHTML = index + ". ";
            document.getElementById("scores").appendChild(title); // Add to HTML
            // Setup score element and attributes
            var score = document.createElement("input"); // Input element
            score.id = index; // ID of input element
            score.onkeydown = calculator; // Each key triggers an event (using a function as a value)
            score.type = "number"; // Use text type to allow typing multiple characters
            score.name = "score"; // Name is used to group all "score" elements (array)
            score.style.textAlign = "right";
            score.style.width = "5em";
            document.getElementById("scores").appendChild(score); // Add to HTML
            // Create and add a blank line after the input box
            var br = document.createElement("br"); // Line break element
            document.getElementById("scores").appendChild(br); // Add to HTML
            // Set focus on the new input line
            document.getElementById(index).focus();
        }
  // Clear Scores Function
        function clearScores() {
            // Clear the table body and reset totals
            var tableBody = document.getElementById('scoreTableBody');
            tableBody.innerHTML = '';
            document.getElementById('total').innerHTML = "0.0";
            document.getElementById('count').innerHTML = "0.0";
            document.getElementById('average').innerHTML = "0.0";
            // Clear input fields
            var array = document.getElementsByName('score');
            for (var i = 0; i < array.length; i++) {
                array[i].value = '';
            }
        }
        // Creates the first input box on Window load
        newInputLine(0);
    </script>
</body>
</html>
