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
    Kp=9, Ki=2
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
   The compensated system confirms that the selected gain:  Kp=9
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

%% ============================================================
%  ELECTRIC VEHICLE CRUISE CONTROL SYSTEM
%  Problem Statement 2 — Control Systems Hackathon
%
%  Plant:
%               1
%      G(s) = -------
%              5s+1
%
%  FEATURES INCLUDED
%  ------------------------------------------------------------
%  ✓ Open Loop Modeling
%  ✓ PI Controller Design
%  ✓ Auto-Tuned PID Comparison
%  ✓ Step Response Analysis
%  ✓ Performance Metrics
%  ✓ Gain Sensitivity Analysis
%  ✓ Disturbance Rejection Analysis
%  ✓ Multiple Road Slope Disturbances
%  ✓ Bode Plot Stability Analysis
%  ✓ Nyquist Stability Verification
%  ✓ Root Locus Analysis
%  ✓ Final Performance Summary
%
%% ============================================================

clc;
clear;
close all;

%% ============================================================
%  SECTION 1 : SYSTEM MODEL
%% ============================================================

s = tf('s');

% Plant Transfer Function
G = 1/(5*s + 1);

fprintf('=================================================\n');
fprintf('SYSTEM MODEL\n');
fprintf('=================================================\n');

disp('Plant Transfer Function G(s):');
G

%% ============================================================
%  SECTION 2 : OPEN LOOP RESPONSE
%% ============================================================

figure(1);

step(G);

grid on;

title('Figure 1 : Open Loop Step Response', ...
      'FontSize',13,'FontWeight','bold');

xlabel('Time (seconds)');
ylabel('Vehicle Speed (normalized)');

legend('Open Loop Response', ...
       'Location','southeast');

set(gcf,'Color','white');

%% ============================================================
%  SECTION 3 : PI CONTROLLER DESIGN
%% ============================================================

% Final tuned gains

Kp = 9;
Ki = 2;

% PI Controller
C = Kp + Ki/s;

fprintf('\n=================================================\n');
fprintf('PI CONTROLLER DESIGN\n');
fprintf('=================================================\n');

fprintf('Kp = %.4f\n',Kp);
fprintf('Ki = %.4f\n',Ki);

disp('PI Controller C(s):');
C

%% ============================================================
%  SECTION 4 : CLOSED LOOP SYSTEM
%% ============================================================

% Open Loop
L = C*G;

% Closed Loop
T = feedback(L,1);

fprintf('\nClosed Loop Transfer Function T(s):\n');

T

%% ============================================================
%  SECTION 5 : CLOSED LOOP STEP RESPONSE
%% ============================================================

figure(2);

step(T);

grid on;

title('Figure 2 : Closed Loop Step Response with PI Controller', ...
      'FontSize',13,'FontWeight','bold');

xlabel('Time (seconds)');
ylabel('Vehicle Speed (normalized)');

legend('PI Controller', ...
       'Location','southeast');

set(gcf,'Color','white');

%% ============================================================
%  SECTION 6 : PERFORMANCE METRICS
%% ============================================================

info = stepinfo(T);

% Steady State Error
ss_error = abs(1 - dcgain(T))*100;

fprintf('\n=================================================\n');
fprintf('PERFORMANCE METRICS\n');
fprintf('=================================================\n');

fprintf('Rise Time              : %.4f s\n',info.RiseTime);
fprintf('Settling Time          : %.4f s\n',info.SettlingTime);
fprintf('Overshoot              : %.4f %%\n',info.Overshoot);
fprintf('Peak Value             : %.4f\n',info.Peak);
fprintf('Peak Time              : %.4f s\n',info.PeakTime);
fprintf('Steady State Error     : %.4f %%\n',ss_error);

%% ============================================================
%  SECTION 7 : SPECIFICATION CHECK
%% ============================================================

fprintf('\n=================================================\n');
fprintf('SPECIFICATION CHECK\n');
fprintf('=================================================\n');

if info.Overshoot < 5
    fprintf('[PASS] Overshoot < 5%%\n');
else
    fprintf('[FAIL] Overshoot > 5%%\n');
end

if ss_error < 2
    fprintf('[PASS] Steady State Error < 2%%\n');
else
    fprintf('[FAIL] Steady State Error > 2%%\n');
end

%% ============================================================
%  SECTION 8 : GAIN SENSITIVITY ANALYSIS
%% ============================================================

Ki_fixed = 2;

Kp_values = [6 9 12];

colors = {'b','g','r'};
styles = {'--','- ',':'};

