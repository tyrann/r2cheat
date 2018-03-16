# r2cheat
A radare2 cheat sheet compiled from various sources
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
