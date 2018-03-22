# r2cheat
A radare2 cheat sheet compiled from various sources

## Debug commands ##
<pre><code>
db[?]                   Breakpoints commands
dbt[?]                  Display backtrace based on dbg.btdepth and dbg.btalgo
dc[?]                   Continue execution
dd[?]                   File descriptors (!fd in r1)
de[-sc] [rwx] [rm] [e]  Debug with ESIL (see de?)
dg [file]               Generate a core-file (WIP)
dH [handler]            Transplant process to a new handler
di[?]                   Show debugger backend information (See dh)
dk[?]                   List, send, get, set, signal handlers of child
dL [handler]            List or set debugger handler
dm[?]                   Show memory maps
do[?]                   Open process (reload, alias for 'oo')
doo[args]               Reopen in debugger mode with args (alias for 'ood')
dp[?]                   List, attach to process or thread id
dr[?]                   Cpu registers
ds[?]                   Step, over, source line
dt[?]                   Display instruction traces (dtr=reset)
dw [pid]                Block prompt until pid dies
dx[?]                   Inject and run code on target process (See gs)
db* > bps               Save breakpoints to a file
. bpd                   Load breakpoints from file
</code></pre>

## Information ##
<pre><code>
iI:             File info
iz:             Strings in data section
izz:            Strings in the whole binary
iS:             Sections
                  iS~w returns writable sections
                  
is:             Symbols
                  is~FUNC exports
                  
il:             Linked libraries
ii:             Imports
ie:             Entrypoint
</code></pre>



## Write commands ##
<pre><code>
wx:             Write hex values in current offset
                    wx 123456
                    wx ff @ 4
                    
wa:             Write assembly #Notes: Use this to modify instructions 
                    wa jnz 0x400d24
                    
wc:             Write cache commit
wv:             Writes value doing endian conversion and padding to byte
wo[x]:          Write result of operation
                    wow 11223344 @102!10
                        write looped value from 102 to 102+10
                        0x00000066  1122 3344 1122 3344 1122 0000 0000 0000
                    wox 0x90
                        XOR the current block with 0x90. Equivalent to wox 0x90 $$!$b (write from current position, a whole block)
                    wox 67 @4!10
                        XOR from offset 4 to 10 with value 67
                        
wf file:        Writes the content of the file at the current address or specified offset (ASCII characters only)
wF file:        Writes the content of the file at the current address or specified offset
wt file [sz]:   Write to file (from current seek, blocksize or sz bytes)
                    Eg: Dump ELF files with wt @@ hit0* (after searching for ELF headers: \x7fELF)
wopO 41424344 : get the index in the De Bruijn Pattern of the given word

</code></pre>

## Function analysis (normal mode) ##
<pre><code>

aa:             Analyze all (fcns + bbs) same that running r2 with -A
ahl [l] [r]:    fake opcode length for a range of bytes
ad:             Analyze data
                  ad@rsp (analyze the stack)                  

af:             Analyze functions
afl:            List all functions
                  number of functions: afl~?
                  
afi:            Returns information about the functions we are currently at
afr:            Rename function: structure and flag
afr off:        Restore function name set by r2
afn:            Rename function
                  afn strlen 0x080483f0

afvd:           output r2 command for displaying the value of args/locals in the debugger
                  
af-:            Removes metadata generated by the function analysis
af+:            Define a function manually given the start address and length
                  af+ 0xd6f 403 checker_loop
                  
axt:            Returns cross references to (xref to)
axf:            Returns cross references from (xref from)

</code></pre>


## Visual Mode
<pre><code>
V:              Enter in Visual Mode
|               Vertical split (i.e print stack: pxw 256 @esp)
</code></pre>