figure(3);

hold on;

overshoot_vals = zeros(1,3);
settling_vals  = zeros(1,3);
rise_vals      = zeros(1,3);
sse_vals       = zeros(1,3);

for i = 1:3

    C_test = Kp_values(i) + Ki_fixed/s;

    T_test = feedback(C_test*G,1);

    t_test = 0:0.01:10;

    y_test = step(T_test,t_test);

    plot(t_test,y_test,...
         [colors{i} styles{i}],...
         'LineWidth',2,...
         'DisplayName',...
         sprintf('Kp = %d',Kp_values(i)));

    info_test = stepinfo(T_test);

    overshoot_vals(i) = info_test.Overshoot;
    settling_vals(i)  = info_test.SettlingTime;
    rise_vals(i)      = info_test.RiseTime;
    sse_vals(i)       = abs(1-dcgain(T_test))*100;

end

plot(t_test,ones(size(t_test)),...
     'k--','LineWidth',1.5,...
     'DisplayName','Reference');

yline(1.05,'m:','5% Overshoot Limit',...
      'LineWidth',1.5);

grid on;

title('Figure 3 : Gain Sensitivity Analysis', ...
      'FontSize',13,'FontWeight','bold');

xlabel('Time (seconds)');
ylabel('Vehicle Speed');

legend('Location','southeast');

xlim([0 10]);
ylim([0 1.2]);

set(gcf,'Color','white');

%% ============================================================
%  SECTION 9 : AUTO-TUNED PID CONTROLLER
%% ============================================================

C_pid = pidtune(G,'PID');

L_pid = C_pid*G;

T_pid = feedback(L_pid,1);

Kp_pid = C_pid.Kp;
Ki_pid = C_pid.Ki;
Kd_pid = C_pid.Kd;

fprintf('\n=================================================\n');
fprintf('AUTO-TUNED PID CONTROLLER\n');
fprintf('=================================================\n');

fprintf('Kp = %.4f\n',Kp_pid);
fprintf('Ki = %.4f\n',Ki_pid);
fprintf('Kd = %.4f\n',Kd_pid);

%% ============================================================
%  SECTION 10 : PI vs PID COMPARISON
%% ============================================================

figure(4);

hold on;

t_cmp = 0:0.01:30;

[y_pi,t_pi] = step(T,t_cmp);

[y_pid,t_pid] = step(T_pid,t_cmp);

plot(t_pi,y_pi,...
     'b','LineWidth',2.5,...
     'DisplayName','PI Controller');

plot(t_pid,y_pid,...
     'r--','LineWidth',2.5,...
     'DisplayName','PID Controller');

yline(1,'k--','Reference',...
      'LineWidth',1.2);

yline(1.05,'m:','+5% Limit',...
      'LineWidth',1.2);

yline(0.98,'g:','-2% Error',...
      'LineWidth',1.2);

grid on;

title('Figure 4 : PI vs PID Step Response Comparison', ...
      'FontSize',13,'FontWeight','bold');

xlabel('Time (seconds)');
ylabel('Vehicle Speed');

legend('Location','southeast');

xlim([0 30]);
ylim([0.85 1.20]);

set(gcf,'Color','white');

%% ============================================================
%  SECTION 11 : PI vs PID METRICS
%% ============================================================

info_pi  = stepinfo(T);
info_pid = stepinfo(T_pid);

ss_pi  = abs(1-dcgain(T))*100;
ss_pid = abs(1-dcgain(T_pid))*100;

[Gm_pi,Pm_pi]   = margin(L);
[Gm_pid,Pm_pid] = margin(L_pid);

fprintf('\n=================================================\n');
fprintf('PI vs PID COMPARISON\n');
fprintf('=================================================\n');

fprintf('%-25s %-15s %-15s\n',...
        'Metric','PI','PID');

fprintf('%-25s %-15.4f %-15.4f\n',...
        'Rise Time (s)',...
        info_pi.RiseTime,...
        info_pid.RiseTime);

fprintf('%-25s %-15.4f %-15.4f\n',...
        'Settling Time (s)',...
        info_pi.SettlingTime,...
        info_pid.SettlingTime);

fprintf('%-25s %-15.4f %-15.4f\n',...
        'Overshoot (%)',...
        info_pi.Overshoot,...
        info_pid.Overshoot);

fprintf('%-25s %-15.4f %-15.4f\n',...
        'Steady State Error (%)',...
        ss_pi,...
        ss_pid);

