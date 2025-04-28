# traffic-light
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Traffic Light Control System</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            max-width: 800px;
            margin: 0 auto;
        }
        h1, h2, h3, h4 {
            color: #333;
        }
        h1 {
            border-bottom: 2px solid #333;
            padding-bottom: 10px;
        }
        h2 {
            border-bottom: 1px solid #ccc;
            padding-bottom: 5px;
        }
        ul, ol {
            margin: 10px 0;
            padding-left: 20px;
        }
        li {
            margin-bottom: 5px;
        }
        pre {
            background-color: #f4f4f4;
            padding: 10px;
            border-radius: 5px;
            overflow-x: auto;
        }
        code {
            font-family: Consolas, monospace;
        }
        a {
            color: #0066cc;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
        p {
            margin: 10px 0;
        }
    </style>
</head>
<body>
    <h1>Traffic-Light Control System</h1>

    <h2>Project Overview</h2>
    <p>This repository contains a traffic light control system designed for a four-way intersection, implemented using Logisim, a digital logic simulator. The system manages traffic lights for North-South (N-S) and East-West (E-W) directions, as well as pedestrian signals, based on vehicle and pedestrian sensor inputs. A 2-bit counter drives a Finite State Machine (FSM) to cycle through four states, controlling the traffic light sequence to ensure safe and efficient traffic flow.</p>
    <p>The system uses majority voting logic to activate the FSM only when three or more vehicle sensors detect traffic, prioritizing busy directions. Pedestrian safety is integrated by allowing crossings only during appropriate Green phases. The design emphasizes efficiency, logical correctness, real-world applicability, smooth transitions, and safety.</p>

    <h2>Features</h2>
    <ul>
        <li><strong>Traffic Light Control</strong>: Manages lights for North-South and East-West directions with Green, Yellow, and Red phases.</li>
        <li><strong>Pedestrian Signals</strong>: Controls pedestrian crossings for North, South, and East directions, ensuring safety.</li>
        <li><strong>Majority Voting Logic</strong>: Activates the traffic light sequence only when three or more vehicle sensors are active.</li>
        <li><strong>Finite State Machine (FSM)</strong>: Uses a 2-bit counter to cycle through four states:
            <ul>
                <li>State0 (00): North-South Green, East-West Red.</li>
                <li>State1 (01): North-South Yellow, East-West Red.</li>
                <li>State2 (10): East-West Green, North-South Red.</li>
                <li>State3 (11): East-West Yellow, North-South Red.</li>
            </ul>
        </li>
        <li><strong>Smooth Transitions</strong>: Includes Yellow phases to prevent abrupt changes, enhancing driver safety.</li>
        <li><strong>Pedestrian Safety</strong>: Pedestrian signals are active only during Green phases and when requested by sensors.</li>
    </ul>

    <h2>Repository Contents</h2>
    <ul>
        <li><code>traffic_light.circ</code>: The Logisim circuit file for the traffic light control system (if included; otherwise, see the implementation steps in the report).</li>
        <li><code>Traffic_Light_Control_System_Report.md</code>: A detailed report explaining the system design, logic, simulation results, and truth tables.</li>
        <li><code>screenshots/</code>: Directory containing screenshots of the circuit and simulation results (optional; add if desired).</li>
    </ul>

    <h2>Prerequisites</h2>
    <ul>
        <li><strong>Logisim</strong>: Download and install Logisim (version 2.7.1 or compatible) from <a href="http://www.cburch.com/logisim/">http://www.cburch.com/logisim/</a>.</li>
        <li>A basic understanding of digital logic circuits (logic gates, counters, FSMs).</li>
    </ul>

    <h2>Setup and Installation</h2>
    <ol>
        <li><strong>Clone the Repository</strong>:
            <pre><code>bash
git clone https://github.com/your-username/traffic-light-control-system.git
cd traffic-light-control-system
            </code></pre>
        </li>
        <li><strong>Install Logisim</strong>:
            <p>Ensure Logisim is installed on your system. If not, download it from the official website and follow the installation instructions.</p>
        </li>
        <li><strong>Open the Circuit</strong>:
            <p>Launch Logisim.</p>
            <p>Go to <code>File &gt; Open</code> and select <code>traffic_light.circ</code> from the repository.</p>
            <p>If the <code>.circ</code> file is not included, follow the implementation steps in the <code>Traffic_Light_Control_System_Report.md</code> to rebuild the circuit.</p>
        </li>
    </ol>

    <h2>Usage</h2>
    <ol>
        <li><strong>Load the Circuit</strong>:
            <p>Open <code>traffic_light.circ</code> in Logisim.</p>
        </li>
        <li><strong>Enable Simulation</strong>:
            <p>Go to <code>Simulate &gt; Simulation Enabled</code> (or press <code>Ctrl+E</code>).</p>
        </li>
        <li><strong>Set Inputs</strong>:
            <p>Use the poke tool (hand icon) to set the vehicle sensors (S_N, S_S, S_E, S_W) and pedestrian sensors (P_N, P_S, P_E, P_W) to 1 or 0 as needed.</p>
            <p>For example, to simulate heavy traffic in North-South, set S_N = 1, S_S = 1, S_W = 1, S_E = 0.</p>
        </li>
        <li><strong>Reset the Circuit</strong>:
            <p>Go to <code>Simulate &gt; Reset Simulation</code> (or press <code>Ctrl+R</code>) to initialize the counter to State0 (00).</p>
        </li>
        <li><strong>Run the Simulation</strong>:
            <p>Set the clock tick frequency to 1 Hz (<code>Simulate &gt; Tick Frequency &gt; 1 Hz</code>).</p>
            <p>Let the clock run, or manually tick using <code>Ctrl+T</code>, to observe the state transitions.</p>
        </li>
        <li><strong>Monitor Outputs</strong>:
            <p>Observe the traffic light LEDs (NG, NY, NR, etc.) and pedestrian signal outputs (P-N-SIGNAL, P-S-SIGNAL, P-E-SIGNAL).</p>
            <p>Use <code>Simulate &gt; Logging</code> to monitor the counter’s outputs (D1, D0) and other signals.</p>
        </li>
    </ol>

    <h2>System Functionality</h2>
    <p>The traffic light control system operates as follows:</p>
    <ul>
        <li><strong>Majority Voting Logic</strong>:
            <p>The system activates only when three or more vehicle sensors are active (e.g., S_N = S_S = S_W = 1).</p>
            <p>The MAJORITY signal gates the clock, ensuring the FSM only cycles during heavy traffic.</p>
        </li>
        <li><strong>State Transitions</strong>:
            <p>The 2-bit counter cycles through four states (00 → 01 → 10 → 11 → 00):</p>
            <ul>
                <li>State0 (00): North-South Green (NG, SG), East-West Red (ER, WR).</li>
                <li>State1 (01): North-South Yellow (NY, SY), East-West Red (ER, WR).</li>
                <li>State2 (10): East-West Green (EG, WG), North-South Red (NR, SR).</li>
                <li>State3 (11): East-West Yellow (EY, WY), North-South Red (NR, SR).</li>
            </ul>
        </li>
        <li><strong>Pedestrian Safety</strong>:
            <p>Pedestrian signals are active only during Green phases and when requested:</p>
            <ul>
                <li>P-N-SIGNAL and P-S-SIGNAL: Active in State0 if P_N = 1 or P_S = 1.</li>
                <li>P-E-SIGNAL: Active in State2 if P_E = 1.</li>
            </ul>
            <p>Signals are off during Yellow and Red phases, ensuring pedestrians do not cross unsafely.</p>
        </li>
        <li><strong>Simulation Scenarios</strong>:
            <ul>
                <li><strong>Heavy Traffic</strong>: The FSM cycles through all states, prioritizing busy directions.</li>
                <li><strong>Low Traffic</strong>: The system remains in its current state if fewer than three sensors are active.</li>
                <li><strong>Pedestrian Priority</strong>: Pedestrian signals activate during Green phases, ensuring safe crossings.</li>
            </ul>
        </li>
    </ul>
    <p>For a detailed explanation, including truth tables for the majority voting logic, FSM state transitions, and pedestrian signal control, refer to <code>Traffic_Light_Control_System_Report.md</code>.</p>

    <h2>Screenshots</h2>
    <p>(Add screenshots of the circuit and simulation results to the <code>screenshots/</code> directory and link them here. For example:)</p>
    <ul>
        <li>Circuit Overview: <img src="screenshots/circuit_overview.png" alt="Circuit Overview"></li>
        <li>Simulation in State0: <img src="screenshots/state0_simulation.png" alt="State0 Simulation"></li>
    </ul>

    <h2>Documentation</h2>
    <ul>
        <li><strong>Detailed Report</strong>: See <a href="Traffic_Light_Control_System_Report.md">Traffic_Light_Control_System_Report.md</a> for:
            <ul>
                <li>Logisim circuit design and implementation steps.</li>
                <li>Logic behind the switching mechanism (FSM with a 2-bit counter).</li>
                <li>How the system adapts to different traffic conditions (majority voting logic).</li>
                <li>How pedestrian safety is integrated (conditional signal activation).</li>
                <li>Simulation results under various traffic scenarios.</li>
                <li>Truth tables for majority voting, FSM transitions, and pedestrian signal control.</li>
            </ul>
        </li>
        <li><strong>Challenges and Solutions</strong>: The report also covers challenges faced (e.g., counter-to-decoder wiring issues) and their solutions.</li>
    </ul>

    <h2>Future Improvements</h2>
    <ul>
        <li><strong>Dynamic Timing</strong>: Adjust state durations based on traffic density.</li>
        <li><strong>State Skipping</strong>: Skip states if no traffic is detected in a direction.</li>
        <li><strong>Emergency Override</strong>: Add an input for emergency vehicles to override the FSM.</li>
        <li><strong>Pedestrian Countdown</strong>: Add a timer for pedestrian crossings in a real-world implementation.</li>
    </ul>

    <h2>Contributing</h2>
    <p>Contributions are welcome! If you have ideas for improvements or find issues, please:</p>
    <ol>
        <li>Fork the repository.</li>
        <li>Create a new branch (<code>git checkout -b feature/your-feature</code>).</li>
        <li>Make your changes and commit them (<code>git commit -m "Add your feature"</code>).</li>
        <li>Push to the branch (<code>git push origin feature/your-feature</code>).</li>
        <li>Open a pull request.</li>
    </ol>

    <h2>License</h2>
    <p>This project is licensed under the MIT License. See the <code>LICENSE</code> file for details.</p>

    <h2>Acknowledgments</h2>
    <ul>
        <li>Logisim: <a href="http://www.cburch.com/logisim/">http://www.cburch.com/logisim/</a></li>
        <li>Thanks to the digital logic design community for inspiration and resources.</li>
    </ul>
</body>
</html>
