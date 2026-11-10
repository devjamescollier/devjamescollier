# James Collier

Electrical and Computer Engineering @ USC | PCB Designer | Embedded Firmware Developer | Hardware Validation | Physics and Mathematics Enthusiast | Builder

## About Me

I'm a junior at the [University of Southern California](https://www.usc.edu/) studying Electrical and Computer Engineering with an emphasis in *Systems, Signals, and Learning*. I have an expected graduation date of May 2028.

I'm a hardware engineer first! I design printed circuit boards (PCBs), write the embedded firmware that brings them up, and validate them on the bench against the numbers I predicted on paper and in simulation. I have taken a **four-layer ESP32 flight computer**, a **dual-channel buck converter board**, and an **STM32 waveform generator** from requirements through layout, fabrication, and measured verification.

Around that hardware, I build the kind of software that flight systems depend on, including a **software-in-the-loop digital twin** of a small satellite's thermal and power systems and a **firmware update engine verified against 266 simulated power-loss points**. I'm especially drawn to spaceflight, and I want to work on hardware where a better circuit makes an entire mission more reliable!

## Projects

I love building things! Check out some of my projects!

### Hardware Projects

I am a hardware developer first. I enjoy PCB design and integrating electronic systems with embedded firmware. Most of my projects center around avionics, signal generation, data acquisition, and power systems!

#### [ESP32-Based Avionics and Telemetry Board](https://github.com/devjamescollier/ESP-32_Based_Avionics_and_Telemetry_Board)

- A compact **4-layer, 80 x 50 mm, 18.4 g flight computer** for small fixed-wing aircraft, built around an **ESP32-WROOM-32E** with dual SPI IMUs (**LSM6DSV32X**, **ASM330LHH**), an I²C magnetometer (**LIS3MDL**) and barometer (**MS5611**), and microSD logging. As the electrical sub-team member, I owned the electrical design from requirements through layout.
- Designed a protected **2S Li-Po power path** for four servos and one ESC: a **15 A fuse**, **P-FET reverse-polarity protection**, a **soft-started servo rail**, and an **AP63203 3.3 V buck**, with the MEMS sensors isolated from switching noise in layout.
- Released Gerbers, BOM, and CPL for **JLCPCB PCBA** after zero-error ERC and DRC, then validated the board with **ESP-IDF firmware in C**: a **3.301 V rail with 8.4 mVpp ripple**, **0 mA under a reversed battery**, and no brown-out in a 30-minute thermal soak.

`Altium Designer` `ESP32` `ESP-IDF` `Embedded C` `4-Layer PCB` `Avionics` `Data Acquisition`

#### [Dual-Channel Embedded Power Control Board](https://github.com/devjamescollier/Dual-Channel_Embedded_Power_Supply_Board)

- A battery-powered, two-layer DC-DC power board based on two **Texas Instruments TPS54331** buck converters. It converts a single **6-12 V** input into regulated **+5 V** and **+3.3 V** rails with reverse-battery protection, input UVLO, a 4 ms soft-start, and status LEDs.
- Wrote a Python generator for a cycle-by-cycle, peak-current-mode **ngspice** model of the TPS54331 built from its datasheet, and computed loop gain and phase margin (**60-67°**) before ordering the board.
- Hand-soldered and validated both rails with an **Agilent MSO-X 3034A**, measuring **90.2% / 90.8% efficiency** and **35 / 38 mVpp ripple at 1 A**, with **±1.5% regulation** across the full input range.

`KiCad EDA` `ngspice` `LTspice` `Python` `DC-DC Conversion` `Power Electronics`

#### [STM32-Based Programmable Waveform Generator](https://github.com/devjamescollier/STM32-Based_Programmable_Waveform_Generator)

