# THESIS REPORT
submitted in final fulfillment of the requirements
for the award of the degree of
Bachelor of Technology in
Electronics and Communication Engineering (ECE)

## RTL to GDS-II Implementation of Diabetic Retinopathy Detection,A Comprehensive Approach from Neural-Networks to VLSI Systems

### K Charan
211001002024, Btech (ECE), TIU Kolkata

#### Abstract

This thesis presents the escalating prevalence of diabetic retinopathy (DR), a severe
microvascular complication of diabetes mellitus, has emerged as a leading cause of vision
impairment and blindness. Its progressive nature often goes unnoticed in the early
stages, highlighting the critical need for timely screening and early diagnosis. Manual
screening of retinal fundus images is not only labor-intensive and time-consuming but
also highly dependent on the availability of skilled ophthalmologists. In response to
these challenges deep learning (DL), has gained prominence in medical image analysis.
However, the real-time deployment of such models in portable, low-power systems
remains constrained by computational demands and energy inefficiency. This thesis
proposes an end-to-end hardware-software co-design for real-time diabetic retinopathy
detection, combining a quantized convolutional neural network (CNN) with a custom
RISC-V processor implemented on FPGA and synthesized for ASIC realization. The
foundation of this approach is a lightweight MobileNetV2 neural network, chosen for its
balance of computational efficiency and classification accuracy. The network is further
optimized through pruning and 8-bit quantization to suit hardware constraints while
retaining diagnostic fidelity. It performs binary classification on retinal images to
distinguish between referable and non-referable DR, with a final softmax layer
computing class probabilities. Retinal images are acquired using an ESP32-CAM
module operating in RGB mode, transmitting frames to the hardware system via
UART. A custom-designed RISC-V processor core, written in Chisel and extended from
the RV32I base instruction set with custom CNN-friendly instructions, serves as the
control unit. This core coordinates memory access, image preprocessing, CNN inference,
and result communication, creating a fully integrated edge AI pipeline. The design is
realized on a Genesys-2 FPGA, where the accelerator achieves real-time inference in 1.2
seconds while consuming only 11 mW of power, making it suitable for battery-powered
or remote clinical settings. The deep learning model is trained using the APTOS 2019
Blindness Detection dataset, which includes high-resolution fundus photographs labeled
according to DR severity. Data preprocessing steps such as grayscale conversion,
histogram equalization (CLAHE), and image normalization are applied to enhance
lesion visibility. Augmentation techniques, including rotation, flipping, and brightness
variation, are used to improve generalization. Training is performed with cross-entropy
loss and Adam optimizer, with early stopping and dropout regularization to prevent
overfitting. The trained model attains a classification accuracy of 94.38% on the test set.
Hardware acceleration is achieved through Verilog-based modules synthesized via Vivado
HLS. The system comprises three primary blocks: (1) an image preprocessor handling
pixel format conversion and contrast enhancement, (2) a CNN engine using 48 DSP
slices for parallel multiply-accumulate (MAC) operations across four convolutional
layers, and (3) a post-processing unit that applies classification thresholding (e.g., score
< 0.2 → No DR, score ≥ 0.8 → Severe DR) using combinational logic. The CNN
weights and intermediate feature maps are stored using a tiered memory architecture
involving DDR3L (1GB), BRAM (64KB), and on-chip registers. Custom AXI4-Lite
interfacing enables seamless communication between modules and with the RISC-V
core. The implementation follows a complete RTL-to-GDSII design flow. After RTL
simulation and FPGA prototyping, the Verilog design is synthesized using Synopsys
Design Compiler with a 65nm standard cell library. Physical design steps including
floorplanning, placement, clock tree synthesis, routing, and parasitic extraction are
performed in Cadence Innovus. Power optimization is achieved via clock gating and
low-Vt cell libraries, resulting in an energy-efficient layout with verified timing closure.
The final GDSII layout is verified for functional and physical correctness using DRC and
LVS checks, demonstrating manufacturability. System performance is validated through
Verilator simulations, logic analysis on the FPGA board, and UART-based debugging
via Python scripts. A C/C++ program compiled using the RISC-V GNU toolchain is
converted into a hex instruction memory, loaded onto the processor through UART, and
executed upon trigger. The system captures output from data memory and validates
classification correctness against expected results. The full pipeline—from image capture
and preprocessing to hardware-accelerated inference and result communication—achieves
deterministic latency and low power usage, ideal for deployment in mobile DR screening
platforms. The integration of neural network inference with hardware-level acceleration,
embedded in a scalable RISC-V framework, represents a modular approach to medical
AI system design. The use of Chisel for processor generation allows future expansion to
support complex neural architectures such as Vision Transformers or hybrid CNN-RNN
models. The processor-accelerator coupling via custom ISA extensions and
memory-mapped registers creates a flexible environment for real-time inference. This
thesis thus demonstrates a robust methodology for designing clinically viable, low-power
AI hardware for medical imaging applications. By showcasing a complete pipeline—from
model selection and optimization to FPGA prototyping and ASIC implementation—it
sets a precedent for future research in edge-based diagnostic systems, particularly for use
in underserved and remote healthcare settings
