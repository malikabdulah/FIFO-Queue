# 10-Slot 4-Bit FIFO Queue Logic Circuit

A hardware level First In First Out (FIFO) queue designed and simulated using standard Transistor Transistor Logic (TTL) integrated circuits. This project implements a pointer based memory architecture to efficiently buffer 4-bit data words across 10 distinct memory slots.

## 🚀 Overview

This digital logic design project demonstrates asynchronous data buffering. Instead of relying on a shift register architecture which can introduce high propagation delays, this design uses stationary registers dynamically addressed by synchronous Read and Write counters. 

### Key Features
* **10 Slot Capacity:** Stores up to ten 4-bit data words.
* **Hardware Level Control:** Built entirely using fundamental TTL ICs.
* **Boundary Flags:** Visual indicators for Queue Full (Red LED) and Queue Empty (Green LED) states to prevent data overwrite and invalid reads.
* **Strict Sequential Operation:** Designed for a specific "Fill then Drain" operational pipeline.

## 🛠️ Components Used

The logic circuit is built around the following core components:
* **74173 (4-Bit D-Type Registers):** Forms the core memory array, providing 10 individual storage slots.
* **74193 (Synchronous Up/Down Counters):** Acts as the dynamic Read Pointer, Write Pointer, and Element Counter.
* **74154 (4-to-16 Line Decoder):** Translates the Write counter value to specific register enable signals for accurate data routing.
* **74157 (Quad 2-to-1 Multiplexer):** Regulates the input flow based on current state flags.
* **Logic Gates:** Custom combinational logic used to trigger Full and Empty boundary states.

## ⚙️ How It Works

This specific queue design follows a strict one way, sequential operational rule. You must fill the buffer entirely before draining it. 

1. **Initialization (Active Low Reset):** Before beginning any operations, the system must be reset. The Reset pin is **active low**. Pulling it to logic `0` clears all internal counters to zero and illuminates the Empty indicator flag. It must be returned to logic `1` to begin standard operation.

2. **Writing Data (Fill Phase):** * Input your 4-bit data.
   * Toggle the Write signal. The 74154 decoder routes the data to the correct 74173 register based on the current Write Pointer.
   * Continue writing until all 10 slots are filled.
   * Once the 10th item is written, the Full indicator flag activates, and any further write signals are safely blocked by the control gates.

3. **Reading Data (Drain Phase):**
   * Once the queue is fully populated, begin toggling the Read signal.
   * The queue will push the stored 4-bit words to the output bus in the exact order they were entered (FIFO).
   * Continue reading until all items are extracted.
   * Once the last item is read, the Empty indicator flag activates, blocking any further read attempts until new data is written.

## 💻 Simulation

This project was built and tested using LogicWorks. 

To view or simulate the circuit:
1. Clone this repository.
2. Open the provided circuit schematic file in LogicWorks.
3. Toggle the active low reset.
4. Use the input switches to load 4-bit data and toggle the Write pin to fill the queue.
5. Toggle the Read pin to output the data and observe the sequential output.
