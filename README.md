# bitsofvim

##  c
**Normal**

navigate:

`G` go to first char of last line

`gg` go to first char of first line

go to insert:

`o` create a new line below (lowercase o)

`O` create a new line above (uppercase o)

`A` end of line

`s` delete character

indent lines:

`>>` indent current line

`>G` indent all lines to end of file

`:put` replay the last register on the next line

`:put a` replay register a on the next line

## Macros

We can record any number of keystrokes into a register and replay/apply them. You can run macros in a dependent series or run them in "independent parallell". 

Its important to try and use the most repeatable actions to replay. Instead of moving with `l` to your desired placement, use text movements such as `f+` to find the `+` correct symbol regardless of character distance.

### Commands:

**How to: start a macro recording to a register**

`q` starts the macro recording

`<register>` designates a letter to save into the register

`q` ends the macro recording

**How to: run a macro**

`@<register>` run the macro

`22@<register>` run the macro 22 times (macro series)

### Basics

`qaA;<Esc>` start macro recording at register a, Append at end of list charater `;` and ESC

#### Macros and series' shortcircuit on failure

**What does that mean?**

If your macro reaches a command, it cannot perform, the macro or the entire series of macros will abort

**How do we take advantage of this?**

Structure your macros with "navigating/finding" commands

**How to: Run a macro series**

```txt
@tmp.txt
1. one
2. two
3. three
4. four
```

```
@vim
vim1> qa - record at register a
vim2> 0f. - go to beginning of the line, find `.`
vim3> r) - replace `.` with `)`
vim3> j - navigate to the next line
vim4> q
vim5> 1000@a

note the shortcircuiting points 
vim3 will shortcircuit on not finding a next line
vim2 will shortcircuit on not finding `.`

vim5 will run until short circuiting
```

#### Run macros on every line individually (parallel)

Why? Files like this will not like your previous macro, since it will shortcircuit on your comment or on `f.`

**How to: Run a macro on all lines (parallel)**

```
@tmp.txt
1. one
2. two
// remember the milk
3. three
4. four
```

- [ ] `VG` create a visual block 
- [ ] `'<,'>normal @a` run the macro

