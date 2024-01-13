1. Make the modifications to `Acse.y`, `Acse.lex` and other source files of the compiler required to add a feature (e.g. adding support for the modulo operator)
2. Modify `program.src` (which is already valid LANCE code) using the added feature
3. `make` to compile the modifications of Acse into new Acse binaries located in `/bin` directory of the current project
4. Use the newly generated binaries to run the test program `program.src` with the new feature in 3 steps:
```
./bin/acse program.src
./bin/asm output.asm
./bin/mace output.o
```