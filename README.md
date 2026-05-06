# rustguess — a number-guessing Linux kernel module in Rust

rustguess is a Linux kernel module that runs a number-guessing game at /dev/rustguess. Users write guesses into the device and read hints back from the kernel.

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


