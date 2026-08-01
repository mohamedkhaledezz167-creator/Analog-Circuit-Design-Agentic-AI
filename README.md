# Analog-Circuit-Design-Agentic-AI
An Agentic AI pipeline for automated GF-180nm analog design. It replaces blind SPICE sweeps with a 3-stage architecture: LLM-guided gm/ID initial sizing, Genetic Algorithm optimization, and heuristic AI fine-tuning. By treating circuits as math functions, it slashes simulation bottlenecks and mimics a Senior Analog Designer's workflow.





# Agentic Analog Circuit Optimization

**MSc Thesis Project by Mohamed**  
*Technology: GF-180nm, 3.3V Supply*

### 📁 Project Resources & Demonstrations
*   **[Watch Demonstration Video 1 (Google Drive)](https://drive.google.com/file/d/1A9Ipviedc0UiwP3iHwZS3PEYmZnQ8Asy/view?usp=drive_link)**
*   **[Watch Demonstration Video 2 (Google Drive)](https://drive.google.com/file/d/17oWXzNKuh1HhPyUddlh5OyucWhQjy8jb/view?usp=drive_link)**
*   **[Watch Demonstration Video 3 (Google Drive)](https://drive.google.com/file/d/1bdhUjFpRPiOOtSaCCRv7zKWV2MW79WOy/view?usp=drive_link)**
---

## Project Overview
The project focuses on Agentic Analog Circuit Optimization, specifically automating the sizing of a 5-Transistor Operational Transconductance Amplifier (5T OTA) using the GF-180nm technology node with a 3.3V supply. It solves the computational bottlenecks of traditional analog design by treating the circuit simulator as a mathematical function and orchestrating the design workflow through specialized AI agents.  

## The Three-Stage Architecture
The system prevents AI models from wasting tokens on blind trial-and-error by breaking the design process into three distinct phases:  

*   **Phase 1: Initial Sizing ($g_m/I_D$ Methodology):** A mid-level reasoning model (Gemini Flash) is paired with a custom Python `LUT_FinderAgent`. The AI determines the high-level methodology, while the Python tool handles precise parameter lookups to generate a highly accurate initial design point ($\vec{x}_{init}$).  
*   **Phase 2: Mathematical Optimization:** The initial design is passed to a Genetic Algorithm (GA). A Python circuit wrapper translates the circuit topology into a pure mathematical mapping of inputs to outputs ($\vec{y} = f(\vec{x})$). The GA then minimizes a custom, multi-part loss function to hit performance targets without relying on the LLM.  
*   **Phase 3: Heuristic Fine-Tuning (The "Senior Designer"):** If the optimizer reaches its simulation limit without hitting all constraints, an advanced reasoning model (Gemini Pro) takes over. It evaluates a heuristic trade-offs map to make smart, system-level adjustments—such as tuning the tail current source width ($W_{ss}$) to increase Unity Gain Frequency (UGF) or lower power consumption ($P_W$) while keeping the Phase Margin (PM) stable.  

## Key Technical Innovations
*   **Simulation Acceleration:** To drastically reduce simulation time, the system avoids massive iterative sweeps. Instead of running DC sweeps to find output voltage swings, the OTA is simulated in a unity-gain buffer configuration where output errors can be measured using a single DC operating point simulation.  
*   **Physical Scaling Overrides:** The architecture inherently understands that parameters like drain current and capacitances scale linearly with transistor width, allowing the optimization space to be strictly bounded and highly efficient.  

## Future Roadmap
*   **Native Python Simulator (PyTorchSim):** Modeling transistors as neural networks directly inside Python to bypass the heavy I/O overhead of writing and reading external SPICE netlists.  
*   **Local Multi-Agent Orchestration:** Transitioning from proprietary cloud IDEs to a localized environment built on LangChain and LangGraph. This will utilize local open-source models (like Qwen or Gemma) to remove context-window limitations and manage specialized tasks like topology architecture and dynamic step-size optimization.
