Creating a Rust style Ownership/borrow/checker system in Go
**Changed default branch to 'version1.2'** as this didn't interfere with current projects. Running the compiler would automatically set up 1.23. If it takes me too long to get a working compiler then 1.23+ might be needed. So I just branched off.
### NOTES:
#### As I progress this will hold my thought process throughout and explanations (for myself mostly)
## **I Have put my daily learnings in another directory, LearnByDay, in an .md file for each day. I will place a daily synopsis here**

**DayOne:** March 8, 2024
- Watching video on creating a parser from scratch.
- I need to create a Parser!
- I need to do a Hand-Written parser.
- Use the Recursive-descent parser.
- Can I just parse my code or do I need to create new types?
- I can't get go tools/go compile to work on my machine. :(

**DayTwo:** March 9, 2024
- Learned about memory leaks in good detail.
- Continued watching parsing videos for information.
- Busy weekend didn't get much else done.

**DayThree:** March 10, 2024
- Looked through GO and Rust compilers.
- Cloned Rust compiler.
- Created a practice parser from a video.
- Studied Rust compiler for a while.
- Pretty much it, too busy.

**DayFour:** March 11, 2024
- Struggled with getting the compiler to work properly on my computer.
- Studying the compiler more.

### Where did the idea come from? 
> I saw a video that described the differences between using a typical programming language and Rust and everyone really came to the same conclusion that - 'It was more difficult'.

Then these questions came to mind:
- Why was it more difficult?
- Does it have to be this way?
- How is it happening that isn't happening(at least publicly) in other languages.
- Why hasn't anybody has attempted to duplicate its principles.
- Watching Pixeled's video 'Let's Create a Compiler',
  - ~11 minutes in and damn it's good.

So today I decided that I would embark on creating a system like Rust's with pretty much zero(0) experience.

### Initial Concept
*this shouldn't much change after today, maybe something I forgot to add.* 
- Compatible with existing code.
- Add only a small amount of code.
- Create a package?
- Do not effect existing function logic.
- No need to change logic to use.
- K.I.S.S. Keep It Super Simple!
- Specify output of variables.
- Automatically drop variable memory once function completes, in some cases, like 'void' returns.
- Lock functions to only accept returns from certain functions.**\*!!!**
- Lock functions to only return values to certain functions.  **\*!!!**

**\***: Will require the use of an LSP.

**!!!**: This I believe is necessary to keep it simple.

Here's an example of my current thought process:
```go
func foo() {
    strA := "AMY"
    strB := "Brian"
    strC := "Charlie" + strB + strA
    
    // All of the below variables will compile fine in Go and not throw any errors, unlike in Rust. Because, we are ONLY concerned about the return value of the function and where it is going.
    strA = strB
    strB = strC

    fmt.printline(strC)
    fmt.printline(strB)
    return strA 
} OUT: bar() // specifies the ONLY function that will accept this return value.

// strA is held in memory and sent to bar()

func bar(strC string) {

} IN: foo(strC) // specifies the ONLY value this function will accept.

// adding End will drop the value from memory
// EX: IN: foo(strC) END // strC is no longer accessible

func bar2(strC string) {
 return str
}

/* You can string multiple functions as follows:
} OUT: bar(strC), bar2(strC), bar3(strC)...
} IN: 
*/
```

LOCKING A FUNCTION:
If a function is just returning to the console. i.e. 
```go
func main() {
//...
fmt.sprintf("Error found %s", err)
} End // This should remove any memory used by this function automatically!
```

## How to Go About It
**I have no idea if it's even possible!?**
- Understand Go compiler.
- Get a general idea for next steps.
*add Day 3*
- Add tokens in tokens.go
- Need to modify the parser!
- AST to where it would actually fit.
- Would it be easier to just make a new parser?
- Scanner.go would need to be changed also.

#### REFERENCES
- **Linux Sys Calls**
https://chromium.googlesource.com/chromiumos/docs/+/master/constants/syscalls.md
- **rax** - temporary register/return value
- **rdi** - used to pass first argument
- **rsi** - used to pass second argument
- **rdx** - used to pass third argument
- **rcx** - used to pass fourth argument // sometimes
  - can be replaced with r10
- **r10/r11** - temporary
- **r8** - used to pass fifth argument
- **r9** used to pass sixth argument
- **A Quick Guide to Go's Assembler**   
https://go.dev/doc/asm
  


#### SOURCES
- **Understanding the Go Compiler - Jesus Espino**
https://www.youtube.com/watch?v=qnmoAA0WRgE&pp=ygULZ28gY29tcGlsZXI%3D by Jesus Espino
  - to get a general overview of the GO compiler.
  - Gave locations on (bottom right hand of screen) code.
<hr>

- **Go 1.20 Memory Arenas Are AMAZING | Prime Reacts**
https://www.youtube.com/watch?v=eglMl21DJz0 by ThePrimeTime
  - I haven't heard of this before and it seemed important.
  - Not important to what I'm doing.
<hr>

- **AoC 2021 Day 24 using Go [Compiler Analysis]**
https://www.youtube.com/watch?v=hmq6veCFo0Y by 
  - This guy is pretty damn good at doing and explaining simultaneously!
  - Interesting take on what I need to look forward to.
<hr>

- **Let's Create a Compiler (Pt.1)**<br>
https://youtu.be/vcSijrRsrY0 by Pixeled
  - UNBELIEVABLY GOOD dude!
  - So much information
<hr>

- **Building a Parser from Scratch**<br>
https://www.youtube.com/watch?v=4m7ubrdbWQU by Dmitry Soshnikov
- So far so good
- Understand now that I need to create/adjust a parser because it deals with the syntax of the language.
<hr>

- **Recursive Descent Parsing** <br>
https://www.youtube.com/watch?v=SToUyjAsaFk&pp=ygUkYnVpbGRpbmcgYSByZWN1cnNpdmUgZGVzY2VudCBwYXJzZXIg by hhp3
- It's hand-written
- Really good explanations
- Excellent!