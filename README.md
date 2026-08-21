# 5-Bit Carry Look-Ahead Adder

VLSI Design : NGSPICE · MAGIC · Verilog

A 5-bit Carry Look-Ahead Adder designed and verified using static CMOS gate design, TSPC flip-flop synchronization, MAGIC layout, pre and post layout SPICE simulation, and Verilog implementation deployed on FPGA.

## Table of Contents
- [Overview](#overview)
- [Why a Carry Look-Ahead Adder?](#why-a-carry-look-ahead-adder)
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

The design is carried through the full flow: transistor-level static CMOS gate design and simulation in **ngspice**, TSPC flip-flop synchronization at the input/output boundaries, full-custom layout in **MAGIC**, pre- and post-layout SPICE verification, and a final **Verilog** implementation

Propagate: Pi = Ai ⊕ Bi
Generate: Gi = Ai · Bi
