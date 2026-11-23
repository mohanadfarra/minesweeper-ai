# 💣 Minesweeper AI — Knowledge-Based Agent

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Pygame](https://img.shields.io/badge/Pygame-2E7D32?style=flat-square)
![AI](https://img.shields.io/badge/AI-propositional%20logic-8b5cf6?style=flat-square)

An AI that plays Minesweeper by **reasoning logically** about the board. It never guesses
while a provably safe move exists.

## 🧠 How the AI thinks

Every time a safe cell is revealed, the AI turns the number on it into a logical **sentence**:

```
{A, B, C, D} = 1      → exactly one of these 4 neighbours is a mine
```

It stores these sentences in a **knowledge base** and keeps drawing conclusions until nothing new can be learned:

| Rule | Example | Conclusion |
|---|---|---|
| **All safe** | `{A, B, C} = 0` | A, B and C are safe |
| **All mines** | `{A, B} = 2` | A and B are mines |
| **Subset inference** | `{A, B, C} = 2` and `{A, B} = 1` | `{C} = 1` → C is a mine |

Each new safe cell or mine is applied to every sentence, which can unlock more conclusions.
The loop repeats until the knowledge base stops changing.

**Choosing a move**
1. Play a cell that is **known to be safe**.
2. Only if none exists, pick a random cell that is **not a known mine**.

## 📊 Results

Tested on **300 random 8×8 boards (8 mines)** with the AI playing alone:

- **214 wins (71 %)**: the remaining losses come only from forced random guesses
- **0 mistakes** on moves the AI marked as safe

## 🎮 Play

```bash
pip install -r requirements.txt
python runner.py
```

- **Left-click** to reveal a cell, **right-click** to place a flag
- **AI Move** lets the AI make the next move
- **Reset** starts a new board (8×8, 8 mines)

## 📁 Files

| File | Contents |
|---|---|
| `minesweeper.py` | Game board, `Sentence` logic and the `MinesweeperAI` agent |
| `runner.py` | Pygame interface |
| `assets/` | Font, flag and mine images |

## 🙏 Credits

Project from Harvard's **CS50's Introduction to Artificial Intelligence with Python**. The game
board and Pygame interface come from the course starter code; the AI's reasoning
(`Sentence` inference, `add_knowledge`, move selection) is my implementation.