- A USB-powered, 52 x 48 mm mixed-signal function generator built around the **STM32C031K6T6** and **MCP4901 SPI DAC**, with a **TLV2372** op-amp output stage, MOSFET output switching, an **LM1117** regulator, onboard controls, status LEDs, and an SWD programming interface.
- Wrote embedded C firmware using SPI, ADC, and timer peripherals to generate **sine and triangle waves to 50 kHz** and **square waves to 100 kHz**, and debugged the board over SWD with an ST-Link/V2.
- Verified the hand-soldered board with an Agilent MSO-X 3034A and Analog Discovery 3: **0.72% THD at 1 kHz**, **12 / 14 ns rise/fall times**, and **±1.2% amplitude accuracy**.

`KiCad EDA` `STM32` `STM32CubeIDE` `Embedded C` `Signals and Systems` `Mixed-Signal Design`

#### [LTspice Simulations](https://github.com/devjamescollier/LTspice_Simulations)

- A collection of five circuit simulations covering power conversion, RF frequency translation, precision analog front ends, and statistical tolerance analysis: a **closed-loop PI buck converter**, a **double-balanced diode ring mixer**, a **three-op-amp instrumentation amplifier**, a **500-run Monte Carlo RC band-pass filter**, and a **three-phase full-bridge inverter**.
- For every circuit, I predicted the behavior by hand first, then simulated it and explained where and why the results agreed. Highlights include **≈130 dB CMRR**, input-referred noise within **3%** of my hand estimate, and mixer LO feedthrough **≈47 dB** below the IF products.

`LTspice` `Transient / AC / Noise / FFT` `Monte Carlo` `Power Electronics` `RF` `Precision Analog`

### Software Projects

If you like my hardware, you'll love my software! Although I primarily focus on hardware, I enjoy writing low-level firmware, and I build mathematical simulations as well as testing platforms!

#### [Satellite Thermal and Power Digital Twin](https://github.com/devjamescollier/Satellite_Thermal_and_Power_Simulation)

- A **software-in-the-loop digital twin** of a small LEO satellite's thermal and electrical power systems. A **C++17** spacecraft simulator and separate C++ flight software run in 1 Hz lockstep over UDP, and the flight software estimates battery state with an **iterated Extended Kalman Filter**.
- A Python ground station streams **CCSDS telemetry** into **InfluxDB**, with **Grafana** mission-control dashboards and nine alert rules on top. Verified with a 50-run Monte Carlo (**0.034% RMS SOC error** after the first orbit), a headless fault campaign, and GoogleTest, pytest, and GitHub Actions CI.

`C++17` `Python` `Eigen` `Kalman Filtering` `CCSDS` `InfluxDB` `Grafana` `Docker`

#### [Power-Fail-Safe Firmware Update Simulator](https://github.com/devjamescollier/Power_Fail-Safe_Firmware_Update_Simulator)

- A firmware update simulator written in **C11** with two image slots, CRC-32 image validation, persistent flash metadata, trial boots, and automatic rollback when an update is not confirmed. The portable update engine uses **no heap and an 80-byte context**, and it reaches storage only through a three-function flash interface.
- A file-backed NOR flash model and a deterministic fault injector cut power at **every one of 266 interruption points** across eight update scenarios, and fresh processes verify recovery after each cut (**266 / 266 PASS**). Mutation testing proves the tests catch real bugs.

`C` `Python` `CMake` `CTest` `ASan / UBSan` `Embedded Software` `Fault Injection`

#### [Schrödinger Equation Simulation](https://github.com/devjamescollier/Schrodinger_Equation_Simulation)

- A numerical solver for the one-dimensional time-dependent Schrödinger equation written in **C++17**, using second-order finite differences and **Crank-Nicolson** time integration with an **O(N)** tridiagonal solve per step, a real-time **OpenGL** viewer, and a reproducible headless mode.
- A built-in suite of **16 validation studies** checks every accuracy claim against analytic solutions: measured **second-order convergence** in space and time, and norm and energy conserved to **~10⁻¹³** over 2,000 steps.

`C++` `OpenGL` `CMake` `Numerical Methods` `Mathematics` `Simulation`

