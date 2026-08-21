# 5-Bit Carry Look-Ahead Adder

VLSI Design : NGSPICE · MAGIC · Verilog

A 5-bit Carry Look-Ahead Adder designed and verified using static CMOS gate design, TSPC flip-flop synchronization, MAGIC layout, pre and post layout SPICE simulation, and Verilog implementation deployed on FPGA.

## Table of Contents
- [Overview](#overview)
- [CLA Design Topology](#cla-design-topology)
- [Transistor Sizing](#transistor-sizing)
- [NGSpice Simulations](#ngspice-simulations)
- [TSPC Flip-Flop Timing](#tspc-flip-flop-timing)
- [Stick Diagrams](#stick-diagrams)
- [Layout in MAGIC](#layout-in-magic)
- [Post-Layout Simulations](#post-layout-simulations)
- [Full Circuit: Pre- and Post-Layout](#full-circuit-pre--and-post-layout)
- [Floor Plan](#floor-plan)
- [Verilog Implementation](#verilog-implementation)
- [FPGA Implementation](#fpga-implementation)
- [Tools Used](#tools-used)

## Overview

Addition is a fundamental operation in digital circuits. A ripple-carry adder computes each carry only after the previous stage resolves, making it inherently sequential and introducing significant propagation delay. This project implements a 5-bit **Carry Look-Ahead Adder**, which computes all carry bits directly from the input bits using **generate (G)** and **propagate (P)** signals, avoiding the ripple delay and enabling much faster computation.

## CLA Design

For each bit position, two signals are defined:
- Propagate: Pi = Ai ⊕ Bi
- Generate: Gi = Ai · Bi

The carry-out of each stage is then expressed directly in terms of the inputs rather than the previous carry, so unlike the Ripple Adder it doesn't depend on previous outputs and is faster.

Expanding this recursively for all 5 bits:

C1 = g1 + p1·C0

C2 = g2 + p2·g1 + p2·p1·C0

C3 = g3 + p3·g2 + p3·p2·g1 + p3·p2·p1·C0

C4 = g4 + p4·g3 + p4·p3·g2 + p4·p3·p2·g1 + p4·p3·p2·p1·C0
C5 = g5 + p5·g4 + p5·p4·g3 + p5·p4·p3·g2 + p5·p4·p3·p2·g1 + p5·p4·p3·p2·p1·C0


Once all carries are available, every sum bit is computed independently and simultaneously:
Si = Pi ⊕ Ci−1

## CLA Design Topology

All logic gates — **AND** (2–6 input), **OR** (2–6 input), **NOT**, and **XOR** — are implemented using **static CMOS** logic. Multi-input AND/OR gates are built as a NAND/NOR stage followed by an inverter, since ngspice simulation showed lower delay from cascading dual-input gates than using single wide-input gates.

Static CMOS was chosen over dynamic logic styles because:
- The full output must resolve within a single clock cycle, which is difficult to guarantee with dynamic logic.
- Dynamic logic is susceptible to charge leakage.
- Precharge/evaluate phases in dynamic logic add power overhead.

Static CMOS also gives a simpler, more straightforward design with high noise margins for a robust implementation.

The circuit is organized into three blocks:
1. **Input flip-flops** — a TSPC (True Single-Phase Clock) flip-flop stage ensures all input bits arrive simultaneously, preventing glitches.
2. **Combinational CLA logic** — P/G generation, carry computation, and sum computation using the static CMOS gates described above. Carries are computed in parallel rather than waiting on previous stages.
3. **Output flip-flops** — a second TSPC stage latches the sum bits and final carry so results are available at the next rising clock edge.

