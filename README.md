# Swift

camelCase

```swift
// define a variable
var firstname = "Tom"

// constent value, cannot be assigned to other value
let lastname = "Smith" 

a...b   // closed range
a..<b   // 3 excluded
...b    // one sided range, upto b, b included
```

## Data Types:
- String
- Int
- Float
- Double
- Bool
- Array
- Dictionary
- Struct

## Function
```swift
// Typed variable 
var firstName: String = "Tom"

for counter in 1...5 { ... }

func addTwoNumbers() { ... }

// parameter label
func addTwoNumbers(using number1: Int, and number2: Int ) -> Int {
    return number1 + number2
}
let sum = addTwoNumbers(using: 5, and: 5)

func addTwoNumbers(number1: Int, number2: Int ) -> Int {
    return number1 + number2
}
let sum = addTwoNumbers(number1: 5, number2: 5)

func addTwoNumbers(_ number1: Int, _ number2: Int ) -> Int {
    return number1 + number2
}
let sum = addTwoNumbers(5, 5)
```

## Struct
```
struct MyStruct {}

struct Town {
    let name: String
    var citizens: [String]
    var resources: [String: Int]
    
    // initialiser
    init(name: String, citizens: [String], resources: [String: Int]) {
        self.name = name
        self.citizens = citizens
        self.resources = resources
    }
    
    // method
    func fortify() {
        print("Defenses increased!");
    }
    
    // can only change a property within struct using mutating
    mutating func harvestRice() {
        resources["Rice"] = 100
    }
}
var anotherTown = Town(name: "Nameless Island", citizens: ["A", "B"], resources: ["Coconuts": 100])
// change a property outside struct is fine
anotherTown.citizens.append("C");
```

## Class
```swift
class Employee {
    var name = "name"
    var salary = 0
    var role = ""
    
    func doWork() {
        print("My name is \(name) and I'm doing the work")
        salary += 1;
    }
}
let employee = Employee()

// inheritance
class Manager: Employee {
    var teamSize = 0
    
    override func doWork() {
        super.doWork()                // My name is Maggie and I'm doing the work
        print("I'm managing people")  // I'm managing people
        salary += 2
    }
    
    func firePeople() {
        print("I'm firing people")
    }
}

let e: Employee = Employee()
e.name = "Tom"
print(e.name)
e.doWork()
print(e.salary)


var m = Manager()
m.name = "Maggie"
m.salary = 2000
m.role = "Manager of IT"
m.teamSize = 10
m.doWork()
m.firePeople()
```

```swift
class Person {
    var name = ""
    init() {
        name = "Joe"
    }
    
    init (_ name:String) {
        self.name = name
    }
}

let p = Person()
print(p.name)       // Joe

let p1 = Person("Tom")
print(p1.name)      // Tom


class Employee: Person {
  var salary = 0
  var role = ""
    
  override init() {
      super.init()
  }
  
  override init(_ name: String) {
      super.init(name)
      self.role = "Analyst"
  }
    
  func doWork() {
      print("My name is \(name) and I'm doing the work")
      salary += 1;
  }
}

let employee = Employee("Mark")     // Employee inherit init() from Person class as well
print(employee.name) // Mark
print(employee.role) // Analyst
```

## Class & Struct
```swift
// Enemy - class - pass by reference
// 1. inheritance. 2. pass by reference
let skeleton1 = Enemy(health: 100, attackStrength: 10)
let skeleton2 = skeleton1

skeleton1.takeDamage(amount: 10)
skeleton1.takeDamage(amount: 10)
skeleton2.takeDamage(amount: 10)
print(skeleton1.health)         // 80
print(skeleton2.health)         // 90

// Enemy - struct
// 1. immutable. 2. pass by value
var skeleton1 = Enemy(health: 100, attackStrength: 10)
var skeleton2 = skeleton1

skeleton1.takeDamage(amount: 10)
print(skeleton2.health)         // 90
```

