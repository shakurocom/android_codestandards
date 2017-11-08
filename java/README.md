# Java Style Guide

## Naming

On the whole, naming should follow Java standards.

### Packages

Package names are all __lower-case__, multiple words concatenated together,
without underscores: `com.shakuro.somewidget` instead of `com.Shakuro.some_widget `

### Fully qualify imports

While excessive methods and imports can be stripped out with proguard, it is good practice to minimize the amount of
code included. More information can be found [here](https://source.android.com/source/code-style.html#fully-qualify-imports)

For Example:  
an import should read `import foo.Bar;` instead of `import foo.*;`

### Fields definition and naming
Fields should be defined at the __top of the file__ and they should follow the naming rules listed below.

* constants `static final` are all caps (`MY_CONST`)
* all other fields should follow [LowerCamelCase](http://en.wikipedia.org/wiki/CamelCase) conventions

Example:

```java
public class MyClass {
    private static final int FOO = 1;
    public static final int SOME_CONSTANT = 42;

    private int privateVar;
    protected int protectedVar;
    int packageVar;
    public int publicVar;
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

```java
if (i == 1) {
    i++;
}
```

Use __8 space__ indentations for line wraps:
```java
Instrument instrument =
        someLongExpression(that, wouldNotFit, on, one, line);
```

### Use standard brace style
Braces go on the same line as the code before them and are always required.

```java
class MyClass {
    int func() {
        if (something) {
            // ...
        } else if (somethingElse) {
            // ...
        } else {
            // ...
        }
    }
}
```

### Class member ordering
There is no single correct solution for this but using a __logical__ and __consistent__ order will improve code
readability. It is recommendable to use the following order:

1. Constants
2. Fields
    1. Constants
    2. Annotated fields (`@Inject`, `@Bind` and etc.)
    7. Member Variables
3. Static methods
4. Constructors
5. Override methods and callbacks (public or private)
6. Public methods
7. Private methods
8. Inner classes or interfaces

Example:

```java
public class MainActivity extends Activity {
    private static final String TAG = "TAG";

    @Bind(R.id.toolbar) //ButterKnife
    Toolbar toolbar;

    private String title;

    public static String getTag() {
        return TAG;
    }

    @Override
    public void onCreate() {
        //...
    }
    
    public void setTitle(@Nullable String title) {
    	this.title = title;
    }

    private void setUpView() {
        //...
    }

    static class AnInnerClass {
        //...
    }
}
```

#### Line-wrapping strategies
There isn't an exact formula that explains how to line-wrap and quite often different solutions are valid. However
there are a few rules that can be applied to common cases.

__Method chain case__

When multiple methods are chained in the same line - for example when using Builders - every call to a method should
go in its own line, breaking the line before the `.`

```java
Picasso.with(context).load("http://ribot.co.uk/images/sexyjoe.jpg").into(imageView);
```

```java
Picasso.with(context)
        .load("http://ribot.co.uk/images/sexyjoe.jpg")
        .into(imageView);
```

__Long parameters case__

When a method has many parameters or its parameters are very long we should break the line after every comma `,`

```java
loadPicture(context, "http://ribot.co.uk/images/sexyjoe.jpg", mImageViewProfilePicture, clickListener, "Title of the picture");
```

```java
loadPicture(context,
        "http://ribot.co.uk/images/sexyjoe.jpg",
        mImageViewProfilePicture,
        clickListener,
        "Title of the picture");
```
