
# Lecture

## Licenses
* MIT - You cannot be 
* GPL - You cannot be 

## Our project
* Multiple teams (4-5 people) all working on the same product, you get to pitch it at the end. That help eacother, what works for your team.

## Java
* There is reference material, that gives you a walkthrough (quickly). Disposable email address to sign up for throwaway stuff.

### Running Programs
* High level code gets translated into low-level machine laguaguge
  * In python we use a program whos job takes high-level statements into low-level language (translator to low-level ) - Interpretation
  * Compilation (C) - Creation of an executable, complied down to low level that can be executed
  * Hybried of the two, get's compiled to bytecode, produces a .class file it has been complied to an intermeidate state that JVM can run. This all happens at once behind the scenes when we click a run button.

### Define Classes in Java
* `public/private` tells us here in the probram where it can be used. We hide instance variables sometimes, since we want to control access to it, the control is given through methods, and operations.
* We can have multiple constructors, there is a default constructor that java has defined, the default for primitives are usual `0` or `false`
Note: null is not an object.
* this: an instance variable whith a value of the adress of the object.
* If return type is void, then 
* Parameters, creates an alias if it's a reference type, though if we pass in a primitive.
### Encapsulation 
* class provides an abstraction, or a service

### Conventions
* protected: accessable only within the package, shared info in a sub-component

### Inheritance
* Everything is a subclass of tyep Object, every class inherits toString, equals...
* We use super.x to call to methods or attributes from the parent class. Though if java can figure out 
* super(args) - intializes the parent class, 
* If A -> B -> C, each one takes care of their own initilization
* Name lookup: 

sub v = new sub(), v.m() runs the lowest 

# Start of class
# Context
* We don't know what we are making yet, could have web interface, could be an app, we get to choose our own solution.
* Physical limitations cause issues, and physical checks takes lots of time and extra costs
* Simply this so that the driver only has to verfy an invoice which cutsdown on cost and time.
* E-Tranfer, (Single Credit Transfer - Bank Account 2 bacnk account.) request to pay "ask for the money", they want to move this from  person to person to the business level. This is a big step. this needs to be automated since at the business level, they get tons of requests, also they must make sure that the controls are implemented for levels of control lfor verification 
* Payments Canada - Government body that works with this

# POV from CC
* Remove as many interchanges that gives them the beneifts, without losing any money.
* They want this feature, since they should observe (verify what they got) at the point of deliverly allows for this. (They don't trust corner stores, haha)
* Many dilivery points, and cc would rather get payed when they deliver. CC, dones't like credcard, as they lose some money to the ccr company, so they prefer neigher cash, for the physical implications and risks associated with it.
* Tell the store the order electronically, dtails about what's being ordered, then the store can verify these properies, pay and then instantly get their money
* Also errors can be made, and it should be able to account for that, they want real money, that is simple and secure.

# Our Job
* Build a demo product and some assumptions, mve(the least, v - it'll work and solve some problem in inudstry(product- take it to market)) - must have, should hava, can be traded off, and nice to have- if everything is good, then it as added on.

### Agile (what we will use)
* No specificants & deadlines, the team decides what they will work on and go ahead themselves.

### Waterfall
* Old proj management
  * Start with a problem, design, specification
  * Then we start building code, then testing. Then you find out the specification was wrong. Because at each face you go down like a waterfall.

## Negotation
* What they want
  * Demoable - Working with product owners, and can be shown to a customer.
* There are different licences
  * And whatever we as students write we own , Permissive (MIT) anyone can do whatever they want.

## Terminology
* Scrum - a work methodolgy for full time, though a team should pick their own process.
* NDA - Non-Discloser Agreement , what you can say.
* p2p - person to person
* Ineract - Owned by banks, make debit card. The plumbing backend, the UI is the bank you choose. Each bank tries to be more attractive.
* NFS - Not sufficient funds

## TODO
- Get rid of the switch statement, in the switch statement  Implement the command pattern
* Agile Manifesto - 
* Watch all videos - How checks are processed (shows how we got to where  we are today)

## Questions
* whhat would happen if we write a private method in class