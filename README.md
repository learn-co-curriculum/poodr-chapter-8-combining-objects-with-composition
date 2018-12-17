## Using Composition for "has a" Relationships

In the previous chapter, we used inheritance for "is a" relationships and explored the use of modules and their subclasses.

Here, we explore another paradigm for structuring our code.

Examples in Ironboard: course.rb

### 8.1 Composing a Bicycle of Parts (Read: More Bikes!)

To get us started down the path of composition, Sandi reused the `Bicycle` heirarchy by abstracting its parts into its own class and having each type of bike inherit from the `Parts` class with their own parts class (`MountainBikeParts`, `RoadBikeParts`).

Before we dive in further, how does the concept of composition feel so far? Have you used it previously or do you wish you used it more?

### 8.2 Composing the Parts Object

The way you name your classes is important. To prevent communication problems, Sandi named the new class `Parts` which will be the parent of `Part`. `Parts` is now a wrapper that contains an array of `Part` objects.

Instead of thinking of `Part` objects as instances, Sandi tells us to think of them as objects that play the role of `Part`.  "They don’t have to be a kind-of the Part class, they just have to act like one; that is, they must respond to name, description, and needs_spare." -pg. 172

Although Parts now contains an array of objects it is not in itself an array. If you need it to behave like an array it may be worth your while to make an a subclass of `Array` but that may lead to unexpected behavior as seen in her example with her `Parts` class unable to respond to the `spares` method. 

Sandi ended up including `Enumerable` to get common searching and traversal methods.

### 8.3 Manufacturing Parts

Instead of having a class that holds an array of objects, we can also create a module that acts as a factory (an object that creates other objects).

Sandi creates a `PartsFactory` module that takes in both `Parts` and a 2D array of`Part`s and makes objects out of them. This condenses the information needed to create `Parts` in one place rather than dispersed throughout the application.

Because it is now condensed, it’s possible to remove the `Part` class entirely and replace it with `OpenStructs` which are simpler than classes and use as a means of bundling attributes. Thinking of these objects as playing `Part` roles now rings true.

#### A more specific definition

Composition in OO dictates “has-a” relationships but it also implies the contained object cannot have a life independent of its container.

Aggregation is when the contained object can have a life independent of the container. Sandi uses a helpful example of universities to departments and departments to professors to make the distinction between composition and aggregation. Departments cannot exist without university therefore this demonstrates composition. However, professors can exist without departments and this is an example of aggregation.

### 8.5 Deciding Between Composition and Inheritance 

With composition, method delegation doesn’t come for free like with inheritance.  

#### Pros and Cons of Inheritance

##### Pros:

- Covers RUE part of our goal to be TRUE: reasonable, usable and exemplary
- Methods defined near the top of the heirarchy are spread easily over everything underneath making changes to behavior relatively easy and reasonable
- Adding a new subclass doesn't require making a change to existing code thus making it usable
- These classes are easily extendible setting an easy pattern to follow. This puts the e in exemplary.

##### Cons:

- You're unable to predict how your code will be used in the future. Future developers may have issues with the dependencies you put in place.
- If the heirearchy has been modeled incorrectly, there is a cost to modifying code close to the top of the heirarchy. Everything will break if you make a change.
- It's difficult to add new behavior if your subclasses are of varying types.
- "...classical inheritance’s greatest strength and biggest weakness; subclasses are bound,
irrevocably and by design, to the classes above them in the hierarchy." - pg. 187

#### Pros and Cons of Composition

##### Pros:

- Covers the TRU part of our goal to be TRUE: true, reasonable and usable.
- Easy to understand (transparent)
- Adding objects is easy as long asthey honor the given interface (reasonable)
- Interchangeable components with "...a high tolerance for change." (usuable) - pg 188

##### Cons:

- Message delegation must be explicit



<p class='util--hide'>View <a href='https://learn.co/lessons/poodr-chapter-8-combining-objects-with-composition'>POODR Chapter 8: Combining Objects with Composition</a> on Learn.co and start learning to code for free.</p>