## Experience

#### HITT Contracting | Construction Intern | May 2026 - August 2026

- Analyzed electrical single-line diagrams and power distribution requirements for a **SpaceX data center**, then evaluated and recommended transformers, UPS systems, and switchgear to drive procurement decisions.
- Specified, designed, and procured electrostatic dissipative (ESD) protection for an **L3Harris submarine test chamber** housing optronic imaging, sonar telemetry, and communications equipment, delivering within a $3,000 budget.

#### Backgrounds Online | Corporate Intern | July 2025 - January 2026

- Built and deployed a **Python data-validation pipeline** that audited county-coverage records across 50+ jurisdictions, surfacing and correcting discrepancies in 12 counties.
- Implemented hierarchical **RBAC** with least-privilege permissions, closing high-risk privilege-escalation paths.

## Technology Stack

For hardware development, I use **Altium Designer** and **KiCad EDA** for schematic capture and PCB layout, along with **LTspice**, **ngspice**, **QSpice**, and **Simulink** for modeling and simulation. I also work with **STM32CubeIDE**, **STM32CubeMX**, and **ESP-IDF** for configuring my microcontrollers, firmware development, and debugging. For mechanical and electromagnetic design, I use **SOLIDWORKS**, **Autodesk Fusion**, **AutoCAD**, **Ansys HFSS**, and **Ansys Maxwell**.

For software development, I work mostly in low-level **C** and **C++** with **Python** and **MATLAB** for testing, analysis, and simulation, as well as **Bash** for scripting. I primarily work with **STM32**, **ESP32**, and **ATmega328P** for embedded development, and I use **Verilog**, **SystemVerilog**, and **VHDL** for digital hardware design. I build with **CMake**, test with **CTest**, **GoogleTest**, and **pytest**, and ship with **Docker** and **GitHub Actions**. **Neovim** is my primary text editor.