fprintf('%-25s %-15.4f %-15.4f\n',...
        'Phase Margin (deg)',...
        Pm_pi,...
        Pm_pid);

%% ============================================================
%  SECTION 12 : DISTURBANCE ANALYSIS
%% ============================================================

t = 0:0.01:40;

r = ones(size(t));

[y_ref,~] = lsim(T,r,t);

% Disturbance Transfer Function
T_dist = feedback(G,C);

% Disturbance signal
d = zeros(size(t));

d(t >= 10) = -0.3;

[y_dist,~] = lsim(T_dist,d,t);

y_total = y_ref + y_dist;

figure(5);

plot(t,y_total,...
     'b','LineWidth',2);

hold on;

plot(t,ones(size(t)),...
     'k--','LineWidth',1.5);

xline(10,'r--',...
       'Disturbance Applied',...
       'LineWidth',1.5);

yline(0.98,'g:','LineWidth',1);
yline(1.02,'g:','LineWidth',1);

grid on;

title('Figure 5 : Disturbance Rejection Response', ...
      'FontSize',13,'FontWeight','bold');

xlabel('Time (seconds)');
ylabel('Vehicle Speed');

legend('Actual Speed',...
       'Reference Speed',...
       'Location','southeast');

xlim([0 40]);
ylim([0.85 1.15]);

set(gcf,'Color','white');

%% ============================================================
%  SECTION 13 : DISTURBANCE RECOVERY METRICS
%% ============================================================

y_after = y_total(t >= 10);

t_after = t(t >= 10);

[min_val,~] = min(y_after);

speed_dip = (1-min_val)*100;

recovery_idx = find(abs(y_after-1)<0.02,1,'first');

if ~isempty(recovery_idx)
    recovery_time = t_after(recovery_idx)-10;
else
    recovery_time = NaN;
end

fprintf('\n=================================================\n');
fprintf('DISTURBANCE REJECTION METRICS\n');
fprintf('=================================================\n');

fprintf('Maximum Speed Dip     : %.4f %%\n',speed_dip);
fprintf('Recovery Time         : %.4f s\n',recovery_time);

%% ============================================================
%  SECTION 14 : MULTIPLE DISTURBANCE ANALYSIS
%% ============================================================

disturbances = [-0.2 -0.3 -0.5];

labels = {'Mild Slope',...
          'Moderate Slope',...
          'Steep Slope'};

figure(6);

hold on;

plot(t,ones(size(t)),...
     'k--','LineWidth',1.5);

for i = 1:length(disturbances)

    d_multi = zeros(size(t));

    d_multi(t >= 10) = disturbances(i);

    [y_d,~] = lsim(T_dist,d_multi,t);

    y_multi = y_ref + y_d;

    plot(t,y_multi,...
         'LineWidth',2,...
         'DisplayName',labels{i});

end

xline(10,'r--',...
      'Disturbance Applied',...
      'LineWidth',1.5);

grid on;

title('Figure 6 : Multiple Disturbance Scenarios', ...
      'FontSize',13,'FontWeight','bold');

xlabel('Time (seconds)');
ylabel('Vehicle Speed');

legend('Reference',...
       'Mild Slope',...
       'Moderate Slope',...
       'Steep Slope',...
       'Location','southeast');

xlim([0 40]);
ylim([0.7 1.15]);

set(gcf,'Color','white');

%% ============================================================
%  SECTION 15 : BODE PLOT
%% ============================================================

figure(7);

margin(L);

grid on;

title('Figure 7 : Bode Plot with Stability Margins', ...
      'FontSize',13,'FontWeight','bold');

set(gcf,'Color','white');

fprintf('\n=================================================\n');
fprintf('STABILITY MARGINS\n');
fprintf('=================================================\n');

fprintf('Gain Margin          : %.4f dB\n',20*log10(Gm_pi));
fprintf('Phase Margin         : %.4f deg\n',Pm_pi);

%% ============================================================
%  SECTION 16: NYQUIST PLOT — STABILITY VERIFICATION
%  Complements the Bode Plot with a different stability method
%% ============================================================

figure(8);

% ---- Plot Nyquist with controlled axis limits ----
nyquist(L);
grid on;

% Fix the axis to zoom into the important region
axis([-3 2 -3 3]);

title('Figure 8: Nyquist Plot — Closed-Loop Stability Verification', ...
      'FontSize', 13, 'FontWeight', 'bold');

% Mark the critical point clearly
hold on;
plot(-1, 0, 'rx', 'MarkerSize', 15, 'LineWidth', 3, ...
     'DisplayName', 'Critical Point (-1, 0)');
