# rustguess — a number-guessing Linux kernel module in Rust

rustguess is a Linux kernel module that runs a number-guessing game at /dev/rustguess — a small example of a stateful, user-driven protocol written entirely in safe Rust.

## Features

- Character device at `/dev/rustguess`
- Guess parsing through `write_iter()`
- Hint responses through `read_iter()`
- Mutex-protected shared game state
- Graceful handling of malformed input
- Win tracking and replay protection

## Build & Run

```bash
make clean && make

sudo insmod rustguess.ko

sudo cat /dev/rustguess

echo 50 | sudo tee /dev/rustguess > /dev/null
sudo cat /dev/rustguess

echo 42 | sudo tee /dev/rustguess > /dev/null
sudo cat /dev/rustguess

sudo rmmod rustguess
```

## Design Notes

The module uses a global mutex-protected `GameState` strucutre to store:
- latest response message
- guess count
- win state

`write_iter()` parses user guess and updates game state, while `read_iter()`

Malformed input is handled safely without panicking the kernel.

## Future Work

- Use the kernel RNG to generate a random secret number at module load time
- Add per-open game state so multiple users can play simultaneously
- Add configurable difficulty levels
- Track guess history
- Add a debug-only reveal command
- Add a `/proc/rustguess` interface

## License

Licensed under GPL-2.0 to match the linux kernel