## Extension
```
extension SomeType {
    // add new functionality
}
extension Double {
    func round(to places: Int) -> Double {
        let precisionNumber = pow(10, Double(places))
        var n = self  // current value of the double
        n = n * precisionNumber
        n.round()
        n = n / precisionNumber
        return n
    }
}

var myDouble = 3.14159
let myRoundedDouble = String(format: "%.1f", myDouble)
myDouble.round(to: 2)


extension UIButton {
    func makeCircle() {
        self.clipsToBounds = true
        self.layer.cornerRadius = self.frame.size.width / 2
    }
}
let button = UIButton(frame: CGRect(x: 0, y: 0, width: 50, height: 50))
button.backgroundColor = .red
button.makeCircle()


extension SomeProtocol {
    // define default behaviour
}
protocol CanFly {
    func fly()
}
extension CanFly {
    func fly() {
        print("The obj can take off into the air")
    }
}
struct Airplane: CanFly {}
let myPlane = Airplane()
myPlane.fly()   // The obj can take off into the air
```

## Optional
```swift
var a: Int? = nil      // declare an optional, int or nil
var b: String? = nil   // declare an optional, string or nil

// c can store a string or nil, but it is wrapped
var c: String?         // default is nil - RECOMMENDED way to declare

// d can store a string or nil, but it is already unwrapped
var d: String!         // 更容易出错，d.method() 时不会再检查 d 是不是 nil

let eggTimes = ["Soft": 5, "Medium": 7, "Hard": 12]
let hardness = sender.currentTitle!    // optional to string
let result = eggTimes[hardness]!  // result is Int type

class  XmasPresent {
    func surprise() -> Int {
        return Int.random(in: 1...10)
    }
}
let present: XmasPresent? = XmasPresent()

// ways to check the optional to see if it contains an object

let myOptional: String?
myOptional = nil

// 1. force unwrapping
let text: String = myOptional!      // will crash if the optional is nil

// 2. check first and then unwrap
if myOptional != nil {
    // have to first unwrap the optional
    let text: String = myOptional!
} else {
    print("myOptional was found to be nil")
}

// 3. optional binding
// if present is nil, pass the if statement
// if present is not nil, unwrap it and assign it to actualPresent
if let safeOptional = myOptional {
    let text: String = safeOptional
    print(safeOptional)
} else {
    print("myOptional was found to be nil")
}

// 4. nil coalescing operator
let text: String = myOptional ?? "default value"

// 5. optional chaining
// if present is nil, nothing happens, otherwise, run the statement
present?.surprise()
```

## Properties
```
// calculated properties
var bonus:Int {
  return teamSize * 1000
}
```

## Designated & Convenience Initializer
```swift
class Person {
    var name:String
    // optional integer
    var networth:Int?
    var gender:String!
    
    // designated initializer ensure that the object is ready to be used and all of its properties are initialized
    init() {
        name = "None"
    }
    
    // convenience initializer is for you to preconfig the object in a certain way. may call designated initializer in it
    convenience init(_ gender:String, _ networth:Int) {
        // call the designated initializer to ensure that the object is ready to go
        self.init()
        
        // set any other properties or custom code to initialize for this scenario
        self.gender = gender
        self.networth = networth
    }
}

let a = Person()
print(a.name)
print(a.networth)   // nil

let b = Person("male", 12222)
```

## Array
```swift
let array = ["Dog", "Car", "Bird"]
for counter in 0...array.count - 1 {
    print(array[counter])
}

for item in array {
    print(item)
}

// array type
var myArray: [String] = ["Dog", "Car", "Bird"]

// how to declare an empty array
var emptyArray:[String] = []
var emptyArray2 = [String]()


myArray.insert("Frog", at: 0)
myArray += ["Frog", "Bear"]
// Frog Dog Car Bird Frog Bear
```

## Switch
```swift
switch hardness {
    case "Soft":
        print(5)
    case "Medium":
        print(7)
    case "Hard":
        print(12)
    default:
        print("Error")
}
```