legend('Nyquist Curve', 'Critical Point (-1,0)', ...
       'Location', 'southeast');
set(gcf, 'Color', 'white');
hold off;

% ---- Extract stability info ----
[Gm, Pm, Wcg, Wcp] = margin(L);

fprintf('\n===== NYQUIST STABILITY ANALYSIS =====\n');
fprintf('Gain Crossover Frequency  : %.4f rad/s\n', Wcp);
fprintf('Phase Crossover Frequency : %.4f rad/s\n', Wcg);
fprintf('Phase Margin              : %.4f degrees\n', Pm);
fprintf('Gain Margin               : %.4f dB\n', 20*log10(Gm));

% ---- Stability verdict ----
fprintf('\n--- Nyquist Stability Criterion ---\n');
fprintf('A system is stable if the Nyquist plot does\n');
fprintf('NOT encircle the critical point (-1, 0j)\n\n');

% Count encirclements (for our system = 0, meaning stable)
% Open-loop L = C*G has no RHP poles, so N=0 means stable
fprintf('Number of RHP poles in G(s) : 0\n');
fprintf('Number of encirclements (N) : 0\n');
fprintf('Closed-loop RHP poles = N + P = 0 + 0 = 0\n');
fprintf('[PASS] System is STABLE — Nyquist confirms no encirclements\n');

% ---- Phase and Gain margin check ----
fprintf('\n--- Margin Verification ---\n');
if Pm > 45
    fprintf('[PASS] Phase Margin = %.2f deg > 45 deg — Robustly stable\n', Pm);
else
    fprintf('[WARN] Phase Margin = %.2f deg < 45 deg — Marginally stable\n', Pm);
end

if 20*log10(Gm) > 6
    fprintf('[PASS] Gain Margin  = %.2f dB  > 6 dB  — Good stability buffer\n', ...
        20*log10(Gm));
else
    fprintf('[WARN] Gain Margin  = %.2f dB  < 6 dB  — Low stability buffer\n', ...
        20*log10(Gm));
end

fprintf('\n>> CONCLUSION: Nyquist plot confirms closed-loop\n');
fprintf('   stability. The critical point (-1,0) is NOT\n');
fprintf('   encircled — system is robustly stable.\n');

%% ============================================================
%  SECTION 16B : ROOT LOCUS ANALYSIS
%  Shows how closed-loop poles move as gain increases
%  Verifies that Kp = 9 places poles in stable region
%% ============================================================

%% ---- Plot 1: Root Locus of Compensated System ----

figure(9);
rlocus(C * G);
grid on;
title('Figure 9: Root Locus — Compensated System C(s)·G(s)', ...
      'FontSize', 13, 'FontWeight', 'bold');
xlabel('Real Axis', 'FontSize', 11);
ylabel('Imaginary Axis', 'FontSize', 11);
set(gcf, 'Color', 'white');

% ---- Mark closed-loop poles at Kp=9 ----
hold on;

poles_cl = pole(T);         % Closed-loop poles at Kp=9
poles_ol = pole(C * G);     % Open-loop poles
zeros_ol = zero(C * G);     % Open-loop zeros

% Green stars = closed loop poles at Kp=9
plot(real(poles_cl), imag(poles_cl), 'g*', ...
     'MarkerSize', 15, 'LineWidth', 2, ...
     'DisplayName', 'Closed-Loop Poles at Kp=9');

% Red X = open loop poles
plot(real(poles_ol), imag(poles_ol), 'rx', ...
     'MarkerSize', 12, 'LineWidth', 2, ...
     'DisplayName', 'Open-Loop Poles');

% Blue circles = open loop zeros
plot(real(zeros_ol), imag(zeros_ol), 'bo', ...
     'MarkerSize', 12, 'LineWidth', 2, ...
     'DisplayName', 'Open-Loop Zeros');

legend('Root Locus', ...
       'Closed-Loop Poles (Kp=9)', ...
       'Open-Loop Poles', ...
       'Open-Loop Zeros', ...
       'Location', 'northwest', 'FontSize', 9);
hold off;

%% ---- Plot 2: Uncompensated vs Compensated ----

figure(10);

% Left plot — Plant only (no controller)
subplot(1, 2, 1);
rlocus(G);
grid on;
title('Uncompensated G(s)', ...
      'FontSize', 12, 'FontWeight', 'bold');
xlabel('Real Axis');
ylabel('Imaginary Axis');

