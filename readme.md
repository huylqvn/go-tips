# Go-tips

This is repo showing key tips and tricks for using go. I collect them from my experience and use them in my projects.

## 1. Resources interview
- [Algo](algo.md)

## Table of contents
0. [Usecase](#0-usecase)
1. [Resources for golang developers](#1-resources-for-golang-developers)
2. [Go Type](#2-go-type)
3. [Interface](#3-interface)
4. [Goroutines and channels](#4-goroutines-and-channels)
5. [Garbage collection](#5-garbage-collection)
6. [Optimizations](#6-optimizations)
7. [Generics](#7-generics)
8. [Error handling](#8-error-handling)
9. [Testing](#9-testing)
10. [Debugging](#10-debugging)
11. [Project Structure](#11-project-structure)
12. [Other Tips](#12-other-tips)
13. [Data structures](#13-data-structures)
14. [Design patterns](#14-design-patterns)

## 0. Usecase
- Restful API server
- gRPC server
- command line tool
- product like webapp-api, ecommerce, chatbot, video call, email service, etc
** Painful:
- lack of libraries for AI, data processing, UI, database enterprise (oracle), etc
- no inheritance
- error checking

## 1.Resources for golang developers
- [Go Tour](https://go.dev/tour/welcome/1) - for beginners learn syntax
- [Go doc](https://go.dev/doc/effective_go) - official documentation for golang
- [Go 101](https://go101.org/article/101.html) - blog and tutorial on golang
- [Dave Cheney](https://dave.cheney.net/practical-go) - understanding principles of golang
- [Microsoft](https://learn.microsoft.com/en-us/training/paths/go-first-steps/) - getting started with golang from Microsoft
- [And many more resources on golang](https://golangresources.com/)

## 2. Go Type
Go Type System

- Overview
  - Static typing
  - Strongly typed

- Primitive Types
  - int, int8, int16, int32, int64
  - uint, uint8, uint16, uint32, uint64
  - float32, float64
  - complex64, complex128
  - bool
  - string
  - rune (alias for int32)

- Composite Types
  - Arrays
  - Slices
  - Maps
  - Structs

- Reference Types
  - Pointers
  - Slices
  - Maps
  - Channels
  - Interfaces
  - Functions

- Type Inference
  - var x = 42 // type inferred as int
  - Short variable declarations

- Type Conversion
  - Explicit type conversion required
  - Convert between compatible types
  - Use type assertion for interfaces

- Interfaces
  - Define behaviors, not data
  - Implicit satisfaction of interfaces
  - Empty interface (interface{})

- Type Embedding
  - Inheritance-like behavior
  - Embedding types within structs
  - Promotes code reuse

- Type Assertions
  - Extract underlying values from interfaces
  - Syntax: value, ok := i.(Type)

- Type Aliases
  - Create aliases for existing types
  - Enhances code readability
  - Example: type Celsius float64

- Type Methods
  - Attach methods to custom types
  - Receiver in method definition
  - Value receivers vs. pointer receivers

- Type Switch
  - Switch statement for types
  - Syntax: switch v := i.(type)

- Empty Interface
  - Interface{} represents any type
  - Commonly used in generic code

- Reflection
  - Inspect types dynamically
  - reflect package
  - Use sparingly due to performance impact

- Type Safety
  - Enforced at compile-time
  - Reduces runtime errors
  - Minimizes ambiguity

- Zero Value
  - Default value for variables
  - Numerical types: 0
  - Strings: ""
  - Pointers: nil

- Best Practices
  - Favor simplicity and clarity
  - Use explicit types for readability
  - Minimize use of empty interfaces

## 3. Interface
- Definition
  - Type with method signatures
  - Contract for method implementation

- Implicit Implementation
  - Types implement without declaration
  - Based on method signatures

- Polymorphism
  - Different types, same interface
  - Code flexibility

- Empty Interface (interface{})
  - Type with zero methods
  - Holds values of any type

- Interface Composition
  - Build complex interfaces
  - Embed other interfaces

- Type Assertion
  - Extract underlying value
  - Recover dynamic type

- Type Switch
  - Conditional logic based on type
  - Simplifies type checking

- Interface Values and Nil
  - Nil interface: nil type, nil value
  - Panics on method call

- Explicit Interface Implementation
  - Explicitly declare interface implementation
  - Provide required methods

- Interfaces Are References
  - Interface holds reference to underlying value
  - Changes reflected in interface variable

- Interface Satisfaction Checked Implicitly
  - Checked at compile-time
  - Compile-time error if methods not provided

- Duck Typing
  - Quacks like a duck, treated as a duck
  - Based on satisfying interface

- Interfaces in Standard Library
  - Many types implement common interfaces
  - Consistent and interoperable experience

## 4. Goroutines and channels
- Concurrency in Go
  - Simultaneous execution
  - Goroutines and channels for concurrency

- Goroutines
  - Lightweight threads
  - Concurrently execute functions
  - Created using "go" keyword

- Channel Basics
  - Communication between Goroutines
  - FIFO (First In, First Out) queue
  - Created using "make" function

- Channel Direction
  - Specify send or receive direction
  - Enhances type safety

- Buffered Channels
  - Capacity for multiple values
  - Blocking only when full

- Select Statement
  - Multiplexing multiple channels
  - Handles concurrent communication

- Closing Channels
  - Signaling the end of data
  - Receivers detect channel closure

- Range and Close
  - Range over channel values
  - Automatically detects closure

- Select with Timeouts
  - Timeout handling in select
  - Prevents indefinite blocking

- Fan-Out, Fan-In
  - Fan-Out: Multiple Goroutines writing
  - Fan-In: Single Goroutine reading

- Worker Pools
  - Managing concurrent tasks
  - Efficient resource utilization

- Context Package
  - Managing Goroutine lifecycle
  - Cancelling, timeouts, and deadlines

- Avoiding Race Conditions
  - Proper synchronization
  - Mutexes and sync package

- Share Memory by Communicating
  - Principle in Go concurrency
  - Emphasizes channel-based communication

- Patterns and Idioms
  - Common usage patterns
  - Ensures clean and effective concurrency

- Best Practices
  - Goroutines: Start, Wait, and End
  - Channel usage: Direction, Close, and Buffers

- Debugging Goroutines
  - Tools and techniques
  - Detecting and resolving issues


## 5. Garbage collection
- Automatic Memory Management
  - Managed by Go runtime
  - No explicit memory deallocation

- Mark and Sweep Algorithm
  - Primary garbage collection algorithm
  - Identifies and reclaims unreachable objects

- Tracing Garbage Collector
  - Identifies live objects
  - Traces object references

- Generational Garbage Collection
  - Objects categorized by age
  - Young and old generations

- Three Generations
  - Young: Newly allocated objects
  - Middle-aged: Survived one garbage collection
  - Old: Survived multiple garbage collections

- Write Barrier
  - Records pointers to newly allocated objects
  - Assists in maintaining object references

- Minor and Major Collections
  - Minor: Collects young generation
  - Major: Collects entire heap, including old generation

- Stop-the-World
  - Pauses application threads during garbage collection
  - Minimizes impact on application performance

- Garbage Collection Triggers
  - Triggered by memory allocation
  - Controlled by the runtime

- GODEBUG Environment Variable
  - Provides insights into garbage collection
  - Useful for debugging and tuning

- Garbage Collection Performance
  - Tuning options available
  - Impact on application performance

- Avoiding Garbage Collection Pauses
  - Reducing allocation rate
  - Using object pools

- Finalizers
  - Special methods executed before object reclamation
  - Used for resource cleanup

- Memory Leaks
  - Managed by garbage collector
  - Rare but possible if references are not managed

- Pros and Cons
  - Pros: Automatic, efficient
  - Cons: Stop-the-world pauses

- Tuning Garbage Collection
  - GOGC environment variable
  - Adjusting garbage collection parameters

- Best Practices
  - Minimize unnecessary allocations
  - Understand the impact on your application

- Memory Profiling
  - go tool pprof for memory profiling
  - Identifying memory-hungry areas

- Continuous Improvement
  - Go runtime evolves
  - Keep up with improvements and best practices


## 6. Optimizations

- Overview
  - Continuous focus on performance
  - Go runtime optimizations

- Profiling
  - go tool pprof
  - Identifying performance bottlenecks

- Benchmarking
  - go test -bench
  - Measure execution time and allocations

- Compiler Optimizations
  - Escape analysis
  - Inlining

- Memory Optimization
  - Minimizing allocations
  - Object pooling

- Concurrency
  - Effective use of Goroutines
  - Avoiding excessive synchronization

- Channel Optimization
  - Buffered channels for performance
  - Reducing contention

- Wait Groups
  - sync.WaitGroup for synchronization
  - Avoiding race conditions

- Context Package
  - context.Context for cancellation
  - Managing Goroutine lifecycles

- Map Optimizations
  - Choosing the right map type
  - Load factor considerations

- String Concatenation
  - Using strings.Builder for efficiency
  - Avoiding repeated concatenation

- Slice Tricks
  - Avoiding unnecessary slices
  - Efficiently appending to slices

- Interface Optimization
  - Minimizing unnecessary interfaces
  - Considerations for performance

- Reflection
  - Efficient use of reflection
  - Reflection vs. performance trade-offs

- Assembly Language
  - Leveraging assembly language for critical sections
  - Platform-specific optimizations

- Cache Locality
  - Designing data structures for cache efficiency
  - Reducing cache misses

- CPU Profiling
  - Identifying CPU-intensive code
  - go tool pprof for CPU profiling

- Network and I/O Optimization
  - Efficient use of network resources
  - Reducing blocking I/O operations

- Continuous Monitoring
  - Monitoring tools for performance tracking
  - Grafana, Prometheus, etc.

- Best Practices
  - Balancing readability and performance
  - Profiling before optimizing

- Platform-Specific Considerations
  - Tailoring optimizations to the deployment environment
  - Understanding platform characteristics

- Community Resources
  - Golang performance blogs
  - Learning from community experiences

- Version Updates
  - Staying updated with Go releases
  - Benefit from performance improvements

- Case Studies
  - Real-world examples of successful optimizations
  - Learning from industry practices

## 7. Generics

- Overview
  - Introduction to generics in Go
  - Proposal and adoption

- Generic Types
  - Functions, structs, interfaces
  - Writing code without specific types

- Type Parameters
  - <T> syntax
  - Naming conventions

- Type Constraints
  - Specifying required behaviors
  - Constraints on type parameters

- Function Generics
  - Writing functions with generic types
  - Increased code reuse

- Slice Functions
  - Examples of generic functions for slices
  - Appending, filtering, mapping

- Interface Constraints
  - Implementing generic interfaces
  - Benefits of constrained types

- Type Assertions with Generics
  - Using type assertions with generic types
  - Ensuring type safety

- Error Handling
  - Generic error types
  - Returning errors from generic functions

- Generic Packages
  - Creating generic packages
  - Packaging reusable generic code

- Code Readability
  - Balancing generic code and readability
  - Guidelines for clear and maintainable code

- Syntax Changes
  - Impact on syntax with generics
  - Understanding new syntax rules

- Performance Considerations
  - Implications for runtime performance
  - Overhead and optimizations

- Compiler and Tool Support
  - Compatibility with gofmt and other tools
  - IDE support for generic code

- Community Adoption
  - Acceptance and usage in the community
  - Success stories and challenges

- Evolution of Go
  - Generics as a language feature
  - Future enhancements and adjustments

- Best Practices
  - Guidelines for using generics effectively
  - Consistent and idiomatic usage

- Compatibility with Existing Code
  - Migrating existing code to use generics
  - Ensuring backward compatibility

- Learning Resources
  - Official documentation on generics
  - Tutorials and examples for hands-on learning

- Case Studies
  - Real-world examples of successful use of generics
  - Learning from practical implementations


## 8. Error handling
- Introduction
  - Importance of proper error handling
  - Design philosophy in Go

- Named Return Values
  - Functions with named return values
  - Enhances code readability

- Check Errors Immediately
  - Immediate error checks after function calls
  - Avoid deferring error handling

- Sentinel Errors
  - Predefined error values for common conditions
  - Simplifies error comparisons

- Wrap Errors with Context
  - fmt.Errorf and errors.Wrap for context
  - Improved error messages for debugging

- Handle or Propagate
  - Handle errors at the appropriate level
  - Propagate errors up the call stack

- Return Errors Unwrapped
  - Return errors using %w for clear error messages
  - Distinguish between different layers

- Logging Errors
  - Use log package or dedicated logging library
  - Include relevant context information

- Graceful Degradation
  - Design code to gracefully degrade in the presence of errors
  - Provide defaults or fallbacks

- Use errors.Is and errors.As
  - Check for specific errors using Is
  - Extract values from error chains using As

- Unit Test Error Paths
  - Write unit tests to cover error paths
  - Ensure thorough testing of error-handling code

- Panic vs. Error
  - Reserve panic for unrecoverable situations
  - Prefer returning errors for expected conditions

- Continuous Improvement
  - Learn from debugging experiences
  - Iterate on error-handling strategies

- Best Practices
  - Balancing simplicity and effectiveness
  - Consistent and idiomatic error handling

- Community Resources
  - Readings, blogs, and discussions on effective error handling
  - Learn from the Go community's experiences

## 9. Testing
- Overview
  - Importance of testing
  - Built-in testing framework

- Test File Naming
  - Suffix: _test.go
  - e.g., package_test.go

- Test Function Naming
  - Prefix: Test
  - Descriptive names
  - e.g., TestFunctionality

- Table-Driven Tests
  - Multiple input cases
  - Improved readability

- Examples in Documentation
  - Living documentation
  - Executable examples

- Parallel Tests
  - Default parallel execution
  - t.Parallel() for individual tests

- Subtests
  - Better organization
  - t.Run for subtests

- Test Coverage
  - go test -cover
  - Aim for high coverage

- Benchmarks
  - Benchmark functions
  - go test -bench

- Avoid Testing Main Code Paths
  - Focus on edge cases
  - Test critical functionality

- Mocking
  - Interfaces for mocking
  - Test doubles for dependencies

- Assertions
  - testing.T for assertions
  - t.Errorf, t.Fatalf, t.Logf

- Test for Expected Errors
  - Explicitly test errors
  - if err != expectedError

- Code Examples in Tests
  - Examples in test files
  - Serve as documentation

- Test Setup and Teardown
  - TestMain for shared logic
  - Encapsulate setup and teardown

- Use Test Constants
  - Define constants for test data
  - Avoid magic numbers/strings

- Continuous Integration
  - Integrate tests into CI
  - Automatic testing on each change

- Documentation for Test Cases
  - Clear and concise documentation
  - Describe purpose, inputs, and outcomes

- Test for Idempotence
  - Tests are idempotent
  - No side effects

- Testing Private Functions
  - Place test file in the same package
  - Access to private functions

- Review and Refactor Tests
  - Regular review and updates
  - Reflect changes in requirements

- Best Practices
  - Consistent and idiomatic
  - Effective and maintainable

## 10. Debugging
- Overview
  - Importance of debugging
  - Go tools and techniques

- Go Debugging Tools
  - Delve debugger
  - go tool pprof
  - Trace and race tools

- Printf Debugging
  - Using fmt.Println
  - Basic debugging technique

- Logging
  - log package for logging
  - Include relevant context

- Debugger: Delve
  - Installation: go get -u github.com/go-delve/delve/cmd/dlv
  - Basic commands: run, break, continue, step, etc.

- Debugging with VSCode
  - VSCode integration with Delve
  - Setting breakpoints, inspecting variables

- Profiling: go tool pprof
  - CPU profiling: go test -cpuprofile
  - Memory profiling: go test -memprofile

- Tracing: go tool trace
  - Execution tracing
  - Visualizing program flow

- Race Detector: go test -race
  - Detecting race conditions
  - Identifying data races

- Printf Debugging Best Practices
  - Use sparingly
  - Remove before committing

- Conditional Debugging
  - Leveraging build tags
  - #ifdef style debugging

- Core Dumps
  - Capture and analyze core dumps
  - Investigate crashes

- Panic and Recover
  - Using panic for exceptional conditions
  - Recovering gracefully

- Unit Testing for Debugging
  - Writing test cases
  - Isolating issues

- Remote Debugging
  - Debugging on a remote server
  - Delve remote debugging

- Stack Traces
  - Analyzing stack traces
  - Identifying error origins

- Version Control for Debugging
  - Using version control effectively
  - Bisecting to identify issues

- IDE Debugging
  - Debugging with GoLand, Visual Studio Code, etc.
  - Utilizing integrated debugging features

- Troubleshooting Dependencies
  - Debugging third-party packages
  - Understanding and resolving issues

- Common Debugging Scenarios
  - Deadlocks
  - Memory leaks
  - Performance bottlenecks

- Continuous Improvement
  - Learning from debugging experiences
  - Iterating on debugging strategies

- Best Practices
  - Efficient and effective debugging
  - Collaborative debugging techniques

## 11. Project Structure

- Overview
  - Importance of a well-organized project structure
  - Maintainability and scalability

- Standard Project Layout
  - Repository structure by Benjamin Radovsky
  - https://github.com/golang-standards/project-layout

- Main Components
  - cmd: Main applications
  - internal: Private application and library code
  - pkg: Library code that may be used across multiple projects
  - api: OpenAPI/Swagger specs, JSON schema files, protocol definition files
  - web: Web application-specific components
  - scripts: Scripts to perform various build, install, analysis, etc. tasks

- Versioning
  - Versioning in the project structure
  - Use of tags or branches for versions

- Configuration
  - Configuration file handling
  - Environment variables for configuration

- Dependency Management
  - Use of Go modules for dependency management
  - go mod tidy for cleaning up unused dependencies

- Testing
  - Separate test files in each package
  - Integration tests in a separate directory
  - Test data in a testdata directory

- Documentation
  - README.md for project documentation
  - Godoc for inline documentation
  - Document code usage and examples

- Logging
  - Consistent logging practices
  - Choose a logging package (e.g., logrus)

- Error Handling
  - Use named return values for errors
  - Centralized error handling if possible

- Conventions
  - Consistent naming conventions
  - Package naming based on functionality
  - Avoid abbreviations, unless widely accepted

- Gitignore
  - Appropriate entries in .gitignore
  - Exclude build artifacts, IDE-specific files

- Continuous Integration
  - CI/CD configuration (e.g., .gitlab-ci.yml, .github/workflows/)
  - Automatic testing and deployment

- Code Formatting
  - Consistent code formatting
  - Use of go fmt or tools like goimports

- Vendor Directory
  - Avoid committing the vendor directory
  - Use go mod vendor if needed

- Makefile
  - Use a Makefile for common tasks
  - Build, test, clean, etc.

- Code Reviews
  - Regular code reviews
  - Adherence to code style and project structure

- Dependency Scanning
  - Regularly check for dependency vulnerabilities
  - Use tools like GoSec or Dependabot

- Versioning Your APIs
  - Follow semantic versioning for APIs
  - Handle breaking changes carefully

- Licensing
  - Include a LICENSE file
  - Clearly specify the project's license

- Security
  - Regular security audits
  - Stay informed about security best practices

- Continuous Improvement
  - Learn from project experiences
  - Regularly update and refine the project structure

- Best Practices
  - Consistent and idiomatic structure
  - Adapt to the project's specific needs

## 12. Other Tips
- Overview
  - Simplicity and readability
  - Robustness and performance

- Syntax and Style
  - Consistent formatting
  - gofmt and goimports tools
  - Minimal use of parentheses

- Naming Conventions
  - Descriptive and idiomatic names
  - Short for local variables, longer for package-level

- Error Handling
  - Named return values for errors
  - Centralized error handling when possible
  - Avoid panic for expected errors

- Concurrency
  - Goroutines for concurrent tasks
  - Use channels for communication
  - Avoid excessive use of locks

- Composition over Inheritance
  - Prefer composition for code reuse
  - Simplicity and flexibility

- Interface Design
  - Small, focused interfaces
  - Prefer many small interfaces over a few large ones
  - Implicit interfaces with duck typing

- Dependency Management
  - Use Go modules for dependency management
  - go get, go mod tidy, and go mod vendor commands
  - Versioning with go.mod

- Testing
  - Table-driven tests for multiple cases
  - Unit tests for individual functions
  - Integration tests for broader scenarios

- Documentation
  - Clear and concise documentation
  - Godoc for inline documentation
  - Examples in documentation

- Code Review
  - Regular code reviews
  - Enforce coding standards
  - Promote collaboration and knowledge sharing

- Avoid Global State
  - Minimize the use of global variables
  - Favor passing dependencies explicitly

- Avoid Reflection Unless Necessary
  - Reflection can be slow and error-prone
  - Use reflection judiciously

- Favor Composition over Inheritance
  - Encourage code reuse through composition
  - Simplicity and flexibility over complex inheritance hierarchies

- Continuous Integration
  - CI/CD pipelines for automated testing
  - Ensure tests run on every push
  - Automatic code formatting checks

- Avoid Premature Optimization
  - Profile before optimizing
  - Optimize based on actual performance bottlenecks
  - Readability and maintainability first

- Graceful Degradation
  - Design for graceful degradation in the presence of errors
  - Provide meaningful defaults or fallbacks

- Avoid Global Variables
  - Minimize the use of global variables
  - Pass dependencies explicitly

- Error Messages
  - Clear and informative error messages
  - Include context information for debugging
  - Use errors.Wrap for richer context

- Cross-Platform Considerations
  - Be aware of platform-specific behaviors
  - Use build tags for platform-specific code

- Avoid Shadowing
  - Avoid shadowing variables
  - Maintain clarity in code

- Best Practices
  - Consistent and idiomatic code
  - Follow the Go Proverbs
  - Learn from the Go community

  Production Tips for Go Applications

- Overview
  - Preparing Go applications for production
  - Ensuring reliability and performance

- Code Optimization
  - Profile and optimize critical paths
  - Use the pprof package for profiling
  - Monitor memory usage and CPU consumption

- Logging
  - Structured logging for easy analysis
  - Include relevant context in logs
  - Use a logging library (e.g., logrus)

- Monitoring
  - Instrument code for metrics
  - Use a monitoring system (e.g., Prometheus)
  - Set up alerts for critical conditions

- Error Handling
  - Propagate meaningful errors to the upper layers
  - Avoid panic in production code
  - Implement error tracking (e.g., Sentry)

- Graceful Shutdown
  - Implement graceful shutdown mechanisms
  - Handle OS signals for clean termination
  - Allow in-flight requests to complete

- Configuration
  - Externalize configuration settings
  - Use environment variables or config files
  - Implement dynamic configuration updates

- Security
  - Regularly update dependencies
  - Use HTTPS for communication
  - Follow security best practices for Go

- Dependency Management
  - Lock dependencies with Go modules
  - Vendor dependencies for reproducibility
  - Regularly update dependencies for security

- Database Connections
  - Use connection pooling for databases
  - Manage database connections efficiently
  - Implement retries for transient errors

- Caching
  - Use caching judiciously
  - Consider distributed caching systems
  - Monitor cache hit rates and performance

- Deployment
  - Create reproducible builds
  - Use containerization (e.g., Docker)
  - Automate deployment processes (e.g., Kubernetes)

- Scalability
  - Design for horizontal scalability
  - Distribute load across multiple instances
  - Monitor system load and adjust resources

- Testing in Production
  - Implement canary releases
  - Gradual rollout of new features
  - Monitor production metrics during testing

- Documentation
  - Maintain comprehensive documentation
  - Include deployment instructions
  - Keep documentation up-to-date

- Backup and Recovery
  - Regularly back up data
  - Test data recovery procedures
  - Implement disaster recovery plans

- Performance Testing
  - Regularly perform load testing
  - Identify and address performance bottlenecks
  - Use tools like Apache Benchmark or wrk

- Continuous Improvement
  - Conduct post-mortems for incidents
  - Learn from failures and improve processes
  - Iterate on architecture and infrastructure

- Team Collaboration
  - Foster collaboration between teams
  - Share knowledge about production systems
  - Cross-train team members on critical components

## 13. Data structures

- Overview
  - Importance of data structures
  - Effective problem-solving

- Slices
  - Dynamic arrays
  - Efficient and flexible
  - Use make() for dynamic sizing

- Arrays
  - Fixed-size collections
  - Less flexible than slices
  - Declared using var or []

- Maps
  - Key-value pairs
  - Unordered collection
  - Use make() to initialize

- Structs
  - Custom data types
  - Aggregate different types
  - No inheritance, but can embed

- Linked Lists
  - Manual implementation
  - No built-in LinkedList type
  - Pointers for linking nodes

- Stacks
  - LIFO (Last In, First Out)
  - Implement with slices or linked lists

- Queues
  - FIFO (First In, First Out)
  - Implement with slices or linked lists

- Trees
  - Hierarchical data structures
  - Binary trees, AVL trees, etc.
  - Useful for search and retrieval

- Heaps
  - Priority queues
  - Min-heap or max-heap
  - Implement with slices

- Graphs
  - Vertices and edges
  - Adjacency lists or matrices
  - Useful for network-related problems

- Trie
  - Tree-like data structure
  - Efficient for string-related tasks
  - Useful for dictionaries, autocomplete

- Bloom Filter
  - Probabilistic data structure
  - Efficient for membership tests
  - False positives possible

- Tips for Go Data Structures
  - Leverage built-in types (slices, maps) where applicable
  - Use structs for custom data types
  - Consider efficiency and readability in design
  - Be mindful of memory usage

- Best Practices
  - Choose the right data structure for the task
  - Understand time and space complexity
  - Write clear and idiomatic code
  - Test and benchmark for performance

## 14. Design patterns

Design Patterns in Golang

- Overview
  - Patterns influenced by Go idioms
  - Emphasis on simplicity and clarity

- Creational Patterns
  - Singleton Pattern
  - Factory Pattern
  - Builder Pattern

- Structural Patterns
  - Adapter Pattern
  - Decorator Pattern
  - Composite Pattern

- Behavioral Patterns
  - Observer Pattern
  - Strategy Pattern
  - Command Pattern
  - Chain of Responsibility Pattern
  - State Pattern
  - Template Method Pattern
  - Visitor Pattern
  - Memento Pattern

- Singleton Pattern
  - Global instance
  - Package-level variable
  - Lazily or eagerly initialized

- Factory Pattern
  - Factory functions
  - Encapsulate object creation
  - Return interface types

- Builder Pattern
  - Separation of construction and representation
  - Use a builder interface
  - Fluent interfaces

- Adapter Pattern
  - Convert interfaces
  - Use adapters to make interfaces compatible

- Decorator Pattern
  - Attach responsibilities dynamically
  - Decorator types
  - Interfaces for components

- Composite Pattern
  - Compose objects into tree structures
  - Treat individual objects and compositions uniformly
  - Use interfaces

- Observer Pattern
  - One-to-many dependency
  - Use channels for communication
  - Publish-subscribe model

- Strategy Pattern
  - Define a family of algorithms
  - Encapsulate each algorithm in a type
  - Use interfaces for strategies

- Command Pattern
  - Encapsulate a request as an object
  - Represent commands as functions or interfaces

- Chain of Responsibility Pattern
  - Pass a request along a chain of handlers
  - Each handler decides to process or pass to the next

- State Pattern
  - Allow an object to alter its behavior when its internal state changes
  - Represent states as types
  - Switch between states

- Template Method Pattern
  - Define the skeleton of an algorithm in the superclass
  - Let subclasses override specific steps

- Visitor Pattern
  - Represent an operation to be performed on elements of an object structure
  - Define a visitor class for each concrete element class

- Memento Pattern
  - Capture and externalize an object's internal state
  - Store the state in a separate memento object

- Best Practices
  - Prioritize simplicity and readability
  - Consider Go idioms and language features
  - Adapt patterns to specific needs

- Resources
  - "Design Patterns in Go" by Tucker, McManus, and Lake
  - Go Design Patterns: github.com/PacktPublishing/Go-Design-Patterns

   Here are examples of how to implement some common design patterns in Go:

1. Singleton Pattern:
```
package singleton

import "sync"

type singleton struct {
    data string
}

var instance *singleton
var once sync.Once

func GetInstance() *singleton {
    once.Do(func() {
        instance = &singleton{"initialized"}
    })
    return instance
}
```

2. Factory Pattern:
```
package factory

type Shape interface {
    Draw() string
}

type Circle struct{}

func (c *Circle) Draw() string {
    return "Drawing Circle"
}

type Rectangle struct{}

func (r *Rectangle) Draw() string {
    return "Drawing Rectangle"
}

func CreateShape(shapeType string) Shape {
    switch shapeType {
    case "Circle":
        return &Circle{}
    case "Rectangle":
        return &Rectangle{}
    default:
        return nil
    }
}
```

3. Observer Pattern:

```

package observer

type Observer interface {
    Update(data string)
}

type Subject struct {
    observers []Observer
}

func (s *Subject) Attach(observer Observer) {
    s.observers = append(s.observers, observer)
}

func (s *Subject) Notify(data string) {
    for _, observer := range s.observers {
        observer.Update(data)
    }
}

type ConcreteObserver struct {
    ID int
}

func (co *ConcreteObserver) Update(data string) {
    // Handle the update
    fmt.Printf("Observer %d received update: %s\n", co.ID, data)
}
```

4. Decorator Pattern:
```
package decorator

type Component interface {
    Operation() string
}

type ConcreteComponent struct{}

func (cc *ConcreteComponent) Operation() string {
    return "ConcreteComponent"
}

type Decorator struct {
    component Component
}

func (d *Decorator) Operation() string {
    return "Decorator(" + d.component.Operation() + ")"
}

type ConcreteDecoratorA struct {
    Decorator
}

func (cda *ConcreteDecoratorA) Operation() string {
    return "ConcreteDecoratorA(" + cda.component.Operation() + ")"
}

```

