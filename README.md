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
- Frame Generator (`frame_gen_0`)
- Frame Decoder (`frame_decoder_0`)
- Demultiplexer (`demux_0`)
- Protocol Decoders (`protocol_decoder_0..3`)
- Trace Analyzers (`trace_analyzer_0..3`)
- Custom AXI Stream Merger (`axis_merger_4to1_0`)
- AXI DMA (`axi_dma_0`)
- AXI SmartConnect
- ILA (debug)

