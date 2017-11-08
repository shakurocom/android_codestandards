# Kotlin Style Guide

On the whole, you should follow [Google’s Android coding standards for source code in the Kotlin Programming Language](https://android.github.io/kotlin-guides/style.html).

There are some most important rules bellow.

### Packages

Package names are all lower-case, multiple words concatenated together, without underscores: `com.shakuro.somewidget` instead of `com.Shakuro.some_widget`

### Fully qualify imports

While excessive methods and imports can be stripped out with proguard, it is good practice to minimize the amount of code included.
For Example: `import foo.Bar` instead of `import foo.*`

### Fields definition and naming
Fields should be defined at the __top of the file__ and they should follow the naming rules listed below.

* constants `val` are all caps (e.x. `MY_CONST`) and can be located either in the [companion object](https://kotlinlang.org/docs/reference/object-declarations.html#companion-objects) or field
* all other fields should follow [LowerCamelCase](http://en.wikipedia.org/wiki/CamelCase) conventions

Example:

```kotlin
public class MyClass {
    companion object {
        public const val SOME_CONSTANT = 42
    }

    private val FOO = 1

    private var privateVar: Int
    protected var protectedVar: Int
    public var publicVar: Int
}
```

### Treat acronyms as words
| Good             | Bad              |
| ---------------- | ---------------- |
| `XmlHttpRequest` | `XMLHTTPRequest` |
| `getCustomerId`  | `getCustomerID`  |
| `String url`     | `String URL`     |
| `long id`        | `long ID`        |


### Use spaces for indentation
Use __4 space__ indentations for blocks:

```kotlin
if (i == 1) {
    i++;
}
```

Use __8 space__ indentations for line wraps:
```kotlin
val instrument =
        someLongExpression(that, wouldNotFit, on, one, line)
```

### Use standard brace style
Braces go on the same line as the code before them and are always required, except in the case of replacing
the ternary operator. e.g.

```kotlin
class MyClass {
    fun test() {
        if (something) {
            // ...
        } else if (somethingElse) {
            // ...
        } else {
            // ...
        }
    }

    //An example of an if...else replacement for a ternary
    fun ternaryFunction(someValue: String): Int {
        return if (someValue.isEmpty()) 0 else 1
    }
}
```

### Class member ordering
There is no single correct solution for this but using a __logical__ and __consistent__ order will improve code
readability. It is recommendable to use the following order:

1. Constants
2. Fields
    1. Constants
    2. Annotated properties (`@Inject`, `@BindExtra` and etc.)
    3. Member Variables
3. Constructors
4. Override methods and callbacks (public or private)
5. Public methods
6. Private methods
7. Inner classes
8. Nested classes or interfaces

Example:

```kotlin
public class MainActivity: Activity {
    companion object {
        private const val ARG_FOO = "TAG"
    }

    @Inject //Dagger
    Prefs prefs

    private var title: String?

    override public fun onCreate() {
        //...
    }

    public fun setTitle(title: String?) {
    	this.title = title;
    }

    private fun setUpView() {
        //...
    }

    //the `inner` keyword indicates the class is a child of `MainActivity`
    private inner class AnInnerClass {
        //...
    }

    //nested classes are static by default in kotlin
    class ANestedClass {
        //...
    }
}
```

### Line-wrapping strategies
There isn't an exact formula that explains how to line-wrap and quite often different solutions are valid. However
there are a few rules that can be applied to common cases.

__Method chain case__

When multiple methods are chained in the same line - for example when using Builders - every call to a method should
go in its own line, breaking the line before the `.`

```kotlin
Picasso.with(context).load("http://ribot.co.uk/images/sexyjoe.jpg").into(imageView)
```

```kotlin
Picasso.with(context).apply {
    load("http://ribot.co.uk/images/sexyjoe.jpg")
    into(imageView)
}
```

__Long parameters case__

When a method has many parameters or its parameters are very long we should break the line after every comma `,`

```kotlin
loadPicture(context, "http://ribot.co.uk/images/sexyjoe.jpg", imageViewProfilePicture, clickListener, "Title of the picture");
```

```kotlin
loadPicture(context,
        "http://ribot.co.uk/images/sexyjoe.jpg",
        imageViewProfilePicture,
        clickListener,
        "Title of the picture");
```

