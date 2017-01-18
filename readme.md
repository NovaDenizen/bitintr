# Portable Bitwise Manipulation Intrinsics

[![crates.io version][crate-shield]][crate] [![Travis build status][travis-shield]][travis] [![Coveralls.io code coverage][coveralls-shield]][coveralls] [![Docs][docs-shield]][docs] [![License][license-shield]][license]

> `0b0000_0010_1001_1010`

The intrinsics are named after their CPU instruction and organized in modules
named after their instruction set: `bitintr::{instruction_set}::{intrinsic_name}`.

They are implemented for all integer types _except_ `u128/i128`. Whether a
fallback software implementation is used depends on the integer types involved
and the instruction sets supported by the target.

The following instruction sets are implemented:

- [`ABM`][abm_link]: Advanced Bit Manipulation instructions.
- [`TBM`][tbm_link]: Trailing Bit Manipulation instructions.
- [`BMI`][bmi1_link]: Bit Manipulation Instruction Set 1.0.
- [`BMI2`][bmi2_link]: Bit Manipulation Instruction Set 2.0.

## Example

```rust
extern crate bitintr;
use bitintr::bmi2::*;

fn main() {
    let x = 1;
    let y = 0;
    // Intrinsics can be used as methods:
    let method_call = x.pdep(y);
    // And as free function calls:
    let free_call = pdep(x, y);
    assert_eq!(method_call, free_call);
}
```

## Supported compilers

> The minimum required rustc version is >= **1.4.0**.

When compiled with a rust stable compiler the intrinsics are implemented using
the software fallback. In release builds LLVM _often_ generates the corresponding
CPU instruction.

When compiled with a rust nightly compiler the following features are used to
generate the corresponding CPU instruction in _all_ cases:

- `cfg_target_feature` for target-dependent behavior,
- `platform_intrinsics` for using the bitwise manipulation intrinsics, and
- `u128` support for _efficient_ 64bit multiplication.

## License

Licensed under the [MIT license][license].

## Contribution

Yes please! Just note that all contributions shall be licensed as above without
any additional terms or conditions.

<!-- Links -->
[travis-shield]: https://img.shields.io/travis/gnzlbg/bitintr.svg?style=flat-square
[travis]: https://travis-ci.org/gnzlbg/bitintr
[coveralls-shield]: https://img.shields.io/coveralls/gnzlbg/bitintr.svg?style=flat-square
[coveralls]: https://coveralls.io/github/gnzlbg/bitintr
[docs-shield]: https://img.shields.io/badge/docs-online-blue.svg?style=flat-square
[docs]: https://gnzlbg.github.io/bitintr
[license-shield]: https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square
[license]: https://github.com/gnzlbg/bitintr/blob/master/license.md
[crate-shield]: https://img.shields.io/crates/v/bitintr.svg?style=flat-square
[crate]: https://crates.io/crates/bitintr
[abm_link]: https://en.wikipedia.org/wiki/Bit_Manipulation_Instruction_Sets#ABM_.28Advanced_Bit_Manipulation.29
[tbm_link]: https://en.wikipedia.org/wiki/Bit_Manipulation_Instruction_Sets#TBM_.28Trailing_Bit_Manipulation.29
[bmi1_link]: https://en.wikipedia.org/wiki/Bit_Manipulation_Instruction_Sets#BMI1_.28Bit_Manipulation_Instruction_Set_1.29
[bmi2_link]: https://en.wikipedia.org/wiki/Bit_Manipulation_Instruction_Sets#BMI2_.28Bit_Manipulation_Instruction_Set_2.29
