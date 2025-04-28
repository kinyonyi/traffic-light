\# traffic-light   Traffic Light Control System body { font-family: Arial, sans-serif; line-height: 1.6; margin: 0; padding: 20px; max-width: 800px; margin: 0 auto; } h1, h2, h3, h4 { color: #333; } h1 { border-bottom: 2px solid #333; padding-bottom: 10px; } h2 { border-bottom: 1px solid #ccc; padding-bottom: 5px; } ul, ol { margin: 10px 0; padding-left: 20px; } li { margin-bottom: 5px; } pre { background-color: #f4f4f4; padding: 10px; border-radius: 5px; overflow-x: auto; } code { font-family: Consolas, monospace; } a { color: #0066cc; text-decoration: none; } a:hover { text-decoration: underline; } p { margin: 10px 0; }

Traffic-Light Control System
============================

Project Overview
----------------

This repository contains a traffic light control system designed for a four-way intersection, implemented using Logisim, a digital logic simulator. The system manages traffic lights for North-South (N-S) and East-West (E-W) directions, as well as pedestrian signals, based on vehicle and pedestrian sensor inputs. A 2-bit counter drives a Finite State Machine (FSM) to cycle through four states, controlling the traffic light sequence to ensure safe and efficient traffic flow.

The system uses majority voting logic to activate the FSM only when three or more vehicle sensors detect traffic, prioritizing busy directions. Pedestrian safety is integrated by allowing crossings only during appropriate Green phases. The design emphasizes efficiency, logical correctness, real-world applicability, smooth transitions, and safety.

Features
--------

*   **Traffic Light Control**: Manages lights for North-South and East-West directions with Green, Yellow, and Red phases.
*   **Pedestrian Signals**: Controls pedestrian crossings for North, South, and East directions, ensuring safety.
*   **Majority Voting Logic**: Activates the traffic light sequence only when three or more vehicle sensors are active.
*   **Finite State Machine (FSM)**: Uses a 2-bit counter to cycle through four states:
    *   State0 (00): North-South Green, East-West Red.
    *   State1 (01): North-South Yellow, East-West Red.
    *   State2 (10): East-West Green, North-South Red.
    *   State3 (11): East-West Yellow, North-South Red.
*   **Smooth Transitions**: Includes Yellow phases to prevent abrupt changes, enhancing driver safety.
*   **Pedestrian Safety**: Pedestrian signals are active only during Green phases and when requested by sensors.

Repository Contents
-------------------

*   `traffic_light.circ`: The Logisim circuit file for the traffic light control system (if included; otherwise, see the implementation steps in the report).
*   `Traffic_Light_Control_System_Report.md`: A detailed report explaining the system design, logic, simulation results, and truth tables.
*   `screenshots/`: Directory containing screenshots of the circuit and simulation results (optional; add if desired).

Prerequisites
-------------

