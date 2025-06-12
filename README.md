# Digital Voting System with Positional Ranking

This repository contains the design and simulation files for a complex digital voting system built entirely from standard TTL logic integrated circuits. The system is designed for a five-contestant election and implements advanced logic to determine not only the vote counts but also the second and third-place winners in real-time.

This project serves as a comprehensive academic exercise in digital systems design, demonstrating the practical application of synchronous counters, combinational logic, and arithmetic circuits to solve a real-world problem.

---

## Key Features

-   **Five Contestant Support:** The system can simultaneously track and display votes for five contestants (A, B, C, D, E).
-   **Real-Time Vote Display:** Each contestant has a dedicated 7-segment display showing their current vote count.
-   **Vote Limiter:** Voting is automatically disabled after a total of 10 votes have been cast across all contestants.
-   **Master Reset:** A single push-button resets all vote counts to zero, allowing the election to be restarted.
-   **Advanced Positional Ranking:** The circuit includes a sophisticated logic module that analyzes the vote counts to determine:
    -   **Second Place Winner:** Indicated by a dedicated LED.
    -   **Third Place Winner:** Indicated by a dedicated LED.
-   **Modular TTL Design:** The entire system is built using standard 74xx series logic chips, making it a pure digital logic implementation without any microcontrollers.

---

## System Architecture

The system is architecturally divided into two primary subsystems: a **Vote Counting Module** and a **Positional Ranking Module**. The vote counts from the first module are fed directly into the second module for analysis.
![{1DD8156D-E0B0-4DB7-B29F-78920EDFB1FF}](https://github.com/user-attachments/assets/b441af50-d273-4a89-a3e4-e9b48914d6dd)

---

## Core Logic: The "Tally of Wins" Method

Determining rank is achieved by comparing each contestant against every other contestant and tallying the number of "wins" (i.e., having a strictly higher vote count). A contestant's final rank is determined by their total number of wins.

Let $S_2, S_1, S_0$ be the first three bits of the win-count sum for a given contestant.

### Logic for Third Place (Win Count = 2)

A contestant is in third place if their win count is exactly 2 (binary `...010`). The logic equation implemented in hardware is:
$$
\text{Is\_Third\_Place} = (\overline{S_2} \land S_1 \land \overline{S_0})
$$

### Logic for Second Place (Win Count = 3)

A contestant is in second place if their win count is exactly 3 (binary `...011`). The logic equation implemented in hardware is:
$$
\text{Is\_Second\_Place} = (\overline{S_2} \land S_1 \land S_0)
$$

This method is implemented using a two-stage adder circuit for each contestant to ensure mathematical correctness for all vote combinations.

---

## Technology and Simulation

-   **Core Technology:** Standard 74xx Series TTL Logic ICs
-   **Simulation Environment:** Proteus Design Suite
-   **Key Components:**
    -   `74LS161` (4-Bit Synchronous Counter)
    -   `74LS85` (4-Bit Magnitude Comparator)
    -   `74LS283` (4-Bit Full Adder)
    -   `74LS47` (BCD to 7-Segment Decoder)
    -   Logic Gates: `74LS04` (NOT), `74LS08` (AND), `74LS32` (OR)

---

## How to Use

1.  Clone this repository to your local machine.
2.  Open the `.pdsprj` file using Proteus Design Suite.
3.  Run the simulation from the main schematic window.
4.  **Important:** After starting the simulation, press the **RESET** button once to clear all counters to zero.
5.  Use the vote buttons to cast votes for contestants A, B, C, D, and E.
6.  Observe the 7-segment displays for individual counts and the ranking LEDs for second and third-place results.

---

## Future Enhancements

-   **First Place & Tie Detection:** Expand the logic to explicitly indicate the first-place winner and to detect tie scenarios.
-   **Physical Implementation:** Translate the simulated design into a physical prototype using a printed circuit board (PCB).
-   **Microcontroller Integration:** Replace the ranking logic with a microcontroller to simplify the circuit and add features like displaying contestant names on an LCD screen.
