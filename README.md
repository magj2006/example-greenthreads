# Green Threads Example

This repo was made to accompany article and gitbook.

Gitbook: [https://cfsamson.gitbook.io/green-threads-explained-in-200-lines-of-rust/](https://cfsamson.gitbook.io/green-threads-explained-in-200-lines-of-rust/)

## Branches
There are a few interesting branches:
1. `master` - this will be the 200 lines of code in the book
2. `commented` - this is the same 200 lines but extensively commented along the way
3. `windows` - this is an implementation with a proper context switch on Windows, also a copy of the code in the book
4. `trait_objects` - this is an implementation where we can take trait objects like `Fn()`, `FnMut()` and `FnOnce()` instead of just function pointers, this is way more useful but currently lags a bit behind the improvements in the first three branches
5. `futures` - I'm collecting data and playing around to tie this in to Rusts Futures and async story - see below

## Futures
The end goal was (and still is) for me to use this as a basis to investigate and implement a simple example of the Executor-Reactor pattern using
Futures 3.0 and Rusts async/await syntax.

The main idea is that Reading these two books will give most people a pretty deep understanding of async code and how Futures work once finished and
thereby bride a gap between the documentation that is certainly going to come from the Rust docs team and in libraries like `Tokio` and use an example driven
approach to learning the basics pretty much from the ground up. I will not be focusing too much on how exactly `tokio`, `romio` or `mio` works since they are good
implementations that carry a large amount of complexity in themselves. This will be a bad implementation (as far as production quality goes), 
but a working example focusing on code that is simple to understand and on what's happening under the hood.

The threading implementation used in the first book will probably be changed slightly to serve as an `exeutor` and instead of just spawning
`fn()` or `trait objects` we spawn futures.

## Update 2019-07-31
I decided to divide this deep dive into asynchronous code into three books.

1. Green Threads

Learn about the way of doing multitasking that GO, Ruby and many other programs use. It also explains a lot about some OS basics since threads and context switching is an important part of how operating systems manage to multitask. We explore this by creating our own green threads implementation.

2. Learn Async programming

This book is about two other ways of performing async execution. Threadpools and epoll/kqueue/IOCP - we explore this by implementing a very simplified version of Nodes event loop. It's an interesting example since it uses both ways of running code asyncrhonously. This book will in some sort be higher level than green threads, but will talk much more about working together with the operating system to run async code effectively.

I'm working on the book right now so if you want to follow along and/or give feedback you can have a look here: https://cfsamson-1.gitbook.io/async-basics-explained-with-rust/

3. Futures in Rust

Ok, so the previous two books set up all we needed to know of basic information to get a good understanding of Rusts futures. I'll try to explain them by implementing a very simplified version of the whole stack: libc, mio (reactor) and an executor runtime (tokio). We'll talk about the design of futures, how they work and why they work the way they do. Since we covered so much in the previous two books, this one will be more Rust Centric and focused on Futures since we already have most of the Async basics we need covered. Work on this book has not really started yet.

