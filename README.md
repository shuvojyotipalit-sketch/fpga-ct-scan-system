# FPGA-Based CT Scan System 

# Overview

This project implements a simplified **CT (Computed Tomography) scan reconstruction system** on FPGA using a streaming architecture. It demonstrates the core concept of **Filtered Back Projection (FBP)** using Verilog HDL.

---

# System Pipeline

Input Projection Data → FIR (Ram-Lak Filter) → Back Projection → Frame Buffer → Output Image

---

# Modules Description

# 1. FIR Ram-Lak Filter (`fir_ramlak.v`)

* Performs basic filtering of input projection data
* Uses a shift register structure
* Simplified implementation (data scaling used instead of real coefficients)

---

# 2. Back Projector (`back_projector.v`)

* Reconstructs pixel values from filtered data
* Uses FSM with states:

  * ACCUM (store data)
  * OUTPUT (send pixels)
  * WAIT (reset cycle)

---

# 3. Frame Buffer (`frame_buffer.v`)

* Stores reconstructed pixels in BRAM
* Supports:

  * Write phase (store image)
  * Read phase (output image)
* Generates `done` signal when frame is complete

---

# 4. Top Module (`top_ct_system.v`)

* Integrates all modules
* Controls data flow between stages

---

# 5. Testbench (`tb_ct_system.v`)

* Provides input stimulus
* Verifies system behavior
* Displays output pixels and completion signal

---

# Simulation

### Input:

* 20 sample values (e.g., 500, 1000, 1500, ...)

### Output:

* Reconstructed pixel values
* `pixel_valid` indicates valid output
* `done` indicates frame completion

---

# Features

* Modular FPGA design
* Streaming data processing
* FSM-based control logic
* BRAM-based image storage
* Fully synthesizable design

---

# Limitations

* Simplified FIR filter (not actual Ram-Lak)
* No angular projection modeling
* 1D reconstruction (not full 2D CT)
* No interpolation or scaling

---

#  Applications

* Medical imaging (CT reconstruction concepts)
* FPGA-based signal processing systems
* Real-time embedded image processing

---

# Novelty

This project demonstrates a **complete CT reconstruction pipeline implemented in hardware**, enabling **real-time processing** using FPGA — which is faster and more efficient compared to software-based approaches.

---

# Tools Used

* Verilog HDL
* Xilinx Vivado (for simulation & synthesis)

---

# Future Improvements

* Implement real Ram-Lak coefficients
* Extend to 2D image reconstruction
* Add rotation/angle handling
* Integrate with FPGA board (Zynq/Artix-7)

---

# License

This project is open-source and available under the MIT License.
