---
title: "<allocators> operators"
description: "Learn more about: <allocators> operators"
ms.date: 11/04/2016
f1_keywords: ["allocators/std::operator!=", "allocators/std::operator=="]
---
# `<allocators>` operators

These are the global template operator functions defined in `<allocators>`. For class member operator functions, see the class documentation.

## <a name="op_neq"></a> `operator!=`

Tests for inequality between allocator objects of a specified class.

```cpp
template <class Type, class Sync>
bool operator!=(
    const allocator_base<Type, Sync>& left,
    const allocator_base<Type, Sync>& right);
```

### Parameters

*`left`*\
One of the allocator objects to be tested for inequality.

*`right`*\
One of the allocator objects to be tested for inequality.

### Return Value

**`true`** if the allocator objects are not equal; **`false`** if allocator objects are equal.

### Remarks

The template operator returns `!(left == right)`.

## <a name="op_eq_eq"></a> `operator==`

Tests for equality between allocator objects of a specified class.

```cpp
template <class Type, class Sync>
bool operator==(
    const allocator_base<Type, Sync>& left,
    const allocator_base<Type, Sync>& right);
```

### Parameters

*`left`*\
One of the allocator objects to be tested for equality.

*`right`*\
One of the allocator objects to be tested for equality.

### Return Value

**`true`** if the allocator objects are equal; **`false`** if allocator objects are not equal.

### Remarks

This template operator returns `left.equals(right)`.

## See also

[`<allocators>`](allocators-header.md)
