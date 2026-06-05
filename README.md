<img width="466" height="269" alt="image" src="https://github.com/user-attachments/assets/6d726376-5e40-4616-bd75-3dbf89770ebd" />

Multi-Source Trace Processing System (FPGA)
This diagram shows the high-level structure of the system.  
The pipeline includes:
- Frame generation and decoding
- Demultiplexing of trace sources
- Parallel trace decoding and analysis
- AXI Stream merging
- DMA-based memory transfer

Overview
This project implements a multi-channel trace processing system on FPGA using a Zynq-based platform.  
It captures trace data, processes it through multiple decoding and analysis stages, and merges the outputs into a single AXI stream for memory storage.

Full Block Design (Vivado)

<img width="919" height="346" alt="image" src="https://github.com/user-attachments/assets/aa06afab-364f-495a-a7b7-148444f23a68" />

<img width="907" height="384" alt="image" src="https://github.com/user-attachments/assets/b2746878-8d87-4ff0-88d7-ebdda4a18e60" /><img width="794" height="381" alt="image" src="https://github.com/user-attachments/assets/c7cf436a-9b1a-484d-8533-8810fa45f0cd" />




This is the complete Vivado block design of the system, showing all IP cores, interconnections, and AXI interfaces.

Main components:
- Zynq Processing System (PS)
Acts as the control and management unit of the system
Configures IP blocks via AXI-Lite
Controls DMA transfers
Provides access to DDR memory
Supplies clocks and resets to the programmable logic
- Frame Generator (`frame_gen_0`)
Converts incoming raw trace data into fixed-size frames (128-bit)
Adds structure to the data stream for easier decoding
Ensures alignment and proper formatting
- Frame Decoder (`frame_decoder_0`)
Extracts useful information from frames
Identifies frame boundaries and metadata (e.g., source ID)
Prepares data for routing in later stages
- Demultiplexer (`demux_0`)
Splits the decoded stream into multiple independent channels
Routes data based on source ID
Enables parallel processing of different trace streams
- Protocol Decoders (`protocol_decoder_0..3`)
Decode the trace data according to the trace protocol format
Convert encoded trace messages into meaningful signals/data
One decoder per channel → enables parallel operation
- Trace Analyzers (`trace_analyzer_0..3`)
Perform analysis on decoded trace data
Extract useful metrics, events, or patterns
Generate processed outputs for each trace channel
- Custom AXI Stream Merger (`axis_merger_4to1_0`)
Combines 4 AXI Stream inputs into 1 output stream
Uses round-robin arbitration to fairly select inputs
Handles:

TVALID, TREADY (handshake)
TLAST, TKEEP signals


Converts multiple analyzer outputs into a single continuous stream
- AXI DMA (`axi_dma_0`)
Transfers data from AXI Stream to DDR memory
Uses S2MM (Stream to Memory-Mapped) channel
Enables high-speed data movement without CPU load
- AXI SmartConnect
Connects multiple AXI components together
Routes data between:

AXI DMA
Zynq PS


Handles arbitration and address decoding
- ILA (debug)
Debugging tool inside FPGA
Captures internal signals in real time
Helps verify:

AXI handshakes
Data flow correctness
Timing issues

