
## Properties 

### Stored properties (class and struct only)

it can be let / var 

means let -- cant chanage after initializer 
var -- can changes/update value anytime

```swift
struct Person {
    let name: String
    var company: String
}

let person1 = Person(name: "ios", company: "apple")
person1.company = "Microsoft" // will get errro bcz struct is value type ..

var person1 = Person(name: "ios", company: "apple")
person1.company = "Microsoft"

```

### Lazy Stored Properties
- will always be 'var' becasue will or calcuate value at time of first call only so it cant't be let
- useful for heavy object those are not needed everytime or needed after intiazlition only.

> Note: 
If a property marked with the lazy modifier is accessed by multiple threads simultaneously and the property hasn’t yet been initialized, there’s no guarantee that the property will be initialized only once.


### Computed properties (class, enum and struct)

They provide a getter and an optional setter to retrieve and set other properties and values indirectly.

```swift
enum HTTPRequestTest {
    case list
    case profile

    var baseURL: String {
        "google.com"
    }
    var methodURL: String {
        switch self {
            case .list:
            return  baseURL + "/list"
            case .profile:
            return  baseURL + "/profile"
        }
    }
    var asRequest: URLRequest? {
        guard let url = URL(string: methodURL) else {
            return nil
        }
       return URLRequest(url: url)
    }
}

```

### Property Observer 

- willSet and didSet 

### property wrapper 

> with this : 
You write the management code once when you define the wrapper, and then reuse that management code by applying it to multiple properties

Ex: Here we crated simple trimming char propertyWrapper 

```swift
@propertyWrapper
struct TrimmingText {
    private var text: String = ""
    var wrappedValue: String {
        get {
            text
        } set {
            text = newValue.trimmingCharacters(in: .whitespacesAndNewlines)
        }
    }
}
```
Usage: 

```swift
@TrimmingText var name: String
```

That's it now whenever we will assign value to name it will auto trim so like this we can resue trim logic for other variable as well this wrapper
