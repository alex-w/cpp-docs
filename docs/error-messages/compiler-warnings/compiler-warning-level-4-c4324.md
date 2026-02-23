---
title: "Compiler Warning (level 4) C4324"
description: "Learn more about: Compiler Warning (level 4) C4324"
ms.date: 07/22/2025
f1_keywords: ["C4324"]
helpviewer_keywords: ["C4324"]
---
# Compiler Warning (level 4) C4324

> '*type*': structure was padded due to alignment specifier

## Remarks

Padding was added at the end of a class/struct/union because you specified an alignment specifier, such as [`alignas`](../../cpp/alignas-specifier.md) or [`__declspec(align)`](../../cpp/align-cpp.md).

## Example

For example, `S1`, `S2`, `U1`, and `C1` generate C4324 because padding is added when the specified alignment is greater than the default alignment for each:

```cpp
// C4324.cpp
// compile with: /W4 /c

struct alignas(8) S1 // C4324
{
    int i;
};   // C4324

union alignas(16) U1
{
    int i;
    float f;
};  // C4324

class alignas(8) C1
{
public:
    int i = 0;
}; // C4324

struct alignas(4) S3
{
    int i;
};   // OK
```
