# the_riddlers_holiday_heist

## Overview

In "The Riddler's Holiday Heist," participants were tasked with helping Batman solve the Riddler's puzzles to track down stolen Christmas gifts in Gotham City and capture the flag.
Challenge Description

The Riddler has concocted a series of riddles, and players must solve them to uncover the location of the stolen Christmas gifts. The challenge involved analyzing HTML files to discover the hidden flag.
File Analysis

Participants were provided with three HTML files:

- index_with_image.html
- part2_with_image.html
- part3_with_flag.html

## Solution Process

### Step 1: Reviewing part3_with_flag.html

- Action: Upon inspecting the part3_with_flag.html file, a JavaScript function checkPassword() was identified. This function was designed to compare the input password with a predefined string.

Snippet from HTML:

```html

    <div class="safe-box">
        <p>Enter the password to retrieve the stolen gifts:</p>
        <input type="password" id="password" placeholder="Enter password">
        <button onclick="checkPassword()">Unlock</button>
    </div>
    <script>
        function checkPassword() {
            var password = document.getElementById('password').value;
            if (password === "ENIGMA") {
                alert("Congratulations! You've cracked the code and saved Christmas!");
                document.getElementById("result").textContent = "Congratulations! Your flag is: CTF{XBicifBLAQjBZcD}";
            } else {
                alert("Incorrect password. Try again.");
            }
        }
    </script>
```

Key Discovery: The password for the safe-box was hard-coded as "ENIGMA" in the script, and entering this password reveals the flag.

### Step 2: Retrieving the Flag

Flag: `CTF{XBicifBLAQjBZcD}`

Method: By either entering the password "ENIGMA" in the web page's input field or directly reading the JavaScript code, the flag was revealed.
