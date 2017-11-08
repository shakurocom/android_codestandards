# Android guideline common for Java and Kotlin

This is a common section for Java and Kotlin android projects. Please refer to [Java guideline](https://github.com/shakurocom/android_codestandards/blob/master/java/README.md) and [Kotlin guideline](https://github.com/shakurocom/android_codestandards/blob/master/kotlin/README.md) for more details.

## Project structure
The project should follow standard [Android project guidelines](https://developer.android.com/studio/projects/index.html)
however in short:
```
root/
  └─ app/
  └─ gradle/
  └─ lib/
  └─ miscFiles.txt
```

## Applications packages structure

The root structure should follow [clean architecture](https://github.com/AndroidArchitecture/AndroidArchitectureBook/blob/master/Intro.md) approach with separation of layers.

```
app
├─ di
│  ├─ payments
│  └─ operation
├─ presentation
│  ├─ view
│  │  ├─ payments
│  │  │  ├─ PaymentsView
│  │  │  └─ PaymentsFragment
│  │  └─ operations
│  │     ├─ OperationsView
│  │     └─ OperationsFragment
│  └─ presenter
│     ├─ payments
│     │  └─ PaymantsPresenter
│     └─ operations
│        └─ OperationsPresenter
├─ domain (business logic)
│  ├─ payments
│  │  ├─ PaymentsInteractor
│  │  ├─ PaymentsInteractorImpl
│  │  └─ CurrencyHandler (helper class for PaymentsInteractor)
│  └─ operations
│     ├─ OperationsInteractor
│     ├─ rubs
│     │  ├─ OperationsInteractorRubs
│     │  └─ RubsManager (helper class for OperationsInteractorRubs)
│     └─ currency
│        ├─ OperationsInteractorCurr
│        └─ CurrencyManager (helper class for OperationsInteractorCurr)
├─ repositories
│  ├─ payments
│  │  ├─ PaymentsRepository
│  │  └─ PaymentsRepositoryImpl
│  └─ operations
│     ├─ OperationsRepository
│     └─ OperationsRepositoryImpl
├─ data
│  ├─ network
│  └─ db
└─ models (dto descriptions)
   ├─ payments
   │  ├─ PaymentsModel
   └─ operations
      ├─ presentation
      │  └─ OperationUIModel
      ├─ domain
      │  ├─ OperationsRubModel
      │  └─ OperationCurrModel
      └─ data
         ├─ OperationsRubNetworkModel
         └─ OperationCurrNetworkModel
```

Structure above is not mandatory, for example you could combine layers by features. 

```
├─ presentation
│  ├─ payments
│  │  ├─ PaymentsView
│  │  ├─ PaymentsFragment
│  │  └─ PaymantsPresenter
│  └─ operations
│     ├─ OperationsView
│     ├─ OperationsFragment
│     └─ OperationsPresenter
```

You can refer to [SkyLocker project](https://github.com/kengura/SkyLocker) as example.

## File naming

### Class files
Class names should be written in [UpperCamelCase](http://en.wikipedia.org/wiki/CamelCase).

For classes that extend an Android component, the name of the class should end with the name of the component; for example:
* `SignInActivity`
* `SignInFragment`
* `ImageUploaderService`
* `ChangePasswordDialog`

### Resources files

Resources file names are written in __lowercase_underscore__. e.g.
* `ic_launcher`
* `background_default`

#### Drawables

##### Icons
Icons should follow the naming scheme seen in [Material Icons](https://github.com/google/material-design-icons/) which
follows the format `ic_<Name>_<Color>_<Size>`; the exception being launcher images which should be named `ic_launcher`.
For example:

* `ic_link_black_24dp.xml`
* `ic_user_white_48dp.xml`


##### Selector States
Assuming a selector state requires an image instead of an embedded shape, each images should be
named based on the main selector (`button_order` in the example) with the states as a suffix. e.g.

| State	       | Suffix       | Example                     |
|--------------|--------------|-----------------------------|
| Normal       | `_normal`    | `button_order_normal.9.png`    |
| Pressed      | `_pressed`   | `button_order_pressed.9.png`   |
| Focused      | `_focused`   | `button_order_focused.9.png`   |
| Disabled     | `_disabled`  | `button_order_disabled.9.png`  |
| Selected     | `_selected`  | `button_order_selected.9.png`  |


#### Layout files
Layout file names should be prefixed with the section the source code will be used by _without_ prefixing
the Android component name. e.g.

| Component        | Class Name             | Layout Name           |
| ---------------- | ---------------------- | --------------------- |
| Activity         | `LoginActivity`        | `login.xml`           |
| Fragment         | `SignUpFragment`       | `sign_up.xml`         |
| Dialog           | `ChangePasswordDialog` | `change_password.xml` |
| AdapterView item | `PersonViewHolder`     | `person.xml`          |


#### Menu files
Menu file names should match the parent layout naming, they should _not_ include `menu` as they are already
separated by the `R.menu.*` reference. e.g.

| Parent Layout      | Menu Name      |
| ------------------ | -------------- |
| `user_profile.xml` | `user_profile` |
| `person.xml`       | `person`       |


## XML rules

### Indentation
Similarly to Java and Kotlin rules, indentation should be **4 characters**.

### Prefer self closing tags
When possible self closing tags should be used. e.g.

```xml
<TextView
	android:id="@+id/profileTextView"
	android:layout_width="wrap_content"
	android:layout_height="wrap_content" />
```

**Not**
```xml
<TextView
    android:id="@+id/profileTextView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" >
</TextView>
```

### Resource naming
Resources should follow __lowercase_underscore__ naming, the exception being Ids, Styles and Themes (described below)

#### IDs
IDs should have a suffix indicating the element or category type in  [LowerCamelCase](http://en.wikipedia.org/wiki/CamelCase). e.g.

| Element              | Suffix              |
| -------------------- | ------------------- |
| `TextView`           | `someTextView`      |
| `ImageView`          | `anImageView`       |
| `Button`             | `helpButton`        |   
| `Menu Item`          | `loginMenuItem`     |
| `Action Mode Menu`   | `artistActionMenu`  |
| `Context Menu`       | `personContextMenu` |


#### Strings
String names start with a prefix that identifies the section they belong to. For example `registration_email_hint`
 or `registration_name_hint`. If a string __doesn't belong__ to any section then a simple name should be used. e.g.

| Name                    | Value                                   |
| ----------------------- | --------------------------------------- |
| `done`                  | `Done`                                  |
| `general_network_error` | `There was an unknown network error`    |


#### Styles and Themes
Unlike the rest of resources, style names are written in [UpperCamelCase](http://en.wikipedia.org/wiki/CamelCase).

### Attribute ordering
Attributes should follow the auto ordering that Android Studio enforces; in general this is

1. `id`
2. `style` and `theme`
3. `layout_width`, `layout_height`, and `layout_weight`
4. Other attributes sorted alphabetically
5. Non-`android` namespace items (e.g. `app`) sorted alphabetically
6. `tools` namespace items sorted alphabetically