*   **Logisim**: Download and install Logisim (version 2.7.1 or compatible) from [http://www.cburch.com/logisim/](http://www.cburch.com/logisim/).
*   A basic understanding of digital logic circuits (logic gates, counters, FSMs).

Setup and Installation
----------------------

1.  **Clone the Repository**:
    
        bash
        git clone https://github.com/your-username/traffic-light-control-system.git
        cd traffic-light-control-system
                    
    
2.  **Install Logisim**:
    
    Ensure Logisim is installed on your system. If not, download it from the official website and follow the installation instructions.
    
3.  **Open the Circuit**:
    
    Launch Logisim.
    
    Go to `File > Open` and select `traffic_light.circ` from the repository.
    
    If the `.circ` file is not included, follow the implementation steps in the `Traffic_Light_Control_System_Report.md` to rebuild the circuit.
    

Usage
-----

1.  **Load the Circuit**:
    
    Open `traffic_light.circ` in Logisim.
    
2.  **Enable Simulation**:
    
    Go to `Simulate > Simulation Enabled` (or press `Ctrl+E`).
    
3.  **Set Inputs**:
    
    Use the poke tool (hand icon) to set the vehicle sensors (S\_N, S\_S, S\_E, S\_W) and pedestrian sensors (P\_N, P\_S, P\_E, P\_W) to 1 or 0 as needed.
    
    For example, to simulate heavy traffic in North-South, set S\_N = 1, S\_S = 1, S\_W = 1, S\_E = 0.
    
4.  **Reset the Circuit**:
    
    Go to `Simulate > Reset Simulation` (or press `Ctrl+R`) to initialize the counter to State0 (00).
    
5.  **Run the Simulation**:
    
    Set the clock tick frequency to 1 Hz (`Simulate > Tick Frequency > 1 Hz`).
    
    Let the clock run, or manually tick using `Ctrl+T`, to observe the state transitions.
    
6.  **Monitor Outputs**:
    
    Observe the traffic light LEDs (NG, NY, NR, etc.) and pedestrian signal outputs (P-N-SIGNAL, P-S-SIGNAL, P-E-SIGNAL).
    
    Use `Simulate > Logging` to monitor the counter’s outputs (D1, D0) and other signals.
    

System Functionality
--------------------

The traffic light control system operates as follows:

*   **Majority Voting Logic**:
    
    The system activates only when three or more vehicle sensors are active (e.g., S\_N = S\_S = S\_W = 1).
    
    The MAJORITY signal gates the clock, ensuring the FSM only cycles during heavy traffic.
    
*   **State Transitions**:
    
    The 2-bit counter cycles through four states (00 → 01 → 10 → 11 → 00):
    
    *   State0 (00): North-South Green (NG, SG), East-West Red (ER, WR).
    *   State1 (01): North-South Yellow (NY, SY), East-West Red (ER, WR).
    *   State2 (10): East-West Green (EG, WG), North-South Red (NR, SR).
    *   State3 (11): East-West Yellow (EY, WY), North-South Red (NR, SR).
*   **Pedestrian Safety**:
    
    Pedestrian signals are active only during Green phases and when requested:
    
    *   P-N-SIGNAL and P-S-SIGNAL: Active in State0 if P\_N = 1 or P\_S = 1.
    *   P-E-SIGNAL: Active in State2 if P\_E = 1.
    
    Signals are off during Yellow and Red phases, ensuring pedestrians do not cross unsafely.
    
*   **Simulation Scenarios**:
    *   **Heavy Traffic**: The FSM cycles through all states, prioritizing busy directions.
    *   **Low Traffic**: The system remains in its current state if fewer than three sensors are active.
    *   **Pedestrian Priority**: Pedestrian signals activate during Green phases, ensuring safe crossings.

For a detailed explanation, including truth tables for the majority voting logic, FSM state transitions, and pedestrian signal control, refer to `Traffic_Light_Control_System_Report.md`.

Screenshots
-----------

(Add screenshots of the circuit and simulation results to the `screenshots/` directory and link them here. For example:)

*   Circuit Overview: ![Circuit Overview](screenshots/circuit_overview.png)
*   Simulation in State0: ![State0 Simulation](screenshots/state0_simulation.png)

Documentation
-------------

*   **Detailed Report**: See [Traffic\_Light\_Control\_System\_Report.md](Traffic_Light_Control_System_Report.md) for:
    *   Logisim circuit design and implementation steps.
    *   Logic behind the switching mechanism (FSM with a 2-bit counter).
    *   How the system adapts to different traffic conditions (majority voting logic).
    *   How pedestrian safety is integrated (conditional signal activation).
    *   Simulation results under various traffic scenarios.
    *   Truth tables for majority voting, FSM transitions, and pedestrian signal control.
*   **Challenges and Solutions**: The report also covers challenges faced (e.g., counter-to-decoder wiring issues) and their solutions.

Future Improvements
-------------------

*   **Dynamic Timing**: Adjust state durations based on traffic density.
*   **State Skipping**: Skip states if no traffic is detected in a direction.
*   **Emergency Override**: Add an input for emergency vehicles to override the FSM.
*   **Pedestrian Countdown**: Add a timer for pedestrian crossings in a real-world implementation.

Contributing
------------

Contributions are welcome! If you have ideas for improvements or find issues, please:

1.  Fork the repository.
2.  Create a new branch (`git checkout -b feature/your-feature`).
3.  Make your changes and commit them (`git commit -m "Add your feature"`).
4.  Push to the branch (`git push origin feature/your-feature`).
5.  Open a pull request.

License
-------

This project is licensed under the MIT License. See the `LICENSE` file for details.

Acknowledgments
---------------

*   Logisim: [http://www.cburch.com/logisim/](http://www.cburch.com/logisim/)
*   Thanks to the digital logic design community for inspiration and resources.