| Task | Tools |
| :---: | :---: |
| **Software Languages** | ![C](https://img.shields.io/badge/C-A8B9CC?logo=c&logoColor=black) ![C++](https://img.shields.io/badge/C%2B%2B-00599C?logo=cplusplus&logoColor=white) ![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white) ![Rust](https://img.shields.io/badge/Rust-000000?logo=rust&logoColor=white) ![MATLAB](https://img.shields.io/badge/MATLAB-E16737?logo=mathworks&logoColor=white) ![Bash](https://img.shields.io/badge/Bash-4EAA25?logo=gnubash&logoColor=white) ![Tcl](https://img.shields.io/badge/Tcl-4D6D9A) ![x86 Assembly](https://img.shields.io/badge/x86%20Assembly-525252) |
| **Hardware Description Languages** | ![Verilog](https://img.shields.io/badge/Verilog-B2B7F8?logoColor=white) ![SystemVerilog](https://img.shields.io/badge/SystemVerilog-6E4C9A?logoColor=white) ![VHDL](https://img.shields.io/badge/VHDL-1F6FB2) |
| **PCB Design** | ![Altium Designer](https://img.shields.io/badge/Altium%20Designer-A5915F?logo=altiumdesigner&logoColor=white) ![KiCad EDA](https://img.shields.io/badge/KiCad%20EDA-314CB0?logo=kicad&logoColor=white) ![Autodesk Fusion Electronics](https://img.shields.io/badge/Fusion%20Electronics-0696D7?logo=autodesk&logoColor=white) ![EasyEDA](https://img.shields.io/badge/EasyEDA-1765F6) |
| **Circuit Simulation** | ![LTspice](https://img.shields.io/badge/LTspice-900028) ![ngspice](https://img.shields.io/badge/ngspice-2C3E50) ![QSpice](https://img.shields.io/badge/QSpice-00539B) ![Simulink](https://img.shields.io/badge/Simulink-E16737?logo=mathworks&logoColor=white) |
| **CAD & Electromagnetics** | ![SOLIDWORKS](https://img.shields.io/badge/SOLIDWORKS-E2231A?logo=dassaultsystemes&logoColor=white) ![Autodesk Fusion](https://img.shields.io/badge/Autodesk%20Fusion-F26A21?logo=autodesk&logoColor=white) ![AutoCAD](https://img.shields.io/badge/AutoCAD-E51050?logo=autodesk&logoColor=white) ![Ansys HFSS](https://img.shields.io/badge/Ansys%20HFSS-FFB71B?logo=ansys&logoColor=black) ![Ansys Maxwell](https://img.shields.io/badge/Ansys%20Maxwell-FFB71B?logo=ansys&logoColor=black) |
| **Microcontrollers & FPGAs** | ![STM32](https://img.shields.io/badge/STM32-03234B?logo=stmicroelectronics&logoColor=white) ![ESP32](https://img.shields.io/badge/ESP32-E7352C?logo=espressif&logoColor=white) ![ATmega328P](https://img.shields.io/badge/ATmega328P-EE0000?logo=microchip&logoColor=white) ![nRF52](https://img.shields.io/badge/nRF52-00A9CE?logo=nordicsemiconductor&logoColor=white) ![nRF54](https://img.shields.io/badge/nRF54-00A9CE?logo=nordicsemiconductor&logoColor=white) ![RP2040](https://img.shields.io/badge/RP2040-A22846?logo=raspberrypi&logoColor=white) ![Cmod A7-35T](https://img.shields.io/badge/Digilent%20Cmod%20A7--35T-5C2D91) ![Tang Nano 20K](https://img.shields.io/badge/Sipeed%20Tang%20Nano%2020K-2E7D32) |
| **Embedded Development** | ![STM32CubeIDE](https://img.shields.io/badge/STM32CubeIDE-03234B?logo=stmicroelectronics&logoColor=white) ![STM32CubeMX](https://img.shields.io/badge/STM32CubeMX-03234B?logo=stmicroelectronics&logoColor=white) ![ESP-IDF](https://img.shields.io/badge/ESP--IDF-E7352C?logo=espressif&logoColor=white) ![FreeRTOS](https://img.shields.io/badge/FreeRTOS-5A9A43?logo=freertos&logoColor=white) ![J-Link](https://img.shields.io/badge/J--Link-8DC63F) ![GDB](https://img.shields.io/badge/GDB-A42E2B?logo=gnu&logoColor=white) |
| **Build, Test & Deploy** | ![GCC](https://img.shields.io/badge/GCC-A42E2B?logo=gnu&logoColor=white) ![Clang / LLVM](https://img.shields.io/badge/Clang%20%2F%20LLVM-262D3A?logo=llvm&logoColor=white) ![Make](https://img.shields.io/badge/Make-6D00CC?logo=gnu&logoColor=white) ![CMake](https://img.shields.io/badge/CMake-064F8C?logo=cmake&logoColor=white) ![GoogleTest](https://img.shields.io/badge/GoogleTest-4285F4?logo=google&logoColor=white) ![pytest](https://img.shields.io/badge/pytest-0A9EDC?logo=pytest&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?logo=githubactions&logoColor=white) |
| **Data & Visualization** | ![Eigen](https://img.shields.io/badge/Eigen-0B5D8C) ![InfluxDB](https://img.shields.io/badge/InfluxDB-22ADF6?logo=influxdb&logoColor=white) ![Grafana](https://img.shields.io/badge/Grafana-F46800?logo=grafana&logoColor=white) ![OpenGL](https://img.shields.io/badge/OpenGL-5586A4?logo=opengl&logoColor=white) |
| **Development Tools** | ![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white) ![GitHub](https://img.shields.io/badge/GitHub-181717?logo=github&logoColor=white) ![Neovim](https://img.shields.io/badge/Neovim-57A143?logo=neovim&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black) ![macOS](https://img.shields.io/badge/macOS-000000?logo=apple&logoColor=white) ![Windows](https://img.shields.io/badge/Windows-0078D6) ![Microsoft Office](https://img.shields.io/badge/Microsoft%20Office-D83B01?logo=microsoft&logoColor=white) |

## Skills

| Area | Skills |
| :---: | :--- |
| **Hardware** | Schematic capture, multilayer PCB layout (2- and 4-layer), component selection, mixed-signal design, DC-DC converter design, power-path and reverse-polarity protection, grounding and noise isolation, manufacturing release (Gerbers, BOM, CPL for PCB assembly), hand soldering, hot-air rework |
| **Firmware** | Embedded C on STM32 and ESP32, peripheral configuration (GPIO, SPI, ADC, timers, interrupts), FreeRTOS, board bring-up, SWD and JTAG debugging, A/B firmware updates with rollback, portable heap-free C |
| **Software** | C, C++17, Python, Rust, MATLAB, Bash, Tcl, x86 Assembly, CMake, Docker, CI with GitHub Actions, InfluxDB and Grafana, CCSDS telemetry over UDP |
| **Communication Protocols** | UART, SPI, I²C, CAN, USB, Ethernet, TCP, MQTT, SWD |
| **Digital Design** | Verilog, SystemVerilog, VHDL, FPGA development (Digilent Cmod A7-35T, Sipeed Tang Nano 20K) |
| **Simulation & Analysis** | LTspice, ngspice, QSpice, Simulink, MATLAB; transient, AC, noise, FFT, and Monte Carlo analysis; control-loop and phase-margin analysis; Kalman filtering; numerical methods (finite differences, Crank-Nicolson, RK4) |
| **Testing & Validation** | Bench validation against hand analysis and simulation, ERC and DRC, fault injection, mutation testing, Monte Carlo validation, unit and integration testing (GoogleTest, pytest, CTest), AddressSanitizer and UndefinedBehaviorSanitizer |
| **Lab Equipment** | Oscilloscope (Agilent MSO-X 3034A), Digilent Analog Discovery 3, logic analyzer, spectrum analyzer, vector network analyzer, multimeter, function generator, DC bench power supply, JTAG and SWD debuggers (ST-Link/V2, J-Link), EEPROM programmer |

## Relevant Coursework

- **Electrical Engineering:** Introduction to Embedded Systems, Linear Circuits, Linear Systems, Distributed Systems for the Internet of Things, Applied Linear Algebra for Engineering, Introduction to Electrical Engineering
- **Mathematics & Physics:** Calculus I-III, Mathematics of Physics and Engineering I, Fundamentals of Physics I (Mechanics, Oscillations, and Waves) and II (Electricity and Magnetism)
- **Computer Science:** Object Oriented Programming, Fundamentals of Computation

## Engineering Interests

- PCB Design
- Avionics and Spaceflight Hardware
- Mixed-Signal Electronics
- Embedded Software
- Power Electronics
- Control Systems
- Hardware Validation
- Signal Processing
- Data Acquisition

## Interests Outside of Engineering

Outside of engineering, I love **mathematics**. I was a mathlete in high school, I'm studying for the **Putnam Competition**, and for fun I write and solve my own problems, like finding when the hands of a clock, treated as vectors, are linearly dependent. I'm also preparing for the **FE Electrical and Computer exam**. I train **Brazilian Jiu Jitsu**, play **chess**, played **varsity tennis** throughout high school, and I'm learning **Italian**. At USC, I'm a member of the **Rocket Propulsion Lab**, **USC Racing** (Formula SAE), and the **Chess Club**.

## Let's Connect!

Contact me if you are interested in working together!

- **Email:** [jwcollie@usc.edu](mailto:jwcollie@usc.edu)
- **LinkedIn:** [jameswyethcollier](https://www.linkedin.com/in/jameswyethcollier)
- **GitHub:** [@devjamescollier](https://github.com/devjamescollier)
