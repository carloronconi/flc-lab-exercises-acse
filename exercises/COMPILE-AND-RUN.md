# General workflow
1. `git checkout changes`
2. Make the modifications to `Acse.y`, `Acse.lex` and other source files of the compiler required to add a feature (e.g. adding support for the modulo operator)
2. Modify `program.src` (which is already valid LANCE code) using the added feature
3. `make` to compile the modifications of Acse into new Acse binaries located in `/bin` directory of the current project
4. Use the newly generated binaries to run the test program `program.src` with the new feature in 3 steps:
```
./bin/acse program.src
./bin/asm output.asm
./bin/mace output.o
```
5. `git add . && git commit -m "Make changes"`
6. `git checkout main`
6. `git diff main changes > exercises/ex5-1.patch`
7. `git add . && git commit -m "solve exercise" && git push`
8. delete changes branch

# To apply patch
1. `git checkout applied-patch`
2. `git apply exercises/ex5-1.patch`: the changes are applied!