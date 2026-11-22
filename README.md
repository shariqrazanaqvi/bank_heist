# Bank Heist

## Section A: Project Introduction

Bank Heist is a console-based puzzle game written in C for the Programming Fundamentals course. The player is a thief who must break into a bank vault by cracking five randomly generated puzzle locks (a number pattern, a scrambled password, a cipher, a laser grid and a recursive lock), with three attempts per puzzle. Every wrong answer raises a four-stage security alert and shrinks the reward, and reaching 100% alert means the police take all the loot. The game also has a hint system, three special abilities (EMP Jammer, Master Key and Extra Try), Easy, Medium and Hard modes, random events, a final PIN-guessing challenge with a bonus reward, a colourful ASCII interface, and file handling that saves every finished heist to `high_scores.txt` and displays the best five scores from that file. It applies conditionals, loops, functions, recursion, strings, arrays, pointers, structures and file handling in a single `main.c` file of about 800 lines.

## Section B: Features & Test Cases (Execution Scenarios)

The puzzles are random, so each case uses inputs whose results do not depend on which puzzle appears. All cases start from the main menu with an empty `high_scores.txt` (the file in the repository is empty; to empty it again use `type nul > high_scores.txt` on Windows or `: > high_scores.txt` on Linux/macOS).

### Case 1: Three Wrong Answers (Security Alert, Shrinking Reward and Game Over)

- **Description:** Checks the three-attempt rule. Each wrong answer raises the security alert and removes 25% of the puzzle's reward, and the third wrong answer locks the vault and ends the heist.
- **Inputs:** `1` (start), `Neo` (codename), `1` (Easy), `0`, `0`, `0` (three wrong answers), `4` (exit)
- **Expected Output:**
  - `Wrong! Security alert +9, reward drops to $7500.`
  - `Wrong! Security alert +9, reward drops to $5000.`
  - `Wrong answer, and that was your last attempt!`, then the vault door slams shut and the red `BUSTED!` jail bars appear.
  - Heist report: 0 of 5 puzzles solved, final alert 100%, final loot $0, rank Rookie. Nothing is saved because the loot is $0.
- **Screenshot:** ![Case 1](screenshots/case1_execution.png)

### Case 2: Hint, Special Ability and Saving a High Score (File Handling)

- **Description:** Checks the hint cost, the Master Key ability, the reward calculation, the PIN clue and the status panel. After the player escapes with the cash, the score is written to `high_scores.txt` and then read back and displayed from the High scores menu.
- **Inputs:** `1` (start), `Neo` (codename), `1` (Easy), `hint`, `ability`, `2` (Master Key), `2` (escape with the cash), `3` (high scores), `4` (exit)
- **Expected Output:**
  - `The hint costs $1000. Hints left: 3. Reward is now $9000.` followed by a `HINT:` line.
  - `The Master Key opens the door, but the reward shrinks to $3600.`, then the vault door art and `Puzzle solved! You grab $3600. Total cash: $3600`.
  - `Clue 1:` about the PIN digits, and the status panel with alert 0% Quiet, `[#][ ][ ][ ][ ]` vaults, cash $3600, 3 hints left, EMP x2, Master Key x1, Extra Try x2.
  - After escaping: `Score saved to high_scores.txt`, then 1 of 5 puzzles solved, final loot $3600, rank Petty Thief.
  - The High scores screen lists Neo, Easy, 1 of 5, $3600, and `high_scores.txt` now contains the line `3600 0 1 Neo`.
- **Screenshot:** ![Case 2](screenshots/case2_execution.png)

### Case 3: Invalid Input and Error Handling (Including an Empty Score File)

- **Description:** Checks that wrong menu choices, wrong answer formats and a score file with no scores are handled with friendly messages, without crashing and without wasting an attempt.
- **Inputs:** `7` (invalid menu choice), `3` (high scores while the file is empty), `1` (start), `Neo` (codename), `9` (invalid difficulty), `1` (Easy), `abc` (text for a number puzzle), `status`, `quit`, `4` (exit)
- **Expected Output:**
  - `Please enter a number from 1 to 4.` for the invalid menu choice.
  - `No scores saved yet. Finish a heist with some cash to get on the board!` for the empty file.
  - `Please enter a number from 1 to 3.` for the invalid difficulty.
  - `That is not a valid entry, so no attempt was used.` for `abc`, and the next prompt still says `Attempts left: 3`.
  - The status panel shows alert 0% Quiet, cash $0 and 4 hints left. `quit` ends the heist with final loot $0 and rank Rookie, and no score is saved.
- **Screenshot:** ![Case 3](screenshots/case3_execution.png)

## Section C: Instructions to Clone and Execute

### Step 1: Clone the Repository

Open your terminal and execute:

```bash
git clone https://github.com/shariqrazanaqvi/bank_heist
cd bank_heist
```

### Step 2: Compile the Code

```bash
gcc main.c -o bank_heist
```

On Windows with MinGW use `gcc main.c -o bank_heist.exe`. In Code::Blocks or Dev-C++, create a console project, add `main.c` and build it.

### Step 3: Run the Program

Linux / macOS:

```bash
./bank_heist
```

Windows (Command Prompt):

```bat
bank_heist.exe
```

The game uses ANSI colours, which work in Linux, macOS and Windows Terminal or Command Prompt on Windows 10 and later. Run it from the repository folder so that it finds `high_scores.txt`; if the file is missing, the game simply creates it when the first score is saved.

## Repository Structure

```
bank_heist/
├── main.c              the complete game
├── high_scores.txt     saved scores (empty at first, written and read by the game)
├── README.md
└── screenshots/
    ├── case1_execution.png
    ├── case2_execution.png
    └── case3_execution.png
```
