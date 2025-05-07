---
permalink: /ut/
title: "ut"
categories:
  - project
tags:
  - project
---

boostext/ut is C++20 μ(micro)/Unit Testing framework compatible with modern C++ features. The following fork [https://github.com/calgray/ut](https://github.com/calgray/ut) is demonstrated in [ska-cpp-modules-template](https://gitlab.com/ska-telescope/templates/ska-cpp-modules-template/-/blob/main/ska-cpp-modules-template/foobar/tests) compatible with Clang 18.

Extensions added include:

* Explicit test runner `main` entrypoint support
* Test runner `--help`
* Test runner case filtering

An example test suite is as follows:

```cpp
// fibonacci.cppm

export module foobar.fibonacci;
import range_v3;
import std;

export template<std::integral T>
ranges::experimental::generator<T> fibonacci()
{
    // Largest index of a fibonacci number not greater than F is:
    // n(F) := floor((log(F+0.5) + log(sqrt(5)) / log(phi))
    constexpr int n_max =
        (std::log2(std::numeric_limits<T>::max()) + std::log2(std::sqrt(5.0)))
        / std::log2(std::numbers::phi_v<double>) - 1;
    T a=0, b=1;
    co_yield a;
    co_yield b;
    for (auto n : ranges::views::iota(0, n_max))
    {
        T s=a+b;
        co_yield s;
        a=b;
        b=s;
    }
}
```

```cpp
// test_fibonacci.cxx

import foobar.fibonacci;
import boost.ut;
import std;
import range_v3;

using namespace boost::ut;

template<typename T>
void test_fibonacci(int expected_count, T expected_max) {
    T first, last;
    auto v = fibonacci<T>() | ranges::views::take(1) | ranges::to<std::vector<T>>();
    first = ranges::front(v);
    for(auto i : fibonacci<T>()) { last = i; }

    expect(first == detail::value<T>(0));
    expect(last == detail::value<T>(expected_max));
    expect(ranges::distance(fibonacci<T>()) == detail::value<int>(expected_count));
    expect(ranges::is_sorted(fibonacci<T>() | ranges::to<std::vector<T>>()));
};

suite fibonacci_suite = [] {
    "int8"_test = [] {
        test_fibonacci<std::int8_t>(12, 89);
    };
    "uint8"_test = [] {
        test_fibonacci<std::uint8_t>(14, 233);
    };
    "int16"_test = [] {
        test_fibonacci<std::int16_t>(24, 28657);
    };
    "uint16"_test = [] {
        test_fibonacci<std::uint16_t>(25, 46368);
    };
    "int32"_test = [] {
        test_fibonacci<std::int32_t>(47, 1836311903);
    };
    "uint32"_test = [] {
        test_fibonacci<std::uint32_t>(48, 2971215073);
    };
    "int64"_test = [] {
        test_fibonacci<std::int64_t>(93, 7540113804746346429l);
    };
    "uint64"_test = [] {
        test_fibonacci<std::uint64_t>(94, 12200160415121876738ul);
    };
};

```
