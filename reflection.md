# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
Initial App Load|Game should start with 0 attempts taken|st.session_state.attempts initializes to 1 cutting the user's total attempts short immediately|none
Clicking New Game Button|Should completely wipe the previous game data and start fresh|The button clears the secret but fails to reset status or history, freezing the UI or leaving it stuck on a previous win/loss|,none
Clicking New Game on Easy/Hard|The new secret number should stay within the chosen difficulty range|It forces random.randint(1, 100), generating secret numbers completely outside the visible difficulty limits|none

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
I used the Cursor AI coding assistant built into my editor.

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
The AI correctly pointed out that while my app.py was trying to use Streamlit's session state, the "New Game" button wasn't resetting everything. It explained that clicking the button left the game state stuck on a previous win or loss, which made the app freeze or look like it wasn't responding. It suggested a clean block of code to reset all variables (secret, attempts, score, status, and history) at once. I verified it by applying the code and playing a live round—clicking "New Game" now completely refreshes everything perfectly.

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
When analyzing the starter code, the AI noticed a weird hack in app.py that forced the secret number to turn into a string on every even attempt (causing bad string-vs-integer comparisons). The AI initially thought this was a framework issue and suggested keeping it, but it was actually a hidden bug meant to break the game. I caught this by looking closely at the logic, rejecting the string hack, and ensuring the refactored check_guess function in logic_utils.py strictly handles numbers. I verified my choice by running pytest in the terminal, and all the tests passed cleanly without the string conversion.
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
I used a two-step approach: first, I relied on automated unit tests to prove the mathematical logic was sound in isolation, and second, I manually played through the game to make sure the interface matched those results and didn't freeze up.

- Describe at least one test you ran (manual or using pytest) and what it showed you about your code.
  I ran pytest in the terminal to execute the test_winning_guess case. It simulated a user guessing the exact secret number and proved that the refactored check_guess function cleanly returned a "Win" outcome instead of triggering a type error or miscalculating the game state.

- Did AI help you design or understand any tests? How?
Yes, the AI helped by mapping out the new automated test structure to match our refactored code. It explained how separating the logic into logic_utils.py allowed us to test inputs (like high, low, or winning guesses) cleanly without needing to launch the entire Streamlit web interface every time.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
Streamlit is like a web page that completely refreshes and wipes its memory every single time you click a button or type something. If you create a regular variable, it gets deleted instantly on that refresh. Streamlit "session state" is like a digital notebook on the side where the app can quickly write down important details (like your current score or the secret number) so it remembers them even after the page reloads.
---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
  I want to reuse the habit of writing automated unit tests with pytest alongside my code. It saves so much time because you can instantly check if your math or logic is broken without manually clicking through the web interface over and over again.

- What is one thing you would do differently next time you work with AI on a coding task?
Next time, I will start by breaking the task down and asking the AI to focus on one small section or single function at a time, rather than letting it analyze or rewrite a massive chunk of a file all at once.

- In one or two sentences, describe how this project changed the way you think about AI generated code.
This project made me realize that AI-generated code often looks correct on the surface but can hide massive, silent logic flaws underneath. It taught me that as a developer, my job isn't just to write code, but to carefully inspect, test, and double-check everything an AI hands me.