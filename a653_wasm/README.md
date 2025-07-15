# a653 - Wasm
Source files related to the fuel driven scheduling

## Notes

### Baseline
- Scheduling implemented in a653_i_sync.c
- Scheduling functions (update partitions and wait) called in main superloop
- Partitions A & B are scheduled

### What adaptions are needed?
- Wasmtime -> Fuel injection -> Each partition gets an amount of fuel
- Fuel tracking/consumption only with .wasm modules possible
- Partitions A & B -> Need to consume fuel in order to advance/consume fuel 
- Out of fuel needs to be detected and partitions need to be switched based on out of fuel case