## Dictionary
```swift
// declare a dictionary
var myDictionary = [String: String]()
let eggTimes = ["Soft": 5, "Medium": 7, "Hard": 12]
var dict: [String: Int] = ["Key" : 123]
dict["Key"]    // 123

// assign data into a distionary
myDictionary["SJD 293"] = "Red Ferrari"
myDictionary["UDS 111"] = "BMW"

// retrieve value as optional string
print(myDictionary["SJD 293"])
print(myDictionary["1"])        // nil

// remove
//myDictionary["SJD 293"] = nil

// loop through
for (key, value) in myDictionary {
    print("\(key) is a \(value)")
}
```

## Protocols
```swift
// define the protocol
protocol MyProtocol {
    // Define requirements
}

// adopting the protocol in both struct and class
struct MyStruct: FirstProtocol, SecondProtocol {}
class MyClass: SuperClass, FirstProtocol {}


protocol CanFly {
    func fly()
}

class Bird {
    var isFemale = true
    func layEgg() {
        if female { ... }
    }
}

class Eagle: Bird, CanFLy {
    func fly() { ... }
    func soar() { ... }
}

class Penguin: Bird {
    func swim() { ... }
}

// struct instead of class, because it does not need to inherit from any parent class
struct Airplane: CanFly {
    func fly() { ... }
}

struct FlyingMuseum {
    func flyingDemo(flyingObject: CanFly) {
        flyingObject.fly()
    }
}
```

## Delegate Design Pattern - with Protocol
```swift
// define the required func in protocol, no implementation
protocol AdvancedLifeSupport {
    func performCPR()
}

// similar to TextField class
// EmergencyCallHandler don't care who can do performCPR, as long as he adopts AdvancedLifeSupport protocol
class EmergencyCallHandler {
    var delegate: AdvancedLifeSupport?
    
    func assessSituation() { ... }
    
    func medicalEmergency() {
        delegate?.performCPR()
    }
}

// Paramedic adopts the AdvancedLifeSupport protocol
struct Paramedic: AdvancedLifeSupport {
    // when the paramedic is going on call  
    init(handler: EmergencyCallHandler) {
        // set the handler's delegate to the paramedic self
        handler.delegate = self
    }

    func performCPR() { // implementation... }
}

class Doctor: AdvancedLifeSupport {
    init(handler: EmergencyCallHandler) {
        handler.delegate = self
    }
    
    func performCPR() { // implementation... }
    func useStethescope() { ... }                                                                       
}

class Surgeon: Doctor {
    override func performCPR() {
        super.performCPR()
        // do more stuff on behalf of Surgeon...
    }
    
    func useElectricDrill() { ... }
}

let emilio = EmergencyCallHandler()
let pete = Paramedic(handler: emilio)
// or let angela = Surgeon(handler: emilio)

emilio.assessSituation()
emilio.medicalEmergency()
```

## Closure
```swift
func calculator(n1: Int, n2: Int, operation: (Int, Int) -> Int) -> Int {
    return operation(n1, n2)
}

func add(n1: Int, n2: Int) -> Int {
    return n1 + n2
}

func multiply(n1: Int, n2: Int) -> Int {
    return n1 * n2
}

calculator(n1: 2, n2: 3, operation: add)         // 5
calculator(n1: 2, n2: 3, operation: multiply)    // 6

// closure syntax
{ (n1: Int, n2: Int) -> Int in
    return n1 * n2
}
calculator(n1: 2, n2: 3, operation: { (n1: Int, n2: Int) -> Int in
    return n1 * n2
})
calculator(n1: 2, n2: 3, operation: {(no1, no2) in no1 * no2})      // 6


let array = [1, 2, 3, 4, 5, 6]
func addOne (n1: Int) -> Int {
    return n1 + 1
}
array.map(addOne)
array.map({ (n1: Int) -> Int in
    return n1 + 1
})
array.map({ n1 in n1 + 1 })
array.map{$0 + 1}

```

OpenWeather
zhangziyi  markzhang.800@gmail.com


