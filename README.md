# -Electric-Vehicle-Cruise-Control-
PROJECT OVERVIEW
This project focuses on the design and analysis of an Electric Vehicle (EV) Cruise Control System using classical control techniques in MATLAB.
The main objective is to maintain a constant vehicle speed under varying road conditions while ensuring:
  Low steady-state error
  Minimal overshoot
  Smooth transient response
  Stable disturbance rejection
The vehicle dynamics are modeled using the first-order transfer function: G(s)=(5s+1)/1
A PI controller is designed and compared with an auto-tuned PID controller to evaluate overall system performance and stability.
Features:
  Open-loop system modeling
  PI controller design and tuning
  Auto-tuned PID controller comparison
  Step response analysis
  Performance metric evaluation
  Gain sensitivity analysis
  Disturbance rejection testing
  Multiple road slope disturbance scenarios
  Bode plot stability analysis
  Nyquist stability verification
  Root Locus Analysis
  Final controller performance summary
Dependencies
  MATLAB R2021a or later
  Control System Toolbox
  MATLAB Functions Used
  tf() → Transfer function modeling
  feedback() → Closed-loop system formation
  step() → Step response simulation
  stepinfo() → Performance metric extraction
  margin() → Stability margin analysis
  nyquist() → Nyquist stability analysis
  lsim() → Disturbance simulation
  pidtune() → Automatic PID tuning
  
PROJECT APPROACH
1. System Modeling
  The EV dynamics are represented using a first-order transfer function.
   System inputs and outputs:
    Input → Throttle control
    Output → Vehicle speed
  The open-loop response is analyzed first to understand the natural behavior of the system.
2. PI Controller Design
  A PI controller is designed with the following tuned gains:
    Kp=120, Ki=150
    The controller is selected to:
    Reduce steady-state error
    Improve transient response
    Maintain system stability
    Keep overshoot below 5%
3. Closed-Loop Analysis
  The PI controller is connected in a unity feedback configuration.
  The closed-loop step response is analyzed to evaluate:
    Rise time
    Settling time
    Overshoot
    Peak time
    Steady-state error
  The obtained performance is verified against the required design specifications.
4. PI vs PID Comparison
  An auto-tuned PID controller is generated using MATLAB’s pidtune() function.
  Both PI and PID controllers are compared based on:
    Response speed
    Overshoot
    Stability margins
    Steady-state accuracy
  The PI controller is selected for final implementation because of:
    Simpler structure
    Smooth response
    Satisfactory performance
5. Gain Sensitivity Analysis
  Different proportional gain (Kp) values are tested.
  The effect of controller tuning on system performance is analyzed in terms of:
    Overshoot
    Rise time
    Settling time
    Stability
  This analysis helps evaluate the robustness of the controller.
6. Disturbance Rejection Analysis
  Road slope disturbances are introduced at t=10s to simulate real-world driving conditions.
  The controller’s ability to reject disturbances and recover the desired speed is evaluated.
  Disturbance Cases Tested
  Mild slope disturbance
  Moderate slope disturbance
  Steep slope disturbance
  Metrics Evaluated
  Maximum speed dip
  Recovery time
  Stability after disturbance
  Stability Analysis
  Bode Plot Analysis
  Frequency response analysis is performed using Bode plots.
  The following stability parameters are evaluated:
  Gain margin
  Phase margin
  Robustness characteristics
7. Nyquist Stability Analysis
  Nyquist plots are used to verify closed-loop stability.
  Stability is confirmed by ensuring that the Nyquist curve does not encircle the critical point (−1,0).
  The analysis confirms:
    Stable closed-loop operation
    Good robustness margins
    Reliable controller performance
8. Root Locus Analysis
   Root locus analysis is used to study the movement of closed-loop poles as controller gain varies.
   It verifies system stability and controller effectiveness.
   The compensated system confirms that the selected gain:  Kp=120
   Places all poles in the Left Half Plane (LHP), ensuring stable operation.
   The analysis compares uncompensated and compensated system behavior.
   Root locus results confirm improved stability and transient response with the PI controller.
9. Performance Summary
  The final PI-controlled cruise control system successfully achieves:
  Steady-state error < 2%
  Overshoot < 5%
  Smooth transient response
  Stable disturbance rejection
  Robust closed-loop stability

CONCLUSION
  This project demonstrates the successful design of an Electric Vehicle Cruise Control System using classical control         engineering techniques.
  Through controller tuning, disturbance analysis, gain sensitivity testing, root locus analysis, and stability verification   using Bode and Nyquist methods, the system achieves reliable and stable speed regulation under varying operating             conditions.
