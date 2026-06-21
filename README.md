# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [] Describe the game's purpose: The application is a number guessing game built using Streamlit that tests a player's ability to find a randomly generated secret number within a limited number of attempts depending on the chosen difficulty.
- [] Detail which bugs you found: The attempts initialized incorrectly at 1 instead of 0, cutting into the allowed player guess count. Additionally, the "New Game" button failed to clear historical variables, causing the app state to freeze on a previous win or loss and lock up the interface.
- [] Explain what fixes you applied: Modularized the architecture by separating game logic from UI code into a distinct `logic_utils.py` file. Corrected the attempt counter to start at 0, and updated the "New Game" action block to fully wipe all session state arrays and variables upon instantiation.

## 📸 Demo Walkthrough

1. The game initializes on "Normal" difficulty spanning a target secret number range between 1 and 100.
2. The user inputs an initial mid-point guess of 50.
3. The game processes the guess and returns an accurate "Too Low" hint banner.
4. The user adjusts upward and inputs a guess of 75, which updates the interface and correctly displays a "Too High" hint.
5. The player isolates the exact target number, submits it, and a victory banner confirms the successful match.
6. Pressing the "New Game" button resets the attempt counter, wipes the sidebar history logs, and safely generates a brand new secret number.

## 🧪 Test Results

```
# Paste your pytest output here, pytest tests/
========================= 3 passed in 0.01s =========================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
