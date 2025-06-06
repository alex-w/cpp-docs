---
title: "<thread> operators"
description: "Learn more about: <thread> operators"
ms.date: 11/04/2016
f1_keywords: ["thread/std::operator!=", "thread/std::operator>", "thread/std::operator>=", "thread/std::operator<", "thread/std::operator<<", "thread/std::operator<=", "thread/std::operator=="]
helpviewer_keywords: ["std::operator!= (thread)", "std::operator> (thread)", "std::operator>= (thread)", "std::operator< (thread)", "std::operator<< (thread)", "std::operator<= (thread)", "std::operator== (thread)"]
---
# `<thread>` operators

The `<thread>` header provides the following operators:

## <a name="op_gt_eq"></a> `operator>=`

Determines whether one `thread::id` object is greater than or equal to another.

```cpp
bool operator>= (
    thread::id Left,
    thread::id Right) noexcept
```

### Parameters

*Left*\
The left `thread::id` object.

*Right*\
The right `thread::id` object.

### Return Value

`!(Left < Right)`

### Remarks

This function does not throw any exceptions.

## <a name="op_gt"></a> `operator>`

Determines whether one `thread::id` object is greater than another.

```cpp
bool operator> (
    thread::id Left,
    thread::id Right) noexcept
```

### Parameters

*Left*\
The left `thread::id` object.

*Right*\
The right `thread::id` object.

### Return Value

`Right < Left`

### Remarks

This function does not throw any exceptions.

## <a name="op_lt_eq"></a> `operator<=`

Determines whether one `thread::id` object is less than or equal to another.

```cpp
bool operator<= (
    thread::id Left,
    thread::id Right) noexcept
```

### Parameters

*Left*\
The left `thread::id` object.

*Right*\
The right `thread::id` object.

### Return Value

`!(Right < Left)`

### Remarks

This function does not throw any exceptions.

## <a name="op_lt"></a> `operator<`

Determines whether one `thread::id` object is less than another.

```cpp
bool operator<(
    thread::id Left,
    thread::id Right) noexcept
```

### Parameters

*Left*\
The left `thread::id` object.

*Right*\
The right `thread::id` object.

### Return Value

**`true`** if *Left* precedes *Right* in the total ordering; otherwise, **`false`**.

### Remarks

The operator defines a total ordering on all `thread::id` objects. These objects can be used as keys in associative containers.

This function does not throw any exceptions.

## <a name="op_neq"></a> operator!=

Compares two `thread::id` objects for inequality.

```cpp
bool operator!= (
    thread::id Left,
    thread::id Right) noexcept
```

### Parameters

*Left*\
The left `thread::id` object.

*Right*\
The right `thread::id` object.

### Return Value

`!(Left == Right)`

### Remarks

This function does not throw any exceptions.

## <a name="op_eq_eq"></a> operator==

Compares two `thread::id` objects for equality.

```cpp
bool operator== (
    thread::id Left,
    thread::id Right) noexcept
```

### Parameters

*Left*\
The left `thread::id` object.

*Right*\
The right `thread::id` object.

### Return Value

**`true`** if the two objects represent the same thread of execution or if neither object represents a thread of execution; otherwise, **`false`**.

### Remarks

This function does not throw any exceptions.

## <a name="op_lt_lt"></a> `operator<<`

Inserts a text representation of a `thread::id` object into a stream.

```cpp
template <class Elem, class Tr>
basic_ostream<Elem, Tr>& operator<<(
    basic_ostream<Elem, Tr>& Ostr, thread::id Id);
```

### Parameters

*Ostr*\
A [basic_ostream](../standard-library/basic-ostream-class.md) object.

*Id*\
A `thread::id` object.

### Return Value

*Ostr*.

### Remarks

This function inserts *Id* into *Ostr*.

If two `thread::id` objects compare equal, the inserted text representations of those objects are the same.

## See also

[\<thread>](../standard-library/thread.md)
