---
description: "Learn more about: safe_cast (C++/CLI and C++/CX)"
title: "safe_cast (C++/CLI and C++/CX)"
ms.date: "10/12/2018"
ms.topic: "reference"
f1_keywords: ["safe_cast", "safe_cast_cpp", "stdcli::language::safe_cast"]
helpviewer_keywords: ["safe_cast keyword [C++]"]
---
# safe_cast (C++/CLI and C++/CX)

The **`safe_cast`** operation returns the specified expression as the specified type. If the operation isn't successful, it throws an `InvalidCastException`.

## All Runtimes

(There are no remarks for this language feature that apply to all runtimes.)

### Syntax

```cpp
[default]:: safe_cast< type-id >( expression )
```

## Windows Runtime

Use **`safe_cast`** to change the type of a specified expression. If you expect a variable or parameter to be convertible to a certain type, use **`safe_cast`** without a **try-catch** block to detect programming errors during development. For more information, see [Casting (C++/CX)](../cppcx/casting-c-cx.md).

### Syntax

```cpp
[default]:: safe_cast< type-id >( expression )
```

### Parameters

*type-id*<br/>
The type to convert *expression* to. A handle to a reference or value type, a value type, or a tracking reference to a reference or value type.

*expression*<br/>
An expression that evaluates to a handle to a reference or value type, a value type, or a tracking reference to a reference or value type.

### Remarks

**`safe_cast`** throws `InvalidCastException` if it can't convert *expression* to the type specified by *type-id*. To catch `InvalidCastException`, specify the [/EH (Exception Handling Model)](../build/reference/eh-exception-handling-model.md) compiler option, and use a **try/catch** statement.

### Requirements

Compiler option: `/ZW`

### Examples

The following code example demonstrates how to use **`safe_cast`** with the Windows Runtime.

```cpp
// safe_cast_ZW.cpp
// compile with: /ZW /EHsc

using namespace default;
using namespace Platform;

interface class I1 {};
interface class I2 {};
interface class I3 {};

ref class X : public I1, public I2 {};

int main(Array<String^>^ args) {
   I1^ i1 = ref new X;
   I2^ i2 = safe_cast<I2^>(i1);   // OK, I1 and I2 have common type: X
   // I2^ i3 = static_cast<I2^>(i1);   C2440 use safe_cast instead
   try {
      I3^ i4 = safe_cast<I3^>(i1);   // Fails because i1 is not derived from I3.
   }
   catch(InvalidCastException^ ic) {
   wprintf(L"Caught expected exception: %s\n", ic->Message);
   }
}
```

```Output
Caught expected exception: InvalidCastException
```

## Common Language Runtime

**`safe_cast`** changes the type of an expression and generates verifiable MSIL code.

### Syntax

```cpp
[cli]:: safe_cast< type-id >( expression )
```

### Parameters

*`type-id`*\
A handle to a reference or value type, a value type, or a tracking reference to a reference or value type.

*`expression`*
An expression that evaluates to a handle to a reference or value type, a value type, or a tracking reference to a reference or value type.

### Remarks

The expression `safe_cast<`*type-id*`>(`*expression*`)` converts the operand *expression* to an object of type *type-id*.

The compiler accepts a [`static_cast`](../cpp/static-cast-operator.md) in most places that it accepts a **`safe_cast`**. However, **`safe_cast`** always produces verifiable MSIL, whereas a **`static_cast`** might produce unverifiable MSIL. For more information on verifiable code, see [Pure and Verifiable Code (C++/CLI)](../dotnet/pure-and-verifiable-code-cpp-cli.md) and [`Peverify.exe` (PEVerify Tool)](/dotnet/framework/tools/peverify-exe-peverify-tool).

Like **`static_cast`**, **`safe_cast`** invokes user-defined conversions.

For more information about casts, see [Casting Operators](../cpp/casting-operators.md).

**`safe_cast`** doesn't apply a **`const_cast`** (cast away **`const`**).

**`safe_cast`** is in the cli namespace. For more information, see [Platform, default, and cli Namespaces](platform-default-and-cli-namespaces-cpp-component-extensions.md).

For more information on **`safe_cast`**, see:

- [C-Style Casts with /clr (C++/CLI)](c-style-casts-with-clr-cpp-cli.md)
- [How to: Use safe_cast in C++/CLI](../dotnet/how-to-use-safe-cast-in-cpp-cli.md)

### Requirements

Compiler option: `/clr`

### Examples

One example of where the compiler doesn't accept a **`static_cast`** but accepts a **`safe_cast`** is for casts between unrelated interface types. With **`safe_cast`**, the compiler doesn't issue a conversion error and performs a check at runtime to see if the cast is possible.

```cpp
// safe_cast.cpp
// compile with: /clr
using namespace System;

interface class I1 {};
interface class I2 {};
interface class I3 {};

ref class X : public I1, public I2 {};

int main() {
   I1^ i1 = gcnew X;
   I2^ i2 = safe_cast<I2^>(i1);   // OK, I1 and I2 have common type: X
   // I2^ i3 = static_cast<I2^>(i1);   C2440 use safe_cast instead
   try {
      I3^ i4 = safe_cast<I3^>(i1);   // fail at runtime, no common type
   }
   catch(InvalidCastException^) {
      Console::WriteLine("Caught expected exception");
   }
}
```

```Output
Caught expected exception
```

## See also

[Component Extensions for .NET and UWP](component-extensions-for-runtime-platforms.md)
