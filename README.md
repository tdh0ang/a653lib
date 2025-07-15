# a653lib with Wasm Fuel Integration

## Current scheduling

### Overview

The forked repo is a base implementation of an ARINC653 scheduler, where two partitions A and B are scheduled. It is compliant with the standard. 

#### main.c
Calls to a653_i_update_partitions() and a653_i_wait_next() -> Scheduling

#### a653_config.h
A653_PARTITION_CONFIG_DEF defintion -> Partition, Num Time Slice

#### a653_lib/a653_i_sync.c
a653_i_update_partitions() and a653_i_wait_next() are implemented here

- **a653_i_update_partitions()**: Switches partitions according to the current time slice. Iteration over all cores, checks if the current time slice differs from the currently running one. If different: Stops and starts a new one, deactivates old one
- **a653_i_wait_next()**: Uses wall-clock time to wait until the next time slice starts


## WebAssembly and Fuel

### WebAssmembly (Wasm)
As of writing, WebAssembly or Wasm is a rather new technology. Intended to replace JavaScript, Wasm provides utility beyond web applications. Wasm is comparable to Java and it is designed to be a portable compilation target for programming languages. It allows applications to run in a sandboxed environment, i.e. a Wasm module cannot access memory outside its own memory space, no arbitrary function calls, no syscalls like with native binaries)

### Fuel
Fuel is a Wasm concept, or more precisely a concept introduced by Wasm runtimes. For more information refer to the Wasmtime documentation: https://docs.wasmtime.dev/examples-interrupting-wasm.html

As of right now, fuel is a concept to assign x units of fuel to a program/Wasm module, instead of a time slice for deterministic interruption. With this underlying idea, fuel opens up potential for an alternative way for scheduling, which differs from the traditional scheduling with time slices. To explore this concept, the a653lib from Airbus is used, where currently scheduling is implemented with time slicing. 

## Objective
Replacing the current time-slice based scheduling of partitions with a Wasm based fuel driven scheduler. Partitions should switch based on fuel consumption rather than elapsed time. 




