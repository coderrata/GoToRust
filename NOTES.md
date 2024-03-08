Creating a Rust style Ownership/borrow/checker system in Go

### NOTES:
#### As I progress this will hold my thought process throughout and explanations (for myself mostly)

### Where did the idea come from? 
> I saw a video that described the differences between using a typical programming language and Rust and everyone really came to the same conclusion that - 'It was more difficult'.

Then these questions came to mind:
- Why was it more difficult?
- Does it have to be this way?
- How is it happening that isn't happening(at least publicly) in other languages.
- Why hasn't anybody has attempted to duplicate its principles.

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

## How to Go About It
I have no idea!
- Understand Go compiler
- Get a general idea for next steps



#### SOURCES
