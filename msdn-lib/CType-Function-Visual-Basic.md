
[Source](https://msdn.microsoft.com/en-us/library/4x2877xb.aspx "Permalink to CType Function (Visual Basic)")

# CType Function (Visual Basic)

Returns the result of explicitly converting an expression to a specified data type, object, structure, class, or interface.
##Syntax

    CType(expression, typename)

##Parts
_expression_

Any valid expression. If the value of _expression_ is outside the range allowed by _typename_, Visual Basic throws an exception.

_typename_

##Remarks

>You can also use the following functions to perform a type conversion:
>* Type conversion functions such as CByte, CDbl, and CInt that perform a conversion to a specific data type. For more information, see [Type Conversion Functions (Visual Basic)][8].
>* [DirectCast Operator (Visual Basic)][9] or [TryCast Operator (Visual Basic)][10]. These operators require that one type inherit from or implement the other type. They can provide somewhat better performance than CType when converting to and from the Object data type.

Any expression that is legal within an **As** clause in a **Dim** statement, that is, the name of any data type, object, structure, class, or interface.

VB.Net is a strongly typed language, meaning all objects represent a specific type (kind) of data.  A given object can represent one, and only one, [Data Type][19].  However, objects may support conversion of the existing data type to some other type.  These conversions are performed using the **CType** [operator][16].

**CType** is compiled inline, which means that the conversion code is part of the code that evaluates the expression. In some cases, the code runs faster because no procedures are called to perform the conversion.

If no conversion is defined from _expression_ to _typename_ (for example, from **Integer** to **Date**), Visual Basic displays a compile-time error message.

If a conversion fails at run time, the appropriate exception is thrown. If a narrowing conversion fails, an [OverflowException][2] is the most common result. If the conversion is undefined, an [InvalidCastException][3] in thrown. For example, this can happen if _expression_ is of type **Object** and its run-time type has no conversion to _typename_.

If the data type of _expression_ or _typename_ is a class or structure you've defined, you can define **CType** on that class or structure as a conversion operator. This makes **CType** act as an _overloaded operator_. If you do this, you can control the behavior of conversions to and from your class or structure, including the exceptions that can be thrown.

###Overloading

The **CType** operator can also be overloaded on a class or structure defined outside your code. If your code converts to or from such a class or structure, be sure you understand the behavior of its **CType** operator. For more information, see [Operator Procedures (Visual Basic)][4].

###Converting Dynamic Objects

Type conversions of dynamic objects are performed by user-defined dynamic conversions that use the [TryConvert][5] or [BindConvert][6] methods. If you're working with dynamic objects, use the [CTypeDynamic][7] method to convert the dynamic object.

The following example uses the **CType** function to convert an expression to the **Single** data type.

    Dim testNumber As Long = 1000
    ' The following line of code sets testNewType to 1000.0.
    Dim testNewType As Single = CType(testNumber, Single)

For additional examples, see [Implicit and Explicit Conversions (Visual Basic)][11].

##See Also
[Data Types in Visual Basic][19]

[OverflowException][12]

[InvalidCastException][13]

[Type Conversion Functions (Visual Basic)][14]

[Conversion Functions (Visual Basic)][15]

[Operator Statement][16]

[How to: Define a Conversion Operator (Visual Basic)][17]

[Type Conversion in the .NET Framework][18]

[1]: https://i-msdn.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635810750817785875
[2]: https://msdn.microsoft.com/en-us/library/system.overflowexception.aspx
[3]: https://msdn.microsoft.com/en-us/library/system.invalidcastexception.aspx
[4]: https://msdn.microsoft.com/en-us/library/xh17yw4c.aspx
[5]: https://msdn.microsoft.com/en-us/library/system.dynamic.dynamicobject.tryconvert.aspx
[6]: https://msdn.microsoft.com/en-us/library/system.dynamic.dynamicmetaobject.bindconvert.aspx
[7]: https://msdn.microsoft.com/en-us/library/ee835926.aspx

[8]: https://msdn.microsoft.com/en-us/library/s2dy91zy.aspx
[9]: https://msdn.microsoft.com/en-us/library/7k6y2h6x.aspx
[10]: https://msdn.microsoft.com/en-us/library/zyy863x8.aspx
[11]: https://msdn.microsoft.com/en-us/library/kca3w8x6.aspx

[12]: https://msdn.microsoft.com/en-us/library/system.overflowexception.aspx
[13]: https://msdn.microsoft.com/en-us/library/system.invalidcastexception.aspx
[14]: https://msdn.microsoft.com/en-us/library/s2dy91zy.aspx
[15]: https://msdn.microsoft.com/en-us/library/1bbh5ae4.aspx
[16]: https://msdn.microsoft.com/en-us/library/hddt295a.aspx
[17]: https://msdn.microsoft.com/en-us/library/yf7b9sy7.aspx
[18]: https://msdn.microsoft.com/en-us/library/98bbex99.aspx
[19]: https://msdn.microsoft.com/en-us/library/ffsdktda.aspx
