# Shape Generator in x86-64 Assembly

A terminal program for Linux, written in pure x86-64 assembly (NASM). It shows a menu
of six shapes and draws the one you pick in the terminal, with colours and full input checks.

University group project, team of 6.

## Shapes

| # | Shape | Built by |
|---|-------|----------|
| 1 | Diamond (manual or random mode) | Akhil |
| 2 | Right Triangle | Duha |
| 3 | Hollow Triangle | **Hajrah (me)** |
| 4 | Parallelogram (random size) | Heiza |
| 5 | Square | Jannat |
| 6 | Hollow Rectangle | Jumanah |

## My part: Hollow Triangle

- Asks for a symbol, a colour (0-7), a height (3-20) and a horizontal offset (0-40)
- Checks every input and asks again if it is wrong
- Builds the colour code (ANSI escape sequence) while the program runs
- Draws each row in a buffer with `rep stosb`, then prints the row with one system call
- The tip and the base are solid; the rows in between show only the edges

## What the program uses

- Linux system calls directly (`read`, `write`, `open`, `close`, `exit`), with no C library
- A random number generator (xorshift64), seeded from `/dev/urandom`
- ANSI escape codes for 15 terminal colours
- Careful register use: `rcx` and `r11` are overwritten by every `syscall`, so they are never used as loop counters

## How to run (Ubuntu / Linux)

```bash
sudo apt install nasm
nasm -f elf64 final.asm -o final.o
ld final.o -o final
./final
```