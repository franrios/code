## Android Studio Coding Style


## Table of Contents

- [Nomenclature](#nomenclature)
  + [Packages](#packages)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Variables & Parameters](#variables--parameters)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Access Level Modifiers](#access-level-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Enum Classes](#enum-classes)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Getters & Setters](#getters--setters)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Annotations](#annotations)
- [XML Guidance](#xml-guidance)
  + [XML File Names](#xml-file-names)
  + [Indentation](#indentation-1)
  + [Use Context-Specific XML Files](#use-context-specific-xml-files)
  + [XML Attribute Ordering](#xml-attribute-ordering)
- [Language](#language)
- [Copyright Statement](#copyright-statement)
- [Smiley Face](#smiley-face)
- [Credit](#credits)


## Nomenclature

On the whole, naming should follow Java standards.

### Packages

Package names are all __lower-case__, multiple words concatenated together,
without
hypens or underscores:

__BAD__:

```java
com.pumpup.funky_widget
```

__GOOD__:

```java
com.pumpup.funkywidget
```

### Classes & Interfaces

Written in __UpperCamelCase__. For example `RadialSlider`. 

### Methods

Written in __lowerCamelCase__. For example `setValue`.

### Fields

Written in __lowerCamelCase__.

Static & constant fields should be written in __uppercase__, with an underscore separating
words:

```java
public static final int THE_ANSWER = 42;
```

Private member variables start with _ (do not put private beside it)
Public member variables start with a letter.
Singletons should be all caps: SINGLETON
Protected member variables will should be treated like privates

Variables with the same type should be grouped. A single return will seperate different types.

Public static variables first, then public, then protected, then private

For example:

```java
public class MyClass 
{
  public static final int SOME_CONSTANT = 42;
  public static final int SOME_OTHER_CONSTANT = 42;

  public int publicField;
  
  private static MyClass SINGLETON;
  
  protected int _protected;
  
  private int _private;
  private int _anotherPrivate;
  
  private string _privateString;
}
```

### Variables & Parameters

Written in __lowerCamelCase__.

Single character values to be avoided except for temporary looping variables.

### Logging

Use `System.out.println` instead of `Log.d()` or `Log.v()`


### Misc

In code, acronyms should be treated as words. For example:

__BAD:__

```java
XMLHTTPRequest
String URL
findPostByID
```
__GOOD:__

```java
XmlHttpRequest
String url
findPostById
```



## Declarations

### Section Comments

Use `//region Name` and `//endregion`

__GOOD__:

```java

//region ButtonAnimations
    /**
     * Need to get the buttons added after fragment animation is done otherwise they appear behind
     */
    public void showSelectionButtons()
    {
        if(_photoSelectIsOpen)
        {
            return;
        }

        _photoSelectIsOpen = true;

        _root.addView(_cancelSelectPhotoButton);
        _root.addView(_confirmSelectPhotoButton);
    }
//endregion

```

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and
member variables.

### Fields & Variables

Prefer single declaration per line.

__BAD:__

```java
String username, twitterHandle;
```

__GOOD:__

```java
String username;
String twitterHandle;
```

### Classes

Exactly one class per source file, although inner classes are encouraged where
scoping appropriate.


### Enum Classes

Enum classes should be avoided where possible, due to a large memory overhead.
Static constants are preferred. See http://developer.android.com/training/articles/memory.html#Overhead
for further details.

Enum classes without methods may be formatted without line-breaks, as follows:

```java
private enum CompassDirection { EAST, NORTH, WEST, SOUTH }
```

## Spacing

Spacing is especially important as code needs to be
easily readable as part of the tutorial. Java does not lend itself well to this.

### Method Spacing

Put 1 return line between methods

__BAD__
```java
    /**
    *Description
    */
    public void updateEditImage(int editImagePosition, Uri uri)
    {
        System.out.println("Setting image at " + editImagePosition + " to this file path " + uri.getPath());
        _editPhotoFragment.addImageFromLibrary(uri);
    }
    /**
     * Adds the select photo fragment to the screen
     */
    public void openSelectPhoto()
    {
      //...
    }
```

__GOOD__
```java
    /**
    *Description
    */
    public void updateEditImage(int editImagePosition, Uri uri)
    {
        System.out.println("Setting image at " + editImagePosition + " to this file path " + uri.getPath());
        _editPhotoFragment.addImageFromLibrary(uri);
    }
    
    /**
     * Adds the select photo fragment to the screen
     */
    public void openSelectPhoto()
    {
      //...
    }
```

### Many parameter spacing

If you have a lot of method parameters then they should start on a new line, and be 1 tab inset from the start of the caller. If you have an operator, it should be 1 space in front of the params. The params should all be flush.

__GOOD__:
```java
        final Handler handler = new Handler();
        handler.postDelayed(
          new Runnable()
          {
              @Override
              public void run()
              {
                  _root.setSystemUiVisibility(
                        View.SYSTEM_UI_FLAG_FULLSCREEN
                      | View.SYSTEM_UI_FLAG_IMMERSIVE_STICKY
                      | View.SYSTEM_UI_FLAG_HIDE_NAVIGATION
                      | View.SYSTEM_UI_FLAG_FULLSCREEN
                      | View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN
                      | View.SYSTEM_UI_FLAG_LAYOUT_STABLE);
              }
          }, 6000
        );
```

__BAD__:
```java
final Handler handler = new Handler();
        handler.postDelayed(new Runnable()
        {
            @Override
            public void run() 
            {
                _root.setSystemUiVisibility(View.SYSTEM_UI_FLAG_FULLSCREEN| View.SYSTEM_UI_FLAG_IMMERSIVE_STICKY| View.SYSTEM_UI_FLAG_HIDE_NAVIGATION,| View.SYSTEM_UI_FLAG_FULLSCREEN | View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN | View.SYSTEM_UI_FLAG_LAYOUT_STABLE);
            }
        }, 6000);
```

### Indentation

Indentation is using spaces - never tabs.

#### Blocks

Indentation for blocks uses 4 spaces:

__GOOD:__

```java
for (int i = 0; i < 10; i++) 
{
    Log.i(TAG, "index=" + i);
}
```

__BAD:__

```java
for (int i = 0; i < 10; i++) 
{
  Log.i(TAG, "index=" + i);
}
```

#### Line Wraps

Indentation for line wraps should use 4 spaces (not the default 8):

__BAD:__

```java
CoolUiWidget widget =
        someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

__GOOD:__

```java
CoolUiWidget widget =
    someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

### Line Length

Lines should be no longer than 100 characters long.


### Vertical Spacing

There should be exactly one blank line between methods to aid in visual clarity 
and organization. Whitespace within methods should separate functionality, but 
having too many sections in a method often means you should refactor into
several methods. 


### Implementation Spacing

If the lines are related to the same task, don't space. If there is a significant difference in the purpose of two lines, add a return. Use your best judgement here. Here is an example

```java
    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);

        //This is required for twitter4j otherwise there is a thread network error
        StrictMode.ThreadPolicy policy = new StrictMode.ThreadPolicy.Builder().permitAll().build();
        StrictMode.setThreadPolicy(policy);

        _root = new RelativeLayout(this);
        _root.setPadding(0, 0, 0, 0);
        _root.setBackgroundColor(Color.BLACK);
        
        if (Build.VERSION.SDK_INT < Build.VERSION_CODES.JELLY_BEAN_MR1) 
        {
          _root.setId(IDGenerator.generateViewId());
        } else 
        {
            _root.setId(View.generateViewId());
        }
        
        setContentView(_root);

        FragmentManager fragmentManager = getFragmentManager();
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
        _editPhotoFragment = F_EditPhoto.newInstance();
        _selectPhotoFragment = new F_SelectPhoto();
        fragmentTransaction.add(_root.getId(), _editPhotoFragment);
        fragmentTransaction.commit();

        //Create buttons for select photo and callback
        int buttonDimension =(int) (0.1* ViewHelper.screenWidthPX(this));
        int offset = (int)(0.02* ViewHelper.screenWidthPX(this));

        _cancelSelectPhotoButton = new ImageButton(this);
        _cancelSelectPhotoButton.setAdjustViewBounds(true);
        _cancelSelectPhotoButton.setBackgroundColor(Color.TRANSPARENT);
        _cancelSelectPhotoButton.setImageResource(R.drawable.deselecticon);
        _cancelSelectPhotoButton.setPadding(0, 0, 0, 0);//Without this the image spits outside the box, SO WEIRD
        _cancelSelectPhotoButton.setScaleType(ImageView.ScaleType.FIT_XY);
        _cancelSelectPhotoButton.setMinimumHeight(buttonDimension);
        _cancelSelectPhotoButton.setMaxHeight(buttonDimension);
        _cancelSelectPhotoButton.setMinimumWidth(buttonDimension);
        _cancelSelectPhotoButton.setMaxWidth(buttonDimension);
        _cancelSelectPhotoButton.setOnClickListener(
            new View.OnClickListener() 
            {
                @Override
                public void onClick(View v) 
                {
                    removeAllSelectionsAndClose();
                }
            }
        );
        _cancelSelectPhotoButton.setX(offset);
        _cancelSelectPhotoButton.setY(ViewHelper.screenHeightPX(this) - buttonDimension - offset);


        _confirmSelectPhotoButton = new ImageButton(this);
        _confirmSelectPhotoButton.setAdjustViewBounds(true);
        _confirmSelectPhotoButton.setImageResource(R.drawable.selectimageicon);
        _confirmSelectPhotoButton.setBackgroundColor(Color.TRANSPARENT);
        _confirmSelectPhotoButton.setMinimumHeight(buttonDimension);
        _confirmSelectPhotoButton.setMaxHeight(buttonDimension);
        _confirmSelectPhotoButton.setMinimumWidth(buttonDimension);
        _confirmSelectPhotoButton.setMaxWidth(buttonDimension);
        _confirmSelectPhotoButton.setOnClickListener(
            new View.OnClickListener() 
            {
                @Override
                public void onClick(View v) 
                {
                    beginCloseSelectPhoto();
                }
            }
        );
        _confirmSelectPhotoButton.setPadding(0, 0, 0, 0);
        _confirmSelectPhotoButton.setScaleType(ImageView.ScaleType.FIT_XY);
        _confirmSelectPhotoButton.setX(ViewHelper.screenWidthPX(this) - buttonDimension - offset);
        _confirmSelectPhotoButton.setY(ViewHelper.screenHeightPX(this) - buttonDimension - offset);

        _photoSelectIsOpen = false;
    }
```

## Getters & Setters

For external access to fields in classes, getters and setters are preferred to
direct access of the fields. Fields should rarely be `public`.

However, it is encouraged to use the field directly when accessing internally
(i.e. from inside the class). This is a performance optimization recommended
by Google: http://developer.android.com/training/articles/perf-tips.html#GettersSetters

## Brace Style

Put braces on new lines:

__GOOD:__

```java
class MyClass
{
  void doSomething()
  {
    if (someTest)
    {
      // ...
    }
    else
    {
      // ...
    }
  }
}
```

__BAD:__

```java
class MyClass {
  void doSomething() {
    if (someTest) {
      // ...
    } else {
      // ...
    }
  }
}
```

For complicated function params (like callbacks) the closing brace should be inline with the start of the method name:

```java
_cancelSelectPhotoButton.setOnClickListener(
    new View.OnClickListener() 
    {
       @Override
       public void onClick(View v) 
       {
          removeAllSelectionsAndClose();
       }
    }
);
```

Conditional statements are always required to be enclosed with braces,
irrespective of the number of lines required.

__BAD:__

```java
if (someTest)
  doSomething();
if (someTest) doSomethingElse();
```

__GOOD:__

```java
if (someTest) 
{
  doSomething();
}
if (someTest) 
{ 
  doSomethingElse(); 
}
```


## Switch Statements

Switch statements fall-through by default, but this can be unintuitive. If you
require this behavior, comment it.

Alway include the `default` case.

__BAD:__

```java
switch (anInput) 
{
  case 1:
    doSomethingForCaseOne();
  case 2:
    doSomethingForCaseOneOrTwo();
    break;
  case 3:
    doSomethingForCaseOneOrThree();
    break;
}
```

__GOOD:__

```java
switch (anInput) 
{
  case 1:
    doSomethingForCaseOne();
    // fall through
  case 2:
    doSomethingForCaseOneOrTwo();
    break;
  case 3:
    doSomethingForCaseOneOrThree();
    break;
  default:
    break;
}
```

## Annotations

Standard annotations should be used - in particular `@Override`. This should
appear the line before the function declaration.

__BAD:__

```java
protected void onCreate(Bundle savedInstanceState) 
{
  super.onCreate(savedInstanceState);
}
```

__GOOD:__

```java
@Override
protected void onCreate(Bundle savedInstanceState) 
{
  super.onCreate(savedInstanceState);
}
```


## XML Guidance

Since Android uses XML extensively in addition to Java, we have some rules
specific to XML.

### XML File Names

View-based XML files should be prefixed with the type of view that they
represent.

__GOOD:__

- `activity_login.xml`
- `fragment_main_screen.xml`
- `button_rounded_edges.xml`

__BAD:__

- `login.xml`
- `main_screen.xml`
- `rounded_edges_button.xml`

### Indentation

Similarly to Java, indentation should be __two characters__.

### Use Context-Specific XML Files

Wherever possible XML resource files should be used:

- Strings => `res/values/strings.xml`
- Styles => `res/values/styles.xml`
- Colors => `res/color/colors.xml`
- Animations => `res/anim/`
- Drawable => `res/drawable`


### XML Attribute Ordering

Where appropriate, XML attributes should appear in the following order:

- `id` attribute
- `layout_*` attributes
- style attributes such as `gravity` or `textColor`
- value attributes such as `text` or `src`

Within each of these groups, the attributes should be ordered alphabetically.


## Language

Use US English spelling.

__BAD:__

```java
String colour = "red";
```

__GOOD:__

```java
String color = "red";
```