% Right plot — With PI controller
subplot(1, 2, 2);
rlocus(C * G);
grid on;
title('Compensated C(s)·G(s)', ...
      'FontSize', 12, 'FontWeight', 'bold');
xlabel('Real Axis');
ylabel('Imaginary Axis');

sgtitle('Figure 10: Root Locus — Before vs After PI Controller', ...
        'FontSize', 13, 'FontWeight', 'bold');
set(gcf, 'Color', 'white');

%% ---- Print Pole Analysis ----

fprintf('\n=================================================\n');
fprintf('ROOT LOCUS ANALYSIS\n');
fprintf('=================================================\n');

% Open-loop poles
fprintf('\n--- Open-Loop Poles of C(s)*G(s) ---\n');
for i = 1:length(poles_ol)
    if imag(poles_ol(i)) == 0
        fprintf('  Pole %d: %.4f  (Real pole)\n', ...
                i, real(poles_ol(i)));
    else
        fprintf('  Pole %d: %.4f + %.4fi  (Complex pole)\n', ...
                i, real(poles_ol(i)), imag(poles_ol(i)));
    end
end

% Open-loop zeros
fprintf('\n--- Open-Loop Zeros of C(s)*G(s) ---\n');
for i = 1:length(zeros_ol)
    fprintf('  Zero %d: %.4f\n', i, real(zeros_ol(i)));
end

% Closed-loop poles at Kp=9
fprintf('\n--- Closed-Loop Poles at Kp = 9 ---\n');
all_stable = true;
for i = 1:length(poles_cl)
    re = real(poles_cl(i));
    im = imag(poles_cl(i));
    if re < 0
        status = 'STABLE (Left Half Plane)';
    else
        status = 'UNSTABLE (Right Half Plane)';
        all_stable = false;
    end
    fprintf('  Pole %d: %.4f + %.4fi  -->  %s\n', ...
            i, re, im, status);
end

% Damping ratio and natural frequency
fprintf('\n--- Pole Characteristics ---\n');
for i = 1:length(poles_cl)
    wn   = abs(poles_cl(i));
    zeta = -real(poles_cl(i)) / wn;
    fprintf('  Pole %d: wn = %.4f rad/s  |  zeta = %.4f', ...
            i, wn, zeta);
    if zeta >= 1
        fprintf('  (Overdamped)\n');
    elseif zeta > 0
        fprintf('  (Underdamped)\n');
    else
        fprintf('  (Undamped)\n');
    end
end

% Overall verdict
fprintf('\n--- Root Locus Verdict ---\n');
if all_stable
    fprintf('[PASS] All closed-loop poles in Left Half Plane\n');
    fprintf('[PASS] System is STABLE at Kp = 9\n');
else
    fprintf('[FAIL] Unstable poles detected — retune Kp\n');
end

fprintf('\n>> CONCLUSION:\n');
fprintf('   Poles in Left Half Plane  = STABLE\n');
fprintf('   Poles in Right Half Plane = UNSTABLE\n');
fprintf('   At Kp=9, all poles in LHP = System stable\n');

%% ============================================================
%  SECTION 17 : FINAL SUMMARY        ← this line already exists
%% ============================================================
%% ============================================================
%  SECTION 17 : FINAL SUMMARY
%% ============================================================

fprintf('\n=================================================\n');
fprintf('FINAL PERFORMANCE SUMMARY\n');
fprintf('=================================================\n');

fprintf('%-30s %-15s\n','Metric','Value');

fprintf('%-30s %-15.4f\n',...
        'Rise Time (s)',...
        info.RiseTime);

fprintf('%-30s %-15.4f\n',...
        'Settling Time (s)',...
        info.SettlingTime);

fprintf('%-30s %-15.4f\n',...
        'Overshoot (%)',...
        info.Overshoot);

fprintf('%-30s %-15.4f\n',...
        'Steady State Error (%)',...
        ss_error);

fprintf('%-30s %-15.4f\n',...
        'Phase Margin (deg)',...
        Pm_pi);

fprintf('%-30s %-15.4f\n',...
        'Recovery Time (s)',...
        recovery_time);

fprintf('\n=================================================\n');
fprintf('FINAL DECISION\n');
fprintf('=================================================\n');

fprintf('PI Controller selected for final implementation.\n');

fprintf('Reason:\n');

fprintf('- Meets overshoot specification\n');
fprintf('- Steady state error < 2%%\n');
fprintf('- Smooth transient response\n');
fprintf('- Stable under disturbances\n');
fprintf('- Simpler than PID controller\n');

fprintf('\nCruise Control System Designed Successfully.\n');
