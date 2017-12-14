## IRL ROS C++ Style Guide

In general, follow [ROS C++ Style Guide](http://wiki.ros.org/CppStyleGuide) and [Google's C++ Style Guide](https://google.github.io/styleguide/cppguide.html) but some minor adjustments and extras. 

Only the main points are extracted from the [ROS C++ Style Guide](http://wiki.ros.org/CppStyleGuide). For more information on how to conform code for areas like inheritance, exceptions, enumerations, etc. please visit their style guide website.

Main differences from this style guide and theirs:
  * 1.5 Functions / Methods

## 1 Naming

  * **CamelCased**: The name starts with a capital letter, and has a capital letter for each new word, with no underscores.
  * **camelCased**: Like CamelCase, but with a lower-case first letter.
  * **under_scored**: The name uses only lower-case letters, with words separated by underscores.
  * **ALL_CAPS**: All capital letters, with words separated by underscores.

  ### 1.1 ROS Packages

  ROS packages are **under_scored**.

  ### 1.2 ROS Topics / Services

  ROS topics and services are **under_scored**

  ### 1.3 Files

  All files are **under_scored**.

  Source files have the extension **.cpp**.

  Header files have the extension **.h**.

  Be descriptive. *Example*: instead of `laser.cpp` use `hokuyo_topurg_laser.cpp`.

  If the file primarily implements a class, name the file after the class. *Example*: the class `ActionServer` would live in the file `action_server.h`.

  ### 1.4 Classes / Types

  The names of all types -- classes, structs, type aliases, enums, and type template parameters -- are **CamelCased**. Normally **nouns**.

  <img src="http://icons.iconarchive.com/icons/paomedia/small-n-flat/1024/star-icon.png" width="15" height="15"> Name the class after what it is. If you can't think of what it is, perhaps you have not thought through the design well enough.

  <img src="http://icons.iconarchive.com/icons/paomedia/small-n-flat/1024/star-icon.png" width="15" height="15"> Compound names of over three words are a clue that your design may be unnecessarily confusing.

  *Example*:
  ```
  // classes & structs
  class ExampleClass
  class HokuyoURGLaser
  struct HokuyoURGLaserProperties

  // typedefs (equivalent to aliases)
  typedef hash_map<HokuyoURGLaserProperties *, string> LaserPropMap;
  typedef hash_map<HokuyoURGLaserProperties *, string> LaserPropertiesMap;

  // aliases (equivalent to typedef)
  using LaserPropMap = <HokuyoURGLaserProperties *, string>;
  using LaserPropertiesMap = <HokuyoURGLaserProperties *, string>;

  // enums
  enum HokuyoURGLaserErrors { ...
  ```  

  See also: [Google's Type Names](https://google.github.io/styleguide/cppguide.html#Type_Names)

  ### 1.5 Function / Methods

  Functions and class method names are **camelCased** and arguments/parameters start with a leading **_underscore**. Normally **verbs**.

  *Example*: `void exampleMethod(int _example_arg);` or `void exampleMethod(int _exampleArg)`

  Functions and methods normally perform an action, so their name should be clear on what they do. Classes as nouns & methods as verbs, as well as following other conventions, programs can be read more naturally.

  *Example*:

  ```
  checkForErrors();  ## Good
  checkErrors();  ## Bad

  dumpDataToFile();  ## Good
  dataFile();  ## Bad
  ```

    ### 1.5.1 Parameter Ordering

    Order is _**inputs then outputs**_. Do not add new parameters to the end of the function just because they are new, place new input parameters before the output parameters. If an input parameter value does not change, place `const` in front.

    _Example_: `void someMethod(const int _input, int _output);`

    (Normally in C++, inputs are references and outputs are pointers. _Ex_: `void someMethod(const int &_input, int *_output);`).

    See also: [Google's Parameter Ordering](https://google.github.io/styleguide/cppguide.html#Function_Parameter_Ordering)

  ### 1.6 Variables

  Variable names are **under_scored**.

  Be reasonably descriptive and try not to be cryptic.

  **_Integral iterator variables_** can be short, such as **i**, **j**, **k**. For consistency, **i** should be outer loop, **j** next inner loop, etc.

  **_STL iterator variables_** should have '_iter' on the end and indicate what they're iterating over, _example_:

  ```
  std::list<int> pid_list;
  std::list<int>::iterator pid_iter;
  ```

  Alternatively, an STL iterator can indicate the type of element that i can point at, _example_:

  ```
  std::list<int> pid_list;
  std::list<int>::iterator int_iter;
  ```

    ### 1.6.1 Constants

    All constants should be in **ALL_CAPS**.

    For global constants, **ALL_CAPS**

    ### 1.6.2 Member variables

    Variables that are members of a class (sometimes called fields) are **under_scored**, with a trailing underscore added.

    _Example_:

    ```
    // Declaration (header file)
    int example_int_;
    ```

    #### 1.6.3 Global variables

    Global variables should almost never be used (see below for more on this). When they are used, global variables are **under_scored** with a leading **g_** added.

    _Example_:

    ```
    // I tried everything else, but I really need this global variable
    int g_shutdown
    ```

    #### 1.6.4 Pointer variables

    Pointers should be have a leading **p_** or ending **ptr**.

    _Example_:

    ```
    String *p_name;
    String *name_ptr, name, address;  ## Note: only name_ptr is a pointer
    ```

  ### 4.7 Namespaces

  Namespace names are **under_scored**.

## 5. License statements

Every source and header file must contain a license and copyright statement at the beginning of the file.

In the **ros-pkg** and **wg-ros-pkg** repositories, the **LICENSE** directory contains license templates, commented for inclusion in C/C++ code.

See [the ROS developer's guide](http://wiki.ros.org/DevelopersGuide) for information on permissible licenses and licensing strategy.

<img src="http://icons.iconarchive.com/icons/paomedia/small-n-flat/1024/star-icon.png" width="15" height="15"> WVU IRL uses [BSD](https://opensource.org/licenses/BSD-3-Clause) license.

## 6. Formatting

Your editor should handle most formating tasks. See [EditorHelp](http://wiki.ros.org/EditorHelp) for example editor configuration files.

Indent each block by 2 spaces. Never insert literal tab characters.

The contents of a namespace are not indented.

Braces, both open and close go on their own lines.

_Example_:

```
if (a < b)
{
  // do stuff
}
else
{
  // do more stuff
}
```

Braces can be ommitted if the enclosed block is a single-line statement, _example_:

```
if (a < b
  x = 2 * a;
```

Always include the braces if the enclosed block is more complex, _example_:

```
if (a < b)
{
  for (int i = 0; i < 10; ++i)
    printItem(i);
}
```

Larger example:

```
 #include <math.h>

 class Point
 {
   public:
    Point(double _xc, double _yc) :
          x_(_xc), y_(_yc)
    {
    }
    /*
     * The above constructor is equivalent to
     * Point(double _xc, double _yc)
     * {
     *    x_ = _xc;
     *    y_ = _yc;
     * }
     */

     double Point::distance(const Point& _other) const;
     int compareX(const Point& _other) const;
     double x_;
     double y_;
 };

  double Point::distance(const Point& _other) const
  {
   double dx = x_ - _other.x_;
   double dy = y_ - _other.y_;
   return sqrt(dx * dx + dy * dy);
  }

  int Point::compareX(const Point& _other) const
  {
  if (x_ < _other.x_)
  {
   return -1;
  }
  else if (x_ > _other.x_)
  {
   return 1;
  }
  else
  {
   return 0;
  }
  }

  namespace foo
  {
  int foo(int _bar) const
  {
   switch (_bar)
   {
     case 0:
       ++_bar;
       break;
     case 1:
       --_bar;
     default:
     {
       _bar += _bar;
       break;
     }
   }
  }
  } // end namespace foo

```

  ### 6.1 Line Length

  Maximum line length is 120 characters.

  ## 6.2 #ifndef gaurds

  All headers must be protected against multiple inclusion by #ifndef guards, e.g.:

  ```
  #ifndef PACKAGE_PATH_FILE_H
  #define PACKAGE_PATH_FILE_H
  ...
  #endif
  ```

  This guard should begin immediately after the license statement, before any code, and should end at the end of the file.

## 7. Documentation

Code must be documented. Undocumented code, however functional it may be, cannot be maintained.

We use [doxygen](http://www.doxygen.org/) to auto-document our code. Doxygen parses your code, extracting documentation from specially formatted comment blocks that appear next to functions, variables, classes, etc. Doxygen can also be used to build more narrative, free-form documentation.

All functions, methods, classes, class variables, enumerations, and constants should be documented. Even a single comment above the class, method, etc stating it's purpose will suffice.

## 8. Console outputs

Avoid printf and friends (e.g., cout). Instead, use [rosconsole](http://wiki.ros.org/rosconsole) for all your outputting needs. It offers macros with both printf- and stream-style arguments. Just like printf, rosconsole output goes to screen. Unlike printf, rosconsole output is:

  * color-coded
  * controlled by verbosity level and configuration file
  * published on **/rosout**, and thus viewable by anyone on the network
  * optionally logged to disk

