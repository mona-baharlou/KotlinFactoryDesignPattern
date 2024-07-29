# KotlinFactoryDesignPattern

The Factory Design Pattern is a creative way of building objects in programming. It gives us a system to create different types of objects without tying our hands to specific classes. Picture it as a factory assembly line: we provide the type of product we want, and the factory makes it—no need to worry about the nitty-gritty details of production.

Let’s take a closer look at a piece of Kotlin code that illustrates how the Factory Design Pattern works:

### Code Breakdown

```kotlin

interface Animal {
    fun makeSound()
}
```
- **Animal Interface**: This is like a contract for all animals. It defines a common method, `makeSound()`, that every animal class will have to implement. Think of it as all animals being required to have a unique way of expressing themselves.

```kotlin
class Dog() : Animal {
    override fun makeSound() {
        println("Haap!")
    }
}

class Cat() : Animal {
    override fun makeSound() {
        println("Meow!")
    }
}
```
- **Dog and Cat Classes**: Here’s where the fun begins! The `Dog` and `Cat` classes each take on the `Animal` interface. When a dog barks, it says "Haap!" and when a cat meows, it says "Meow!" This is a great example of polymorphism, where different animals (classes) show their own personalities (implementations of the same method).

```kotlin
object AnimalFactory {
    fun createAnimal(animalType: AnimalType): Animal {
        return when (animalType) {
            AnimalType.DOG -> Dog()
            AnimalType.CAT -> Cat()
            else -> throw IllegalArgumentException("Unknown Animal Type")
        }
    }
}
```
- **AnimalFactory Object**: This handy object acts as the animal-shaped assembly line. The function `createAnimal` takes in an `AnimalType` enum value and decides whether to create a `Dog` or a `Cat`. If it encounters an unrecognized type, it throws an error. This keeps our object creation neat and organized!


```kotlin
val myDog: Animal = AnimalFactory.createAnimal(AnimalType.DOG)
val myCat: Animal = AnimalFactory.createAnimal(AnimalType.CAT)
```
- **Creating Instances**: This is where we put our factory to use! We ask the `AnimalFactory` to create a `Dog` and a `Cat`. The result is two new animal buddies, `myDog` and `myCat`, without us needing to know how they were made.

```kotlin
myDog.makeSound()
myCat.makeSound()
```
- **Using the Instances**: Now it's showtime! We call the `makeSound()` method on both animals. The dog barks and the cat meows, showcasing their distinct sounds. They act in line with the `Animal` interface but express themselves in their unique ways.

```kotlin
enum class AnimalType {
    DOG, CAT
}
```
- **AnimalType Enum**: Think of this enum as our factory's menu. It clearly lists the types of animals we can create: `DOG` and `CAT`. This makes our code safer and easier to read.


### Summary

In a nutshell, the Factory Design Pattern makes life easier for developers by keeping object creation separate from the code that uses those objects. This loose coupling means that we can extend our code later without significant changes. If we decide to add a new type of animal, we can create a new class that implements the `Animal` interface and update the `AnimalFactory` accordingly, all while keeping existing usage intact! It's a flexible, maintainable approach that opens up possibilities for future expansion.
