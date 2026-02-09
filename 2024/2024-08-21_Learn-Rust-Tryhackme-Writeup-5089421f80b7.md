---
title: "Learn Rust Tryhackme Writeup 5089421f80b7"
platform: Medium
original_file: 2024-08-21_Learn-Rust-Tryhackme-Writeup-5089421f80b7.md
---

# Learn Rust Tryhackme Writeup 5089421f80b7

::: {}
# Learn Rust Tryhackme Writeup {#learn-rust-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/rust Note: This room is free
:::

::::::: {.section .e-content field="body"}
:::::: {#c1c7 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Learn Rust Tryhackme Writeup {#23c6 .graf .graf--h3 .graf--leading .graf--title name="23c6"}

<figure id="ff5b" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*J28KGulwa9XZKqxz.png"
class="graf-image" data-image-id="0*J28KGulwa9XZKqxz.png"
data-width="459" data-height="258" />
</figure>

**Room link:**
[https://tryhackme.com/room/rust](https://tryhackme.com/room/rust){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/rust"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

### Task 1: What is Rust? {#35bf .graf .graf--h3 .graf-after--p name="35bf"}

### Introduction {#4b63 .graf .graf--h3 .graf-after--h3 name="4b63"}

Rust is a new programming language created in 2015 by a small team of
people, and later adopted by Mozilla (the organisation that created &
maintains Firefox).

It is a compiled low level language, which aims (and succeeds) to be the
same speed as C++, but while incorporating some higher level language
features from fan-favorites such as Python or JavaScript.

Rust has 3 goals:

- [Fast]{#1491}
- [Secure]{#5e91}
- [Productive]{#5768}

### Fast {#0729 .graf .graf--h3 .graf-after--li name="0729"}

Rust aims to be similar in terms of performance to C++.

Rust is statically typed, which means the data type of a variable is
known at compile time. This allows the compiler to optimise the code
further than if we didn't know the types.

Rust does not use garbage collection (despite being a low level
programming language). Garbage collection is where the program attempts
to reclaim memory from garbage. Garbage is memory occupied by objects
that are no longer in use by the program.

Go, a high level programming language similar syntactically to Python
but is fast & compiled, uses garbage collection. This caused a massive
overhead at Discord, which forced them to switch from Go to Rust.
[https://blog.discord.com/why-discord-is-switching-from-go-to-rust-a190bbca2b1f](https://blog.discord.com/why-discord-is-switching-from-go-to-rust-a190bbca2b1f){.markup--anchor
.markup--p-anchor
data-href="https://blog.discord.com/why-discord-is-switching-from-go-to-rust-a190bbca2b1f"
rel="noopener ugc nofollow noopener" target="_blank"}

Something to note is that Python and JavaScript use garbage collection.
These abstractions may cause issues (as in Discord's case), which is why
many choose a low level programming language.

### Secure {#555b .graf .graf--h3 .graf-after--p name="555b"}

Rust is completely memory safe. This means that exploits involving
memory aren't possible in Rust, unless you explicitly specify unsafe
Rust code.

The [Microsoft Security Response
Centre](https://msrc-blog.microsoft.com/2019/07/22/why-rust-for-safe-systems-programming/){.markup--anchor
.markup--p-anchor
data-href="https://msrc-blog.microsoft.com/2019/07/22/why-rust-for-safe-systems-programming/"
rel="noopener ugc nofollow noopener" target="_blank"} states that 70% of
all CVE's MSRC assigns are memory safety issues. In Microsoft's own
words:

"This means that if that software had been written in Rust, 70% of these
security issues would most likely have been eliminated. And we're not
the only company to [have reported such
findings](https://hacks.mozilla.org/2019/02/rewriting-a-browser-component-in-rust/){.markup--anchor
.markup--p-anchor
data-href="https://hacks.mozilla.org/2019/02/rewriting-a-browser-component-in-rust/"
rel="noopener ugc nofollow noopener" target="_blank"}."

Sometimes programmers must perform unsafe operations. Rust provides
tools to wrap these unsafe actions so unsafe code can be statically
enforced by the Rust compiler.

The memory safety is guaranteed by the concept of ownership. All Rust
code follows these rules:

- [Each value has a variable, called an owner.]{#f2bb}
- [There can only be one owner at a time.]{#a9bc}
- [When the owner goes out of scope, the value will be dropped.]{#eb88}

Values can be moved or borrowed between variables, but no value can have
more than 1 owner.

Let's see an example of Python failing with this:

``` {#7f91 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
squares = (val * val for val in range(100))
print(min(squares))                 
print(max(squares))
```

What we want is:

``` {#412f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
0
9801
```

But what we get is:

``` {#9975 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
>>> print(min(squares))
0
>>> print(max(squares))
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: max() arg is an empty sequence
```

This is because min alters the variable squares. It's strange, because
we just wanted the minimum --- not to alter the whole variable!

In Rust, the same code is:

``` {#f455 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="php"}
fn main()
   let squares = (0..100).map(|val| val * val); 
   println!("{:?}", squares.min());   
   println!("{:?}", squares.max());      
}
```

When we try to compile this, Rust tells us:

I'll talk more about this in a later task, but the important part is
that **Python allows functions to alter variables they do not own,
whereas Rust doesn't.**

PS: Notice how the Rust compiler explicitly points out the values, the
lines, the exact characters, where the error occurred as well as a full
error message explaining why it won't allow that code. Whereas Python
simply said .

``` {#5fbb .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
max() arg is an empty sequence
```

### Productivity {#452e .graf .graf--h3 .graf-after--pre name="452e"}

Rust's 3rd largest goal is a strange one. Productivity!

Rust provides all of the tools developers need to be productive, shipped
with the platform itself.

*Note: The below list is read as:*

- [*Tool*]{#172a}

*Explanation of the above tool.*

Some of these include:

- [Cargo]{#a1e9}

Rust's version of NPM or PyPi. Download packages others have created.

- [Clippy]{#9f27}

Microsoft Clippy, but re-imagined for Rust to aid with development.

- [RustFmt]{#6031}

Automatically formats Rust code

- [Cargo Test]{#eae1}

A built in testing application created by the Rust developers.

- [Cargo docs]{#613f}

Automatically generate documentation for your code, using documentation
comments (written in Markdown). This documentation is then sent to
[docs.rs](http://docs.rs/){.markup--anchor .markup--p-anchor
data-href="http://docs.rs/" rel="noopener ugc nofollow noopener"
target="_blank"} upon publishing to Cargo. Not to mention that examples
written in documentation are automatically tested for you. No more
untested documentation examples!

- [Rust-Analyzer]{#9d50}

Think IDE but more intelligent. Rust Analyzer clearly labels what is
wrong with your code, why it is wrong, the exact characters that
conflict and cause the error, and 90% of the time it provides an
"auto-fix" function that automatically fixes these errors for you.

- [The Rust Book & Docs]{#5b9f}

Rust has a book, called The Book which details everything you could want
to know about Rust. Neatly chaptered, easily searchable and at your
disposal for free. If this isn't good enough, thanks to Rust's
documentation comments almost every library you'll use will have
extensive documentation online.

With all of these tools at your disposal, it is incredibly rare to
compile a Rust program and have bugs in it. In fact, I have only
experienced this once. 99% of the time, the tooling and language will
have picked up on it long before I hit compile.

### Conclusion {#2aff .graf .graf--h3 .graf-after--p name="2aff"}

If you are looking for something extremely fast and memory safe but
while maintaining good productivity, Rust is the language for you.

As Pentesters our job is offering solutions to developers. Telling
Python developers that a low-level language is a good alternative sounds
wacky at first.

But Rust can hold your hand, as it supports calls from functions written
in other languages (foreign function interfacing).

We can use Rust to rewrite security or performance critical code which
will cooperate with our existing codebase.

Here's an example of calling C code

``` {#c8c8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
extern "C" {
    fn abs(input: i32) -> i32;
}fn main() {
    unsafe {
        println!("C believes that the absolute value of -3 is: {}", abs(-3));
    }
}
```

**Q.1:** What other language is Rust similar to in terms of performance?

> ***Answer: c++***

**Q.2:** What famous company switched from Go to Rust, mentioned in this
task?

> ***Answer: Discord***

**Q.3:** Microsoft Security Centre reports what percentage of CVE's they
assign are memory safety issues? Include the % sign.

> ***Answer: 70%***

**Q.4:** What is Rust's version of NPM or PyPi?

> ***Answer: cargo***

### Task 2: Installing & Tooling {#de6b .graf .graf--h3 .graf-after--blockquote name="de6b"}

Before we dive into the language, let's install Rust.

Rust recommends using the tool `rustup`{.markup--code .markup--p-code}
to manage multiple versions of Rust. If you are familiar with Python,
you may have used virtualenvs to achieve a similar result. That is,
different versions of Python on the same machine.

This is another great tool created by the Rust team for productivity.

Install RustUp with this command:

`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`{.markup--code
.markup--p-code}

This command can also be found on the Rust website
[https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install){.markup--anchor
.markup--p-anchor data-href="https://www.rust-lang.org/tools/install"
rel="noopener ugc nofollow noopener" target="_blank"}

This command will install the stable version of Rust for your OS.

Rust comes in 3 flavours. Stable, Beta, and Nightly.

Stable is the latest stable release of Rust (stable releases are usually
shipped every 6 weeks). Beta updates periodically. Nightly updates when
the language itself updates.

Now, let's install some Rust tools to aid our development.

The command we just ran also installs `Cargo`{.markup--code
.markup--p-code},

Cargo is the package manager for Rust. All the packages get uploaded to
[https://crates.io](https://crates.io/){.markup--anchor
.markup--p-anchor data-href="https://crates.io/"
rel="noopener ugc nofollow noopener" target="_blank"} and does a lot of
cool things.

The 3 core Cargo commands are:

**cargo install**

Install a package from [Crates.io](http://crates.io/){.markup--anchor
.markup--p-anchor data-href="http://crates.io/"
rel="noopener ugc nofollow noopener" target="_blank"}

**Cargo publish**

Publish a package to [crates.io](http://crates.io/){.markup--anchor
.markup--p-anchor data-href="http://crates.io/"
rel="noopener ugc nofollow noopener" target="_blank"}

**Cargo update**

Updates all of the local packages

But, since we are developing RustCode there are 3 more important
commands

**Cargo test**

Run the tests for our code

**Cargo fmt**

Runs the formatting tool. This tool automatically formats your code
(apply the argument `--all`{.markup--code .markup--p-code} to format all
code). Similar to Python\'s Black but built in.

**Cargo clippy**

Microsoft Clippy but for Rust! Clippy will point out common errors in
your code and help you correct them.

**Community tools**

There is one tool, that is a community based tool --- that is seen as
absolutely essential to the Rust ecosystem.

That tool is Rust-Analyzer. Imagine an IDE but smarter and more
advanced. Rust-Analyzer will analyse your code as you write it, spot
errors before you compile & provide an auto-fix option to automatically
fix the errors.

Rust-Analyzer states that their most supported version is VS Code, but
they are available on many other platforms.

Something cool to note is that the main tools of Rust are written by the
Rust developers themselves. In languages like Python, we may argue over
whether `setuptools`{.markup--code .markup--p-code} or
`poetry`{.markup--code .markup--p-code} is right. Or whether
`pytest`{.markup--code .markup--p-code} is better than
`unittest`{.markup--code .markup--p-code}. Arguing over the right tool
to use is procrastination. Rust says \"these are the tools you will
use\" and that\'s it. This boosts productivity, as you don\'t have to
worry about what tools to use but can impede development as the tool may
not be fully complete.

**Q.1:** What is the tool we used to install Rust called?

> ***Answer: Rustup***

**Q.2:** How do we install the package rustscan using cargo?

> ***Answer: cargo install rustscan***

**Q.3:** What command do we run to format our code?

> ***Answer: cargo fmt***

### Task 3: Hello, World! {#09f1 .graf .graf--h3 .graf-after--blockquote name="09f1"}

It wouldn't be a programming tutorial without a basic "Hello, World!".

Create a new folder, and in the terminal type:

``` {#fd3a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
cargo init
```

This makes Cargo initialise a new Rust repository. Cargo will take care
of most of the work for you.

The file structure is as follows:

``` {#067e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="markdown"}
- Cargo.toml
- src/
    - main.rs
```

`cargo.toml`{.markup--code .markup--p-code} is the configuration file
for our Rust project. It includes our dependencies, project name,
authors, the version of Rust we are using and more.

When we have just ran `cargo init`{.markup--code .markup--p-code}, our
file will look like this:

``` {#10b1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
[package]
name = "Hello_world"
version = "0.1.0"
authors = ["bee <bee@fake.com>"]
edition = "2018"
# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html[dependencies]
```

Our `main.rs`{.markup--code .markup--p-code}file in the folder
`src`{.markup--code .markup--p-code} is the main file where we write our
code. Every single Rust project **must** have a main file, and every
main file must have a main function.

``` {#b8ba .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
fn main() {
    println!("Hello, world!");
}
```

**Fun fact** In the original C book, "Hello, World!" is stylised with a
capital letter on the word world.

In Rust, we use curly braces to denote blocks of code. And a semi-colon
to express the end of an expression.

To print in Rust, we use the macro `println!`{.markup--code
.markup--p-code}.

We know `println`{.markup--code .markup--p-code} is a macro, as it is
called with an exclamation mark. Macros, in a nutshell, allow us to
write code that writes more code. To put it even simpler, we can create
our own syntax that translate to different code.

To run this program, we execute:

`cargo run`{.markup--code .markup--p-code}

This should result in:

``` {#7618 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
➜ cargo run 
   Compiling hello_world v0.1.0 (/tmp/hello_world)
    Finished dev [unoptimized + debuginfo] target(s) in 0.21s
     Running `target/debug/hello_world`
Hello, world!
```

This command:

- [Compiles the code with the unoptimised build (to increase the speed
  of compilation)]{#89b6}
- [Runs the code]{#c4bb}

You'll also notice a new folder has been created, `target`{.markup--code
.markup--p-code}.

`target`{.markup--code .markup--p-code} contains the binaries for our
project.

``` {#265e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="markdown"}
- Cargo.toml
- src/
    - main.rs
- target/
    - debug/
        = build/
        - deps/
        - examples/
        - hello_world
        - hello_world.d
        - incremental/
```

Right now, the only important file is `hello_world`{.markup--code
.markup--p-code}

This file is actually the binary for our program.

We can tell its a binary by running ls -l in the directory

``` {#7e94 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
drwxr-xr-x    - bee 31 Jul 23:35 build
drwxr-xr-x    - bee 31 Jul 23:35 deps
drwxr-xr-x    - bee 31 Jul 23:35 examples
.rwxr-xr-x 2.9M bee 31 Jul 23:35 hello_world
.rw-r--r--   72 bee 31 Jul 23:35 hello_world.d
drwxr-xr-x    - bee 31 Jul 23:35 incremental
```

To build our project without running it, run:

`cargo build`{.markup--code .markup--p-code}

And now we can run the binary directly.

`./target/debug/hello_world`{.markup--code .markup--p-code}

This is exactly the same as `cargo run`{.markup--code .markup--p-code},
but 2 commands.

When we want to build our project and optimise it, run it with the
release profile:

`cargo build --release`{.markup--code .markup--p-code}

Use the normal cargo build for quick checking of the code. Use the
release argument to optimise the code to the maximum possible that the
Rust compiler will allow.

We call `--release`{.markup--code .markup--p-code} a profile,
specifically the release profile. The Rust compiler has different levels
of optimisation depending on what you want.

**Q.1:** How do we initialise a new Rust project?

> ***Answer: cargo init***

**Q.2:** What character represents a macro?

> ***Answer: !***

**Q.3:** What does every Rust project need as a file?

> ***Answer: main.rs***

**Q.4:** If we wanted to add a dependency to our Rust project, what file
would we edit?

> ***Answer: cargo.toml***

**Q.5:** How do we run our Rust project?

> ***Answer: cargo run***

**Q.6:** How do we build the project RustScan with the release profile
(most optimised)?

> ***Answer: cargo build -release***

**Q.7:** What folder are the release binaries stored in?

> ***Answer: target/release***

**Q.8:** How many release profiles does Rust have using optimisation
level?

> ***Answer: 4***

### Task 4: Variables {#e699 .graf .graf--h3 .graf-after--blockquote name="e699"}

All variables, by default, are immutable in Rust.

This is a safety feature, but also a productivity feature. Variables
that don't change mean you don't have to track down when the value
changed, and immutable variables are great for concurrency

Let's see this in action.

``` {#af05 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
fn main() {
     let x = 5;
     println!("The value of x is: {}", x);
     x = 1;
     println!("The value of x is: {}", x);
 }
```

This code does not compile\*\*.\*\* It returns with the error:

`error[E0384]: cannot assign twice to immutable variable `{.markup--code
.markup--p-code}x\`\`\
\--\> src/main.rs:4:5\
\|\
2 \| let x = 5;\
\| -\
\| \|\
\| first assignment to \`x\`\
\| help: make this binding mutable: \`mut x\`\
3 \| println!(\"The value of x is: {}\", x);\
4 \| x = 1;\
\| \^\^\^\^\^ cannot assign twice to immutable variable

The error tells us everything we need to know.

`cannot assign twice to immutable variable`{.markup--code
.markup--p-code}

This is telling us that we are assigning a value to an immutable
variable (a variable that cannot be changed), twice. Which cannot
happen.

It is important we get compile-time errors, as this can lead to bugs and
undefined behaviour --- which can lead to insecure code. In Rust, once
an immutable variable is set Rust guarantees it will never change in its
lifetime.

To make a variable mutable, we place the mut keyword in front of it like
so:

``` {#5e00 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
fn main() {     let mut x = 9;     println!("The value of x is:  {}", x);     let x = 4;     println!("The value of x is: {}", x); }
```

This code compiles & runs correctly:

`➜ cargo run`{.markup--code .markup--p-code}\
Compiling hello_world v0.1.0 (/tmp/hello_world)\
Finished dev \[unoptimized + debuginfo\] target(s) in 0.14s\
Running \`target/debug/hello_world\`\
The value of x is: 9\
The value of x is: 4

Being unable to change the value of a variable might have reminded you
of another programming concept that most other languages have:
constants. Like immutable variables, constants are values that are bound
to a name and are not allowed to change, but there are a few differences
between constants and variables.

Refer to this code for the tasks.

**Question 1**

`fn main() {`{.markup--code .markup--p-code}\
let x: u32 = 5;\
println!(\"The value of x is: {}\", x);\
x = \"hello\";\
println!(\"The value of x is: {}\", x);\
}

**Question 2**

`fn main() {`{.markup--code .markup--p-code}\
let x: u32 = 5;\
println!(\"The value of x is: {}\", x);\
x = 5;\
println!(\"The value of x is: {}\", x);\
}

**Q.1:** In question 1, does this code compile? T(rue) or F(alse)

> ***Answer: F***

**Q.2:** What is the error code returned by question 1?

> ***Answer: E0308***

**Q.3:** Does the code in question 2 compile? T(rue) or F(alse)

> ***Answer: F***

**Q.4:** What is the error **message** returned?

> ***Answer: cannot assign twice to immutable variable***

### Task 5: Constant Variables {#f112 .graf .graf--h3 .graf-after--blockquote name="f112"}

Rust also has constants. These are values that aren't just immutable by
default, but are always immutable.

Constants can be declared in any scope, including the global scope. This
means that we can use their value in any part of our code, or in
multiple places at once.

Constants can only be constant, they cannot be set to a function call or
any other value that may change at runtime.

We declare constants with the `const`{.markup--code .markup--p-code}
keyword like so:

`const HUNDRED_THOUSAND: u32 = 100_000;`{.markup--code .markup--p-code}

Notice how in Rust, we can use the `_`{.markup--code .markup--p-code}
character to denote a space in number without it affecting the value
itself. This is purely for readability.

Also note that it is tradition to name a constant in all uppercase.

**Shadowing**

I'm going to show you something that might not make sense at first.

``` {#75bb .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
fn main(){
    let x = 6;
    let x = x + 1;
    println!("{}", x)
}
```

This is called *shadowing*. Rustaceans (Rust programmers) say that:

*"The first variable is shadowed by the second"*

Which means the second variables value appears when used. We can change
the type of an immutable variable once it has been defined.

Here's an explanation from the official Rust docs about this principle
(edited to match the example)

"This program first binds x to a value of 6. Then it shadows x by
repeating let x =, taking the original value and adding 1 so the value
of x is then 7."

By using let, we can perform transformations on the variable but have
the variable still be immutable after all the transformations have
completed.

We're effectively creating a new variable with the `let`{.markup--code
.markup--p-code} keyword, which means we can change the type of the
value.

``` {#9c4b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
let word = "hello";
let word = word.len();
```

Which is allowed.

However, if we tried to use mut, it wouldn't be allowed --- as mut
cannot change types.

``` {#2a27 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
let mut word = "hello";
word = word.len();
```

``` {#9040 .graf .graf--pre .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="go"}
error[E0308]: mismatched types
 --> src/main.rs:3:12
  |
3 |     word = word.len();
  |            ^^^^^^^^^^ expected `&str`, found `usize`
```

**Q.1:** How do we define a constant in Rust?

> ***Answer: const***

**Q.2:** Can we shadow a constant? T(rue) or F(alse)

> ***Answer: F***

**Q.3:** What do we use to change the type of an immutable variable once
it has been defined?

> ***Answer: shadowed***

**Q.4:** Will the code "CONST word = "yes"" compile? T(rue) or F(alse)

> ***Answer: F***

**Q.5:** We have "let word = "hello"", how do we get the length of the
variable?

> ***Answer: word.len()***

### Task 6: Data Structures {#d869 .graf .graf--h3 .graf-after--blockquote name="d869"}

In Rust we'll very often see the compiler complain that our variables
and functions aren't type hinted. We saw type hints with CONST earlier.
A type hint defines what the data type of a variable is at compile time.

`let ports: u32 = 65535`{.markup--code .markup--p-code}

The `: u32`{.markup--code .markup--p-code} states that the variable
`ports`{.markup--code .markup--p-code} is of size `u32`{.markup--code
.markup--p-code}.

The `u`{.markup--code .markup--p-code} in the integer means unsigned,
and the `32`{.markup--code .markup--p-code} is how many bits it has.

Unsigned integers can only ever be positive, signed integers can be both
positive and negative.

Integers range from 16 bits up to 128 bits. Some operating systems can't
use integers higher than u32, and using such large integer types may
slow down the program on some systems.

<figure id="7b01" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*HaWMRVgR-LaVn_xx.png"
class="graf-image" data-image-id="0*HaWMRVgR-LaVn_xx.png"
data-width="846" data-height="298" />
</figure>

s you explore Rust, you will come across many, many different data
types. It would be foolish for me to try and teach them all, so I have
elected to teach only what I believe will help you understand Rust right
now.

We've seen how integers work, but what about strings?

### Strings {#1932 .graf .graf--h3 .graf-after--p name="1932"}

There are two types of strings in Rust. `String`{.markup--code
.markup--p-code} and `&str`{.markup--code .markup--p-code}.

`String`{.markup--code .markup--p-code} is a growable allocated data
structure whereas `str`{.markup--code .markup--p-code} is an immutable
fixed-length string somewhere in memory.

`&str`{.markup--code .markup--p-code} is a `string slice`{.markup--code
.markup--p-code} of `string.`{.markup--code .markup--p-code}

Strings are confusing for beginners in Rust, but these are the core
principles. [Here's a list to the relevant Rust book page on Strings for
more
information.](https://doc.rust-lang.org/book/ch08-02-strings.html){.markup--anchor
.markup--p-anchor
data-href="https://doc.rust-lang.org/book/ch08-02-strings.html"
rel="noopener ugc nofollow noopener" target="_blank"}

**Q.1:** Given the number -6, is this signed or unsigned?

> ***Answer: signed***

**Q.2:** Given the number 65536, what is the smallest unsigned datatype
we can fit this into?

> ***Answer: u32***

**Q.3:** What's the smallest sized signed integer in rust?

> ***Answer: i16***

**Q.4:** Create a mutable u32 variable called "tryhackme" and assign it
the number 9

> ***Answer: let mut tryhackme: u32 = 9;***

**Q.5:** What data type is used to represent a string slice?

> ***Answer: &str***

**Q.6:** Let's say you had a variable, X. You wanted to typehint the
variable as a string. What would you write? Include X in the variable
but not the let or = parts.

> ***Answer: x: String***

### Task 7: Functions {#af49 .graf .graf--h3 .graf-after--blockquote name="af49"}

We've already seen a special kind of function earlier, the
`main`{.markup--code .markup--p-code} function.

The `main`{.markup--code .markup--p-code} function is the first function
called of the `main`{.markup--code .markup--p-code} file, which is the
first file called.

Every binary file written in Rust needs a `main`{.markup--code
.markup--p-code} file, and every main file needs a `main`{.markup--code
.markup--p-code} function.

Functions in Rust are defined as:

``` {#cf9f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
fn hello() -> u16{
    println!("hello!");
    6
}
```

The main function is the same as this, but in a binary file it doesn't
return anything.

``` {#c3f2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
fn main(){
    println!("I do not return!")
}
```

Now, you might have noticed in the `hello`{.markup--code
.markup--p-code} function that we have a 6 on the end.

*"What???"* I can hear you saying.

Well, Rust returns the final expression of the function.

Alternatively, we can use the `return`{.markup--code .markup--p-code}
statement to return earlier. However, it\'s not very nice to use it to
return the value at the end of the function --- Rustaceans and Clippy
will dislike that 😢

`6`{.markup--code .markup--p-code} is an expression that returns 6, so
our `hello`{.markup--code .markup--p-code} function returns 6.

Our main function does not return anything, which is the way it should
be.

Let's add some arguments to our functions.

``` {#304a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
fn print_name(name: String){
    println!("{}", name);
}
```

Our function arguments have to include the type of each argument.

Now let's try to make this function return something.

``` {#f7dc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
fn print_name(name: String) -> u16{
    println!("{}", name);
    6;
}
```

When we return data, we have to type hint the type of data that is being
returned.

This may seem annoying, but it makes writing clean code so much easier.

Compare these two functions, one in Pythonic pseudocode and one in Rust.
Note: we only have the definitions.

`def to_ip_address(ip):`{.markup--code .markup--p-code}

Now in Rust:

`fn to_ip_address(ip: String) -> IpAddr{`{.markup--code .markup--p-code}

By just adding the types we can clearly see we are taking in a string,
and turning it into an IP address.

With proper function naming and typehints, we can tell what most
functions do just from their definitions. How's that for clean code 😜

**Question 1**

``` {#e724 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
fn hello(){
    8172192: u16;
}
```

**Question 2**

``` {#5b73 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
fn return(){
    6;
}
```

**Question 3**

``` {#0ab3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="scss"}
fn test(name) {
    println!("{}", name);
}
test("bee");
```

**Q.1:** Will question 1 return 8172192? T(rue) or F(alse)

> ***Answer: F***

**Q.2:** Will example 2 run? T(rue) or F(alse)

> ***Answer: F***

**Q.3:** What type should we give to the argument for question 3?

> ***Answer: &str***

**Q.4:** The last expression in a function (the return) needs to have a
semicolon. T(rue) or F(alse)

> ***Answer: F***

**Q.5:** Every function need to return something. T(rue) or F(alse)

> ***Answer: F***

**Q.6:** Functions in Rust can be nested within other functions. T(rue)
or F(alse)

> ***Answer: T***

**Q.7:** What keyword do we use to return early from a function?

> ***Answer: return***

**Q.8:** You nest a function named main, inside another function named
main. Will this run? T(rue) or F(alse)

> ***Answer: T***

### Task 8: Loops {#bce2 .graf .graf--h3 .graf-after--blockquote name="bce2"}

here are 3 loops in Rust.

### loop {#0331 .graf .graf--h3 .graf-after--p name="0331"}

The `loop`{.markup--code .markup--p-code} keyword loops forever or until
we explicitly tell it to stop.

``` {#e41f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
fn main(){
    loop {
        println!("TryHackMe Rocks!");
    }
}
```

We can either break with ctrl+c or we can tell Rust to break with break

``` {#f1f5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
fn main(){
    loop {
        println!("TryHackMe Rocks!");
        break;
    }
}
```

### Conditional While Loops {#53ed .graf .graf--h3 .graf-after--pre name="53ed"}

Rust also has while loops, which loop while a condition is true.

Look at this example for some code, taken from the [Rust
Book](https://doc.rust-lang.org/book/ch03-05-control-flow.html){.markup--anchor
.markup--p-anchor
data-href="https://doc.rust-lang.org/book/ch03-05-control-flow.html"
rel="noopener ugc nofollow noopener" target="_blank"}:

``` {#b2fb .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
fn main() {
    let mut number = 3;while number != 0 {
        println!("{}!", number);number -= 1;
    }println!("LIFTOFF!!!");
}
```

### For loops {#9c5e .graf .graf--h3 .graf-after--pre name="9c5e"}

Rust also has for loops, which we can use to iterate over elements of a
collection.

``` {#46f6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
fn main() {
    let a = [10, 20, 30, 40, 50];for element in a.iter() {
        println!("the value is: {}", element);
    }
}
```

Note the a.iter. We turn a into an iterable using this. This will become
very important to us very soon.

**Q.1:** How do we break out of a loop?

> ***Answer: break***

**Q.2:** Simplest keyword to make an infinite loop?

> ***Answer: loop***

**Q.3:** Turn let a = \[10, 20\]; into something we can iterate over.

> ***Answer: a.iter()***

**Q.4:** While loops can also be infinite. T(rue) or F(alse).

> ***Answer: T***

### Task 9: Zero Cost Abstractions {#3b37 .graf .graf--h3 .graf-after--blockquote name="3b37"}

This task is copied from my blog, where I wrote about [Zero Cost
Abstractions
once](https://bees.substack.com/p/vtubers-random-algorithms-constraints){.markup--anchor
.markup--p-anchor
data-href="https://bees.substack.com/p/vtubers-random-algorithms-constraints"
rel="noopener ugc nofollow noopener" target="_blank"}.

Rust has this really cool thing called Zero Cost Abstractions. It's also
a thing in other low level languages, but being a Python Surfer Dude I
haven't come across it before.

Zero cost abstraction is:

> *"What you don't use, you don't pay for. And what you do use, you
> couldn't do any better if you coded by hand."*

Let's talk about the 2 parts of this sentence.

> *"What you don't use, you don't pay for."*

The language shouldn't have a global cost for a feature that isn't used.
Let's say to use a for loop, the language needs to have some massive 1gb
file that slows down everything else. If we never use a for loop, we
still pay for the for loop!

> *"And what you do use, you couldn't do any better if you coded by
> hand."*

Here's the kicker.

Say you wrote some code, a function that calculated Fibonacci numbers.
And you compiled this code down into assembly.

Now let's say you hand-write assembly to do the same
function --- calculate Fibonacci numbers but this time in assembly.

Handwriting it in assembly would mean we would either gain no
performance, or we would lose performance.

By using zero cost abstractions, we write abstracted code (not
handwritten assembly) and we couldn't do any better if we tried to
hand-write assembly. Now that's cool!

Now, let's explore iterators.

Iterators are a way of processing a series of items with Rust, much like
a for loop.

We saw earlier `a.iter()`{.markup--code .markup--p-code}. This code
turns the variable `a`{.markup--code .markup--p-code} into an iterator
over the items of `a`{.markup--code .markup--p-code}. But this code by
itself doesn\'t do anything useful.

This is because iterators are *lazy*. You have to tell them to do
something to get values from them.

Let's take a look at a real example.

``` {#e67d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
let a = vec![1, 2, 3];
let a_iter = a.iter();
for val in a_iter {
    println!("The value is {}, val);
}
```

We make the iterator do something by calling it in this for loop.

Now we can make the code do something and `consume`{.markup--code
.markup--p-code} the iter using some nifty functional programming
skills. To square every number in an iterator, and then to sum it we can
do:

``` {#bc3e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
let a = vec![1, 2, 3];
a.iter()
.map(|&i| i * i
.sum()
```

Note, in Rust, we can separate applications of methods with new lines.

This is just a small portion of what iterators can do. Read the entire
chapter on them from the [Rust Book
here](https://doc.rust-lang.org/book/ch13-02-iterators.html#processing-a-series-of-items-with-iterators){.markup--anchor
.markup--p-anchor
data-href="https://doc.rust-lang.org/book/ch13-02-iterators.html#processing-a-series-of-items-with-iterators"
rel="noopener ugc nofollow noopener" target="_blank"}.

However, let's get back to the important tasks at hand. Zero cost
abstractions.

Iterators are zero cost abstractions in Rust. For loops are not. This is
according to the [Rust
Book.](https://doc.rust-lang.org/book/ch13-04-performance.html){.markup--anchor
.markup--p-anchor
data-href="https://doc.rust-lang.org/book/ch13-04-performance.html"
rel="noopener ugc nofollow noopener" target="_blank"}

By using iterators, we are taking advantage of the fantastic zero cost
abstraction. Speeding up our entire program.

**Q.1:** Iterators are lazy. T(rue) or F(alse).

> ***Answer: T***

**Q.2:** For loops are explicitly mentioned in the Rust book as zero
cost abstractions. T(rue) or F(alse).

> ***Answer: F***

**Q.3:** Zero Cost Abstractions are common in high level languages like
Python or JavaScript T(rue) or F(alse).

> ***Answer: F***

### Task 10: Rayon {#dec2 .graf .graf--h3 .graf-after--blockquote name="dec2"}

Rayon is an external crate for Rust, and normally I wouldn't include
external libraries. However, it's just so awesome and fits so well with
the last few tasks I just had to mention it.

Rayon makes multi threading easy. No, really. It's extremely easy.

Go to [Crates.io](https://crates.io/crates/rayon){.markup--anchor
.markup--p-anchor data-href="https://crates.io/crates/rayon"
rel="noopener ugc nofollow noopener" target="_blank"} and copy the big
black box containing the crate with the version number.

<figure id="1aef" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*p13AHkmU_O9qxbFr.png"
class="graf-image" data-image-id="0*p13AHkmU_O9qxbFr.png"
data-width="875" data-height="629" />
</figure>

Now go into cargo.toml, and include it in the dependencies section. Just
copy and paste it across.

Okay, now let's take our iter in the last task and make it multi
threaded.

``` {#b6ea .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="scss"}
fn sum_of_squares(input: &[i32]) -> i32 {
    input.iter()
         .map(|&i| i * i)
         .sum()
}
```

This is our previous code.

``` {#fed1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
use rayon::prelude::*;
fn sum_of_squares(input: &[i32]) -> i32 {
    input.par_iter() // <-- just change that!
         .map(|&i| i * i)
         .sum()
}
```

This is our multi-threaded code.

Look at how easy that is! We change iter() into par_iter() and we're
done. We're now multi threaded.

**Q.1:** What crate do we use to easily make an iter multi threaded?

> ***Answer: Rayon***

**Q.2:** How do we tell Rust to include an external crate into our
program? **What file do we place this information in?**

> ***Answer: cargo.toml***

**Q.3:** Turn a.iter() into a multi threaded parallel iter using Rayon

> ***Answer: a.par_iter()***

**Q.4:** What website do we go to for Crates?

> ***Answer: crates.io***

### Task 11: If Statements {#575a .graf .graf--h3 .graf-after--blockquote name="575a"}

**Q.1:** We can assign variables based on an if statement on one line
T(rue) or F(alse)

> ***Answer: T***

### Task 12: Error Handling {#ba9f .graf .graf--h3 .graf-after--blockquote name="ba9f"}

Now we get into the inner-workings of Rust, the thing that helps keep it
safe. Error handling.

In Rust, anything that *can* error will return a result. Specifically
`Result<T, E>`{.markup--code .markup--p-code}. `T`{.markup--code
.markup--p-code} is the result you are looking for, `E`{.markup--code
.markup--p-code} is the error.

``` {#89a2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="scss"}
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

Anytime you open a file, the file might not be there or it may fail to
open the file successfully. It will return a Result, and you will have
to deal with it that way.

In Python, exception handling is given to the user. If you want to open
a file, go ahead. But don't forget to write an exception for if the file
isn't there!

But in Rust, no matter what (unless you explicitly tell the compiler to
ignore it) errors must be handled.

Let's look at an example.

``` {#4863 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
use std::fs::File;fn main() {
    let f = File::open("hello.txt");
}
```

Here we go to open a file. The file isn't stored in f, what is stored is
actually a Result enum.

There are 2 ways to check if something returns an result.

1.  [Rust Analyzer will tell us what the return type is.]{#fbb3}
2.  [We assign a type we know is wrong, and the compiler will tell
    us.]{#e4e5}

If we assigned `let f: u32 = File::open("hello.txt");`{.markup--code
.markup--p-code} the compiler will tell us.

``` {#3301 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
--> src/main.rs:4:18
  |
4 |     let f: u32 = File::open("hello.txt");
  |            ---   ^^^^^^^^^^^^^^^^^^^^^^^ expected `u32`, found enum `std::result::Result`
  |            |
  |            expected due to this
  |
  = note: expected type `u32`
             found enum `std::result::Result<std::fs::File, std::io::Error>`
```

So now we know that we have to handle the error, but the question is
*how.*

I'm going to show you 3 ways.

1\. Unwrap

Unwrap is the easiest to implement. It tells Rust "I'm pretty sure this
won't fail so just go ahead and take the value". If it does fail, well,
Rust panics!

``` {#cb7a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
use std::fs::File;fn main() {
    let f = File::open("hello.txt").unwrap();
}
```

2\. Match

Match is how you'd expect this to work, if you're used to Python.

We do one thing for an Ok, and we do another for an Error.

``` {#5cba .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
use std::fs::File;fn main() {
    let f = File::open("hello);
    match f {
        Ok(file) => file,
        Err(_) => panic!("Couldn't open file."),
    }
}
```

If the result is `Ok`{.markup--code .markup--p-code}, that means the
result is successful and we can just take the file.

If it's an `Err`{.markup--code .markup--p-code} that means an error
occurred and we need to do something about it. In this case, the program
panics.

3. ?

The ? operator states "if the result is Ok, carry on in this function.
Else if it is an Err, propagate it back up the stack to the function
that called me. "

To illustrate this, let's look at this example I took from a [Rust blog
post](https://doc.rust-lang.org/edition-guide/rust-2018/error-handling-and-panics/the-question-mark-operator-for-easier-error-handling.html){.markup--anchor
.markup--p-anchor
data-href="https://doc.rust-lang.org/edition-guide/rust-2018/error-handling-and-panics/the-question-mark-operator-for-easier-error-handling.html"
rel="noopener ugc nofollow noopener" target="_blank"}.

``` {#23df .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
fn read_username_from_file() -> Result<String, io::Error> {
    let f = File::open("username.txt");let mut f = match f {
        Ok(file) => file,
        Err(e) => return Err(e),
    };let mut s = String::new();match f.read_to_string(&mut s) {
        Ok(_) => Ok(s),
        Err(e) => Err(e),
    }
}
```

We have 2 matches in this code. A bit unruly. Ideally if we fail to open
the file, or fail to read to string we propagate a single error back up
the stack saying that this function failed.

If it didn't, we should return the Ok result. That way, the function
that called us will receive a `Result`{.markup--code .markup--p-code}
type that it can more easily handle, and without us dealing with
multiple `match`{.markup--code .markup--p-code} statements.

``` {#5072 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
fn read_username_from_file() -> Result<String, io::Error> {
    let mut f = File::open("username.txt")?;
    let mut s = String::new();f.read_to_string(&mut s)?;Ok(s)
}
```

### Conclusion {#855f .graf .graf--h3 .graf-after--pre name="855f"}

This is one of the most important concepts in Rust. Errors normally do
not happen, because every error has to be dealt with in some way. This
helps keep your code safe.

**Q.1:** What is the data type returned from opening a file?

> ***Answer: Result***

**Q.2:** Write the datatype of a generic Result with type hints

> ***Answer: Result T,E\>***

**Q.3:** We're in a function and we get given a Result enum. If the
Result is okay we want to continue working on it in this function. If
the result is Err we want to return to the parent function with Err.
What should we use?

> ***Answer: ?***

**Q.4:** We're certain our result will always return Ok, what should we
use?

> ***Answer: unwrap***

### Task 13: Challenge {#79fa .graf .graf--h3 .graf-after--blockquote name="79fa"}

Challenge file 1.

"M3I6r2IbMzq9" is the text.

The text is encrypted with:

plaintext -\> ROT13 -\> base64 -\> rot13

Go the opposite way and decrypt the file.

rot13 -\> base64 -\> ROT13 -\> plaintext

You'll notice it's the same order either way, so you don't have to worry
about order. Just make sure ROT13 is on the inside.

You might run into lifetime borrow checker issues.

Here's some hints in case you do:

1\. Google is your friend.

2\.
[https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html){.markup--anchor
.markup--p-anchor
data-href="https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html"
rel="noopener ugc nofollow noopener" target="_blank"}

3\. Stop trying to do so many things at once. Break it down to the bare
necessities and slowly build back up to see what causes the errors.

**Q.1:** Challenge 1

Answer: THM{\*\*\*\*}

**Hint:-** Which Language your learn

### Promote and Collaborate on Cybersecurity Insights {#558e .graf .graf--h3 .graf-after--p name="558e"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#7225 .graf .graf--h3 .graf-after--p name="7225"}

[Vijay
Gupta](https://medium.com/@bevijaygupta/who-is-vijay-gupta-2ecad87f92a2){.markup--anchor
.markup--p-anchor
data-href="https://medium.com/@bevijaygupta/who-is-vijay-gupta-2ecad87f92a2"
rel="noopener" target="_blank"} is a cybersecurity enthusiast with
several years of experience in cyber security, [cyber crime forensics
investigation](https://play.google.com/store/books/details?id=VRz7EAAAQBAJ){.markup--anchor
.markup--p-anchor
data-href="https://play.google.com/store/books/details?id=VRz7EAAAQBAJ"
rel="noopener ugc nofollow noopener" target="_blank"}, and security
awareness training in schools and colleges. With a passion for
safeguarding digital environments and educating others about
cybersecurity best practices, Vijay has dedicated his career to
promoting cyber safety and resilience. Stay connected with Vijay Gupta
on various social media platforms and professional networks to access
valuable insights and stay updated on the latest cybersecurity trends.
:::
::::
::::::
:::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [August 21, 2024](https://medium.com/p/5089421f80b7).

[Canonical
link](https://medium.com/@bevijaygupta/learn-rust-tryhackme-writeup-5089421f80b7){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
