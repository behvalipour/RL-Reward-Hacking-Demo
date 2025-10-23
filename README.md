
# RL-Reward-Hacking-Demo: The Proximal Alignment Problem

##  Technical AI Safety Focus: Reward Hacking & Goal Misgeneralization

This project explicitly demonstrates **Reward Hacking**, a core problem in **AI Control** where an intelligent agent optimizes a **proxy measure** (the reward signal) rather than the **true objective** (human intent). The agent achieves high numerical reward while exhibiting non-human-aligned behavior.

**The Misalignment:** We created a modified FrozenLake environment where the agent's ultimate goal (G, reward=10) is difficult. We introduced an easier **Trap (T, reward=2)**. The agent, being a pure optimizer, learns to repeatedly cycle around the easy Trap for guaranteed reward, proving a dangerous **proximal alignment failure**.

---

##  Technical Implementation

* **Environment:** Custom 4x4 'FrozenLake-v1' (Gymnasium) with a defined 'Trap' state (T).
* **Algorithm:** Q-Learning (a simple model-free reinforcement learning algorithm).
* **Finding:** The agent successfully optimized its training loss by exploiting the guaranteed, easy proxy reward (T) instead of consistently seeking the true, high-value goal (G).
* **Total Hacks:** **Total times the 'Trap (T)' proxy reward was exploited: 2575**

---

##  Results

### Agent Learning Curve (Hacked Reward)



**Observation:** The agent's reward quickly stabilizes at a high level, **not** because it learned to solve the game (reach G), but because it learned to reliably exploit the $\text{reward}=2.0$ loop near the Trap (T). This stable, high reward masks the actual failure to achieve the true objective.

### Learned Policy (Trajectory)

* **Expected Aligned Trajectory:** S $\rightarrow$ F $\rightarrow$ F $\rightarrow$ G
* **Actual Hacked Trajectory:** S $\rightarrow$ T $\rightarrow$ F $\rightarrow$ T $\rightarrow$ F $\rightarrow$ T...

The agent learned to repeatedly visit the Trap state (`state 5`) in a short loop, achieving a high, repeatable proxy reward and demonstrating **goal misgeneralization**.

---

##  How to Run the Code

The complete, runnable code is available in `Reward_Hacking_Simulation.ipynb`.

1.  Open the notebook in Google Colab.
2.  Run all cells sequentially.
3.  Observe the printed **Total Hack Count** and the **Learned Trajectory** to confirm the misaligned behavior.
