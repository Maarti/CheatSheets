# Unreal Engine C++ cheatsheet

## [C++](https://www.sololearn.com/learning/1051)

### Constructors
public:
	MyClass(string n){
		name = n
	}
MyClass myVar("Bryan")

### Const
Cannot modify the object's member variables of a const instance, and only call const functions.

Const functions can't change member variables.

### Abstract/Virtual
Virtual function = will be overridden by a derived class.

Pure virtual function: `virtual void attack() = 0;` (`=0` means "no body").

An abstract class is a class with a pure virtual function

### Template / Generic typing

```cpp
template <class T, class U>
T smaller(T a, U b) {
  return (a < b ? a : b);
}
```

### [Pointers / References](https://isocpp.org/wiki/faq/references#overview-refs)
Pointers are simply a data type that can hold the memory address of other variables.

```cpp
string food = "Pizza";
string* ptr = &food;   // Memory address of obj: 0x6dfed4
```

Dereference operator:
`string food = *ptr;`

Access an object's members with a pointer:
`(*ptr).name   <=>   ptr->name`   // use the dot member for an object, use the arrow member with a pointer to the object


## Unreal Types
FString s = "string"
FString::FromInt(IntVariable);
TMap
TArray

## Logging
UE_LOG(LogTemp, Display, TEXT("Name %s, Age %d"), *Name, Age);

## Misc
1rst include: header file with the name of your project
last include: generated header file