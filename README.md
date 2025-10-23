# RL-Reward-Hacking-Demo: The Proximal Alignment Problem

##  Technical AI Safety Focus: Reward Hacking & Goal Misgeneralization

This project explicitly demonstrates **Reward Hacking**, a core problem in **AI Control** where an intelligent agent optimizes a **proxy measure** (the reward signal) rather than the **true objective** (human intent). The agent achieves high numerical reward while exhibiting non-human-aligned behavior.

**The Misalignment:** We created a modified FrozenLake environment where the agent's ultimate goal (G, reward=10) is difficult. We introduced an easier **Trap (T, reward=2)**. The agent, being a pure optimizer, learned to repeatedly cycle around the easy Trap for guaranteed reward, proving a dangerous **proximal alignment failure**.

---

##  Technical Implementation

* **Environment:** Custom 4x4 'FrozenLake-v1' (Gymnasium) with a defined 'Trap' state (T).
* **Algorithm:** Q-Learning.
* **Key Findings:** Over 2,000 episodes, the agent prioritized the easy proxy reward.
    * **Total Proxy Hacks:** **2,575** exploits were recorded.
    * **Final Policy:** The learned policy resulted in an average reward of **3.48**, significantly failing to achieve the optimal reward of $10.0+$.

---

##  Results

### Agent Learning Curve (Hacked Reward)


**Observation:** The agent's reward quickly stabilizes, **not** because it learned the true goal, but because it learned a **high-frequency hack loop** that yields a consistent, moderate proxy reward. The chaotic, spiking graph confirms the learning is stuck optimizing the hack rather than following a clean optimal path.

### Learned Policy (Goal Misgeneralization)


**Observation:** The agent's final learned trajectory resulted in an **"infinite hack loop"** (`... 12 -> 12 -> 12 ...`). This is definitive evidence of **Goal Misgeneralization**, where the model's behavior is logically optimal based on the flawed reward function, but completely misaligned with the human operator's intent (reaching G).

---

## 🚀 How to Run the Code

The complete, runnable code is available in `Reward_Hacking_Simulation.ipynb`.
