# with the -g option to generate debug information.
swiftc -g Factorial.swift

# run it through the LLDB debugger
lldb app


# Set a breakpoint on line 2 of the factorial(n:) function with the breakpoint set (b) command
b 2

(lldb) breakpoint set --file foo.c --line 12
(lldb) breakpoint set -f foo.c -l 12 

# Run the process with the run (r) command.
r

# Use the print (p) command to inspect the value of the n parameter.
p n

# Use the backtrace (bt) command to show the frames leading to factorial(n:) being called.
bt

# Use the continue (c) command to resume the process until the breakpoint is hit again.
c

# Use the breakpoint disable (br di) command to disable all breakpoints and the continue (c) command to have the process run until it exits.
br di # d in gdb
c
