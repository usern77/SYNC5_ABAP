<a name="top"></a>

# ABAP Object Orientation

- [ABAP Object Orientation](#abap-object-orientation)
  - [Classes and Objects](#classes-and-objects)
    - [Creating Classes](#creating-classes)
      - [Creating a Global Class](#creating-a-global-class)
      - [Creating a Local Class](#creating-a-local-class)
      - [Excursion: Class Pool and Include Programs](#excursion-class-pool-and-include-programs)
    - [Visibility of Components](#visibility-of-components)
      - [Creating the Visibility Sections](#creating-the-visibility-sections)
    - [Defining Components](#defining-components)
      - [Class Attributes](#class-attributes)
      - [Methods](#methods)
      - [Parameter Interface](#parameter-interface)
      - [Formal and Actual Parameters](#formal-and-actual-parameters)
      - [Complete Typing of Formal Parameters](#complete-typing-of-formal-parameters)
      - [Generic Typing of Formal Parameters](#generic-typing-of-formal-parameters)
      - [Defining Parameters as Optional](#defining-parameters-as-optional)
      - [Defining Input Parameters as Preferred](#defining-input-parameters-as-preferred)
      - [Constructors](#constructors)
  - [Working with Objects and Components](#working-with-objects-and-components)
    - [Declaring Object Reference Variables](#declaring-object-reference-variables)
    - [Creating Objects](#creating-objects)
    - [Working with Reference Variables](#working-with-reference-variables)
    - [Accessing Attributes](#accessing-attributes)
    - [Calling Methods](#calling-methods)
      - [Excursion: Inline Declarations, Returning Parameters](#excursion-inline-declarations-returning-parameters)
    - [Self-Reference me](#self-reference-me)
    - [Method Chaining and Chained Attribute Access](#method-chaining-and-chained-attribute-access)
    - [Excursion: Example Class](#excursion-example-class)
  - [Inheritance](#inheritance)
    - [Inheritance-Related Syntax](#inheritance-related-syntax)
    - [Excursion: Inheritance Example](#excursion-inheritance-example)
  - [Polymorphism and Casting (Upcast/Downcast)](#polymorphism-and-casting-upcastdowncast)
    - [Demonstrating Upcasts and Downcasts Using the RTTS Inheritance Tree](#demonstrating-upcasts-and-downcasts-using-the-rtts-inheritance-tree)
  - [Interfaces](#interfaces)
    - [Defining Interfaces](#defining-interfaces)
    - [Implementing Interfaces](#implementing-interfaces)
    - [Interface Reference Variables and Accessing Objects](#interface-reference-variables-and-accessing-objects)
    - [Excursion: Example Interface](#excursion-example-interface)
  - [Excursions](#excursions)
    - [Friendship](#friendship)
      - [Friendship between Global and Local Classes](#friendship-between-global-and-local-classes)
    - [Events](#events)
    - [Examples for Design Patterns: Factory Methods and Singletons](#examples-for-design-patterns-factory-methods-and-singletons)
    - [Class-Based Exceptions](#class-based-exceptions)
    - [ABAP Unit Tests](#abap-unit-tests)
    - [ABAP Doc Comments](#abap-doc-comments)
  - [More Information](#more-information)
  - [Executable Examples](#executable-examples)

> **💡 Note**<br>
> - This ABAP cheat sheet provides an overview on selected syntax options and concepts related to ABAP object orientation. It is supported by code snippets and an executable example. They are **not** suitable as role models for object-oriented design. Their primary focus is on the syntax and functionality. For more details, refer to the respective topics in the ABAP Keyword Documentation. Find an overview in the topic [ABAP Objects - Overview](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenabap_objects_oview.htm).
> - The [executable examples](#executable-examples) reflect several points and code snippets covered in the cheat sheet.


## Classes and Objects

Object-oriented programming in ABAP means dealing with
[classes](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenclass_glosry.htm "Glossary Entry")
and
[objects](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenobject_glosry.htm "Glossary Entry").

Objects ...

-   are
    [instances](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninstance_glosry.htm "Glossary Entry")
    of a
    [type](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abentype_glosry.htm "Glossary Entry").
    In this context, they are instances of a
    [class](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenclass_glosry.htm "Glossary Entry").
    The terms *object* and *instance* are used synonymously.
-   exist in the [internal
    session](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninternal_session_glosry.htm "Glossary Entry")
    of an [ABAP
    program](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenabap_program_glosry.htm "Glossary Entry").


Classes ...
-   are templates for objects, i. e. they determine how
    all instances of a class are set up. All instances are created (i.e they are [instantiated](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninstantiation_glosry.htm "Glossary Entry")) based on this template and, thus, have the same setup.
    -   To give an example: If, for example, a vehicle represents a class, then the
        instances of the class `vehicle` have the same setup.
        That means they all share the same kind of components like a brand, model and color or the same functionality like the acceleration or braking distance.
        However, the values of these components are different from instance to instance. For example, one
        instance is a red sedan of brand A having a certain
        acceleration; another instance is a black SUV of brand B and so on. You can create an object (or instance respectively) that stands
        for an actual vehicle with which you can work with. You might create any number of objects that are based on such a class - if instantiation is allowed.
-   contain
    [components](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abencomponent_glosry.htm "Glossary Entry"):
    -   [Attributes](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenattribute_glosry.htm "Glossary Entry")
        of the objects (the data object declarations)
    -   [Methods](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenmethod_glosry.htm "Glossary Entry")
        that determine the behavior of an object
    -   [Events](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenevent_glosry.htm "Glossary Entry") to trigger the processing of ABAP code


<p align="right"><a href="#top">⬆️ back to top</a></p>

### Creating Classes

You can either create local or global classes:

<table>
<tr>
    <td><a href="https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenlocal_class_glosry.htm">Local classes</a></td>
    <td><ul><li>can be defined within an <a href="[https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenlocal_class_glosry.htm](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenabap_program_glosry.htm)">ABAP program</a> such as in the <a href="https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenccimp_glosry.htm">CCIMP include</a> of global classes (Local Types tab in ADT) or in executable programs ("reports"; in <a href="https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenstandard_abap_glosry.htm">Standard ABAP</a> only)</li><li>can only be used in the ABAP program in which the class is defined</li></ul></td>
</tr>
<tr>
    <td><a href="https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenglobal_class_glosry.htm">Global
classes</a></td>
    <td><ul><li>are defined as
    <a href="https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenglobal_type_glosry.htm">global types</a>, i. e. they are visible as a repository object - in contrast to local classes. As a global type, they can be used - as the name implies - globally in other ABAP programs or global classes</li><li>are declared in <a href="https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenclass_pool_glosry.htm">class pools</a> that contain a <a href="https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenccimp_glosry.htm">CCIMP include</a> and other <a href="https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninclude_program_glosry.htm">include programs</a></li></ul> </td>
</tr>
</table>

> **💡 Note**<br>
> - If a class is only used in one ABAP program, creating a local class is enough. However, if you choose to create a global class, you must bear in mind that such a class can be used everywhere. Consider the impact on the users of the global class when you change, for example, the visibility section of a component or you delete it.
> - Apart from ADT, global classes can also be created in the ABAP Workbench (`SE80`) or with transaction `SE24` in [classic ABAP](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenclassic_abap_glosry.htm).

Basic structure of classes:
- [Declaration part](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abendeclaration_part_glosry.htm "Glossary Entry") that includes declarations of the class components.
- [Implementation part](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenimplementation_part_glosry.htm "Glossary Entry") that includes method implementations.
- Both are introduced by `CLASS` and ended by `ENDCLASS`.

#### Creating a Global Class
The code snippet shows a basic skeleton of a global class. There are [further
additions](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapclass_options.htm)
possible for the declaration part.

``` abap
"Declaration part
CLASS global_class DEFINITION
  PUBLIC                       "Makes the class a global class in the class library.
  FINAL                        "Means that no subclasses can be derived from this class.
  CREATE PUBLIC.               "This class can be instantiated anywhere it is visible.

    ... "Here go the declarations for all components and visibility sections.

ENDCLASS.

"Implementation part
CLASS global_class IMPLEMENTATION.

    ... "Here go the method implementations.
        "Only required if you declare methods in the DEFINITION part.

ENDCLASS.
```
> **💡 Note**<br>
> - The code snippet above shows the syntax to create a global class (indicated by `PUBLIC`), that is instantiable everywhere (indicated by `CREATE PUBLIC`) but that does not allow inheritance (indicated by `FINAL`, and which is covered further down).
> - There are more additions that can be specified. Find more information on the additions [here](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapclass_options.htm).
> - Examples: 
>   - `... CREATE PROTECTED.`: The class can only be instantiated in methods of its [subclasses](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abensubclass_glosry.htm "Glossary Entry"), of the class itself, and of its [friends](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenfriend_glosry.htm "Glossary Entry").
>   - `... CREATE PRIVATE.`: The class can only be instantiated in methods of the class itself or of its friends. Hence, it cannot be instantiated as an inherited component of subclasses.
>   - `... INHERITING FROM superclass ...`: As the name implies, it is used to inherit from a visible [superclass](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abensuperclass_glosry.htm). If the addition is not specified, the created class implicitly inherits from the predefined empty, abstract class `object` (the root object).
>   - `... ABSTRACT ...`: To define [abstract](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenabstract_glosry.htm) classes. These classes cannot be instantiated. Abstract methods can only be implemented in [subclasses](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abensubclass_glosry.htm).
>   - `... [GLOBAL] FRIENDS class ...`: Used to define [friendships](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenfriend_glosry.htm) (also possible for interfaces). Friends of a class have unrestricted access to all components of that class. The `GLOBAL` addition can be used together with the `PUBLIC` addition and be specified with other global classes/interfaces following `GLOBAL FIRENDS`. Note: For local classes/interfaces, the addition [`LOCAL FRIENDS`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapclass_local_friends.htm) is available.
>   - `... FOR TESTING ...`: For [ABAP Unit](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenabap_unit_glosry.htm) tests. Find more information in the [ABAP Unit Tests](14_ABAP_Unit_Tests.md) cheat sheet.
>   - `... FOR BEHAVIOR OF ...`: To define [ABAP behavior pools](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenbehavior_pool_glosry.htm). Find more information in the [ABAP for RAP: Entity Manipulation Language (ABAP EML)](08_EML_ABAP_for_RAP.md) cheat sheet.
>   - `... DEFINITION DEFERRED.`: Making a local class known in a program before the actual class definition. It is typically used in test classes of ABAP Unit. Find more information [here](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapclass_deferred.htm).


<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Creating a Local Class

- You can create local classes, for example, in the [CCIMP include](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenccimp_glosry.htm) (*Local Types* tab in ADT) of a [class pool](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenclass_pool_glosry.htm). 
- Local classes are used in their own ABAP program. While dynamic access beyond program boundaries is possible, it is not recommended.
- The cheat sheet's focus is on global classes. Local classes are also mentioned in the [friendship](#friendship) section.

The following snippet shows the skeleton of local class declaration. 
- It does not specify any class options after `DEFINITION`. 
- The `PUBLIC` addition makes a class a global class in the class library. Not possible in the context of local classes.
- It does not specify `CREATE ...`. Note that `CREATE PUBLIC` is the default, which means that not specifying any `CREATE ...` addition makes the class implicitly specified with `CREATE PUBLIC`.

``` abap
"Declaration part
CLASS local_class DEFINITION.

    ... "Here go the declarations for all components and visibility sections.
        "You should place the declarations at the beginning of the program.

ENDCLASS.

"Implementation part
CLASS local_class IMPLEMENTATION.

    ...  "Here go the method implementations.
         "Only required if you declare methods in the declaration part.

ENDCLASS.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Excursion: Class Pool and Include Programs

- A class pool is an ABAP program containing the definition of one global class (*Global Class* tab in ADT)
- Global classes are marked as such with the `PUBLIC` addition to the `CLASS` statement: `CLASS zcl_demo_test DEFINITION PUBLIC ...` 
- Additionally, a class pool can also contain local classes that are defined in dedicated include programs (CCDEF and the other include names are internal names the include programs end with):
  - CCDEF include (*Class-relevant Local Types* tab in ADT): Is included in front of the declaration part of the global class
  - CCIMP include (*Local Types* tab in ADT): Is included behind the declaration part and in front of the implementation part of the global class
  - CCAU include (*Test classes* tab in ADT): Test include; contains ABAP Unit test classes 

The following simplified example demonstrates include programs.

<details>
   <summary>🟢 Click to expand for more details</summary>
  <!-- -->

  Global class:
- Create a new global class (the example uses the name `zcl_demo_test`) and copy and paste the following code in the *Global Class* tab in ADT.
- The method in the private section makes use of local types that are defined in the CCDEF include. In the example the method is deliberately included in the private visibility section. Having it like this in the public section is not possible due to the use of local types.
- The `if_oo_adt_classrun~main` implementation contains method calls to this method. It also contains method calls to a method implemented in a local class in the CCIMP include.
- As a prerequisite to activate the class, you also need to copy and paste the code snippets further down for the CCDEF and CCIMP include. Once you have pasted the code, the syntax errors in the global class will disappear.
- You can run the class using F9. Some output is displayed.
- When you have copied and pasted the CCAU code snippet for the simple ABAP Unit test, and activated the class, you can choose *CTRL+Shift+F10* in ADT to run the ABAP Unit test. Alternatively, you can make a right click in the class code, choose *Run As* and *4 ABAP Unit Test*.

```abap
CLASS zcl_demo_test DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.

  PROTECTED SECTION.
  PRIVATE SECTION.
    "This method uses types (data type c1 and the local exception class)
    "defined in the CCDEF include
    METHODS calculate IMPORTING num1          TYPE i
                                operator      TYPE c1
                                num2          TYPE i
                      RETURNING VALUE(result) TYPE i
                      RAISING   lcx_wrong_operator.
ENDCLASS.

CLASS zcl_demo_test IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.

    "---- The method called has formal parameters using type declarations from the CCDEF include ----
    TRY.
        DATA(result1) = calculate( num1 = 10 operator = '+' num2 = 4 ).
        out->write( data = result1 name = `result1` ).
      CATCH lcx_wrong_operator.
        out->write( `Operator not allowed` ).
    ENDTRY.

    TRY.
        DATA(result2) = calculate( num1 = 10 operator = '-' num2 = 4 ).
        out->write( data = result2 name = `result2` ).
      CATCH lcx_wrong_operator.
        out->write( `Operator not allowed` ).
    ENDTRY.

    TRY.
        DATA(result3) = calculate( num1 = 10 operator = '*' num2 = 4 ).
        out->write( data = result3 name = `result3` ).
      CATCH lcx_wrong_operator.
        out->write( `Operator not allowed` ).
    ENDTRY.

    "---- Using local class implemented in the CCIMP include ----
    DATA(hi1) = lcl_demo=>say_hello( ).
    out->write( data = hi1 name = `hi1` ).
    DATA(hi2) = lcl_demo=>say_hello( xco_cp=>sy->user( )->name ).
    out->write( data = hi2 name = `hi2` ).

    "--------------- Test include (CCAU) ---------------
    "For running the ABAP Unit test, choose CTRL+Shift+F10 in ADT.
    "Or you can make a right click in the class code, choose
    "'Run As' and '4 ABAP Unit Test'.
  ENDMETHOD.

  METHOD calculate.
    result = SWITCH #( operator
                       WHEN '+' THEN num1 + num2
                       WHEN '-' THEN num1 - num2
                       ELSE THROW lcx_wrong_operator( ) ).
  ENDMETHOD.

ENDCLASS.
```
Code snippet for the CCDEF include:
```abap
CLASS lcx_wrong_operator DEFINITION INHERITING FROM cx_static_check.
ENDCLASS.

TYPES c1 TYPE c LENGTH 1.
```

Code snippet for the CCIMP include:
```abap
CLASS lcl_demo DEFINITION.
  PUBLIC SECTION.
    CLASS-METHODS: say_hello IMPORTING name TYPE string optional
                             RETURNING VALUE(hi) type string.

ENDCLASS.

CLASS lcl_demo IMPLEMENTATION.

  METHOD say_hello.
    hi = |Hallo{ COND #( WHEN name IS SUPPLIED THEN ` ` && name ) }!|.
  ENDMETHOD.

ENDCLASS.
```

Code snippet for the test include (CCAU):
```abap
CLASS ltc_test DEFINITION DEFERRED.
CLASS zcl_demo_test DEFINITION LOCAL FRIENDS ltc_test.

CLASS ltc_test DEFINITION FOR TESTING
RISK LEVEL HARMLESS
DURATION SHORT.

  PRIVATE SECTION.
    METHODS test_calculate FOR TESTING.

ENDCLASS.

CLASS ltc_test IMPLEMENTATION.

  METHOD test_calculate.
    "Creating an object of the class under test
    DATA(ref_cut) = NEW zcl_demo_test( ).

    "Calling method that is to be tested
    TRY.
        DATA(result1) = ref_cut->calculate( num1 = 10 operator = '+' num2 = 4 ).
      CATCH lcx_wrong_operator.
    ENDTRY.

    TRY.
        DATA(result2) = ref_cut->calculate( num1 = 10 operator = '-' num2 = 4 ).
      CATCH lcx_wrong_operator.
    ENDTRY.

    "Assertions
    cl_abap_unit_assert=>assert_equals(
          act = result1
          exp = 14
          quit = if_abap_unit_constant=>quit-no ).

    cl_abap_unit_assert=>assert_equals(
          act = result2
          exp = 6
          quit = if_abap_unit_constant=>quit-no ).
  ENDMETHOD.

ENDCLASS.
```
</details>



<p align="right"><a href="#top">⬆️ back to top</a></p>

### Visibility of Components

In the class declaration part, you specify three [visibility sections](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenvisibility_section_glosry.htm "Glossary Entry") and include class components to define their visibility. These visibility sections serve the purpose of encapsulation in ABAP Objects. For example, you do not want to make certain components publicly available for all users. The visibility sections are as follows:

<table>
<tr>
  <td><pre>PUBLIC SECTION.</pre></td>
    <td>Components declared in this section can be accessed from within the class and from all users of the class.</td>
</tr>
<tr>
 <td><pre>PROTECTED SECTION.</pre></td>
    <td>Components declared in this section can be
    accessed from within the class and <a href="https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abensubclass_glosry.htm">subclasses</a> as well as <a href="https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenfriend_glosry.htm">friends</a>
     - concepts related to <a href="https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninheritance_glosry.htm">inheritance</a>.</td>
</tr>
  <tr>
 <td><pre>PRIVATE SECTION.</pre></td>
    <td>Components declared in this section can only be accessed from within the class in which they are declared and its friends.</td>
</tr>
</table>

Summary:

| Visible for  | PUBLIC SECTION  |  PROTECTED SECTION |  PRIVATE SECTION |
|---|---|---|---|
|  Same class and its friends |  X | X  |  X |
| Any subclasses	  |  X | X  | -  |
|  Any repository objects | X  |  - | -  |


#### Creating the Visibility Sections
At least one section must be specified.
``` abap
CLASS zcl_some_class DEFINITION
  PUBLIC                       
  FINAL                        
  CREATE PUBLIC.  

    PUBLIC SECTION.
      "Here go the components.
    PROTECTED SECTION.
      "Here go the components.
    PRIVATE SECTION.
      "Here go the components.
ENDCLASS.

...
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Defining Components

All components, i. e.
- attributes (using `TYPES`, `DATA`, `CLASS-DATA`, and `CONSTANTS` for data types and data
objects),
- methods (using `METHODS` and `CLASS-METHODS`),
- events (using `EVENTS` and `CLASS-EVENTS`) as well as
- interfaces,

are declared in the declaration part of the class. There, they must be
assigned to a visibility section.

Two
kinds of components are to be distinguished when, for example, looking at declarations using `DATA` and `CLASS-DATA` having a preceding `CLASS-`:

-   [Instance components](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninstance_component_glosry.htm "Glossary Entry"):
    Components that exist separately for each instance and can only be accessed in instances of a class.
-   [Static components](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenstatic_component_glosry.htm "Glossary Entry") (the declarations with `CLASS-`):
    Components that exist only once per class. They do no not exclusively exist for specific instances. They can be addressed using the name of the class.

#### Class Attributes

-   The attributes of a class (or interface) mean the data objects declared within a
    class (or interface).
-   [Instance
    attributes](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninstance_attribute_glosry.htm "Glossary Entry")
    (`DATA`): Determine the state of a objects of a class. The data
    is only valid in the context of an instance. As shown further down,
    instance attributes can only be accessed via an [object reference
    variable](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenobject_refer_variable_glosry.htm "Glossary Entry").
-   [Static
    attributes](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenstatic_attribute_glosry.htm "Glossary Entry")
    (`CLASS-DATA`): Their content is independent of instances of
    a class and, thus, valid for all instances.  That means that if you change such a static
    attribute, the change is visible in all instances. As shown further down,
    static attributes can be accessed by both using an object reference variable and using the class name without a prior creation of an instance.


> **💡 Note**<br>
> - You can declare constant data objects that should not be
changed using
[`CONSTANTS`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapconstants.htm)
statements. You specify the values for the constants (which are also static attributes) when you declare
them in the declaration part of a class.
> - The addition
[`READ-ONLY`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapdata_options.htm#!ABAP_ADDITION_2@2@)
can be used in the public visibility section. Effect:
>   - Can be read from outside of the class
>   - Cannot be changed from outside
>   - Can only be changed using methods of the class or its subclasses
> - Note that when creating attributes in the public visibility section, they are globally visible and can therefore be globally used. Note the consequences on the users when changing attributes in the public visibility section (e.g. making an attribute read-only at a later point in time when, for example, other classes use the attribute).

Declaring attributes in visibility sections. In the code snippet below, all attributes are declared in the public section.
``` abap
CLASS zcl_some_class DEFINITION
  PUBLIC                       
  FINAL                        
  CREATE PUBLIC.  

    PUBLIC SECTION.
      TYPES some_type TYPE c LENGTH 3.               "Type declaration

      DATA: inst_number TYPE i,                      "Instance attributes
            inst_string TYPE string,
            dobj_r_only TYPE c LENGTH 5 READ-ONLY.   "Read-only attribute

      CLASS-DATA: stat_number TYPE i,                "Static attributes
                  stat_char   TYPE c LENGTH 3.

      CONSTANTS const_num TYPE i VALUE 123.          "Non-changeable constant

    PROTECTED SECTION.
      "Here go more attributes if needed.

    PRIVATE SECTION.
      "Here go more attributes if needed.

ENDCLASS.

CLASS zcl_some_class IMPLEMENTATION.

      ... "Here go all method implementations.

ENDCLASS.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Methods

-   Are internal
    [procedures](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenprocedure_glosry.htm "Glossary Entry")
    determining the behavior of the class.
-   Can access all of the attributes of a class and, if not defined
    otherwise, change their content.
-   Have a [parameter
    interface](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenparameter_interface_glosry.htm "Glossary Entry")
    (also known as
    [signature](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abensignature_glosry.htm "Glossary Entry"))
    with which methods can get values to work with when being called and pass values
    back to the caller (see the notes on formal and actual parameters below).
-   [Static
    methods](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenstatic_method_glosry.htm "Glossary Entry")
    can only access static attributes of a class and trigger static
    events. You declare them using `CLASS-METHODS` statements in
    a visibility section.
-   [Instance
    methods](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninstance_method_glosry.htm "Glossary Entry")
    can access all of the attributes of a class and trigger all events.
    You declare them using `METHODS` statements in a visibility
    section. Note that you must create an instance of a class first before using instance methods.
- `CLASS-METHODS` and `METHODS` can be followed by a colon to list one or more methods, separated by commas, or without a colon to declare a single method.


The following code snippet shows (which anticipates aspects described in the following sections, such as specifying the method signature, constructors etc.) multiple method definitions in the public section of a global class. Most of the formal
parameters of the demo methods below are defined by just using the
parameter name. This means passing by reference (returning parameters
require to be passed by value).
``` abap
CLASS zcl_some_class DEFINITION
  PUBLIC                       
  FINAL                        
  CREATE PUBLIC. 

    PUBLIC SECTION.
      METHODS: inst_meth1,                                      "instance methods

               inst_meth2 IMPORTING a TYPE string,

               inst_meth3 IMPORTING b TYPE i
                          EXPORTING c TYPE i,

               inst_meth4 IMPORTING d TYPE string
                          RETURNING VALUE(e) TYPE string,

               "Note that method declarations should be done with care. An example
               "as follows may not be advisable, e.g. specifying multiple output
               "parameters (both exporting and returning parameters for a method).
               "As is valid for all examples in the cheat sheet, the focus is on
               "syntax options.
               inst_meth5 IMPORTING f TYPE i
                          EXPORTING g TYPE i
                          CHANGING  h TYPE string
                          RETURNING VALUE(i) TYPE i
                          RAISING   cx_sy_zerodivide,

              constructor IMPORTING j TYPE i.                   "instance constructor with importing parameter

      CLASS-METHODS: stat_meth1,                                "static methods  

                     stat_meth2 IMPORTING k TYPE i              
                                EXPORTING l TYPE i,

                     class_constructor,                         "static constructor

                     "Options of formal parameter definitions
                     stat_meth3 IMPORTING VALUE(m) TYPE i,       "pass by value
                     stat_meth4 IMPORTING REFERENCE(n) TYPE i,   "pass by reference
                     stat_meth5 IMPORTING o TYPE i,              "same as n; the specification of REFERENCE(...) is optional
                     stat_meth6 RETURNING VALUE(p) TYPE i,       "pass by value once more (note: it's the only option for returning parameters)

                     "OPTIONAL/DEFAULT additions
                     stat_meth7 IMPORTING q TYPE i DEFAULT 123
                                          r TYPE i OPTIONAL,

                     "The examples above use a complete type for 
                     "the parameter specification. Generic types
                     "are possible.
                     stat_meth8 IMPORTING s TYPE any           "Any data type
                                          t TYPE any table     "Any internal table type                 
                                          u TYPE clike.        "Character-like types (c, n, string, d, t and character-like flat structures)

ENDCLASS.

CLASS zcl_some_class IMPLEMENTATION.
   METHOD inst_meth1.
      ...
   ENDMETHOD.

  ... "Further method implementations. Note that all declared methods must go here.
ENDCLASS.
```



<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Parameter Interface

In the simplest form, methods can have no parameter at all. Apart from that, methods can be defined with the following parameters:

| Addition  | Details  |
|---|---|
|`IMPORTING`|Defines one or more input parameters to be imported by the method.  |
|`EXPORTING`|Defines one or more output parameters to be exported by the method.  |
|`CHANGING`|Defines one or more input or output parameters, i. e. that can be both imported and exported.  |
|`RETURNING`|For [functional methods](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenfunctional_method_glosry.htm "Glossary Entry"), i. e. such methods have only one `RETURNING` parameter that can be defined. As an output parameter like the `EXPORTING` parameter, `RETURNING` parameters pass back values (note that the formal parameters of returning parameters must be passed by value as covered below; the parameter must be [completely typed](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abencomplete_typing_glosry.htm)). In contrast to `EXPORTING` for which multiple parameters can be specified, only one `RETURNING` parameter can be specified in a method. If you only need one output parameter, you can benefit from using a `RETURNING` parameter by shortening the method call and enabling method chaining. Another big plus is that such functional methods can, for example, be used in expressions. In case of standalone method calls, the returned value can be accessed using the addition `RECEIVING`.  |
|`RAISING` | Used to declare the [class-based exceptions](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenclass_based_exception_glosry.htm "Glossary Entry") that can be propagated from the method to the caller. It can also be specified with the addition `RESUMABLE` for [resumable exceptions](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenresumable_exception_glosry.htm). Find more information in the [Exceptions and Runtime Errors](27_Exceptions.md) cheat sheet. |


> **💡 Note**<br>
> - Find more information [here](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapmethods_general.htm).
> - You may find the addition `EXCEPTIONS` especially in definitions of older classes. They are for non-class-based exceptions. This addition should not be used in ABAP for Cloud Development.

<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Formal and Actual Parameters

- [Formal parameters](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenformal_parameter_glosry.htm "Glossary Entry"): You define method parameters by specifying a name with a type which can be a [generic](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abengeneric_data_type_glosry.htm "Glossary Entry") or  [complete](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abencomplete_data_type_glosry.htm "Glossary Entry")
    type. 
- Examples:
  - `fp` is the formal parameter that has a complete type: `... meth IMPORTING fp TYPE string ...`
  - `gen` is the formal parameter that has a generic type: `... meth IMPORTING gen TYPE any ...`
  - Find more information about generic types also in the [Data Types and Data Objects](16_Data_Types_and_Objects.md#generic-types) cheat sheet.
- This formal parameter includes the specification of how the value passing should happen. Parameters can be passed by ...
  - [reference](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenpass_by_reference_glosry.htm "Glossary Entry"): `... REFERENCE(param) ...`; note that just specifying the parameter name `... param ...` - as a shorter syntax - means passing by reference by default) 
  - [value](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenpass_by_value_glosry.htm "Glossary Entry"): `... VALUE(param) ...`
- An [Actual parameter](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenactual_parameter_glosry.htm "Glossary Entry") represents the data object whose content is passed to or copied from a formal parameter as an argument when a procedure is called. 
- If passing by reference is used, a local data object is not created for the actual parameter. Instead, the procedure is given a [reference](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenreference_glosry.htm "Glossary Entry") to the actual parameter during the call and works with the actual parameter itself. 
- Note that parameters that are input and passed by reference cannot be modified in the procedure. However, the use of a reference is beneficial regarding the performance compared to creating a local data object.

The following example (which anticipates aspects described in the following sections, such as calling methods) shows a class with a simple method demonstrating the syntax for formal parameter specifications. Complete types are used. 

```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.

    "Passing by reference and value
    METHODS: meth IMPORTING i_a            TYPE i
                            REFERENCE(i_b) TYPE string
                            VALUE(i_c)     TYPE i
                  RETURNING VALUE(r_a)     TYPE string.


  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.



CLASS zcl_some_class IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.

    "The values 1, hello, and 2 are actual parameters supplied when 
    "the method is called.
    DATA(result) = meth( i_a = 1
                         i_b = `hello`
                         i_c = 2 ).

  ENDMETHOD.

  METHOD meth.
    ... "Method implementation

    "Input parameters passed by reference cannot be changed in the method implementation.
    "i_a += 1.
    "i_b &&= ` world`.

    "Input parameters passed by value can be changed in the method implementation.
    i_c += 1.

  ENDMETHOD.

ENDCLASS.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Complete Typing of Formal Parameters

Syntax for [completely](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abencomplete_data_type_glosry.htm "Glossary Entry") typing a formal parameter: 
- `TYPE complete_type`
- `TYPE LINE OF complete_type`
- `TYPE REF TO type`
- `LIKE dobj`
- `LIKE LINE OF dobj`
- `LIKE REF TO dobj`

> **💡 Note**<br>
> - `complete_type`: Stands for a non-generic built-in ABAP, ABAP DDIC, ABAP CDS, a public data type from a global class or interface, or a local type declared with `TYPES`
> - `REF TO` types as a reference variable. A generic type cannot be specified after `REF TO`. A typing with `TYPE REF TO data` and `TYPE REF TO object` is considered as completely typing a formal parameter.
> - Enumerated types can also be used to type the formal parameter.
> - The considerations also apply to the typing of field symbols.

```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.

    "Local types and data objects used in the example
    TYPES c3 TYPE c LENGTH 3.
    TYPES der_type TYPE TABLE FOR CREATE zdemo_abap_rap_ro_m.
    DATA int TYPE i.
    DATA itab TYPE TABLE OF zdemo_abap_fli_ve WITH EMPTY KEY.

    "Various syntax options for completely typing formal parameters
    "Note: The example parameters are all specified for passing
    "actual parameters by reference.
    METHODS: meth IMPORTING
                    "---- Non-generic built-in ABAP types ----
                    i_a TYPE i
                    i_b TYPE string
                    "---- ABAP DDIC types ----
                    i_c TYPE land1           "elementary type
                    i_d TYPE timestampl      "elementary type
                    i_e TYPE zdemo_abap_fli "structured type based on DDIC database table
                    i_f TYPE string_hashed_table "table type
                    "---- ABAP CDS types (all of the examples are structured types) ----
                    i_g TYPE zdemo_abap_fli_ve "CDS view entity
                    i_h TYPE zdemo_abap_abstract_ent "CDS abstract entity
                    i_i TYPE zdemo_abap_table_function "CDS table function
                    "---- Data types declared in public section of a class ----
                    i_j TYPE zcl_demo_abap_dtype_dobj=>t_pub_text_c30 "elementary type
                    i_k TYPE zcl_demo_abap_amdp=>carr_fli_struc "structured type
                    i_l TYPE zcl_demo_abap_amdp=>carr_fli_tab "table type
                    "---- Data types declared in an interface ----
                    i_m TYPE zdemo_abap_get_data_itf=>occ_rate "elementary type
                    i_n TYPE zdemo_abap_get_data_itf=>carr_tab "table type
                    "---- Local types ----
                    i_o TYPE c3 "elementary type
                    i_p TYPE der_type "table type (BDEF derived type)
                    "---- Note: Examples such as the following are not allowed type specifications of formal parameters. ----
                    "---- In the following cases, extra (local) type declarations with TYPES are required before the --------
                    "---- method declaration to type the formal parameters. -------------------------------------------------
                    "i_no1 TYPE c LENGTH 3
                    "i_no2 TYPE TABLE OF zdemo_abap_fli WITH EMPTY KEY
                    "---- Reference types ----
                    i_q TYPE REF TO i "Data reference
                    i_r TYPE REF TO zdemo_abap_carr "Data reference
                    i_s TYPE REF TO zcl_demo_abap_unit_test "Object reference
                    i_t TYPE REF TO data "Data reference (considered as complete typing, too)
                    i_u TYPE REF TO object "Object reference (considered as complete typing, too)
                    "---- TYPE LINE OF addition (structured type based on a table type) ----
                    i_v TYPE LINE OF zcl_demo_abap_amdp=>carr_fli_tab
                    i_w TYPE LINE OF der_type
                    "---- LIKE addition (types based on existing data objects) ----
                    i_x LIKE int "Local data object
                    i_y LIKE zcl_demo_abap_dtype_dobj=>comma "Constant specified in a class
                    i_z LIKE zdemo_abap_objects_interface=>stat_str "Data object specified in an interface
                    "---- LIKE LINE OF addition (types based on existing internal tables) ----
                    i_1 LIKE LINE OF itab "Local internal table
                    "---- LIKE REF TO addition (reference types based on existing data object) ----
                    i_2 LIKE REF TO int "Local elementary data object
                    i_3 LIKE REF TO itab "Local internal table
                  .

  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.



CLASS zcl_some_class IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.

    "Calling methods and providing actual parameters
*    meth(
*      i_a = 1
*      i_b = `hello`
*      ... ).

  ENDMETHOD.

  METHOD meth.
    ... "Method implementation
  ENDMETHOD.

ENDCLASS.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Generic Typing of Formal Parameters

Find more information on generic types in the [Data Types and Data Objects](16_Data_Types_and_Objects.md#generic-types) cheat sheet. The following code snippet anticipates aspects described in the following sections, such as calling methods.

```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.

    "Example method demonstrating the generic typing of formal parameters
    METHODS: meth IMPORTING
                    "---- Any data type ----
                    i_data           TYPE data
                    i_any            TYPE any

                    "---- Character-like types ----
                    i_c              TYPE c         "Text field with a generic length
                    i_clike          TYPE clike     "Character-like (c, n, string, d, t, and character-like flat structures)
                    i_csequence      TYPE csequence "Text-like (c, string)
                    i_n              TYPE n         "Numeric text with generic length
                    i_x              TYPE x         "Byte field with generic length
                    i_xsequence      TYPE xsequence "Byte-like (x, xstring)

                    "---- Numeric types ----
                    i_decfloat       TYPE decfloat "decfloat16 decfloat34
                    i_numeric        TYPE numeric  "Numeric (i, int8, p, decfloat16, decfloat34, f, (b, s))
                    i_p              TYPE p        "Packed number (generic length and number of decimal places)

                    "---- Internal table types ----
                    i_any_table      TYPE ANY TABLE      "Internal table with any table type
                    i_hashed_table   TYPE HASHED TABLE
                    i_index_table    TYPE INDEX TABLE
                    i_sorted_table   TYPE SORTED TABLE
                    i_standard_table TYPE STANDARD TABLE
                    i_table          TYPE table          "Standard table

                    "---- Other types ----
                    i_simple         TYPE simple "Elementary data type including enumerated types and
                    "structured types with exclusively character-like flat components
                  .
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.



CLASS zcl_some_class IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.

    "Structure including various components of specific types
    "They represent actual parameters in the method call below
    DATA: BEGIN OF s,
            c3        TYPE c LENGTH 3,
            c10       TYPE c LENGTH 10,
            n4        TYPE n LENGTH 4,
            str       TYPE string,
            time      TYPE t,
            date      TYPE d,
            dec16     TYPE decfloat16,
            dec34     TYPE decfloat34,
            int       TYPE i,
            pl4d2     TYPE p LENGTH 4 DECIMALS 2,
            tab_std   TYPE STANDARD TABLE OF string WITH EMPTY KEY,
            tab_so    TYPE SORTED TABLE OF string WITH NON-UNIQUE KEY table_line,
            tab_ha    TYPE HASHED TABLE OF string WITH UNIQUE KEY table_line,
            xl1       TYPE x LENGTH 1,
            xstr      TYPE xstring,
            structure TYPE zdemo_abap_carr, "character-like flat structure
          END OF s.

    "The following method call specifies various actual parameters for the
    "generic formal parameters.
    "Note the comments for allowed and not allowed example assignments of
    "actual parameters.
    meth(
      "------------- Any data type -------------
      "--- data/any: Allowed (examples) ---
      i_data = s-c3
      "i_data = s-time
      "i_data = s-tab_std
      "i_data = s-xstr

      i_any = s-c3
      "i_any = s-time
      "i_any = s-tab_std
      "i_any = s-xstr

      "------------- Character-like types -------------
      "--- c: Allowed (examples) ---
      i_c = s-c3
      "i_c = s-c10
      "--- c: Not allowed (examples) ---
      "i_c = s-str
      "i_c = s-n4

      "--- clike: Allowed (examples) ---
      i_clike = s-c3
      "i_clike = s-c10
      "i_clike = s-str
      "i_clike = s-structure
      "i_clike = s-time
      "i_clike = s-date
      "i_clike = s-n4
      "--- clike: Not allowed (examples) ---
      "i_clike = s-xstr
      "i_clike = s-xl1
      "i_clike = s-pl4d2

      "--- csequence: Allowed (examples) ---
      i_csequence  = s-c3
      "i_csequence  = s-c10
      "i_csequence  = s-str
      "--- csequence: Not allowed (examples) ---
      "i_csequence  = s-time
      "i_csequence  = s-date
      "i_csequence  = s-structure

      "--- n: Allowed ---
      i_n = s-n4
      "--- n: Not allowed (examples) ---
      "i_n = s-c3
      "i_n = s-int

      "--- x: Allowed ---
      i_x = s-xl1
      "--- x: Not allowed (examples) ---
      "i_x = s-xstr
      "i_x = s-c3

      "--- xsequence: Allowed ---
      i_xsequence = s-xstr
      "i_xsequence = s-xl1
      "--- xsequence: Not allowed (examples) ---
      "i_xsequence = s-c3
      "i_xsequence = s-str

      "--- decfloat: Allowed ---
      i_decfloat = s-dec16
      "i_decfloat = s-dec34
      "--- decfloat: Not allowed (examples) ---
      "i_decfloat = s-int
      "i_decfloat = s-pl4d2

      "--- numeric: Allowed (examples) ---
      i_numeric  = s-int
      "i_numeric = s-dec16
      "i_numeric = s-dec34
      "i_numeric = s-pl4d2
      "--- numeric: Not allowed (examples) ---
      "i_numeric = s-n4
      "i_numeric = s-date

      "--- p: Allowed ---
      i_p = s-pl4d2
      "--- p: Not allowed (examples) ---
      "i_p = s-dec16
      "i_p = s-dec34

      "--- any table: Allowed ---
      i_any_table = s-tab_std
      "i_any_table = s-tab_ha
      "i_any_table = s-tab_so
      "--- any table: Not allowed (examples) ---
      "i_any_table = s-structure
      "i_any_table = s-c3

      "--- hashed table: Allowed ---
      i_hashed_table = s-tab_ha
      "--- hashed table: Not allowed ---
      "i_hashed_table = s-tab_std
      "i_hashed_table = s-tab_so

      "--- index table: Allowed ---
      i_index_table = s-tab_std
      "i_index_table = s-tab_so
      "--- index table: Not allowed ---
      "i_index_table = s-tab_ha

      "--- sorted table: Allowed ---
      i_sorted_table = s-tab_so
      "--- sorted table: Not allowed ---
      "i_sorted_table = s-tab_std
      "i_sorted_table = s-tab_ha

      "--- standard table/table: Allowed ---
      i_standard_table = s-tab_std
      i_table = s-tab_std
      "--- standard table/table: Not allowed ---
      "i_standard_table = s-tab_so
      "i_standard_table = s-tab_ha
      "i_table = s-tab_so
      "i_table = s-tab_ha

     "--- simple: Allowed (examples) ---
      i_simple = s-structure
      "i_simple = s-c3
      "i_simple = s-n4
      "i_simple = s-int
      "i_simple = s-pl4d2
      "i_simple = s-xstr
      "i_simple = s-str
      "--- simple: Not allowed (examples) ---
      "i_simple = s-tab_ha
      "i_simple = s-tab_so

       ).

  ENDMETHOD.

  METHOD meth.
    ... "Method implementation
  ENDMETHOD.

ENDCLASS.
```


<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Defining Parameters as Optional

- Parameters specified after `IMPORTING` and `CHANGING` can be defined as optional using the `OPTIONAL` and `DEFAULT` additions: 
  - [`OPTIONAL`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapmethods_parameters.htm#!ABAP_ONE_ADD@1@): It is then not mandatory to pass an actual
    parameter. 
  - [`DEFAULT`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapmethods_parameters.htm#!ABAP_ONE_ADD@1@): Also makes the passing of an actual parameter optional. However, when using this addition, as the name implies, a default value is set.
  - In the method implementations you may want to check whether an actual parameter was passed. You can use predicate expressions using `IS SUPPLIED`. See the example further down.


The following example (which anticipates aspects described in the following sections, such as calling methods) includes three methods that specify optional parameters. The methods are called with and without providing actual parameters. The method implementations include the use of the predicate expression `IS SUPPLIED` with `IF` statements and the `COND` operator. The console output of the example, run with F9, is as follows:

```
meth1_result_a                                    
The parameter is not supplied. Initial value: "0".
meth1_result_b                        
The parameter is supplied. Value: "2".
meth2_result_a                                    
The parameter is not supplied. Default value: "1".
meth2_result_b                        
The parameter is supplied. Value: "3".
meth3_result_b                                                                                      
num1: "4" / num2 (is not supplied; initial value): "0" / num3 (is not supplied; default value): "1" 
meth3_result_c                                                                   
num1: "5" / num2 (is supplied): "6" / num3 (is not supplied; default value): "1" 
meth3_result_d                                                                   
num1: "7" / num2 (is not supplied; initial value): "0" / num3 (is supplied): "8" 
```

```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    METHODS meth1 IMPORTING num        TYPE i OPTIONAL
                  RETURNING VALUE(str) TYPE string.
    METHODS meth2 IMPORTING num        TYPE i DEFAULT 1
                  RETURNING VALUE(str) TYPE string.
    METHODS meth3 IMPORTING num1       TYPE i
                            num2       TYPE i OPTIONAL
                            num3       TYPE i DEFAULT 1
                  RETURNING VALUE(str) TYPE string.

  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.

CLASS zcl_some_class IMPLEMENTATION.
  METHOD if_oo_adt_classrun~main.

    DATA(meth1_result_a) = meth1( ).
    DATA(meth1_result_b) = meth1( 2 ).

    DATA(meth2_result_a) = meth2( ).
    DATA(meth2_result_b) = meth2( 3 ).

    "The commented out statement is not possible as there is one
    "non-optional parameter.
    "DATA(meth3_result_a) = meth3( ).
    DATA(meth3_result_b) = meth3( 4 ).
    DATA(meth3_result_c) = meth3( num1 = 5 num2 = 6 ).
    DATA(meth3_result_d) = meth3( num1 = 7 num3 = 8 ).

    out->write( data = meth1_result_a name = `meth1_result_a` ).
    out->write( data = meth1_result_b name = `meth1_result_b` ).
    out->write( data = meth2_result_a name = `meth2_result_a` ).
    out->write( data = meth2_result_b name = `meth2_result_b` ).
    out->write( data = meth3_result_b name = `meth3_result_b` ).
    out->write( data = meth3_result_c name = `meth3_result_c` ).
    out->write( data = meth3_result_d name = `meth3_result_d` ).

  ENDMETHOD.

  METHOD meth1.
    IF num IS SUPPLIED.
      str = |The parameter is supplied. Value: "{ num }".|.
    ELSE.
      str = |The parameter is not supplied. Initial value: "{ num }".|.
    ENDIF.
  ENDMETHOD.

  METHOD meth2.
    str = COND #( WHEN num IS SUPPLIED THEN |The parameter is supplied. Value: "{ num }".|
                  ELSE |The parameter is not supplied. Default value: "{ num }".|  ).
  ENDMETHOD.

  METHOD meth3.
    str = |num1: "{ num1 }" / |.

    str &&= |{ COND #( WHEN num2 IS SUPPLIED THEN |num2 (is supplied): "{ num2 }"|
                       ELSE |num2 (is not supplied; initial value): "{ num2 }"| ) } / |.

    str &&= |{ COND #( WHEN num3 IS SUPPLIED THEN |num3 (is supplied): "{ num3 }"|
                       ELSE |num3 (is not supplied; default value): "{ num3 }"| ) } |.
  ENDMETHOD.

ENDCLASS.
```


<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Defining Input Parameters as Preferred

- Using the `PREFERRED PARAMETER` addition, you can flag an input parameter from the list as preferred.
- All parameters must be optional (i.e. specified with `OPTIONAL` or `DEFAULT`).
- The preferred parameter is implicitly optional, but you should explicitly specify it as `OPTIONAL` or `DEFAULT`, or a warning will be displayed.
- When you call a method and specify a single actual parameter without specifying the name of the formal parameter in an assignment, the actual parameter is automatically assigned to the preferred parameter.

The following example (which anticipates aspects described in the following sections, such as calling methods) shows a simple method with input parameters of type `i` (an addition is performed using the actual parameter values), where one parameter is preferred. The `IS SUPPLIED` addition in `COND` statements checks whether parameters are supplied. The final output shows the preferred parameter assigned automatically when the formal parameter is not specified explicitly.
To try the example out, create a demo class named `zcl_some_class` and paste the code into it. After activation, choose *F9* in ADT to execute the class. The example is set up to display output in the console. The example should display the following:

```
IS SUPPLIED: num1 "X", num2 "X", num3 "X" / Addition result "9"
IS SUPPLIED: num1 "X", num2 "X", num3 "" / Addition result "7"
IS SUPPLIED: num1 "", num2 "X", num3 "X" / Addition result "6"
IS SUPPLIED: num1 "X", num2 "", num3 "X" / Addition result "6"
IS SUPPLIED: num1 "", num2 "X", num3 "" / Addition result "4"
IS SUPPLIED: num1 "", num2 "", num3 "X" / Addition result "3"
IS SUPPLIED: num1 "", num2 "", num3 "" / Addition result "1"
IS SUPPLIED: num1 "X", num2 "", num3 "" / Addition result "4"
```

Example code:

```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.

    CLASS-METHODS meth
      IMPORTING num1        TYPE i OPTIONAL
                num2        TYPE i OPTIONAL
                num3        TYPE i DEFAULT 1
                PREFERRED PARAMETER num1
      RETURNING VALUE(text) TYPE string.
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.

CLASS zcl_some_class IMPLEMENTATION.
  METHOD if_oo_adt_classrun~main.

    DATA(text1) = meth( num1 = 3 num2 = 3 num3 = 3 ).
    out->write( text1 ).

    DATA(text2) = meth( num1 = 3 num2 = 3 ).
    out->write( text2 ).

    DATA(text3) = meth( num2 = 3 num3 = 3 ).
    out->write( text3 ).

    DATA(text4) = meth( num1 = 3 num3 = 3 ).
    out->write( text4 ).

    DATA(text5) = meth( num2 = 3 ).
    out->write( text5 ).

    DATA(text6) = meth( num3 = 3 ).
    out->write( text6 ).

    DATA(text7) = meth( ).
    out->write( text7 ).

    "Not specifying the name of the formal parameter. The
    "actual parameter is assigned to the preferred input
    "parameter.
    DATA(text8) = meth( 3 ).
    out->write( text8 ).
  ENDMETHOD.

  METHOD meth.
    DATA(addition) = num1 + num2 + num3.
    text = |IS SUPPLIED: num1 "{ COND #( WHEN num1 IS SUPPLIED THEN 'X' ELSE '' ) }", | &&
           |num2 "{ COND #( WHEN num2 IS SUPPLIED THEN 'X' ELSE '' ) }", | &&
           |num3 "{ COND #( WHEN num3 IS SUPPLIED THEN 'X' ELSE '' ) }" / | &&
           |Addition result "{ addition }"|.
  ENDMETHOD.

ENDCLASS.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Constructors

-   [Constructors](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenconstructor_glosry.htm "Glossary Entry")
    are special methods that are usually used for setting a defined
    initial value for attributes of the class or its objects.
-   A class has exactly one [instance
    constructor](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninstance_constructor_glosry.htm "Glossary Entry")
    and one [static
    constructor](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenstatic_constructor_glosry.htm "Glossary Entry").
-   The declaration and use of constructors is optional.
-   Static constructor:
    - Declared using the predefined name `class_constructor` as part of a
    `CLASS-METHODS` statement in the public visibility section.
    - Has no parameters.
    - Automatically and immediately called once for each class when calling a class for
    the first time in an internal session, i. e. when, for example, an instance of a class is created or a component is used. Note: If it is not explicitly declared and implemented, it is merely an empty method.
-   Instance constructor:
    - Declared using the predefined name `constructor` as part of a
    `METHODS` statement. In case of global classes, it can only be declared in the public visibility section.
    - Automatically called when a class is
    instantiated and an instance is created.
    - Can have `IMPORTING` parameters and raise exceptions.

The following example (which anticipates aspects described in the following sections, such as creating instances of classes) demonstrates static and instance constructors. To try the example out, create a demo class named `zcl_some_class` and paste the code into it. After activation, choose *F9* in ADT to execute the class. The example is set up to display output in the console.

Notes:  
- The example class defines the instance and static constructors.  
- The instance constructor includes an optional importing parameter, which static constructors do not allow. If the parameter were not optional, the class would not run with F9, as it could not pass an actual parameter. In the example, the actual parameter indicates the name of the instance created for output purposes.
- The example class creates multiple instances.
- Both instance and static attributes of each instance are accessed and added to an internal table, which is then output.
- The constructor implementations include:  
  - Instance constructor:  
    - Stores the current timestamp in an instance attribute.  
    - Maintains a call counter for the number of times the instance constructor is called, stored in a static attribute to reflect the count per internal session.  
    - Stores the manually provided instance name in an instance attribute.  
  - Static constructor:  
    - Stores the current timestamp in a static attribute.  
    - Maintains a call counter for static constructor calls, stored in a static attribute.  
- The constructors demonstrate:  
  - The static constructor is called only once, even when multiple class instances are created, leading to a constant `static_timestamp` value and `stat_constr_call_count` value, which remains 1.  
  - The `instance_timestamp` attribute shows different timestamps for each created instance.  
  - The static attribute `instance_constr_call_count` increases with each instance. Note that running the class with F9 in ADT also calls the instance and static constructors. Thus, the final `instance_constr_call_count` totals the number of `DO` loop passes plus 1, starting with 2 for `inst1` instead of 1.


```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    METHODS constructor IMPORTING text TYPE string OPTIONAL.
    CLASS-METHODS class_constructor.
  PROTECTED SECTION.
  PRIVATE SECTION.
    DATA instance_timestamp TYPE utclong.
    CLASS-DATA static_timestamp TYPE utclong.
    DATA instance_name TYPE string.
    CLASS-DATA stat_constr_call_count TYPE i.
    CLASS-DATA instance_constr_call_count TYPE i.
ENDCLASS.

CLASS zcl_some_class IMPLEMENTATION.
  METHOD if_oo_adt_classrun~main.

    DATA itab TYPE string_table.

    DO 5 TIMES.
      DATA(inst) = NEW zcl_some_class( |inst{ sy-index }| ).
      APPEND |-------------- Instance "{ inst->instance_name }" --------------| TO itab.
      APPEND |instance_timestamp: { inst->instance_timestamp }| TO itab.
      APPEND |static_timestamp: { inst->static_timestamp }| TO itab.
      APPEND |instance_constr_call_count: { inst->instance_constr_call_count }| TO itab.
      APPEND |stat_constr_call_count: { inst->stat_constr_call_count }| TO itab.
      APPEND INITIAL LINE TO itab.
    ENDDO.

    out->write( itab ).
  ENDMETHOD.

  METHOD class_constructor.
    static_timestamp = utclong_current( ).
    stat_constr_call_count += 1.
  ENDMETHOD.

  METHOD constructor.
    instance_timestamp = utclong_current( ).
    instance_constr_call_count += 1.

    IF text IS SUPPLIED AND text IS NOT INITIAL.
      instance_name = text.
    ENDIF.
  ENDMETHOD.

ENDCLASS.
```


<p align="right"><a href="#top">⬆️ back to top</a></p>

## Working with Objects and Components

### Declaring Object Reference Variables
- To create an object, an [object reference variable](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenobject_refer_variable_glosry.htm "Glossary Entry") must be declared. 
- It is also necessary for accessing objects and their components. That means objects are not directly accessed but only via references that point to
those objects. 
- This object reference variable contains the reference to the object - after assigning the reference to the object (see further down).

``` abap
"Declaring object reference variables
DATA: ref1 TYPE REF TO local_class,
      ref2 TYPE REF TO global_class,
      ref3 LIKE ref1.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Creating Objects

-   Using the instance operator
    [`NEW`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenconstructor_expression_new.htm),
    you can create objects of a class (and [anonymous data
    objects](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenanonymous_data_object_glosry.htm "Glossary Entry"), too, that are not dealt with here). As a result,
    you get a [reference variable](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenreference_variable_glosry.htm "Glossary Entry")
    that points to the created object.
-   Regarding the type specifications before and parameters within the
    parentheses:
    - Right before the first parenthesis after `NEW`, the type, i. e. the class, must be specified. The `#` character - instead of the class name -
means that the type (`TYPE REF TO ...`) can be derived from the context (in this case from the type of the reference variable). You can
also omit the explicit declaration of a reference variable by declaring a new reference variable
[inline](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abendata_inline.htm),
for example, using `DATA`. In this case, the name of the class must be placed after `NEW` and before the first parenthesis.
    -   No parameter specified within the parentheses: No values are
        passed to the instance constructor of an object. However, non-optional input parameters of the
        instance constructor of the instantiated class must be filled.
        No parameters are passed for a class without an explicitly declared
        instance constructor. See more information:
        [here](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abennew_constructor_params_class.htm).
- The operator
    basically replaces the syntax [`CREATE OBJECT`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapcreate_object.htm) you might stumble on. However, `CREATE OBJECT` statements are still required (i.e. they are the only option, `NEW` is not possible for them) for creating objects dynamically. For more information, see the [Dynamic Programming](06_Dynamic_Programming.md) cheat sheet.

``` abap
"Declaring object reference variable
DATA: ref1 TYPE REF TO some_class.

"Creating objects
ref1 = NEW #( ).                     "Type derived from already declared ref1

DATA(ref2) = NEW some_class( ).      "Reference variable declared inline, explicit type
                                     "(class) specification
"The assumption is that this class has no mandatory importing parameters for the 
"instance constructor. If a class has, actual parameters must be provided.                                      
DATA(ref_mand_param) = NEW another_class( ip1 = ... ip2 = ... ).

"Older syntax, replaced by NEW operator 
"However, the CREATE OBJECT is required in dynamic object creation.
CREATE OBJECT ref3.                  "Type derived from already declared ref3
CREATE OBJECT ref4 TYPE some_class.  "Corresponds to the result of the expression above
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Working with Reference Variables

This section covers some aspects of working with reference variables.

**Assigning Reference Variables**

To assign or copy reference variables, use the [assignment
operator](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenassignment_operator_glosry.htm "Glossary Entry")
`=`. In the example below, both object reference variables have the same type. Note the concepts of polymorphism, upcasts and downcasts when assigning reference variables covered further down.

``` abap
DATA: ref1 TYPE REF TO some_class,
      ref2 TYPE REF TO some_class.

ref1 = NEW #( ).

"Assigning existing reference
ref2 = ref1.
```

**Overwriting reference variables**: An [object
reference](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenobject_reference_glosry.htm "Glossary Entry")
is overwritten when a new object is created with a reference variable
already pointing to an instance.
``` abap
ref1 = NEW #( ).

"Existing reference is overwritten
ref1 = NEW #( ).
```

**Retaining object references**:
- If your use case is to retain the object references, for example, if you create multiple objects using the same object reference variable, you can put the reference variables in internal tables that are declared using `... TYPE TABLE OF REF TO ...`.
- The following code snippet just visualizes that the object references are not overwritten. Three objects are created with the same reference variable. The internal table includes all object references and, thus, their values are retained.
``` abap
DATA: ref TYPE REF TO some_class,
      itab TYPE TABLE OF REF TO some_class.

DO 3 TIMES.
  ref = NEW #( ).
  itab = VALUE #( BASE itab ( ref ) ).   "Adding the reference to itab
ENDDO.
```

**Clearing object references**: You can use
[`CLEAR`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapclear.htm)
statements to explicitly clear a reference variable.
```abap
CLEAR ref.
```

> **💡 Note**<br>
> Objects use up space in the memory and should therefore be
cleared if they are no longer needed. However, the [garbage collector](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abengarbage_collector_glosry.htm "Glossary Entry") is called periodically and automatically by the [ABAP runtime framework](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenabap_runtime_frmwk_glosry.htm "Glossary Entry") and clears all objects without any reference.

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Accessing Attributes
- Instance attributes: Accessed using
the [object component selector](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenobject_component_select_glosry.htm "Glossary Entry")
`->` via a reference variable.
- Static attributes: Accessed (if the attributes are visible) using the [class component
selector](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenclass_component_select_glosry.htm "Glossary Entry")
`=>` via the class name. You can also declare data objects and
types by referring to static attributes.
``` abap
"Accessing instance attribute via an object reference variable

... ref->some_attribute ...

"Accessing static attributes via the class name

... some_class=>static_attribute ...

"Without the class name only within the class itself
... static_attribute ...

"Type and data object declarations

TYPES some_type LIKE some_class=>some_static_attribute.
DATA dobj1      TYPE some_class=>some_type.
DATA dobj2      LIKE some_class=>some_static_attribute.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Calling Methods
- Similar to accessing attributes, instance
methods are called using `->` via a reference variable.
- Static
methods are called using `=>` via the class name. When used
within the class in which it is declared, the static method can also be
called without `class_name=>...`.
- When methods are called, the (non-optional) parameters must be specified within parentheses.
- You might also stumble on method calls with [`CALL METHOD`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapcall_method_static.htm)
statements. These statements should no longer be used. Note that `CALL METHOD` statements are the only option in the context of [dynamic programming](06_Dynamic_Programming.md). Therefore, `CALL METHOD` statements should be reserved for dynamic method calls.


Examples for instance method calls and static method calls:
``` abap
"Calling instance methods via reference variable;
"within the parentheses, the parameters must be specified and assigned - if required

ref->inst_meth( ... ).

"Calling static methods via/without the class name

class_name=>stat_meth( ... ).

"Only within the program in which it is declared.
stat_meth( ... ).

"Calling (static) method having no parameter

class_name=>stat_meth( ).

"Calling (static) methods having a single importing parameter:

"Note that in the method call, the caller exports values to the
"method having importing parameters defined; hence, the addition
"EXPORTING is relevant for the caller. The following three method calls are the same

"Explicit use of EXPORTING.
class_name=>meth( EXPORTING a = b ).

"Only importing parameters in the method signature: explicit EXPORTING not needed

class_name=>meth( a = b ).

"If only a single value must be passed:
"the formal parameter name (a) and EXPORTING not needed

stat_meth( b ).

"Calling (static) methods having importing/exporting parameters
"Parameters must be specified if they are not marked as optional

class_name=>meth( EXPORTING a = b c = d     "a/c: importing parameters in the method signature
                  IMPORTING e = f ).        "e: exporting parameter in the method signature

"To store the value of the parameter, you may also declare it inline.

class_name=>meth( EXPORTING a = b c = d
                  IMPORTING e = DATA(z) ).  

"Calling (static) methods having a changing parameter;
"should be reserved for changing an existing local variable and value

DATA h TYPE i VALUE 123.
class_name=>meth( CHANGING g = h ).

"Calling (static) methods having a returning parameter.
"Basically, they do the same as methods with exporting parameters
"but they are way more versatile, and you can save lines of code.

"They do not need temporary variables.
"In the example, the return value is stored in a variable declared inline.

"i and k are importing parameters
DATA(result) = class_name=>meth( i = j k = l ).

"They can be used with other statements, e. g. logical expressions.
"In the example below, the assumption is that the returning parameter is of type i.
IF class_name=>meth( i = j k = l ) > 100.
  ...
ENDIF.

"They enable method chaining.
"The example shows a method to create random integer values.
"The methods have a returning parameter.
DATA(random_no) = cl_abap_random_int=>create( )->get_next( ).

"RECEIVING parameter: Available in methods defined with a returning parameter;
"used in standalone method calls only.
"In the snippet, m is the returning parameter; n stores the result.
class_name=>meth( EXPORTING i = j k = l RECEIVING m = DATA(n) ).
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Excursion: Inline Declarations, Returning Parameters

<details>
  <summary>🟢 Click to expand for more information and example code</summary>
  <!-- -->

<br>


- The example code below highlights the convenience of inline declarations when defining target data objects for output parameters. 
- This approach allows you to create data objects on the spot, eliminating the need for additional helper variables. 
- It also mitigates the risk of type mismatches. 
- However, when declaring a method with both exporting and returning parameters, it is not possible to specify target data objects for both inline at the same time in case of functional method calls. 
- Additional code snippets illustrate various ways to use methods declared with returning parameters in expression positions.

```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    CLASS-METHODS meth1 IMPORTING i_str        TYPE string
                                  i_tab        TYPE string_table OPTIONAL
                        EXPORTING e_dec        TYPE decfloat34
                                  e_tab        TYPE string_table
                        RETURNING VALUE(r_int) TYPE i.
    CLASS-METHODS meth2 RETURNING VALUE(r_tab) TYPE string_table.
  PROTECTED SECTION.
  PRIVATE SECTION.

ENDCLASS.


CLASS zcl_some_class IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.    
    "Note: Calling the method in the same class means specifying 'zcl_some_class=>' is optional here.

    "Standalone method call
    "Specifying target data objects for all output parameters
    "Inline declarations are handy because you can create an
    "appropriately typed data object in place. No need to
    "create an extra variable, check on the type etc.
    zcl_some_class=>meth1(
      EXPORTING
        i_str = `ABAP`
      IMPORTING
        e_dec = DATA(a)
        e_tab = DATA(b)
      RECEIVING
        r_int = DATA(c)
    ).

    "Functional method call
    "The target data object of the returning parameter is specified on the left side of an assignment.
    "Note: In this case, you cannot specify inline declarations for the exporting parameters.
    DATA e TYPE decfloat34.
    DATA f TYPE string_table.
    DATA(g) = zcl_some_class=>meth1(
      EXPORTING
        i_str = `ABAP`
      IMPORTING
        "e_dec = DATA(h)
        "e_tab = DATA(i)
        e_dec = e
        e_tab = f
    ).

    "Benefits of returning parameters: They can, for example, be used in expressions
    "The following snippets show a selection (and ignore the available exporting
    "parameters).

    CASE zcl_some_class=>meth1( i_str = `ABAP` ).
      WHEN 0. ...
      WHEN 1. ...
      WHEN OTHERS. ...
    ENDCASE.

    IF zcl_some_class=>meth1( i_str = `ABAP` ) > 5.
      ...
    ELSE.
      ...
    ENDIF.

    "IF used with a predicative method call
    "The result of the relational expression is true if the result of the functional
    "method call is not initial and false if it is initial. The data type of the result
    "of the functional meth1od call, i. e. the return value of the called functional method,
    "is arbitrary. A check is made for the type-dependent initial value.
    IF zcl_some_class=>meth1( i_str = `ABAP` ).
      ...
    ELSE.
      ...
    ENDIF.

    DO zcl_some_class=>meth1( i_str = `ABAP` ) TIMES.
      ...
    ENDDO.

    "Method call result as actual parameter
    DATA(j) = zcl_some_class=>meth1( i_str = `ABAP` i_tab = zcl_some_class=>meth2( ) ).

    "Examples of returning parameters typed with a table type
    LOOP AT zcl_some_class=>meth2( ) INTO DATA(wa1).
      ...
    ENDLOOP.

    READ TABLE zcl_some_class=>meth2( ) INTO DATA(wa2) INDEX 1.

  ENDMETHOD.
  
  METHOD meth1.
    ... "Method implementation
  ENDMETHOD.

  METHOD meth2.
    ... "Method implementation
  ENDMETHOD.

ENDCLASS.
```

</details>  


<p align="right"><a href="#top">⬆️ back to top</a></p>

### Self-Reference me

When implementing instance methods, you can optionally make use of the implicitly available object reference variable [`me`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenme.htm) which is always available at runtime and points to the respective object itself. You can use it, for example, to refer to components of the instance of a particular class:
``` abap
... some_method( ... ) ...

... me->some_method( ... ) ...
```

You can also address the entire object, which is illustrated in the example of section [Method Chaining and Chained Attribute Access](#method-chaining-and-chained-attribute-access).
The following code snippet declares a local data object in a method. It has the same name as a data object declared in the private visibility section. shows a method implementation. `me` is used to access the non-local data object.

``` abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
  PROTECTED SECTION.
  PRIVATE SECTION.
    DATA str TYPE string.
    METHODS meth RETURNING VALUE(text) TYPE string.
ENDCLASS.

CLASS zcl_some_class IMPLEMENTATION.
  METHOD if_oo_adt_classrun~main.

    str = `AP`.
    DATA(text) = meth( ).
    ASSERT text = `ABAP`.

  ENDMETHOD.

  METHOD meth.

    "Declaring a local data object having the same
    "name as a data object declared in a visibility section
    DATA str TYPE string VALUE `AB`.

    "Addressing locally declared data object
    DATA(local_string) = str.

    "Addressing data object declared in private visibility section
    DATA(other_string) = me->str.

    text = local_string && other_string.

  ENDMETHOD.

ENDCLASS.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Method Chaining and Chained Attribute Access

- As shown in a previous example, method chaining is possible for functional method calls (i.e. methods that have exactly one return value declared with `RETURNING`) at appropriate read positions. 
- In this method design, the return values are reference variables that point to objects with the next method in question. The methods in the example class below assign the objects to the returning parameter using the self-reference `me`. 
- The method's return value is then used as an ABAP operand.
- A chained method call can consist of multiple functional methods that are linked using component selectors `->`. 
- Class attributes can also be added to the chain.
- In the context of method chaining, constructor expressions (e.g. with `NEW`) come in handy. The example class below shows functional method calls (i.e. the return value of the method is used as an ABAP operand), and a standalone statement.

The following example illustrates method chaining. Find a self-contained example class further down.

```abap
"The following class creates random integers. Find more information in the
"class documentation.
"Both methods have returning parameters specified.
DATA(some_int1) = cl_abap_random_int=>create( seed = cl_abap_random=>seed( )
                                              min  = 1
                                              max  = 10 )->get_next( ).

"Getting to the result as above - not using method chaining and inline declarations.
DATA some_int2 TYPE i.
DATA dref TYPE REF TO cl_abap_random_int.

dref = cl_abap_random_int=>create( seed = cl_abap_random=>seed( )
                                   min  = 1
                                   max  = 10 ).

some_int2 = dref->get_next( ).

"Using the RECEIVING parameter in a standalone method call
DATA some_int3 TYPE i.
dref->get_next( RECEIVING value = some_int3 ).

"IF statement that uses the return value in a read position
IF cl_abap_random_int=>create( seed = cl_abap_random=>seed( )
                               min  = 1
                               max  = 10 )->get_next( ) < 5.
  ... "The random number is lower than 5.
ELSE.
  ... "The random number is greater than 5.
ENDIF.

"Examples using classes of the XCO library (see more information in the
"ABAP for Cloud Development and Released ABAP Classes cheat sheets), in which
"multiple chained method calls can be specified. Each of the methods
"has a returning parameter specified.

"In the following example, 1 hour is added to the current time.
DATA(add1hour) = xco_cp=>sy->time( xco_cp_time=>time_zone->user )->add( iv_hour = 1 )->as( xco_cp_time=>format->iso_8601_extended )->value.

"In the following example, a string is converted to xstring using a codepage
DATA(xstr) = xco_cp=>string( `Some string` )->as_xstring( xco_cp_character=>code_page->utf_8 )->value.

"In the following example, JSON data is created. First, a JSON data builder
"is created. Then, using different methods, JSON data is added. Finally,
"the JSON data is turned to a string.
DATA(json) = xco_cp_json=>data->builder( )->begin_object(
  )->add_member( 'CarrierId' )->add_string( 'DL'
  )->add_member( 'ConnectionId' )->add_string( '1984'
  )->add_member( 'CityFrom' )->add_string( 'San Francisco'
  )->add_member( 'CityTo' )->add_string( 'New York'
  )->end_object( )->get_data( )->to_string( ).
```

Self-contained example class demonstrating chained method calls with a functional method call and a standalone statement:

```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    METHODS add_text IMPORTING str        TYPE string
                     RETURNING VALUE(ref) TYPE REF TO zcl_some_class.
    METHODS add_space RETURNING VALUE(ref) TYPE REF TO zcl_some_class.
    METHODS add_period RETURNING VALUE(ref) TYPE REF TO zcl_some_class.
    METHODS return_text RETURNING VALUE(str) TYPE string.
    METHODS display_text IMPORTING cl_run_ref TYPE REF TO if_oo_adt_classrun_out.
    DATA text TYPE string.
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.

CLASS zcl_some_class IMPLEMENTATION.
  METHOD if_oo_adt_classrun~main.

    "----------------------------------------------------------------
    "-------- Method chaining with a functional method call ---------
    "----------------------------------------------------------------

    "Hallo NAME. This is an example of method chaining.
    DATA(text1) = NEW zcl_some_class(
                      )->add_text( `Hallo`
                      )->add_space(
                      )->add_text( xco_cp=>sy->user( )->name
                      )->add_period(
                      )->add_space(
                      )->add_text( `This`
                      )->add_space(
                      )->add_text( `is`
                      )->add_space(
                      )->add_text( `an`
                      )->add_space(
                      )->add_text( `example`
                      )->add_space(
                      )->add_text( `of`
                      )->add_space(
                      )->add_text( `method`
                      )->add_space(
                      )->add_text( `chaining`
                      )->add_period(
                      )->return_text( ).

    out->write( text1 ).

    "The following example chained method call includes a chained attribute
    "access at the end so that the target variable contains the content of
    "the attribute.

    "Example result: Today is 2025-03-05. It's 14:30:38. Have a nice day.
    DATA(text2) = NEW zcl_some_class(
                      )->add_text( `Today`
                      )->add_space(
                      )->add_text( `is`
                      )->add_space(
                      )->add_text( xco_cp=>sy->date( )->as( xco_cp_time=>format->iso_8601_extended )->value
                      )->add_period(
                      )->add_space(
                      )->add_text( `It's`
                      )->add_space(
                      )->add_text( xco_cp=>sy->time( xco_cp_time=>time_zone->user
                                    )->as( xco_cp_time=>format->iso_8601_extended
                                    )->value
                      )->add_period(
                      )->add_space(
                      )->add_text( `Have`
                      )->add_space(
                      )->add_text( `a`
                      )->add_space(
                      )->add_text( `nice`
                      )->add_space(
                      )->add_text( `day`
                      )->add_period(
                      )->text.

    out->write( text2 ).

    "----------------------------------------------------------------
    "-------- Method chaining with a standalone statement -----------
    "----------------------------------------------------------------

    "In the example, the final method call in the chain receives
    "the classrun instance available in the implementation of the
    "if_oo_adt_classrun~main method. The method implementation
    "includes the writing to the console.

    "Console output: Lorem ipsum dolor sit amet
    NEW zcl_some_class( )->add_text( `Lorem`
                        )->add_space(
                        )->add_text( `ipsum`
                        )->add_space(
                        )->add_text( `dolor`
                        )->add_space(
                        )->add_text( `sit`
                        )->add_space(
                        )->add_text( `amet`
                        )->display_text( out ).

  ENDMETHOD.

  METHOD add_text.
    text &&= str.
    ref = me.
  ENDMETHOD.

  METHOD add_space.
    text &&= ` `.
    ref = me.
  ENDMETHOD.

  METHOD display_text.
    cl_run_ref->write( text ).
  ENDMETHOD.

  METHOD add_period.
    text &&= `.`.
    ref = me.
  ENDMETHOD.

  METHOD return_text.
    str = me->text.
  ENDMETHOD.

ENDCLASS.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>


### Excursion: Example Class

Expand the following collapsible section for an example class. The commented example class explores various aspects covered in the previous sections. You can create a demo class called `zcl_demo_test` and copy and paste the following code. Once activated, you can choose *F9* in ADT to run the class. The example is designed to display output in the console that shows the result of calling different methods.

<details>
  <summary>🟢 Click to expand for example code</summary>
  <!-- -->

<br>

```abap
CLASS zcl_demo_test DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.

    "------------------------ Attributes ------------------------
    "Instance attributes
    DATA: inst_attr   TYPE utclong,
          inst_string TYPE string.

    "Static attribute
    CLASS-DATA stat_attr TYPE utclong.

    "Attribute with the READ-ONLY addition. It is also possible for instance
    "attributes. Such an attribute can only be read from outside the class,
    "not changed. Inside the class, it can be changed. This also applies to
    "subclasses (note that the example class does not allow inheritance).
    CLASS-DATA read_only_attr TYPE string VALUE `read only` READ-ONLY.

    "------------------------ Methods ------------------------
    "The parameter interfaces (signatures) of the methods are intended to
    "demonstrate various syntax options described in the cheat sheet.

    "Instance methods
    METHODS:
      "No parameter specified
      inst_meth1,

      "Single importing parameter
      inst_meth2 IMPORTING ip TYPE string,

      "Importing and exporting parameters
      inst_meth3 IMPORTING ip1 TYPE i
                           ip2 TYPE i
                 EXPORTING ep  TYPE i,

      "Returning parameters
      inst_meth4 RETURNING VALUE(ret) TYPE string,

      inst_meth5 IMPORTING ip1        TYPE string
                           ip2        TYPE string
                 EXPORTING ep         TYPE string
                 RETURNING VALUE(ret) TYPE string,

      "Changing parameter
      inst_meth6 CHANGING chg TYPE string,

      "Raising exceptions
      inst_meth7 IMPORTING ip1        TYPE i
                           ip2        TYPE i
                 RETURNING VALUE(ret) TYPE i
                 RAISING   cx_sy_arithmetic_overflow,

      inst_meth8 IMPORTING ip1        TYPE i
                 RETURNING VALUE(ret) TYPE string
                 RAISING   cx_uuid_error,

      "Instance constructor
      "Instance constructors can optionally have importing parameters
      "and raise exceptions.
      constructor.

    "Static methods
    CLASS-METHODS:
      "Options of formal parameter definitions
      stat_meth1 IMPORTING REFERENCE(ip1) TYPE string  "pass by reference (specifying REFERENCE(...) is optional)
                           ip2            TYPE string  "pass by reference
                           VALUE(ip3)     TYPE string  "pass by value
                 RETURNING VALUE(ret)     TYPE string, "pass by value (mandatory for returning parameters)

      "OPTIONAL/DEFAULT additions
      "Both additions denote that passing values is optional. DEFAULT: If not supplied,
      "the default value specified is used.
      stat_meth2 IMPORTING ip1        TYPE string DEFAULT `ABAP`
                           ip2        TYPE string OPTIONAL
                 RETURNING VALUE(ret) TYPE string_table,

      "Generic types are possible for field symbols and method parameters
      "All of the previous formal parameters are typed with complete types (e.g. type i).
      "The following method includes several formal parameters typed with generic
      "types. Find more information in the 'Data Types and Objects' cheat sheet.
      "Note: Returning parameters must be completely typed.
      stat_meth3 IMPORTING ip_data      TYPE data      "Any data type
                           ip_clike     TYPE clike     "Character-like data type (such as c, n, string, etc.)
                           ip_numeric   TYPE numeric   "Numeric type (such as i, p, decfloat34 etc.)
                           ip_any_table TYPE ANY TABLE "Any table type (standard, sorted, hashed)
                 RETURNING VALUE(ret)   TYPE string,   "No generic type possible for returning parameters

      "Static constructor
      "No parameters possible
      class_constructor.
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.



CLASS zcl_demo_test IMPLEMENTATION.
  METHOD if_oo_adt_classrun~main.

    "Note:
    "This is a self-contained example. Usually, you must create an instance
    "of a class first before using instance methods - when calling methods
    "from outside, e.g. from another class. Within the class itself, you can
    "indeed call the instance methods without a prior instance creation.
    "To demonstrate 'calls from external', an instance of the class is
    "nevertheless created in the example.

    "--------------- Constructors ---------------

    "Instance constructor: Automatically called when a class is instantiated
    "and an instance is created.
    "Creating an instance of a class and accessing an instance attribute
    "using the object component selector ->.
    DATA(oref) = NEW zcl_demo_test( ).
    out->write( data = oref->inst_attr name = `oref->inst_attr` ).

    "Creating more instances
    "The example is implemented in a way that an instance attribute
    "is assigned a time stamp when the instance constructor is called.
    "As instance constructors are called once for each instance, the
    "inst_attr values differ.
    DATA(oref2) = NEW zcl_demo_test( ).
    out->write( data = oref2->inst_attr name = `oref2->inst_attr` ).

    DATA(oref3) = NEW zcl_demo_test( ).
    out->write( data = oref3->inst_attr name = `oref3->inst_attr` ).

    "Static constructor: Automatically and immediately called once for each class
    "when calling a class for the first time in an internal session (e.g. an instance
    "is created or a component is used).
    "The example is implemented in a way that a static attribute is assigned a time
    "stamp when the static constructor is called. The class was called with creating
    "an instance above, and so the static constructor was called once. There is no new
    "time stamp assigment, no new calls of the static constructor in this internal session.
    "Therefore, the value of stat_attr is the same.
    "The access is done using the class name, the class component selector =>, and
    "the attribute name.
    out->write( data = zcl_demo_test=>stat_attr name = `zcl_demo_test=>stat_attr` ).

    "Static attributes are also accessible via the object reference variable
    out->write( data = oref->stat_attr name = `oref->stat_attr` ).

    "Checking that the values of the instance attribute that is modified when calling
    "the instance constructor differ from instance to instance.
    IF ( oref3->inst_attr > oref2->inst_attr )
    AND ( oref2->inst_attr > oref->inst_attr ).
      out->write( `Instance attribute check: All values differ.` ).
    ELSE.
      out->write( `Instance attribute check: At least one check is not successful.` ).
    ENDIF.

    "Checking that the value of the static attribute that is modified when calling
    "the static constructor is identical from instance to instance (it is only changed
    "when the class is called for the first time).
    IF ( oref3->stat_attr = oref2->stat_attr )
    AND ( oref2->stat_attr = oref->stat_attr )
    AND ( oref->stat_attr = zcl_demo_test=>stat_attr ).
      out->write( `Static attribute check: All values are identical.` ).
    ELSE.
      out->write( `Static attribute check: At least one check is not successful.` ).
    ENDIF.

    "Excursion: See the note above. In the self-contained example, in this class itself, the
    "components can be called without reference variable or providing the class name. The
    "assumption in the following snippets of the example is that the class is called
    "from outside and instances are created outside of the class, so the variable/class
    "name are provided.
    "The following access is possible in the same class (not outside of this class):
    DATA(a) = inst_attr.
    DATA(b) = stat_attr.

    "The following is also possible inside the class (it is the only option outside of
    "this class):
    DATA(c) = oref->inst_attr.
    DATA(d) = zcl_demo_test=>stat_attr.
    DATA(e) = oref->stat_attr.

    "--------------- Method calls ---------------

    "Calling instance methods
    "Instance methods are called using the object component selector ->
    "via reference variables.

    "--- Method without parameters ---
    oref->inst_meth1( ).

    "To show an effect of the method call in the example, the method implementation
    "simply includes the change of an instance attribute value.
    out->write( data = oref->inst_string name = `oref->inst_string` ).

    "Notes:
    "- See the method implementation of inst_meth1. It shows that
    "  instance methods can access both static and instance attributes.
    "- As mentioned above regarding the attributes, in the same class and
    "  in this example, you can call the methods directly (without using
    "  a reference variable).
    inst_meth1( ).

    "--- Methods that specify importing parameters ---
    "Similar to the inst_meth1 method, the implementation includes the
    "change of an instance attribute.
    "Notes:
    "- In the method call, the caller exports values to the
    "  method having importing parameters defined. Therefore, the addition
    "  EXPORTING is relevant for the caller.
    "- If a method only specifies importing parameters, specifying EXPORTING
    "  is optional.
    "- If a method only specifies a single importing parameter, specifying
    "  EXPORTING and the formal parameter name is optional.

    "Method with a single importing parameter (the following three method
    "calls are basically the same)
    "Method call that specifies EXPORTING and the formal parameter name
    oref->inst_meth2( EXPORTING ip = `hello` ).

    out->write( data = oref->inst_string name = `oref->inst_string` ).

    "Method call that specifies the formal parameter, without EXPORTING
    oref->inst_meth2( ip = `world` ).

    out->write( data = oref->inst_string name = `oref->inst_string` ).

    "Method call that only includes the actual parameter
    oref->inst_meth2( `ABAP` ).

    out->write( data = oref->inst_string name = `oref->inst_string` ).

    "--- Methods that specify exporting parameters ---
    "For the method call, specify EXPORTING for importing parameters,
    "and IMPORTING for exporting parameters.
    "The method implementation performs a calculation. The calculation
    "result is assigned to the exporting parameter. You can assign the
    "value to a suitable data object.
    DATA calc_result1 TYPE i.
    oref->inst_meth3( EXPORTING ip1 = 5
                                ip2 = 3
                      IMPORTING ep = calc_result1 ).

    out->write( data = calc_result1 name = `calc_result1` ).

    "Inline declaration is also possible.
    oref->inst_meth3( EXPORTING ip1 = 2
                                ip2 = 4
                      IMPORTING ep = DATA(calc_result2) ).

    out->write( data = calc_result2 name = `calc_result2` ).

    "--- Methods that specify returning parameters ---
    DATA(result1) = oref->inst_meth4( ).
    out->write( data = result1 name = `result1` ).

    "The RECEIVING addition is available in standalone method
    "calls only if methods are defined with a returning parameter.
    "Inline declaration is also possible here.
    oref->inst_meth4( RECEIVING ret = DATA(result2) ).
    out->write( data = result2 name = `result2` ).

    "The following example method specifies multiple parameters,
    "among them 2 output parameters (exporting and reporting).

    "Functional method call
    "In a functional method call, inline declaration is not possible
    "for 'ep'.
    DATA str1 TYPE string.
    DATA(str2) = oref->inst_meth5( EXPORTING ip1 = `AB`
                                             ip2 = `AP`
                                   IMPORTING ep = str1 ).

    out->write( data = str1 name = `str1` ).
    out->write( data = str2 name = `str2` ).

    "Standalone method call (including inline declarations)
    oref->inst_meth5( EXPORTING ip1 = `AB`
                                ip2 = `AP`
                      IMPORTING ep = DATA(str3)
                      RECEIVING ret = DATA(str4) ).

    out->write( data = str3 name = `str3` ).
    out->write( data = str4 name = `str4` ).

    "Returning parameters enable ...
    "... the use of method calls in other statements, for example,
    "in logical expressions, instead of storing the method call
    "result in an extra variable.
    IF oref->inst_meth4( ) IS INITIAL.
      out->write( `Initial` ).
    ELSE.
      out->write( `Not initial` ).
    ENDIF.

    "... method chaining to write more concise code and avoid
    "declaring helper variables.
    "The following example uses a class that creates random integers.
    "The 'create' method has a returning parameter. It returns an
    "instance of the class (an object reference) based on which
    "more methods can be called. Using method chaining, you can
    "do the following in one go.
    DATA(inst) = cl_abap_random_int=>create( seed = cl_abap_random=>seed( )
                                             min  = 1
                                             max  = 10 ).
    DATA(random_integer1) = inst->get_next( ).

    DATA(random_integer2) = cl_abap_random_int=>create( seed = cl_abap_random=>seed( )
                                                        min  = 1
                                                        max  = 10 )->get_next( ).

    out->write( data = random_integer1 name = `random_integer1` ).
    out->write( data = random_integer2 name = `random_integer2` ).

    "--- Method that specifies a changing parameter ---
    "Changing parameters should be reserved for changing an existing
    "local variable and value.
    "The method implementation includes the demonstration of the
    "self-reference 'me'. For this purpose, a data object is created
    "in the method implementation that has the same name as a data
    "object declared in the class's declaration part.

    "Changing the value of the instance attribute with the same name
    "as the local data object in the method implementation.
    oref->inst_string = `TEST`.

    DATA local_var TYPE string VALUE `hello`.
    oref->inst_meth6( CHANGING chg = local_var ).

    out->write( data = local_var name = `local_var` ).

    "--- Methods that specify RAISING ---
    "The following example method declares an exception of the category
    "CX_DYNAMIC_CHECK. That is, the check is not performed until runtime.
    "There is no syntax warning shown at compile time.
    "The ipow function is included in the method implementation. The
    "second example raises the exception.

    "No TRY control structure, no syntax warning at compile time. However,
    "the calculation works.
    DATA(power_res1) = oref->inst_meth7( ip1 = 5 ip2 = 2 ).
    out->write( data = power_res1 name = `power_res1` ).

    "The example raises the exception because the resulting number is too high.
    "Not catching the exception results in a runtime error.
    TRY.
        DATA(power_res2) = oref->inst_meth7( ip1 = 10 ip2 = 10 ).
        out->write( data = power_res2 name = `power_res2` ).
      CATCH cx_sy_arithmetic_overflow.
        out->write( `cx_sy_arithmetic_overflow was raised` ).
    ENDTRY.

    "The following example method declares an exception of the category
    "CX_STATIC_CHECK. That is, it is statically checked. Without the
    "TRY control structure and catching the exception, a syntax warning
    "is displayed. And in the case of the example implementation,
    "the exception is indeed raised. Not catching the exception results
    "in a runtime error.
    TRY.
        DATA(test) = oref->inst_meth8( ip1 = 1 ).
        out->write( data = test name = `test` ).
      CATCH cx_uuid_error.
        out->write( `cx_uuid_error was raised` ).
    ENDTRY.

    "A syntax warning is displayed for the following method call.
    "DATA(test2) = oref->inst_meth8( ip1 = 1 ).

    "Calling static methods
    "The method definitions/implementations cover further aspects.

    "--- Pass by reference/value ---
    "The following example method emphasizes pass by reference and
    "by value.
    "Notes:
    "- Returning parameters can only be declared with VALUE(...)
    "- When passing by reference, the content of the data objects
    "  cannot be changed in the method implementation.
    "- The method implementation includes that ...
    "  - attributes declared with READ-ONLY can be changed within
    "    the class they are declared.
    "  - static methods can only access static attributes.
    DATA(res) = zcl_demo_test=>stat_meth1( ip1 = `a` "pass by reference (declaration with REFERENCE(...))
                                           ip2 = `b` "pass by reference (without REFERENCE(...))
                                           ip3 = `c` "pass by value (declaration with VALUE(...))
                                         ).
    out->write( data = res name = `res` ).

    "--- OPTIONAL/DEFAULT additions ---
    "The method implementation includes the predicate expression IS SUPPLIED
    "that checks whether a formal parameter is populated.

    DATA(res_tab1) = zcl_demo_test=>stat_meth2( ip1 = `aaa` ip2 = `bbb` ).
    out->write( data = res_tab1 name = `res_tab1` ).

    DATA(res_tab2) = zcl_demo_test=>stat_meth2( ip1 = `ccc` ).
    out->write( data = res_tab2 name = `res_tab2` ).

    DATA(res_tab3) = zcl_demo_test=>stat_meth2( ip2 = `ddd` ).
    out->write( data = res_tab3 name = `res_tab3` ).

    DATA(res_tab4) = zcl_demo_test=>stat_meth2( ).
    out->write( data = res_tab4 name = `res_tab4` ).

    "--- Generically typed formal parameters ---
    "In the following method calls, various data objects are
    "assigned to formal parameters. Note that returning parameters
    "must be completely typed.
    "In the example, the value passed for parameter ip_clike (which is
    "convertible to type string) is returned.
    DATA(res_gen1) = zcl_demo_test=>stat_meth3( ip_data = VALUE string_table( ( `hi` ) ) "any data type
                                                ip_clike = abap_true "Character-like data type (such as c, n, string, etc.)
                                                ip_numeric = 1 "Numeric type (such as i, p, decfloat34 etc.)
                                                ip_any_table = VALUE string_table( ( `ABAP` ) ) "Any table type (standard, sorted, hashed)
                                              ).

    out->write( data = res_gen1 name = `res_gen1` ).

    DATA(res_gen2) = zcl_demo_test=>stat_meth3( ip_data = 123
                                                ip_clike = 'ABAP'
                                                ip_numeric = CONV decfloat34( '1.23' )
                                                ip_any_table = VALUE string_hashed_table( ( `hello` ) ( `world` ) )
                                              ).

    out->write( data = res_gen2 name = `res_gen2` ).

  ENDMETHOD.

  METHOD class_constructor.
    "Assigning the current UTC timestamp to a static attribute
    stat_attr = utclong_current( ).
  ENDMETHOD.

  METHOD constructor.
    "Assigning the current UTC timestamp to an instance attribute
    inst_attr = utclong_current( ).
  ENDMETHOD.

  METHOD inst_meth1.
    inst_string = `Changed in inst_meth1`.

    "Instance methods can access both static and instance attributes.
    DATA(a) = inst_attr.
    DATA(b) = stat_attr.
  ENDMETHOD.

  METHOD inst_meth2.
    inst_string = |Changed in inst_meth2. Content of passed string: { ip }|.
  ENDMETHOD.

  METHOD inst_meth3.
    ep = ip1 + ip2.
  ENDMETHOD.

  METHOD inst_meth4.
    ret = |This string was assigned to the returning parameter at { utclong_current( ) }|.
  ENDMETHOD.

  METHOD inst_meth5.
    ep = |Strings '{ ip1 }' and '{ ip2 }' were assigned to the exporting parameter at { utclong_current( ) }|.
    ret = |Strings '{ ip1 }' and '{ ip2 }' were assigned to the returning parameter at { utclong_current( ) }|.
  ENDMETHOD.

  METHOD inst_meth6.
    "Demonstrating the self-reference 'me'
    "Its use is optional. The following data object intentionally
    "has the same name as an instance attribute specified in the
    "class's declaration part.
    DATA inst_string TYPE string.
    inst_string = `Local string`.

    chg = |The local data object was changed: '{ to_upper( chg ) }'\nChecking the self-reference me:\ninst_string: '{ inst_string }'\nme->inst_string: '{ me->inst_string }'|.
  ENDMETHOD.

  METHOD inst_meth7.
    ret = ipow( base = ip1 exp = ip2 ).
  ENDMETHOD.

  METHOD inst_meth8.
    IF ip1 = 1.
      RAISE EXCEPTION TYPE cx_uuid_error.
    ELSE.
      ret = `No exception was raised.`.
    ENDIF.
  ENDMETHOD.

  METHOD stat_meth1.
    "Static methods can only access static attributes.
    "DATA(test1) = inst_attr.
    DATA(test2) = stat_attr.

    "Only read access possible when parameters are passed by value
    DATA(a) = ip1.
    DATA(b) = ip2.

    "Write access is not possible (however, if you need to work with them
    "and change the content, you can create copies as above)
    "ip1 = `y`.
    "ip2 = `z`.

    "Pass by value, modification is possible
    ip3 = to_upper( ip3 ) && `##`.

    "Modifying a read only attribute is possible in the class
    "in which it is declared.
    read_only_attr = `Read-only attribute was modified`.

    ret = |ip1 = '{ ip1 }', ip2 = '{ ip2 }', ip3 (modified) = '{ ip3 }' / read_only_attr = '{ read_only_attr }'|.
  ENDMETHOD.

  METHOD stat_meth2.
    "Using IS SUPPLIED in an IF control structure
    IF ip1 IS SUPPLIED.
      APPEND |ip1 is supplied, value: '{ ip1 }'| TO ret.
    ELSE.
      APPEND |ip1 is not supplied, value: '{ ip1 }'| TO ret.
    ENDIF.

    "Using IS SUPPLIED with the COND operator
    APPEND COND #( WHEN ip2 IS SUPPLIED
                   THEN |ip2 is supplied, value: '{ ip2 }'|
                   ELSE |ip2 is not supplied, value: '{ ip2 }'| ) TO ret.
  ENDMETHOD.

  METHOD stat_meth3.
    "You may check the content in the debugger.
    DATA(a) = REF #( ip_data ).
    DATA(b) = REF #( ip_clike ).
    DATA(c) = REF #( ip_numeric ).
    DATA(d) = REF #( ip_any_table ).

    ret = ip_clike.
  ENDMETHOD.

ENDCLASS.
```

</details> 




<p align="right"><a href="#top">⬆️ back to top</a></p>


## Inheritance

-   Concept: Deriving a new class (i. e.
    [subclass](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abensubclass_glosry.htm "Glossary Entry"))
    from an existing one
    ([superclass](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abensuperclass_glosry.htm "Glossary Entry")).
- In doing so, you create a hierarchical relationship between superclasses and subclasses
    (an [inheritance hierarchy](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninheritance_hierarchy_glosry.htm "Glossary Entry")) to form an [inheritance
    tree](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninheritance_tree_glosry.htm "Glossary Entry"). This is relevant for a class that can have multiple subclasses and one direct superclass.
-   Subclasses ...
    -   inherit and thus adopt all components from superclasses.
    -   can be made more specific by declaring new components and
        redefining instance methods (i. e. you can alter the implementation of inherited methods). In case a subclass has no further components, it contains exactly the components of the superclass - but the ones of the private visibility section are not visible there.
    - can redefine the public and protected instance methods of all preceding superclasses. Note: Regarding the static components of superclasses, accessing them is possible but not redefining them.
    - can themselves have multiple direct subclasses but only one direct superclass.
-   Components that are changed or added to subclasses are not visible to superclasses, hence, these changes are only relevant for the class itself and its subclasses.
-   Classes can rule out derivation: classes cannot inherit from classes that are specified with the addition
        [`FINAL`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapmethods_abstract_final.htm#!ABAP_ADDITION_2@2@)
        (e. g. `CLASS global_class DEFINITION PUBLIC FINAL CREATE PUBLIC. ...`).

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Inheritance-Related Syntax

The table below includes selected syntax related to inheritance in class and method declarations.  

> **💡 Note**<br>
> - Some of the syntax options have already been mentioned previously. This is to summarize. 
> - Here, the emphasis is on global classes.
> - The snippets provided do not represent all possible syntax combinations. For the complete picture, refer to the ABAP Keyword Documentation. Additional syntax options are available in the context of friendship (`GLOBAL FRIENDS/FRIENDS`), testing (`FOR TESTING`), [RAP](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenarap_glosry.htm) (`FOR BEHAVIOR OF`; to declare [ABAP behavior pools](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenbehavior_pool_glosry.htm)), and more.
> - The order of the additions can vary.


**Declarations in Classes**

<table>

<tr>
<td> Syntax Example </td> <td> Details </td>
</tr>

<tr>
<td> 

``` abap
CLASS zcl_demo DEFINITION     
  PUBLIC
  FINAL
  CREATE PUBLIC .
``` 

 </td>
<td>

<br>

- `... PUBLIC ...`: Specifies that the class is a global class, available globally within the class library. Most of the subsequent snippets use the `PUBLIC` addition as the focus is on global classes.
- `... FINAL ...`: Specifies that the class cannot have any subclasses, effectively prohibiting inheritance. This addition seals off a branch of the inheritance tree. In final classes, all methods are automatically final.
- `... CREATE PUBLIC ...`: Specifies that the class can be instantiated wherever it is visible.

</td>
</tr>

<tr>
<td> 

``` abap
CLASS zcl_demo DEFINITION   
  PUBLIC
  CREATE PUBLIC .
``` 

 </td>
<td>

<br>

This class permits inheritance because it does not include the `FINAL` addition. Subclasses can be derived from this superclass.

</td>
</tr>

<tr>
<td> 

``` abap
CLASS zcl_demo DEFINITION    
  PUBLIC
  CREATE PROTECTED .
``` 

 </td>
<td>

<br>

- This class permits inheritance because it does not include the `FINAL` addition. 
- `... CREATE PROTECTED ...`: Specifies that the class can only be instantiated within its own methods, its subclasses' methods, or those of its friends.

</td>
</tr>

<tr>
<td> 

``` abap
CLASS zcl_demo DEFINITION    
  FINAL
  CREATE PRIVATE .
``` 

 </td>
<td>

<br>

- This class does not permit inheritance because it includes the `FINAL` addition.
- `... CREATE PRIVATE ...`: Specifies that the class can only be instantiated within its own methods or those of its friends. It cannot be instantiated as a component of (not befriended) subclasses.
- Consider the implications of defining a superclass in this manner:
  - External users cannot instantiate a subclass.
  - If inheritance is allowed, subclasses cannot instantiate themselves though. This is because they cannot access the superclass's instance constructor, preventing the creation of subclass instances. However, this can be altered if the subclass is a friend of the superclass.
  - Similarly, subclass objects cannot be created within their superclass if declared using `CREATE PROTECTED` or `CREATE PRIVATE`. This is only possible if the superclasses are friends with their subclasses.
- The `FINAL` addition can be beneficial with `CREATE PRIVATE` to prevent the derivation of subclasses.
- Note: In each class, the `CREATE PUBLIC`, `CREATE PROTECTED`, and `CREATE PRIVATE` additions of the `CLASS` statement control who can create an instance of the class and who can call its instance constructor.


</td>
</tr>

<tr>
<td> 

``` abap
CLASS zcl_demo DEFINITION     
  PUBLIC
  ABSTRACT
  CREATE ...
``` 

 </td>
<td>

<br>

- `... ABSTRACT ...`:
  - Defines abstract classes
  - Abstract classes cannot be instantiated.
  - To use the instance components of an abstract class, you can instantiate a subclass of that class.
  - Abstract classes may contain both abstract and concrete instance methods. However, abstract methods are not implemented within abstract classes.
  - By adding the `FINAL` addition, abstract classes can be made final. In these cases, only static components are usable. While instance components may be declared, they are not usable.

</td>
</tr>

<tr>
<td> 

``` abap
CLASS zcl_sub DEFINITION       
  INHERITING FROM zcl_demo       
  ...
``` 

 </td>
<td>

<br>

- `... INHERITING FROM ...`: 
  - Can be specified in subclasses inheriting from visible superclasses  
  - If not specified, the class implicitly inherits from the predefined, empty, abstract class `OBJECT` (the root object).
  - A subclass inherits all components of the superclasses. 
    - For example, if an internal table `itab` is declared as a static component in superclass `zcl_super`, subclasses can refer to `itab` directly, not necessarily by specifying the class name as with `zcl_super=>itab` (which is also possible). 
    - If the superclass defines a type, subclasses cannot define a type with the same name.
  - The visibility of the components remains unchanged. 
  - Only the public and protected components of the superclass are visible in the subclass.
  - Private components of superclasses are inaccessible in subclasses.
  - The properties of inherited components are immutable. However, subclasses can declare additional components (with unique names) and redefine inherited methods without altering the interface.
  - Upon instantiation of a subclass, all superclasses are also instantiated, ensuring the initialization of superclass attributes through calling superclass constructors.

</td>
</tr>


</table>


**Declarations in Instance Methods**

<table>

<tr>
<td> Syntax Example </td> <td> Details </td>
</tr>

<tr>
<td> 

``` abap
METHODS some_meth FINAL ...    
``` 

 </td>
<td>

<br>

- Declares final methods
- These methods cannot be overridden in subclasses.
- Note: In final classes, all methods are inherently final. Therefore, the `FINAL` addition cannot be specified. Instance constructors are always final, but the use of the `FINAL` addition is optional.

</td>
</tr>

<tr>
<td> 

``` abap
METHODS some_meth ABSTRACT ...    
``` 

 </td>
<td>

<br>

- Declares abstract methods
- Can only be used in abstract classes
- You can implement these methods in a subclass (by redefining using the `REDEFINITION`addition), not in the abstract class itself. When declared, there is no implementation part in the abstract class.  
- All instance methods can be declared as abstract, except for instance constructors.
- Private methods cannot be redefined and can therefore not be declared as abstract.
- If abstract methods are declared in classes that are both abstract and final, they cannot be implemented. Therefore, the methods are not usable.
- In interfaces, methods are implicitly abstract as interfaces do not contain method implementations.

</td>
</tr>


<tr>
<td> 

``` abap
"Instance constructor
METHODS constructor. 
"Static constructor
CLASS-METHODS class_constructor.
``` 

 </td>
<td>

<br>

- Instance constructors (`constructor`):
  - Subclasses cannot redefine the instance constructors of superclasses.
  - These constructors are automatically invoked when creating an object, not explicitly called.
  - In inheritance, a subclass's instance constructor must call the instance constructors of all its superclasses. This requires calling `super->constructor( ).` to call the instance constructor of the direct superclass, even if the superclass does not explicitly declare the instance constructor. Note that any non-optional importing parameters must be filled.
- Static constructors (`class_constructor`):
  - These constructors are implicitly available in all classes, whether declared or not.
  - They are called when creating a class instance for the first time in an ABAP program or when addressing a static component, excluding types and constants.
  - In inheritance, the static constructors of all classes up the inheritance tree are called first.
  - A static constructor can only be called once during program runtime.


</td>
</tr>


<tr>
<td> 

``` abap
METHODS some_meth REDEFINITION.           
METHODS another_meth FINAL REDEFINITION.      
``` 

 </td>
<td>

<br>

- Specified in subclasses to redefine inherited methods from superclasses.
- The method's implementation is expected to reimplement the inherited method. However, the subclass's new implementation conceals the superclass's implementation.
- The redefined method accesses the private components of its class, not any similarly named private components in the superclass.
- The superclass's implementation can be called in the redefined method using the [pseudo reference](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenpseudo_reference_glosry.htm "Glossary Entry") `super->meth( ).`. Note that non-optional importing parameters must be filled.
- The redefinition is valid for subclasses until the method is redefined again.
- The `FINAL` addition can be specified, preventing further redefinition of the method in other subclasses.

</td>
</tr>

</table>

<p align="right"><a href="#top">⬆️ back to top</a></p>


### Excursion: Inheritance Example

> **💡 Note**<br>
> This example is also included in the ABAP cheat sheet repository: [zcl_demo_abap_oo_inheritance_1](./src/zcl_demo_abap_oo_inheritance_1.clas.abap)

Expand the following collapsible section for example classes. The example classes explore inheritance and demonstrate a selection of the inheritance-related syntax described above. The inheritance tree consists of four example classes. The base class includes the implementation of the classrun interface. The example is designed to output information to the console. So, you can execute this class using F9 in ADT.
The purpose of the example and information output is to visualize and explore concepts and syntax related to inheritance, checking out when and how methods are called, redefining methods, abstract and final classes and methods.


<details>
  <summary>🟢 Click to expand for more information and example code</summary>
  <!-- -->

<br>

The inheritance tree of the example classes is as follows: 

```
ZCL_DEMO_ABAP_OO_INHERITANCE_1
  |
  |--ZCL_DEMO_ABAP_OO_INHERITANCE_2
  |   |
  |   |--ZCL_DEMO_ABAP_OO_INHERITANCE_3
  |   |   |
  |   |   |--ZCL_DEMO_ABAP_OO_INHERITANCE_4
```

Notes on the example: 
- All classes include instance and static constructor declarations.
- Many instance methods are declared in all classes to demonstrate inheritance. However, there is no meaningful implementation in these methods in all classes. All instance methods include the same code. 
  - The purpose of the code in the method implementations is to add a line to a log table (which is output to the console) with various pieces of information: 
      - Name of the method that is called 
      - In which class the method is implemented when it is called
      - From which class the method is called
      - Whether the method is inherited, redefined, final, or a static method
      - Visibility of the method
      - Time stamp of when the method is called 
  - The information retrieval is implemented in a static method in the `ZCL_DEMO_ABAP_OO_INHERITANCE_1` class by getting callstack information to determine which method in which class was called by whom. Based on the retrieved class and method names, RTTI is used to get detailed information about the methods.
- `ZCL_DEMO_ABAP_OO_INHERITANCE_1`
  - Allows inheritance and represents the root class of the inheritance hierarchy
  - Declares several instance methods in each visibility section
    - One of them is declared with `FINAL`, so no redefinition is possible in subclasses.
  - Includes the implementation of the classrun interface meaning this class is executable using F9 in ADT.
    - The class includes an internal table that represents a log table and that is output to the console as described above.    
- `ZCL_DEMO_ABAP_OO_INHERITANCE_2`
  - Inherits from `ZCL_DEMO_ABAP_OO_INHERITANCE_1` and allows inheritance itself 
  - Specifies `CREATE PROTECTED`, so the class can only be instantiated in methods of its subclasses, of the class itself, and of its friends   
    - You may want to try to create an instance of the class in `ZCL_DEMO_ABAP_OO_INHERITANCE_1` like this `DATA(oref) = NEW zcl_demo_abap_oo_inheritance_2( ).` It is not possible. In `ZCL_DEMO_ABAP_OO_INHERITANCE_3` and `ZCL_DEMO_ABAP_OO_INHERITANCE_4`, for example, it is possible.
  - Declares several instance methods
    - One of them is declared with `FINAL`, so no redefinition is possible in subclasses
    - Instance methods of the direct superclass are redefined
      - Note: Private methods of superclasses cannot be redefined. You cannot specify abstract methods, which is only possible in abstract classes. Abstract methods are generally not possible in the private visibility section since they cannot be redefined.
   - Declares a static method to delegate method calls of this class
     - The implementation includes the creation of an instance of the class and instance method calls (including redefined methods).
     - It is called in the classrun implementation in `ZCL_DEMO_ABAP_OO_INHERITANCE_1`.
- `ZCL_DEMO_ABAP_OO_INHERITANCE_3`
  - Inherits from `ZCL_DEMO_ABAP_OO_INHERITANCE_2` and thus from `ZCL_DEMO_ABAP_OO_INHERITANCE_1`     
  - Declared as abstract class using the `ABSTRACT` addition, so no instances can be created from the class
  - Declares several instance methods
    - Two abstract methods are included using the `ABSTRACT` addition, so they can only be implemented in subclasses (there is no implementation of these methods in the class) 
    - Instance methods of the direct superclass are redefined as well as methods from two levels up the inheritance hierarchy
    - One redefined method specifies `FINAL REDEFINITION`, so a further redefinition in subclasses is not possible.
- `ZCL_DEMO_ABAP_OO_INHERITANCE_4`
  - Inherits from `ZCL_DEMO_ABAP_OO_INHERITANCE_3` and thus from `ZCL_DEMO_ABAP_OO_INHERITANCE_2` and `ZCL_DEMO_ABAP_OO_INHERITANCE_1`
  - Specifies `FINAL` and so does not allow inheritance     
  - Declares several instance methods
    - Instance methods of the direct superclass, which is an abstract class, are redefined. It is mandatory to redefine the abstract methods. 
    - Other instance methods from further levels up the inheritance hierarchy are redefined (except one method that is declared with `FINAL REDEFINITION` in `ZCL_DEMO_ABAP_OO_INHERITANCE_3`)
    - For demonstration purposes, instance methods implemented in the abstract direct superclass (instances of abstract classes cannot be created) are called in the respective redefined methods by referring to the direct superclass using the syntax `super->...`.
  - Declares a static method to delegate method calls of this class


To try the example classes out, create four demo classes named 

- `ZCL_DEMO_ABAP_OO_INHERITANCE_1` 
- `ZCL_DEMO_ABAP_OO_INHERITANCE_2`
- `ZCL_DEMO_ABAP_OO_INHERITANCE_3`
- `ZCL_DEMO_ABAP_OO_INHERITANCE_4`

and paste the code into it. After activation, choose *F9* in ADT to execute the class `ZCL_DEMO_ABAP_OO_INHERITANCE_1`. The example is set up to display output in the console.


<br>

Class `ZCL_DEMO_ABAP_OO_INHERITANCE_1` 

```abap
CLASS zcl_demo_abap_oo_inheritance_1 DEFINITION
  PUBLIC
  CREATE PUBLIC .

  PUBLIC SECTION.
    "Classrun interface
    INTERFACES if_oo_adt_classrun.

    "Instance/static constructor declarations
    METHODS constructor.
    CLASS-METHODS class_constructor.

    "Instance method declarations
    METHODS meth_public_1.
    "Final method
    METHODS meth_public_1_final FINAL.

    "Components used for logging information about method calls
    TYPES: BEGIN OF s_log,
             method            TYPE string,
             implemented_where TYPE string,
             called_from       TYPE syrepid,
             is_inherited      TYPE abap_boolean,
             is_redefined      TYPE abap_boolean,
             is_final          TYPE abap_boolean,
             visibility        TYPE abap_visibility,
             is_static_method  TYPE abap_boolean,
             called_at         TYPE utclong,
           END OF s_log,
           t_log TYPE TABLE OF s_log WITH EMPTY KEY.

    CLASS-DATA log_tab TYPE t_log.
    CLASS-METHODS get_method_info RETURNING VALUE(info) TYPE s_log.

  PROTECTED SECTION.
    METHODS meth_protected_1.

  PRIVATE SECTION.
    METHODS meth_private_1.
ENDCLASS.



CLASS zcl_demo_abap_oo_inheritance_1 IMPLEMENTATION.
  METHOD if_oo_adt_classrun~main.

    "----- First level in the inheritance hierarchy ----
    "Creating an instance of the class
    DATA(oref_super) = NEW zcl_demo_abap_oo_inheritance_1( ).

    "Calling methods of the class
    oref_super->meth_public_1( ).
    oref_super->meth_public_1_final( ).
    oref_super->meth_protected_1( ).
    oref_super->meth_private_1( ).

    "----- Second level in the inheritance hierarchy ----
    "The instance creation and method calling is delegated to
    "a static method in the class
    zcl_demo_abap_oo_inheritance_2=>perform_meth_calls_2( ).

    "----- Third level in the inheritance hierarchy ----
    "Note: The class zcl_demo_abap_oo_inheritance_3 is abstract and contains
    "both non-abstract and abstract instance methods. Instances of abstract
    "classes cannot be created. So, the following statement is not possible.
    "DATA(oref_3) = NEW zcl_demo_abap_oo_inheritance_3( ).

    "Instance components of an abstract class can be accessed via its subclasses.
    "zcl_demo_abap_oo_inheritance_4 inherits from zcl_demo_abap_oo_inheritance_3 and
    "redefines methods of zcl_demo_abap_oo_inheritance_3. Both abstract methods (which
    "are mandatory to implement) and non-abstract methods are redefined. To also access
    "the method implementations of the non-abstract instance methods of
    "zcl_demo_abap_oo_inheritance_3, the respective implementations of the redefined
    "methods in zcl_demo_abap_oo_inheritance_4 include method calls to the direct
    "superclass using the syntax super->meth( ).. The instance methods of
    "zcl_demo_abap_oo_inheritance_3 are called in the context of the static method call
    "via zcl_demo_abap_oo_inheritance_4 below.

    "----- Fourth level in the inheritance hierarchy ----
    "As above, the instance creation and method calling is delegated to
    "a static method in the class. This method call includes method calls to
    "non-abstract instance methods implemented in zcl_demo_abap_oo_inheritance_3.
    zcl_demo_abap_oo_inheritance_4=>perform_meth_calls_4( ).

    "Writing the log table to the console
    out->write( data = log_tab name = `log_tab` ).

    "Excursion: Using RTTI to retrieve the name of the superclass
    "As this class starts an inheritance hierarchy, the superclass of this class
    "is the root class OBJECT.
    DATA(tdo_cl) = CAST cl_abap_classdescr( cl_abap_typedescr=>describe_by_name( 'ZCL_DEMO_ABAP_OO_INHERITANCE_1' ) ).
    DATA(superclass) = tdo_cl->get_super_class_type( )->get_relative_name( ).
    out->write( |\n\n| ).
    out->write( data = superclass name = `superclass` ).

  ENDMETHOD.

  METHOD class_constructor.
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD constructor.
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_private_1.
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_protected_1.
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_1.
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_1_final.
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD get_method_info.
    "This method retrieves callstack information to determine which method in which
    "class was called by whom.
    "Based on the retrieved class and method names, RTTI is used to get detailed
    "information about methods (such as the visibility or whether the method is
    "inherited, redefined, final, and a static method).

    "Getting callstack information
    DATA(call_stack_tab) = xco_cp=>current->call_stack->full( )->from->position( 2
                            )->to->position( 2 )->as_text( xco_cp_call_stack=>format->adt( )
                            )->get_lines( )->value.

    IF lines( call_stack_tab ) < 2.
      RETURN.
    ENDIF.

    LOOP AT call_stack_tab INTO DATA(wa) TO 2.
      DATA(tabix) = sy-tabix.
      SPLIT wa AT ` ` INTO TABLE DATA(entry).
      DELETE entry WHERE table_line IS INITIAL.

      DATA(class_name) = condense( val = entry[ 1 ] to = `` ).

      IF tabix = 1.
        info-implemented_where = class_name.

        DATA(meth_name) = condense( val = to_upper( entry[ 2 ] ) to = `` ).
        info-method = meth_name.

        IF class_name IS NOT INITIAL AND meth_name IS NOT INITIAL.
          DATA(tdo_cl) = CAST cl_abap_classdescr( cl_abap_typedescr=>describe_by_name( class_name ) ).
          DATA(methods_cl) = tdo_cl->methods.
          DATA(meth_info) = VALUE #( methods_cl[ name = meth_name ] OPTIONAL ).
          IF meth_info IS NOT INITIAL.
            info-is_inherited = meth_info-is_inherited.
            info-is_redefined = meth_info-is_redefined.
            info-is_final = meth_info-is_final.
            info-visibility = meth_info-visibility.
            info-is_static_method = meth_info-is_class.
          ENDIF.
        ENDIF.

      ELSE.
        info-called_from = class_name.
      ENDIF.
    ENDLOOP.

  ENDMETHOD.

ENDCLASS.
```

Class `ZCL_DEMO_ABAP_OO_INHERITANCE_2` 

```abap
CLASS zcl_demo_abap_oo_inheritance_2 DEFINITION
  INHERITING FROM zcl_demo_abap_oo_inheritance_1
  PUBLIC
  CREATE PROTECTED .

  PUBLIC SECTION.
    "Instance/static constructor declarations
    METHODS constructor.
    CLASS-METHODS class_constructor.

    "Instance method declarations
    METHODS meth_public_2.
    METHODS meth_public_2_final FINAL.

    "Static method declaration for display purposes
    CLASS-METHODS perform_meth_calls_2.

    "Redefining method from the class one level up in the inheritance hierarchy
    "(i.e. the direct superclass)
    METHODS meth_public_1 REDEFINITION.

    "Excursions:
    "- Redefining the final public method of the superclass is not possible.
    "- The same applies to constructors.
    "- The following type has the same name as a type in the superclass. Since components
    "  are inherited, the following declaration is not possible.
    "TYPES t_log TYPE string_table.
    "- Similary, the log table, which is a static component in the superclass, can be
    "  referenced in the method implementations using 'log_table'. Using the class name
    "  and => is also possible, but not required.
    "INSERT VALUE #( ) INTO TABLE zcl_demo_abap_oo_inheritance_1=>log_tab.

  PROTECTED SECTION.
    "Instance method declaration
    METHODS meth_protected_2.

    "Redefining method from the class one level up in the inheritance hierarchy
    "(i.e. the direct superclass)
    METHODS meth_protected_1 REDEFINITION.

  PRIVATE SECTION.
    "Ecursion:
    "- The following declarations are not possible.
    "- Private methods cannot be redefined.
    "METHODS meth_private_1 REDEFINITION.
    "- Abstract methods can only be declared in abstract classes. And, since
    "  private methods cannot be redefined, abstract private methods are not
    "  possible.
    "METHODS meth_private_2_abstract ABSTRACT.
ENDCLASS.



CLASS zcl_demo_abap_oo_inheritance_2 IMPLEMENTATION.
  METHOD class_constructor.
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD constructor.
    super->constructor( ).
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_2.
    "Method of this class
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_2_final.
    "Method of this class
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_protected_2.
    "Method of this class
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_1.
    "Reimplementing a method from the class one level up in the inheritance hierarchy (direct superclass)
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_protected_1.
    "Reimplementing a method from the class one level up in the inheritance hierarchy (direct superclass)
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD perform_meth_calls_2.
    "Method of this class
    "Creating an instance of the class
    DATA(oref_2) = NEW zcl_demo_abap_oo_inheritance_2( ).

    "Calling methods of this class
    oref_2->meth_public_2( ).
    oref_2->meth_public_2_final( ).
    oref_2->meth_protected_2( ).
    "Calling redefined methods from the class one level up in the inheritance hierarchy (direct superclass)
    oref_2->meth_protected_1( ).
    oref_2->meth_public_1( ).

  ENDMETHOD.

ENDCLASS.
```

Class `ZCL_DEMO_ABAP_OO_INHERITANCE_3` 

```abap
CLASS zcl_demo_abap_oo_inheritance_3 DEFINITION
  INHERITING FROM zcl_demo_abap_oo_inheritance_2
  PUBLIC
  ABSTRACT
  CREATE PUBLIC .

  PUBLIC SECTION.
    "Instance/static constructor declarations
    METHODS constructor.
    CLASS-METHODS class_constructor.

    "Instance method declarations
    METHODS meth_public_3.
    "Abstract method
    METHODS meth_public_3_abstract ABSTRACT.

    "Redefining methods from the class ...
    "... one level up in the inheritance hierarchy (i.e. the direct superclass)
    METHODS meth_public_2  REDEFINITION.
    "... two levels up in the inheritance hierarchy
    METHODS meth_public_1 REDEFINITION.

  PROTECTED SECTION.
    "Instance method declarations
    METHODS meth_protected_3.
    "Abstract method
    METHODS meth_protected_3_abstract ABSTRACT.

    "Redefining methods from the class ...
    "... one level up in the inheritance hierarchy (i.e. the direct superclass)
    METHODS meth_protected_2 REDEFINITION.
    "... two levels up in the inheritance hierarchy
    "Specifying the FINAL addition
    METHODS meth_protected_1 FINAL REDEFINITION.

  PRIVATE SECTION.
ENDCLASS.



CLASS zcl_demo_abap_oo_inheritance_3 IMPLEMENTATION.

  METHOD class_constructor.
     INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD constructor.
    super->constructor( ).
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_3.
    "Method of this class
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_protected_3.
    "Method of this class
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_2.
    "Reimplementing a method from the class one level up in the inheritance hierarchy (direct superclass)
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_protected_2.
    "Reimplementing a method from the class one level up in the inheritance hierarchy (direct superclass)
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_protected_1.
    "Reimplementing a method from the class two levels up in the inheritance hierarchy
    "Note that the method is specified with FINAL REDEFINITION. So, a further redefinition in subclasses is not possible.
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_1.
    "Reimplementing a method from the class two levels up in the inheritance hierarchy
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.
ENDCLASS.
```

Class `ZCL_DEMO_ABAP_OO_INHERITANCE_4` 

```abap
CLASS zcl_demo_abap_oo_inheritance_4 DEFINITION
  INHERITING FROM zcl_demo_abap_oo_inheritance_3
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    "Instance/static constructor declarations
    METHODS constructor.
    CLASS-METHODS class_constructor.

    "Instance method declaration
    METHODS meth_public_4.
    "Static method declaration for display purposes
    CLASS-METHODS perform_meth_calls_4.

    "Redefining methods from the class ...
    "... one level up in the inheritance hierarchy (i.e. the direct superclass)
    METHODS meth_public_3 REDEFINITION.
    "Note: Redefining the abstract method here is mandatory.
    METHODS meth_public_3_abstract REDEFINITION.
    "... two levels up in the inheritance hierarchy
    METHODS meth_public_2 REDEFINITION.
    "... three levels up in the inheritance hierarchy
    METHODS meth_public_1 REDEFINITION.

  PROTECTED SECTION.

    "Instance method declaration
    METHODS meth_protected_4.

    "Redefining methods from the class ...
    "... one level up in the inheritance hierarchy (i.e. the direct superclass)
    METHODS meth_protected_3 REDEFINITION.
    "Note: Redefining the abstract method here is mandatory.
    METHODS meth_protected_3_abstract REDEFINITION.
    "... two levels up in the inheritance hierarchy
    METHODS meth_protected_2 REDEFINITION.
    "... three levels up in the inheritance hierarchy
    "The meth_protected_1 method is specified with FINAL REDEFINITION in the
    "direct superclass. Therefore, a further redefinition is not possible.
    "The following statement is not possible.
    "METHODS meth_protected_1 REDEFINITION.

  PRIVATE SECTION.
ENDCLASS.



CLASS zcl_demo_abap_oo_inheritance_4 IMPLEMENTATION.

  METHOD class_constructor.
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD constructor.
    super->constructor( ).
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_4.
    "Method of this class
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_protected_4.
    "Method of this class
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_3.
    "Reimplementing a method from the class one level up in the inheritance hierarchy (direct superclass)
    "Calling this instance method that is redefined in the abstract direct superclass (instances of abstract classes cannot be created)
    "by referring to the direct superclass using the syntax super->...
    super->meth_public_3( ).
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_protected_3.
    "Reimplementing a method from the class one level up in the inheritance hierarchy (direct superclass)
    "This method is a non-abstract instance method of the abstract direct superclass. Instances of abstract classes
    "cannot be created. The syntax super->meth is used to also call instance methods of the abstract direct superclass
    "for output purposes.
    super->meth_protected_3( ).
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_3_abstract.
    "Implementating abstract methods are only possible in subclasses of abstract classes
    "Reimplementing a method from the class one level up in the inheritance hierarchy (direct superclass)
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_protected_3_abstract.
    "Implementating abstract methods are only possible in subclasses of abstract classes
    "Reimplementing a method from the class one level up in the inheritance hierarchy (direct superclass)
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_2.
    "Reimplementing a method from the class two levels up in the inheritance hierarchy
    "Calling this instance method that is redefined in the abstract direct superclass (instances of abstract
    "classes cannot be created) by referring to the direct superclass using the syntax super->....
    super->meth_public_2( ).
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_protected_2.
    "Reimplementing a method from the class two levels up in the inheritance hierarchy
    "Calling this instance method that is redefined in the abstract direct superclass (instances of abstract
    "classes cannot be created) by referring to the direct superclass using the syntax super->....
    super->meth_protected_2( ).
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD meth_public_1.
    "Reimplementing a method from the class three levels up in the inheritance hierarchy
    "Calling this instance method that is redefined in the abstract direct superclass (instances of abstract
    "classes cannot be created) by referring to the direct superclass using the syntax super->....
    super->meth_public_1( ).
    INSERT VALUE #( called_at = utclong_current( ) ) INTO TABLE log_tab ASSIGNING FIELD-SYMBOL(<fs>).
    <fs> = CORRESPONDING #( BASE ( <fs> ) get_method_info( ) EXCEPT called_at ).
  ENDMETHOD.

  METHOD perform_meth_calls_4.
    "Method of this class
    "Creating an instance of the class
    DATA(oref_4) = NEW zcl_demo_abap_oo_inheritance_4( ).

    "Calling methods of this class
    oref_4->meth_public_4( ).
    oref_4->meth_protected_4( ).
    "Calling redefined methods from the class ...
    "... one level up in the inheritance hierarchy (direct superclass)
    "Among them are abstract methods that can only be implemented in subclasses.
    "Note that the implementations of the non-abstract, redefined methods in this
    "class includes method calls of the abstract direct superclass so that
    "also these implementations are called for output purposes.
    oref_4->meth_public_3( ).
    oref_4->meth_public_3_abstract( ).
    oref_4->meth_protected_3( ).
    oref_4->meth_protected_3_abstract( ).
    "... two levels up in the inheritance hierarchy
    oref_4->meth_public_2( ).
    oref_4->meth_protected_2( ).
    "... three levels up in the inheritance hierarchy
    oref_4->meth_public_1( ).
    "Note: The following method call calls the method implementation in
    "class zcl_demo_abap_oo_inheritance_3. The method is specified with FINAL
    "REDEFINITION. So, it cannot be redefined in this class inheriting from
    "zcl_demo_abap_oo_inheritance_3.
    oref_4->meth_protected_1( ).
  ENDMETHOD.

ENDCLASS.
```

</details>  

<p align="right"><a href="#top">⬆️ back to top</a></p>

## Polymorphism and Casting (Upcast/Downcast)

The object orientation concept
[polymorphism](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenpolymorphism_glosry.htm "Glossary Entry")
means you can address differently implemented methods belonging to different objects of different classes using one and the
same reference variable, for example,
object reference variables pointing to a superclass can point to objects of a subclass.

Note the concept of static and dynamic type in this context:

-   Object reference variables (and also interface reference variables) have both a
    [static](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenstatic_type_glosry.htm "Glossary Entry")
    and a [dynamic
    type](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abendynamic_type_glosry.htm "Glossary Entry").
-   When declaring an object reference variable, e. g. `DATA oref TYPE REF TO cl`, you determine the static type, i. e.
    `cl` - a class - is used to declare the reference variable that is statically defined in the code. This is the class of an object to which the reference variable points to.
- Similarly, the dynamic type also defines the class of an object which the reference variable points to. However, the dynamic type is determined at runtime, i. e. the class of an object which the reference variable points to can change.
- Relevant for? This differentiation enters the picture in polymorphism when a reference variable typed with reference to a subclass can always be assigned to reference variables typed with reference to one of its superclasses or their interfaces. That's what is called [upcast](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenup_cast_glosry.htm "Glossary Entry") (or widening cast). Or the assignment is done the other way round. That's what is called [downcast](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abendown_cast_glosry.htm "Glossary Entry") (or narrowing cast).

> **✔️ Hints**<br>
> - The following basic rule applies: The static type is always more general than or the same as the dynamic type. The other way round: The dynamic type is always more special than or equal to the static type.
>- That means:
>  - If the static type is a class, the dynamic type must be the same class or one of its subclasses.
>  - If the static type is an interface, the dynamic type must implement the interface.

-   Regarding assignments: If it can be statically checked that an assignment is possible
    although the types are different, the assignment is done using the
    [assignment
    operator](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenassignment_operator_glosry.htm "Glossary Entry")
    `=` that triggers an upcast automatically.
-   Otherwise, it is a
    [downcast](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abendown_cast_glosry.htm "Glossary Entry").
    Here, the assignability is not checked until runtime. The downcast - in contrast to upcasts -
    must be triggered explicitly using the [casting
    operator](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abencasting_operator_glosry.htm "Glossary Entry")
    [`CAST`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenconstructor_expression_cast.htm). You might see code using the older
    operator [`?=`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapmove_cast.htm).
-   See more information in the topic [Assignment Rules for Reference
    Variables](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenconversion_references.htm).

As an example, assume there is an inheritance tree with `lcl_super` as the superclass and `lcl_sub` as a direct subclass. `lcl_sub2` is a direct subclass of `lcl_sub`.

In the following code snippet, the rule is met since the superclass is either the same as or more generic than the subclass (the subclass has, for example, redefined methods and is, thus, more specific). Hence, the assignment of an object reference variable pointing to the subclass to a variable pointing to a superclass works. An upcast is triggered. After this casting, the type of `oref_super` has changed and the methods of `lcl_sub` can be accessed via `oref_super`.

``` abap
"Creating object references
DATA(oref_super) = NEW lcl_super( ).

DATA(oref_sub) = NEW lcl_sub( ).

"Upcast
oref_super = oref_sub.

"The casting might be done when creating the object.
DATA super_ref TYPE REF TO lcl_super.

super_ref = NEW lcl_sub( ).
```

- As mentioned above, a downcast must be triggered
manually. Just an assignment like `oref_sub = oref_super.`
does not work. A syntax error occurs saying the right-hand variable's type cannot be converted to the left-hand variable's type.
- If you indeed want to carry out this casting, you must use
`CAST` (or you might see code using the older operator `?=`) to overcome this syntax error (but just the syntax error!). Note: You might also use these casting operators for the upcasts. That means `oref_super = oref_sub.` has the same effect as `oref_super = CAST #( oref_sub ).`. Using the casting operator for upcasts is usually not necessary.
- At runtime, the assignment is checked and if the conversion does not work, you face a (catchable) exception. Even more so, the assignment `oref_sub = CAST #( oref_super ).` does not throw a syntax error but it does not work in this example either because it violates the rule mentioned above (`oref_sub` is more specific than `oref_super`).
- To check whether such an assignment is possible
on specific classes, you can use the predicate expression [`IS INSTANCE OF`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenlogexp_instance_of.htm)
or the case distinction [`CASE TYPE OF`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapcase_type.htm). Carrying out an upcast before the downcast ensures that the left-hand variable's type is compatible to the right-hand variable's type.

``` abap
DATA(oref_super) = NEW lcl_super( ).
DATA(oref_sub) = NEW lcl_sub( ).
DATA(oref_sub2) = NEW lcl_sub2( ).

"Downcast impossible (oref_sub is more specific than oref_super);
"the exception is caught here

TRY.
  oref_sub = CAST #( oref_super ).
  CATCH cx_sy_move_cast_error INTO DATA(e).
    ...
ENDTRY.

"Working downcast with a prior upcast

oref_super = oref_sub2.

"Due to the prior upcast, the following check is actually not necessary.

IF oref_super IS INSTANCE OF lcl_sub.
  oref_sub = CAST #( oref_super ).
  ...
ENDIF.

"Excursion RTTI: Downcasts, CAST and method chaining
"Downcasts particularly play, for example, a role in the context of
"retrieving type information using RTTI. Method chaining is handy
"because it reduces the lines of code in this case.
"The example below shows the retrieval of type information
"regarding the components of a structure. 
"Due to the method chaining in the second example, the three
"statements in the first example are reduced to one statement.

DATA struct4cast TYPE zdemo_abap_carr.

DATA(rtti_a) = cl_abap_typedescr=>describe_by_data( struct4cast ).
DATA(rtti_b) = CAST cl_abap_structdescr( rtti_a ).
DATA(rtti_c) = rtti_b->components.

DATA(rtti_d) = CAST cl_abap_structdescr(
  cl_abap_typedescr=>describe_by_data( struct4cast )
      )->components.
```

### Demonstrating Upcasts and Downcasts Using the RTTS Inheritance Tree

The examples in the following code snippet use object reference variables to illustrate the class hierarchy of the [Runtime Type Services (RTTS)](#runtime-type-services-rtts), which is covered in more detail in the [Dynamic Programming](06_Dynamic_Programming.md) cheat sheet. 

Hierarchy tree of the classes:
```abap
CL_ABAP_TYPEDESCR
  |
  |--CL_ABAP_DATADESCR
  |   |
  |   |--CL_ABAP_ELEMDESCR
  |   |   |
  |   |   |--CL_ABAP_ENUMDESCR
  |   |
  |   |--CL_ABAP_REFDESCR
  |   |--CL_ABAP_COMPLEXDESCR
  |       |
  |       |--CL_ABAP_STRUCTDESCR
  |       |--CL_ABAP_TABLEDESCR
  |
  |--CL_ABAP_OBJECTDESCR
     |
     |--CL_ABAP_CLASSDESCR
     |--CL_ABAP_INTFDESCR
``` 

Examples:

```abap
"------------ Object reference variables ------------

"Static and dynamic types
"Defining an object reference variable with a static type
DATA tdo TYPE REF TO cl_abap_typedescr.

"Retrieving type information
"The reference the reference variable points to is either cl_abap_elemdescr,
"cl_abap_enumdescr, cl_abap_refdescr, cl_abap_structdescr, or cl_abap_tabledescr.
"So, it points to one of the subclasses. The static type of tdo refers to
"cl_abap_typedescr, however, the dynamic type is one of the subclasses mentioned.
"in the case of the example, it is cl_abap_elemdescr. Check in the debugger.
DATA some_string TYPE string.
tdo = cl_abap_typedescr=>describe_by_data( some_string ).

"Some more object reference variables
DATA tdo_super TYPE REF TO cl_abap_typedescr.
DATA tdo_elem TYPE REF TO cl_abap_elemdescr.
DATA tdo_data TYPE REF TO cl_abap_datadescr.
DATA tdo_gen_obj TYPE REF TO object.

"------------ Upcasts ------------

"Moving up the inheritance tree
"Assignments:
"- If the static type of target variable is less specific or the same, an assignment works.
"- The target variable inherits the dynamic type of the source variable.

"Static type of target variable is the same
tdo_super = tdo.

"Examples for static types of target variables that are less specific
"Target variable has the generic type object
tdo_gen_obj = tdo.

"Target variable is less specific because the direct superclass of cl_abap_elemdescr
"is cl_abap_datadescr
"Note: In the following three assignments, the target variable remains initial 
"since the source variables do not (yet) point to any object.
tdo_data = tdo_elem.

"Target variable is less specific because the direct superclass of cl_abap_datadescr
"is cl_abap_typedescr
tdo_super = tdo_data.

"Target variable is less specific because the class cl_abap_typedescr is higher up in
"the inheritance tree than cl_abap_elemdescr
tdo_super = tdo_elem.

"The casting happens implicitly. You can also excplicitly cast and use
"casting operators, but it is usually not required.
tdo_super = CAST #( tdo ).
tdo_super ?= tdo.

"In combination with inline declarations, the CAST operator can be used to provide a
"reference variable with a more general type.
DATA(tdo_inl_cast) = CAST cl_abap_typedescr( tdo_elem ).

CLEAR: tdo_super, tdo_elem, tdo_data, tdo_gen_obj.

"------------ Downcasts ------------

"Moving down the inheritance tree
"Assignments:
"- If the static type of the target variable is more specific than the static type
"  of the source variable, performing a check whether it is less specific or the same
"  as the dynamic type of the source variable is required at runtime before the assignment
"- The target variable inherits the dynamic type of the source variable, however, the target
"  variable can accept fewer dynamic types than the source variable
"- Downcasts are always performed explicitly using casting operators

"Static type of the target is more specific
"object -> cl_abap_typedescr
tdo_super = CAST #( tdo_gen_obj ).
"cl_abap_typedescr -> cl_abap_datadescr
"Note: Here, the dynamic type of the source variable is cl_abap_elemdescr.
tdo_data = CAST #( tdo ).
"cl_abap_datadescr -> cl_abap_elemdescr
tdo_elem = CAST #( tdo_data ).
"cl_abap_typedescr -> cl_abap_elemdescr
tdo_elem = CAST #( tdo_super ).

"------------ Error prevention in downcasts ------------

"In the examples above, the assignments work. The following code snippets
"deal with examples in which a downcast is not possible. An exception is
"raised.
DATA str_table TYPE string_table.
DATA tdo_table TYPE REF TO cl_abap_tabledescr.

"With the following method call, tdo points to an object with
"reference to cl_abap_tabledescr.
tdo = cl_abap_typedescr=>describe_by_data( str_table ).

"Therefore, the following downcast works.
tdo_table = CAST #( tdo ).

"You could also achieve the same in one statement and with inline
"declaration.
DATA(tdo_table_2) = CAST cl_abap_tabledescr( cl_abap_typedescr=>describe_by_data( str_table ) ).

"Example for an impossible downcast
"The generic object reference variable points to cl_abap_elemdescr after the following
"assignment.
tdo_gen_obj = cl_abap_typedescr=>describe_by_data( some_string ).

"Without catching the exception, the runtime error MOVE_CAST_ERROR
"occurs. There is no syntax error at compile time. The static type of
"tdo_gen_obj is more generic than the static type of the target variable.
"The error occurs when trying to downcast, and the dynamic type is used.
TRY.
    tdo_table = CAST #( tdo_gen_obj ).
  CATCH cx_sy_move_cast_error.
ENDTRY.
"Note: tdo_table sill points to the reference as assigned above after trying
"to downcast in the TRY control structure.

"Using CASE TYPE OF and IS INSTANCE OF statements, you can check if downcasts
"are possible.
"Note: In case of ...
"- non-initial object reference variables, the dynamic type is checked.
"- initial object reference variables, the static type is checked.

"------------ IS INSTANCE OF ------------
DATA some_tdo TYPE REF TO cl_abap_typedescr.
some_tdo = cl_abap_typedescr=>describe_by_data( str_table ).

IF some_tdo IS INSTANCE OF cl_abap_elemdescr.
  DATA(tdo_a) = CAST cl_abap_elemdescr( some_tdo ).
ELSE.
  "This branch is executed. The downcast is not possible.
  ...
ENDIF.

IF some_tdo IS INSTANCE OF cl_abap_elemdescr.
  DATA(tdo_b) = CAST cl_abap_elemdescr( some_tdo ).
ELSEIF some_tdo IS INSTANCE OF cl_abap_refdescr.
  DATA(tdo_c) = CAST cl_abap_refdescr( some_tdo ).
ELSEIF some_tdo IS INSTANCE OF cl_abap_structdescr.
  DATA(tdo_d) = CAST cl_abap_structdescr( some_tdo ).
ELSEIF some_tdo IS INSTANCE OF cl_abap_tabledescr.
  "In this example, this branch is executed. With the check,
  "you can make sure that the downcast is indeed possible.
  DATA(tdo_e) = CAST cl_abap_tabledescr( some_tdo ).
ELSE.
  ...
ENDIF.

DATA initial_tdo TYPE REF TO cl_abap_typedescr.

IF initial_tdo IS INSTANCE OF cl_abap_elemdescr.
  DATA(tdo_f) = CAST cl_abap_elemdescr( some_tdo ).
ELSEIF initial_tdo IS INSTANCE OF cl_abap_refdescr.
  DATA(tdo_g) = CAST cl_abap_refdescr( some_tdo ).
ELSEIF initial_tdo IS INSTANCE OF cl_abap_structdescr.
  DATA(tdo_h) = CAST cl_abap_structdescr( some_tdo ).
ELSEIF initial_tdo IS INSTANCE OF cl_abap_tabledescr.
  DATA(tdo_i) = CAST cl_abap_tabledescr( some_tdo ).
ELSE.
  "In this example, this branch is executed. The static
  "type of the initial object reference variable is used,
  "which is cl_abap_typedescr here.
  ...
ENDIF.

"------------ CASE TYPE OF ------------
"The examples are desinged similarly to the IS INSTANCE OF examples.

DATA(dref) = REF #( str_table ).
some_tdo = cl_abap_typedescr=>describe_by_data( dref ).

CASE TYPE OF some_tdo.
  WHEN TYPE cl_abap_elemdescr.
    DATA(tdo_j) = CAST cl_abap_elemdescr( some_tdo ).
  WHEN TYPE cl_abap_refdescr.
    "In this example, this branch is executed. With the check,
    "you can make sure that the downcast is indeed possible.
    DATA(tdo_k) = CAST cl_abap_refdescr( some_tdo ).
  WHEN TYPE cl_abap_structdescr.
    DATA(tdo_l) = CAST cl_abap_structdescr( some_tdo ).
  WHEN TYPE cl_abap_tabledescr.
    DATA(tdo_m) = CAST cl_abap_tabledescr( some_tdo ).
  WHEN OTHERS.
    ...
ENDCASE.

"Example with initial object reference variable
CASE TYPE OF initial_tdo.
  WHEN TYPE cl_abap_elemdescr.
    DATA(tdo_n) = CAST cl_abap_elemdescr( some_tdo ).
  WHEN TYPE cl_abap_refdescr.
    DATA(tdo_o) = CAST cl_abap_refdescr( some_tdo ).
  WHEN TYPE cl_abap_structdescr.
    DATA(tdo_p) = CAST cl_abap_structdescr( some_tdo ).
  WHEN TYPE cl_abap_tabledescr.
    DATA(tdo_q) = CAST cl_abap_tabledescr( some_tdo ).
  WHEN OTHERS.
    "In this example, this branch is executed. The static
    "type of the initial object reference variable is used,
    "which is cl_abap_typedescr here.
    ...
ENDCASE.
```


<p align="right"><a href="#top">⬆️ back to top</a></p>

## Interfaces

Interfaces ...

-   represent a template for the components in the public visibility
    section of classes.
- enhance classes by adding interface components.
-   are possible as both
    [local](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenlocal_interface_glosry.htm "Glossary Entry")
    and [global
    interfaces](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenglobal_interface_glosry.htm "Glossary Entry").
-   support
    [polymorphism](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenpolymorphism_glosry.htm "Glossary Entry") in classes. Each class that implements an interface can implement its methods differently. [Interface reference variables](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninterface_ref_variable_glosry.htm "Glossary Entry") can point to objects of all classes that implement the associated interface.
- can be implemented by classes of an inheritance tree. It can be any number of interfaces. However, each interface can be implemented only once in an inheritance tree.
-   are different from classes in the following ways:
    -   They only consist of a part declaring the components without an
        implementation part. The implementation is done in classes that use the interface.
    -   There are no visibility sections. All components of an interface are visible.
    -   No instances can be created from interfaces.
    -   Declarations as mentioned for classes, e. g. `DATA`,
        `CLASS-DATA`, `METHODS`,
        `CLASS-METHODS`, are possible. Constructors are not
        possible.

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Defining Interfaces
- Can be done either globally in the repository or locally in an ABAP program.

``` abap
INTERFACE intf.
"The addition PUBLIC is for global interfaces:
"INTERFACE intf_g PUBLIC.

    DATA ...
    CLASS-DATA ...
    METHODS ...
    CLASS-METHODS ...

ENDINTERFACE.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Implementing Interfaces
-   A class can implement multiple interfaces.
-   Interfaces must be specified in the
    declaration part of a class using the statement
    [`INTERFACES`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapinterfaces.htm).
-   Since all interface components are public, you must include this
    statement and the interfaces in the public visibility section of a class. When an interface is implemented in a class, all interface components are added to the other components of the class in the public visibility section.
- Interface components can be addressed using the [interface component
    selector](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abeninterface_comp_selector_glosry.htm "Glossary Entry"): `... intf~comp ...`.
- You can specify alias names for the interface components using the statement [`ALIASES ... FOR ...`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapaliases.htm). The components can then be addressed using the alias name.
- The class must implement the methods of all implemented interfaces in it unless the methods are flagged as abstract or final. You can adapt some interface components to requirements of your class.
    - You can specify the additions [`ABSTRACT METHODS`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapinterfaces_class.htm) followed by method names or [`ALL METHODS ABSTRACT`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapinterfaces_class.htm) for the `INTERFACES` statement in the declaration part of
    classes. In this case, the class(es) need not
    implement the methods of the interface. The implementation is then relevant for a subclass inheriting from a superclass that includes
    such an interface declaration. Note that the whole class must be abstract.
    - The additions [`FINAL METHODS`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapinterfaces_class.htm) followed by method names or [`ALL METHODS FINAL`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapinterfaces_class.htm) for the `INTERFACES` statement in the declaration part of classes flag the method(s) as final.
- In the interface, methods can mark their implementation as optional using the additions [`DEFAULT IGNORE`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapmethods_default.htm) or [`DEFAULT FAIL`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapmethods_default.htm).
  - `DEFAULT IGNORE`: When a method with such a declaration is called without an implementation, it behaves as though no implementation exists.
  - `DEFAULT FAIL`: If an unimplemented method is called, it triggers the `CX_SY_DYN_CALL_ILLEGAL_METHOD` exception.


Syntax for using interfaces in classes:
``` abap
CLASS class DEFINITION.
  PUBLIC SECTION.
    "Multiple interface implementations possible
    INTERFACES intf.
    ALIASES meth_alias FOR intf~some_method.
ENDCLASS.

CLASS class IMPLEMENTATION.
  METHOD intf~some_meth.           "Method implementation using the original name
   ...
  ENDMETHOD.

  "Just for demo purposes: Method implementation using the alias name
  "METHOD meth_alias.
  " ...
  "ENDMETHOD.

  ...
ENDCLASS.

"----------------------- Abstract class -----------------------
CLASS cl_super DEFINITION ABSTRACT.
  PUBLIC SECTION.
    INTERFACES intf ALL METHODS ABSTRACT.
    ALIASES:
      meth1 FOR intf~meth1,
      meth2 FOR intf~meth2.
ENDCLASS.

"Subclass inheriting from abstract class and implementing interface methods
CLASS cl_sub DEFINITION INHERITING FROM cl_super.
  PUBLIC SECTION.
    METHODS:
      meth1 REDEFINITION,
      meth2 REDEFINITION.
ENDCLASS.

CLASS cl_sub IMPLEMENTATION.
  METHOD meth1.
    ...
  ENDMETHOD.
  METHOD meth2.
    ...
  ENDMETHOD.
ENDCLASS.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Interface Reference Variables and Accessing Objects

- Addressing an object happens via an object reference variable with reference to a class.
- An interface variable can contain references to objects of classes that implement the corresponding interface.
- You create an interface reference variable like this: `DATA i_ref TYPE REF TO intf.`

Addressing interface components:
- Addressing instance components using interface reference variable
    - attribute: `i_ref->attr`
    - instance method: `i_ref->meth( )`
- Addressing instance components using an object reference variable (Note: The type is a class that implements the interface) is also possible but it's not the recommended way:
    - attribute: `cl_ref->intf~attr`
    - instance method: `cl_ref->intf~meth`
- Addressing static components:
    - static attribute: `class=>intf~attr`,
    - static method: `class=>intf~meth( )`
    - constant: `intf=>const`


``` abap
"Addressing instance interface components using interface reference variable
DATA i_ref TYPE REF TO intf.

DATA cl_ref TYPE REF TO class.

"Creating an instance of a class that implements the interface intf
cl_ref = NEW #( ).

"If the class class implements an interface intf,
"the class reference variable cl_ref can be assigned
"to the interface reference variable i_ref.
"The reference in i_ref then points to the same object
"as the reference in cl_ref.
i_ref = cl_ref.

"Can also be done directly, i. e. directly creating an object to which the interface reference variable points
i_ref = NEW class( ).

"Instance interface method via interface reference variable
... i_ref->inst_method( ... ) ...

"Instance interface attribute via interface reference variable
... i_ref->inst_attr ...

"Addressing instance components using the class reference variable
"is also possible but it's not the recommended way.
... cl_ref->intf~inst_method( ... ) ...
... cl_ref->intf~inst_attr ...

"Addressing static interface components
"class=> can be dropped if the method is called in the same class that implements the interface
... class=>intf~stat_method( ... ) ...
... class=>intf~stat_attr ...

"Just for the record: Static interface components can be called via reference variables, too.
... i_ref->stat_method( ... ) ...
... i_ref->stat_attr ...
... cl_ref->intf~stat_method( ... ) ...

"Constants
"A constant can be addressed using the options mentioned above.
"Plus, it can be addressed using the following pattern
... intf=>const ...
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Excursion: Example Interface

Expand the following collapsible section for example code. To try it out, create a demo interface named `zif_some_interface`, a class named `zcl_some_class`, and paste the code into the artifacts. After activation, choose *F9* in ADT to execute the class. The example is set up to display output in the console.

<details>
   <summary>🟢 Click to expand for more information and example code</summary>
  <!-- -->
<br>

Example interface:
```abap
INTERFACE zif_some_interface
  PUBLIC .

  TYPES c3 type c length 3.
  DATA add_result TYPE i.
  CLASS-DATA: subtr_result TYPE i.
  METHODS addition IMPORTING num1          TYPE i
                             num2          TYPE i.
  CLASS-METHODS subtraction IMPORTING num1          TYPE i
                                      num2          TYPE i.

  METHODS meth_ignore DEFAULT IGNORE returning value(int) type i.
  METHODS meth_fail DEFAULT FAIL returning value(int) type i.

ENDINTERFACE.
```

When you have activated the interface, create the class. The following steps comment on various things.

Example class implementations:

1) 
- When you create the class, you can add `INTERFACES zif_some_interface.` to the public visibility section.
- Using the quick fix in ADT, you can automatically add the method implementation skeletons of the interface methods.
- Note that the interface methods declared with `DEFAULT IGNORE` and `DEFAULT FAIL` are not automatically added. If implementations are desired, you can manually add the implementations for these methods. See the following step.
- The example class also implements the interface `if_oo_adt_classrun`.

```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    INTERFACES zif_some_interface.
  PROTECTED SECTION.
  PRIVATE SECTION.

ENDCLASS.


CLASS zcl_some_class IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
  ENDMETHOD.

  METHOD zif_some_interface~addition.
  ENDMETHOD.

  METHOD zif_some_interface~subtraction.
  ENDMETHOD.

ENDCLASS.
```

2) 
- Adding the implementations for the interface methods declared with `DEFAULT IGNORE` and `DEFAULT FAIL`.

```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    INTERFACES zif_some_interface.
  PROTECTED SECTION.
  PRIVATE SECTION.

ENDCLASS.


CLASS zcl_some_class IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.
  ENDMETHOD.

  METHOD zif_some_interface~addition.
  ENDMETHOD.

  METHOD zif_some_interface~subtraction.
  ENDMETHOD.

  METHOD zif_some_interface~meth_fail.
  ENDMETHOD.

  METHOD zif_some_interface~meth_ignore.
  ENDMETHOD.

ENDCLASS.
``` 

3) 
- The following example class represents an executable example that displays output in the ADT console. 
- Apart from simple demo implementations, it includes alias names specified for interface components.
- The interface methods declared with `DEFAULT IGNORE` and `DEFAULT FAIL` are intentionally not implemented, but the methods are nevertheless called. 
   - Interface method declared with `DEFAULT IGNORE`: No implementation available, and no value is assigned for the returning parameter. Therefore, the value is initial. 
   - Interface method declared with `DEFAULT FAIL`: If the exception is not caught, a runtime error occurs.
- The example demonstrates method calls using object and interface reference variables.

```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
    INTERFACES zif_some_interface.
    ALIASES res FOR zif_some_interface~add_result.
    ALIASES add FOR zif_some_interface~addition.
    ALIASES subtr FOR zif_some_interface~subtraction.
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.


CLASS zcl_some_class IMPLEMENTATION.

  METHOD if_oo_adt_classrun~main.

    "Examples using an object reference variable
    DATA(oref) = NEW zcl_some_class( ).

    oref->add( num1 = 1 num2 = 2 ).
    DATA(res1) = oref->res.
    out->write( res1 ).

    oref->subtr( num1 = 1 num2 = 2 ).
    DATA(res2) = oref->zif_some_interface~subtr_result.
    out->write( res2 ).

    "Referring to a type declared in the interface
    DATA char_a TYPE zif_some_interface~c3.
    DATA char_b TYPE zif_some_interface=>c3.

    "Calling non-implemented methods
    DATA(int_ig_a) = oref->zif_some_interface~meth_ignore( ).
    ASSERT int_ig_a = 0.

    TRY.
        DATA(int_fl_a) = oref->zif_some_interface~meth_fail( ).
      CATCH cx_sy_dyn_call_illegal_method INTO DATA(error).
        out->write( error->get_text( ) ).
    ENDTRY.

    "Similar examples using an interface reference variable
    DATA iref TYPE REF TO zif_some_interface.
    iref = NEW zcl_some_class( ).

    iref->addition( num1 = 3 num2 = 5 ).
    DATA(res3) = iref->add_result.
    out->write( res3 ).

    iref->subtraction( num1 = 3 num2 = 5 ).
    DATA(res4) = iref->subtr_result.
    out->write( res4 ).

    "Referring to a type declared in the interface
    DATA char_c TYPE iref->c3.

    "Calling non-implemented methods
    DATA(int_ig_b) = iref->meth_ignore( ).
    ASSERT int_ig_b = 0.

    TRY.
        DATA(int_fl_b) = iref->meth_fail( ).
      CATCH cx_sy_dyn_call_illegal_method INTO error.
        out->write( error->get_text( ) ).
    ENDTRY.
  ENDMETHOD.

  METHOD add.
    res = num1 + num2.
  ENDMETHOD.

  METHOD subtr.
    zif_some_interface~subtr_result = num1 - num2.
  ENDMETHOD.
ENDCLASS.
```


</details>  

<p align="right"><a href="#top">⬆️ back to top</a></p>

## Excursions

### Friendship

- The concept of friendship enters the picture if your use case for your classes is to work together very closely. This is true, for example, for [unit
tests](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenunit_test_glosry.htm "Glossary Entry") if you want to test private methods.
- Classes can grant access to invisible components for their [friends](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenfriend_glosry.htm "Glossary Entry").
- The friends can be other classes and interfaces. In case of interfaces, friendship is granted to all classes that implement the interface.
- Impact of friendship:
    - Access is granted to all components, regardless of the visibility section or the addition `READ-ONLY`.
    - Friends of a class can create instances of the class without restrictions.
    - Friendship is a one-way street, i. e. a class granting friendship to another class is not granded friendship the other way round. If class `a` grants friendship to class `b`, class `b` must also explicitly grant friendship to class `a` so that `a` can access the invisible components of class `b`.
    - Friendship and inheritance: Heirs of friends and interfaces that contain a friend as a component interface also become friends. However, granting friendship is not inherited, i. e. a friend of a superclass is not automatically a friend of its subclasses.


You specify the befriended class in the definition part using a `FRIENDS` addition:
``` abap
"For local classes. Friendship can be granted to all classes/interfaces
"of the same program and the class library.
"Multiple classes can be specified as friends.
CLASS lo_class DEFINITION FRIENDS other_class ... .
...

CLASS lo_class DEFINITION CREATE PRIVATE FRIENDS other_class ... .

"Addition GLOBAL only allowed for global classes, i. e. if the addition PUBLIC is also used
"Other global classes and interfaces from the class library can be specified after GLOBAL FRIENDS.
CLASS global_class DEFINITION CREATE PUBLIC FRIENDS other_global_class ... .
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

#### Friendship between Global and Local Classes

Expand the following collapsible section for an example class. It demonstrates granting friendship between a global class and a local class (in the CCIMP include, *Local Types* tab in ADT). In the example, friendship is granted in both ways so that the global class can access private components of the local class, and the local class can access private components of the global class.
For more information, see the following topics: 
- [`LOCAL FRIENDS`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapclass_local_friends.htm) 
- [`DEFERRED`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapclass_deferred.htm)

<details>
  <summary>🟢 Click to expand for more information and example code</summary>
  <!-- -->

<br>


**Global class**
- Create a new global class (the example uses the name `zcl_some_class`) and copy and paste the following code in the *Global Class* tab in ADT.
- The class has a type and method declaration in the private section. They are used in the local class.
- Once activated (and the code of the other includes has been inserted), you can choose *F9* in ADT to run the class.
- When running the class, a method of the local class that is declared in the private section there is called. As a result of this method call, a string is assigned to an attribute that is also declared in the private section of the local class. This attribute is accessed by the global class, and finally displayed in the ADT console.

```abap
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
  PROTECTED SECTION.
  PRIVATE SECTION.
    TYPES str TYPE string.
    CLASS-METHODS get_hello RETURNING VALUE(hello) TYPE str.
ENDCLASS.



CLASS zcl_some_class IMPLEMENTATION.
  METHOD if_oo_adt_classrun~main.
    local_class=>say_hello( ).
    DATA(hello) = local_class=>hello.
    out->write( hello ).
  ENDMETHOD.
  METHOD get_hello.
    hello = `Hello`.
  ENDMETHOD.
ENDCLASS.
```

**CCDEF include (*Class-relevant Local Types* tab in ADT)**
- Regarding the includes, see the information in section [Excursion: Class Pool and Include Programs](#excursion-class-pool-and-include-programs)
- The `LOCAL FRIENDS` addition makes the local class a friend of the global class. The private components of the global class can then be accessed by the local class.

```abap
CLASS local_class DEFINITION DEFERRED.
CLASS zcl_some_class DEFINITION LOCAL FRIENDS local_class.
```

**CCIMP include (*Local Types* tab in ADT)**
- The `FRIENDS` addition makes the global class a friend of the local class. The private components of the local class can then be accessed by the global class.
- A type declared in the private section of the global class is used to type an attribute.
- The method, which is also declared in the private section, includes a method call in the implementation. It is a method declared in the private section of the global class.


```abap
CLASS local_class DEFINITION FRIENDS zcl_some_class.

  PUBLIC SECTION.
  PROTECTED SECTION.
  PRIVATE SECTION.
    CLASS-DATA hello TYPE zcl_some_class=>str.
    CLASS-METHODS say_hello.
    
ENDCLASS.

CLASS local_class IMPLEMENTATION.
  METHOD say_hello.
    hello = |{ zcl_some_class=>get_hello( ) } { sy-uname }.|.
  ENDMETHOD.
ENDCLASS.
```

</details>  




<p align="right"><a href="#top">⬆️ back to top</a></p>

### Events

- [Events](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenevent_glosry.htm "Glossary Entry")
can trigger the processing of [processing blocks](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenprocessing_block_glosry.htm "Glossary Entry").
- Declaring events: Can be declared in a visibility section of the declaration part of a class or in an interface, e. g. as
  - instance event using an [`EVENTS`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapevents.htm) statement. Note that they can only be raised in instance methods of the same class.
  - static event using [`CLASS-EVENTS`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapclass-events.htm). They can be raised in all methods of the same class or of a class that implements the interface. Static event handlers can be called by the event independently of an instance of the class.

``` abap
"Declaration part of a class/interface
"Instance events
EVENTS: i_evt1,

"Events can only have output parameters that are passed by value
        i_evt2 EXPORTING VALUE(num) TYPE i ...
...
"Static events
CLASS-EVENTS: st_evt1,
              st_evt2 EXPORTING VALUE(num) TYPE i ...

```

- Event handlers:
  - An event is raised by a [`RAISE EVENT`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapraise_event.htm) statement in another method or in the same method.
  - Raising an event means that [event handlers](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenevent_handler_glosry.htm "Glossary Entry") are called.
  - This event handler must be declared with the following syntax (see more information and more additions [here](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapmethods_event_handler.htm)):

``` abap
"Event handlers for instance events
METHODS: handler_meth1 FOR EVENT i_evt1 OF some_class,

         "Parameter names must be the same as declared;
         "no further additions possible for the parameter (e.g. TYPE);
         "the predefined, implicit parameter sender as another formal parameter is possible with instance events,
         "it is typed as a reference variable, which itself has the class/interface as a static type,
         "If the event handler is called by an instance event, it is passed a reference to the raising object in sender.
         handler_meth2 FOR EVENT i_evt2 OF some_class IMPORTING num sender,
...
```

- To make sure that an event handler handles a raised event, it must be registered with the statement [`SET HANDLER`](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapset_handler.htm). See more information [here](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abapset_handler.htm) (for example, events can also be deregistered).

```abap
"Registering event for a specific instance
SET HANDLER handler1 FOR ref.

"Registering event for all instances
SET HANDLER handler2 FOR ALL INSTANCES.

"Registering static event for the whole class/interface
SET HANDLER handler3.
"Note that multiple handler methods can be specified.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Examples for Design Patterns: Factory Methods and Singletons

In object-oriented programming, there a plenty of design patterns. Covering these ones here to get a rough idea: factory methods and singletons. Both are relevant if you want to restrict or control the instantiation of a class by external users of this class.

A singleton is a design pattern in which it is only up to the class to create objects. In doing so, the class ensures that only one object exists for every internal session that is made available to consumers.

The following code snippet shows an implementation of the singleton design pattern. The `get_instance` method is used to return the object reference to the object created. Only one instance can be created.

```abap
"Using the addition CREATE PRIVATE, objects can only be created by the class itself.
CLASS singleton_class DEFINITION CREATE PRIVATE.
  PUBLIC SECTION.
    CLASS-METHODS get_instance RETURNING VALUE(ret) TYPE REF TO singleton_class.

  PRIVATE SECTION.
    CLASS-DATA inst TYPE REF TO singleton_class.
ENDCLASS.

CLASS singleton_class IMPLEMENTATION.
  METHOD get_instance.
    IF inst IS NOT BOUND.
      inst = NEW #( ).
    ENDIF.
    ret = inst.
  ENDMETHOD.
ENDCLASS.
```

Controlling the creation of objects - the instantiation of a class - can be realized using a factory method. For example, certain checks might be required before a class can be instantiated. If a check is not successful, the instantiation is denied.
You might create a (static) factory method as follows:
- A check is carried out in the factory method, for example, by evaluating importing parameters.
- If the check is successful, an object of the class is created.
- The method signature includes an output parameter that returns an object reference to the caller.

This is rudimentarily demonstrated in the following snippet:

``` abap
CLASS class DEFINITION CREATE PRIVATE.
  PUBLIC SECTION.
  CLASS-METHODS
    factory_method IMPORTING par ...,
                   RETURNING VALUE(obj) TYPE REF TO class.
  ...
ENDCLASS.

CLASS class IMPLEMENTATION.
  METHOD factory_method.
    IF par = ...
       obj = NEW class( ).
      ELSE.
      ...
    ENDIF.

  ENDMETHOD.
  ...
ENDCLASS.
...

"Calling a factory method.
DATA obj_factory TYPE REF TO class.

obj_factory = class=>factory_method( par = ... ).
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

### Class-Based Exceptions

- [Catchable exceptions](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abencatchable_exception_glosry.htm) are represented by exception objects of exception classes.
- Find an overview in the [Exceptions and Runtime Errors](27_Exceptions.md) cheat sheet.

<p align="right"><a href="#top">⬆️ back to top</a></p>

### ABAP Unit Tests

- [ABAP Unit](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenabap_unit_glosry.htm) is a test tool integrated into the ABAP runtime framework. 
- It can be used to run individual or mass tests, and to evaluate test results. 
- In ABAP programs, individual unit tests are implemented as [test methods](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abentest_method_glosry.htm) of local [test classes](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abentest_class_glosry.htm). 
- Find information on ABAP Unit tests in the [ABAP Unit Tests](14_ABAP_Unit_Tests.md) cheat sheet.

<p align="right"><a href="#top">⬆️ back to top</a></p>


### ABAP Doc Comments

- The ABAP Doc documentation tool allows you to add special ABAP Doc comments to ABAP source code for documentation.  
- ABAP Doc comments consist of one or more lines starting with `"!`.  
- You can place these comments before declarations (e.g., in classes and methods) to document functionality, add notes, and so on.  
- In ADT, click, for example, on class names or methods to display ABAP Doc comments (if available) in the *ABAP Element Info* tab, or choose F2 to display the information.
- Find more information on ABAP Doc [here](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/ABENDOCCOMMENT.html).
- The following example demonstrates ABAP Doc comments, showing various commenting options, including:  
  - Using HTML tags for formatting. Only a selected set of HTML tags is supported. You can choose *CTRL + Space* in the ABAP Doc comment for input help.
  - Special tagging and linking options. Refer to the [documentation](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/ABENDOCCOMMENT.html) for more details.
  - Special method signature specifications like `@parameter | ...` for parameters and `@raising | ...` for declared exceptions.


```abap
"! <p class="shorttext">Demo ABAP Doc comments</p>
"!
"! <p>This class serves as an example to illustrate comments for ABAP Doc.
"! The comments begin with the string <strong>"!</strong>, a special form of regular comments introduced by <strong>"</strong>. <br/><br/>
"! The {@link zcl_some_class.METH:calculate} method of the example class performs a calculation. </p>
"! <h2>Notes</h2>
"! <ul>
"! <li>ABAP Doc documents declarations in ABAP programs.</li>
"! <li>The ABAP development tools for Eclipse (ADT) support ABAP Doc.</li>
"! <li>The content of ABAP Doc comments is converted to HTML and displayed appropriately.</li>
"! <li>Check out the supported HTML tags by choosing <em>CTRL + Space</em> after <em>"!</em>. h1 - h3 tags can also be used.</li>
"! <li>Escaping special characters:  <strong>&quot;, &apos;, &lt;, &gt;, &#64;, &#123;, &#124;, and &#125;</strong></li>
"! </ul>
"! <h2>Steps</h2>
"! <ol>
"! <li>Create a demo class named <em>zcl_some_class</em></li>
"! <li>Copy and paste the code of this example and activate.</li>
"! <li>Click the class name to display the comments in the <em>ABAP Element Info</em> ADT tab.</li>
"! <li>You can also choose F2 for the class name to display the information.</li>
"! </ol>
"! <h3>More examples</h3>
"! Find more code examples in ABAP cheat sheet demo classes, such as {@link zcl_demo_abap_objects} and others. <br/>
"! <h3>Link examples</h3>
"! <ul>
"! <li>Repository objects such as the following, and more:
"! <ul><li>Classes, e.g. {@link zcl_some_class}</li>
"! <li>Interfaces, e.g. {@link if_oo_adt_classrun}</li>
"! <li>CDS artifacts, e.g. {@link i_apisforclouddevelopment}</li>
"! <li>DDIC database tables, e.g. {@link zdemo_abap_carr}</li>
"! <li>DDIC data elements, e.g. {@link land1}</li></ul>
"! <li>Method: {@link zcl_some_class.METH:calculate}</li>
"! <li>Constant: {@link zcl_some_class.DATA:const}</li>
"! <li>Data object: {@link zcl_some_class.DATA:dobj}</li>
"! <li>Method parameter: {@link zcl_some_class.METH:calculate.DATA:operator}</li>
"! <li>Interface implemented in a class: {@link zcl_some_class.INTF:if_oo_adt_classrun}</li>
"! <li>Interface method implemented in a class: {@link zcl_some_class.INTF:if_oo_adt_classrun.METH:main}</li>
"! <li>DDIC domain: {@link DOMA:land1}</li>
"! <li>XSLT: {@link XSLT:id}</li>
"! </ul>
CLASS zcl_some_class DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.

    TYPES: basetype TYPE c LENGTH 1,
           BEGIN OF ENUM t_enum_calc STRUCTURE en_calc BASE TYPE basetype,
             init     VALUE IS INITIAL,
             plus     VALUE '+',
             minus    VALUE '-',
             multiply VALUE '*',
             divide   VALUE '/',
           END OF ENUM t_enum_calc STRUCTURE en_calc.

    "! <p>This method performs a calculation.</p>
    "! @parameter num1 | First number for the calcation
    "! @parameter num2 | Second number for the calcation
    "! @parameter operator | Operator. Only one of the four operators +, -, *, / is allowed.
    "! The value is represented by an enumerated type. Note that there is no handling if
    "! the assigned value is initial.
    "! @parameter result | Result of the calculation
    "! @raising cx_sy_zerodivide | Zero division
    "! @raising cx_sy_arithmetic_overflow | Arithmetic overflow
    CLASS-METHODS calculate IMPORTING num1          TYPE i
                                      num2          TYPE i
                                      operator      TYPE t_enum_calc
                            RETURNING VALUE(result) TYPE decfloat34
                            RAISING   cx_sy_zerodivide cx_sy_arithmetic_overflow.

    "! This is an ABAP Doc comment for a constant
    CONSTANTS const TYPE i VALUE 123.

    "! This is an ABAP Doc comment for a static attribute of a class
    CLASS-DATA dobj TYPE i.
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.

CLASS zcl_some_class IMPLEMENTATION.
  METHOD if_oo_adt_classrun~main.

    DATA(result_plus) = calculate( num1 = 1 num2 = 10 operator = en_calc-plus ).
    DATA(result_minus) = calculate( num1 = 1 num2 = 10 operator = en_calc-minus ).
    DATA(result_multiply) = calculate( num1 = 2 num2 = 5 operator = en_calc-multiply ).
    DATA(result_divide) = calculate( num1 = 10 num2 = 5 operator = en_calc-divide ).

    out->write( data = result_plus name = `result_plus` ).
    out->write( data = result_minus name = `result_minus` ).
    out->write( data = result_multiply name = `result_multiply` ).
    out->write( data = result_divide name = `result_divide` ).

  ENDMETHOD.

  METHOD calculate.

    result = SWITCH #( operator
                       WHEN en_calc-plus THEN num1 + num2
                       WHEN en_calc-minus THEN num1 - num2
                       WHEN en_calc-multiply THEN num1 * num2
                       WHEN en_calc-divide THEN num1 / num2
                       ELSE '0' ).

  ENDMETHOD.
ENDCLASS.
```

<p align="right"><a href="#top">⬆️ back to top</a></p>

## More Information
You can check the subtopics of

- [ABAP Objects - Overview](https://help.sap.com/doc/abapdocu_cp_index_htm/CLOUD/en-US/index.htm?file=abenabap_objects_oview.htm)
- [Programming Guidlines - Object-Oriented Programming (F1 docu for standard ABAP)](https://help.sap.com/doc/abapdocu_latest_index_htm/latest/en-US/index.htm?file=abenobj_oriented_gdl.htm)
  
in the ABAP Keyword Documentation.

## Executable Examples

- [zcl_demo_abap_objects](./src/zcl_demo_abap_objects.clas.abap) 
- [zcl_demo_abap_objects_misc](./src/zcl_demo_abap_objects_misc.clas.abap): Additional syntax examples  
- [zcl_demo_abap_oo_inheritance_1](./src/zcl_demo_abap_oo_inheritance_1.clas.abap): Focuses on inheritance; the inheritance tree consists of 4 example classes 

> **💡 Note**<br>
> - The steps to import and run the code are outlined [here](README.md#-getting-started-with-the-examples).
> - [Disclaimer](./README.md#%EF%B8%8F-disclaimer)
