# GridHunter - Q-Learning for Grid Treasure Hunting

## Project Overview
This submission is for CDS524 Assignment 1, implementing a grid-based treasure hunting game using the Q-Learning reinforcement learning algorithm. The core goal is to train an AI agent that autonomously navigates a 10×10 grid, collects items (stars + gems), avoids obstacles/traps, and maximizes cumulative rewards. The project includes AI training, auto-demo, and human-AI battle modes, fully meeting the assignment's requirements.

## Assignment Deliverables
| Deliverable Category       | File Name                                      | Detailed Description                                                                 |
|----------------------------|------------------------------------------------|-------------------------------------------------------------------------------------|
| Google Colab Equivalent    | `Assignment1_GridHunter_5537735_LIUYueyue.ipynb` | Core code with in-line explanations (environment, agent, training, demo, human-AI battle) |
| Brief Report  | `Assignment1_GridHunter_5537735_LIUYueyue_Report_EN.pdf` | Documentation of game design, Q-Learning implementation, evaluation results, challenges & solutions |
| Pre-trained Model          | `grid_hunter_q_table_fixed.npy`                 | Trained Q-table (load directly for demo; no retraining needed)                       |
| YouTube Demo Video         | [YouTube Link](https://youtu.be/owDxAHgiqog?si=o_67jEnCiafmMHWM) | Demonstrates AI auto-play, human-AI battle, algorithm explanation, and problem-solving |

## How to Run the Project
### 1. Prerequisites
- Python: 3.7+ recommended
- Dependencies: Install via pip (below)

### 2. Step-by-Step Execution
1. Clone this repository:
   ```bash
   git clone https://github.com/yueyueliu50-creator/CDS524-Assignment1-GridHunter.git
   ```
2. Install dependencies:
   ```bash
   pip install numpy matplotlib ipywidgets
   ```
3. Open the core code file in Jupyter Notebook/Lab or Google Colab:
   - File: `Assignment1_GridHunter_5537735_LIUYueyue.ipynb`
4. Run cells in sequence:
   - **Training**: Run all cells to train from scratch.
   - **AI Demo**: Skip training, run demo cells to load the pre-trained model.
   - **Human vs AI**: Run battle cells, control the blue player via on-screen buttons.

## Key Features
### 1. Game Design 
- **1.1 Clear Objective & Rules**: 10×10 grid; collect stars (+15) and gems (+40); avoid fixed obstacles and dynamic traps (refresh every 10 steps); game ends after 300 steps.
- **1.2 Well-Defined State/Action Spaces**:
  - State: 4D discrete state `(agent_row, agent_col, dx+10, dy+10)` (agent position + relative distance to nearest item).
  - Action: 4 moves (0=UP, 1=DOWN, 2=LEFT, 3=RIGHT); `get_valid_actions()` filters invalid moves.
- **1.3 Valid Reward Function**:
  - Positive: +15 (star), +40 (gem), +0.5 (approach item).
  - Negative: -10 (collision), -2 (out-of-bounds), -0.05 (per step), -0.2 (move away from item).
- **1.4 Documented Design**: Report includes grid diagrams, UI screenshots, and reward function tables.

### 2. Q-Learning Implementation
- **2.1 Correct Algorithm**: Full Q-Learning implementation in Python (Q-table init, Bellman equation update).
- **2.2 Reward-Maximizing Policy**: 3000 episodes → avg reward=1244.35, avg score=98.13.
- **2.3 Exploration-Exploitation Balance**: Epsilon-greedy (1.0→0.01 decay); α=0.1, γ=0.95.
- **2.4 Documented Implementation**: Code comments + report detail algorithm logic and hyperparameter tuning.

### 3. Game Interaction 
- **3.1 Interactive UI**: Agent/player interacts with environment (movement, collection, collision).
- **3.2 Real-Time Display**: UI shows step count, last action, immediate reward, and total score.
- **3.3 Appropriate Libraries**: Matplotlib (rendering) + ipywidgets (controls) → cross-platform compatibility.
- **3.4 Smooth UX**: No lag/unresponsiveness; intuitive buttons for human-AI battle.

### 4. Challenges & Solutions
| Challenge                                  | Solution                                                                 |
|--------------------------------------------|--------------------------------------------------------------------------|
| Slow convergence from sparse rewards       | Dense reward function with distance-guided feedback.                     |
| Item-trap position overlap (logic bug)     | Full position verification in `spawn_items()` and `refresh_traps()`.      |
| Jupyter Lab compatibility (ipycanvas issues) | Reconstruct UI with Matplotlib + ipywidgets; use Output container.       |
| Unbalanced exploration vs exploitation    | Exponential ε decay (1.0 → 0.01).                                       |

## References
[1] Sutton, R. S., & Barto, A. G. (2018). *Reinforcement learning: An introduction* (2nd ed.). The MIT Press.
[2] Bazhenov, V. V. (2025). Multi-agent model-based deep reinforcement learning: Testing the method in grid-world environments. In *2025 7th International Youth Conference on Radio Electronics, Electrical and Power Engineering (REEPE)*. IEEE.
