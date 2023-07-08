# Rust Interview Handbook

Send me a PR if you know of any of Rust's interview questions

## Overview
Rust is a modern computer programming language developed by Mozilla in 2010. It was initially developed to tackle the issue of invalid memory access faced by C and C++ developers while building applications. If you are looking for the

## Interview Questions

1. #### What is Rust?
   Rust is a systems programming language that focuses on safety, concurrency, and performance.
   
2. #### What is the cargo and what are the most popular cargo commands?
   [Cargo](https://doc.rust-lang.org/cargo/) is the Rust package manager that can download dependencies, compile the project, make distributable packages, and upload them to the Rust community's package registry creates.io. The most popular cargo commands are:
    1.  Create a new package that builds an executable: `cargo new IntmainApp`
    2.  Create a new package that builds a library: `cargo new --lib IntmainLib`
    3.  Build a package and all its dependencies: `cargo build`
    4.  Build a package with optimization: `cargo build -- release`
    5.  Run a binary of local package: `cargo run`.  Arguments to the binary are followed by two dashes (--): `cargo run -- args`
    6.  Remove generated artifacts from the target directory: `cargo clean`
    7.  Display a tree of dependencies in the project: `cargo tree`
    8.  Compile and execute unit, integration, and documentation tests: `cargo test`

4. #### What is Cargo.toml and Cargo.lock?
   The Cargo.toml file is a manifest file where we can specify metadata such as name, version, etc, project settings, and dependencies(crates) for our project. The Cargo.lock file contains exact information about dependencies and Cargo maintains it. If we are building a rust library, then put Cargo.lock in the .gitignore but if we are building end products application then Cargo.lock should be checked into the git repo.

5. #### Difference between String and str in Rust?
   The `String` type is the most common [string](https://intmain.co/string-in-rust-programming-language/) type in rust and it has ownership over the content of the string. It is heap-allocated, growable, and not null-terminated. A String is stored as a vector of bytes(`Vec<u8>`), and guaranteed to be a valid UTF-8 sequence. [String](https://intmain.co/string-in-rust-programming-language/) literals or [`str`](https://intmain.co/string-in-rust-programming-language/) is the most primitive string type. A Rust &str is like a `char*`. `str` is an immutable sequence of UTF-8 bytes of dynamic length somewhere in memory. Since the size is unknown, one can only handle it behind a pointer, hence it most commonly appears as `&str`: a reference to some UTF-8 data, normally called a "string slice"
   
6. #### Copy vs Clone in Rust?
   The [`Clone`](https://intmain.co/difference-between-copy-and-clone-trait-in-rust/) trait defines the ability to explicitly create a deep copy of an object T. When we call `Clone` for type T, it does all the arbitrarily complicated operations required to create a new T. The [`Copy`](https://intmain.co/difference-between-copy-and-clone-trait-in-rust/) trait in Rust defines the ability to implicitly copy an object. The behavior `Copy` is not overloadable. It is always a simple bitwise copy. This is available for the types that have a fixed size and are stored entirely on the stack. Read more about copy and clone traits [here...](https://intmain.co/difference-between-copy-and-clone-trait-in-rust/)

7. #### Struct in rust?
   Struct is a user-defined data type that can hold different types of data together. `struct` the keyword is used to create structure in Rust. Example of struct:
    
    ```
    //Defining a struct
    struct Employee{
        empid :String,
        name  :String,
        email :String,
    }
    
    //Instantiating a struct
    let emp = Employee{empid: 5, name: "Dev", email: "dev@intmain.co"};
    
    **//Accessing the Struct data**
    let id    = emp.empid;
    let name  = emp.name;
    let email = emp.email;
    ```
    
8. #### Why do we use the owned String type rather than the &str string slice type as the struct field?
   Each instance of a struct owns all of its data and for that, the data should remain valid as long as the struct is valid. Hence we use owned string type rather than the string slice. It’s also possible for structs to store references to data owned by something else, but to do so we are required to use the _lifetimes_ because lifetimes ensure that the data referenced by a struct is valid for as long as the struct is.

 9. #### What is the Option type in Rust, and why is it useful?
     The `Option` type in rust is used to represent an optional value(presence or absence of a value). Every option is either `Some` and contains some value or `None` and doesn't contain any value. To check if the Option type contains some value so that you can unwrap it and access it, use the `is_some()` method which returns true if the option type is some.
    
10. #### What is a trait in Rust, and how is it different from an interface in other languages?
    The Rust traits are a set of methods that can be defined for particular types. Traits allow you to define shared behavior that can be used by multiple types. A trait method is able to access other methods within that trait.
    
    Let's say we want to create a library crate that can display summaries of data that might be stored in a NewsArcticle, BlogPost struct instance. To do this, we need a summary from each type, and we’ll request that summary by calling a `summarize` method on an instance.

    ```
    pub trait Summary{
        fn summarize(&self) -> String {
             format!("Read More {}, by {} ...", self.title, self.author)
        }
    
        fn summarize_post(&self) -> String;
    }
    
    struct NewsArticle{
        title   :String,
        author  :String,
        content :String,
    }
    
    impl Summary for NewsArticle{
        fn summarize_post(&self) -> String{
            format!("{}", self.content);
        }
    }
    
    struct BlogPost{
        title  :String,
        author :String,
        post   :String,
    }
    
    impl Summary for BlogPost{
       fn summarize_post(&self) -> String{
           format!("{}", self.content);
       }
    }
    
    let news = NewsArticle { 
               title  : String::from("News Title"), 
               author : String::from("Author name"), 
               content: String::from("Latest news in detail", };
    
    println!("News summary: {}", news.summarize());
    println!("Post summary: {}", news.summarize\_post());

    ```
    
10. #### What is unsafe in rust and when to use it?
    Rust guarantees memory safety and it is enforced at runtime, but Rust also provides functionality for bypassing these safety checks and this can be done by placing the code in `unsafe` block. Unsafe code tells the compiler, “Trust me, I know what I’m doing.” `unsafe` keyword is used to mark blocks, functions, or traits that contain code that the compiler cannot guarantee to be safe. Unsafe provides the ability to:
    1.  Dereference a raw pointer.
    2.  Call an unsafe function or method.
    3.  Access or modify a mutable static variable.
    4.  Implement an unsafe trait.
    5.  Access fields of `union` Remember that unsafe doesn’t turn off the borrow checker or disable any other of Rust’s safety checks: if you use a reference in unsafe code, it will still be checked.
