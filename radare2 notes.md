# [radare2 tutorial playlist (Binary Adventure)](https://www.youtube.com/watch?v=oW8Ey5STrPI&list=PLg_QXA4bGHpvsW-qeoi3_yhiZg8zBzNwQ&index=1)
---
### Basic Navigation
- `?` to get help for a module/sub-module
- `:aaa` to analyze the entire file
	- the `-A` switch when launching r2 with a file is equivalent to `:aaa`
- `s` to seek, can also be done by moving through the disassembly
- `v` (code view/visual view) and `V` (graph view) to enter and cycle dissassembly views
	- `VV` to enter graph view (similar to other GUI based disassemblers)
	- navigate the `v` view toolbar using `<alt + h j k l>`
	- you can also use your mouse
- to perform commands inside views use the prompt `:` (like in vim) 
	- this prompt is the same the regular prompt r2 starts off at when launched normally
	- press `<return>` on an empty prompt line to exit prompt mode.
- `<p>` to change views (rotate print modes) (window specific), `<shift+p>` to switch back
- radare2 supports multi-window modes (like tmux)
- seek and press enter to follow call in a disassembly view, `<u>` to go back
---
### X-ref checking
- `:ax[t or f]` for x-referencing mode (`a` : analysis, `x` : x-refs) modifiers: `t` : to and `f` : from
- `[return]` to exit `:` (prompt) mode and update screen
---
### List important information
- `:ii` to list imports
- `:iE` to list exports
- `:iS` to list sections
- `:is` to list symbols
- `:afl` to list functions
	- `:afll` for more verbosity
- `:iz` to get strings from the `.data` section
	- `:izz` to get strings from the entire binary
---
### Other radare2 tools
- rabin2 is used for getting binary info (metadata)
- rafind2 is used to search through binary files
---
### Patching binaries
- make a backup of the binary to be patched
- open file with `-w` option to enable writing, i.e. `$ r2 -w ./binary`
- `:w` is the writing module
- do `:w?` to get more information on write (patching) functionality
- seek to desired instruction and press `<shift + a>` to edit the instruction
---
### Debugging Binaries (asm level)
- open file with `-d` option to launch the binary in debug mode
- `:d` is the debugging module
- do `:d?` to get more information on debugging functionality
- navigate to debugger view
- to change stack size do `:e stack.size = <number of bytes to display, ideally 16x[number of lines]>`
- `<f7>` : step into
- `<f8>` : step over
- `:db` to display breakpoints  `:db <address or symbol>` to insert breakpoint
- `:dc` to continue code execution
- `:do` to reopen and reattach`
-  to get back to the instruction pointer after navigating away in visual mode, press `<.>` (this also moves the seek back to the IP)
- `:dsf` to step until the end of the current frame (stop at the next return)
- `:ds` to list stepping commands
---
### Navigating graph view `(:VV)`
- once inside graph view using `:VV` , use the arrow keys to pan around the graph
- to navigate through the code, use the tags `[<letters>]` that are next to the various jumps and calls.
	- press the letter keys inside the tag in the given order to jump into graph view at the point of the tag. 
	- note that this changes the seek address
- press `<p>` and `<shift + p>` to jump through the different views.
- press `<x>` to get the x-references to the given function call like `:axt`
	- to jump to a x-ref, press its index given to the left (like `[0]`)
- 