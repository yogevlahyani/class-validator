
# [0.10.0-rc.1](https://github.com/typestack/class-validator/compare/v0.9.1...v0.10.0-rc.1) (2019-07-26)

### Bug Fixes

* add correct signature for custom error message handler ([249c41d](https://github.com/typestack/class-validator/commit/249c41d))

### Features

* add `IsISO31661Alpha3` and `IsISO31661Alpha2` validators ([#273](https://github.com/typestack/class-validator/issues/273)) ([55c57b3](https://github.com/typestack/class-validator/commit/55c57b3))
* **IsDecimal:** implement `IsDecimal` from validatorjs ([#359](https://github.com/typestack/class-validator/issues/359)) ([b4c8e21](https://github.com/typestack/class-validator/commit/b4c8e21))
* add `isPort` decorator ([#282](https://github.com/typestack/class-validator/issues/282)) ([36684ec](https://github.com/typestack/class-validator/commit/36684ec))
* allow validate Map/Set ([#365](https://github.com/typestack/class-validator/issues/365)) ([f6fcdc5](https://github.com/typestack/class-validator/commit/f6fcdc5))
* new `ValidatePromise` decorator - resolve promise before validate ([#369](https://github.com/typestack/class-validator/issues/369)) ([35ec04d](https://github.com/typestack/class-validator/commit/35ec04d))
* replace instanceof Promise and support Promise/A+  ([#310](https://github.com/typestack/class-validator/issues/310)) ([59eac09](https://github.com/typestack/class-validator/commit/59eac09))
* `isNumberString` now accept validator.js `IsNumericOptions` as second parameter ([#262](https://github.com/typestack/class-validator/issues/262))

### BREAKING CHANGES

* update @types/validator from 10.4.0 to version 10.11.2 - please check it's [changelog][validator-js-release-notes] ([cb960dd](https://github.com/typestack/class-validator/commit/cb960dd))
* `isDateString` now check to match only entire ISO Date ([#275](https://github.com/typestack/class-validator/issues/275)) ([5012464](https://github.com/typestack/class-validator/commit/5012464))
* remove `IsCurrencyOptions`, `IsURLOptions`, `IsEmailOptions`, `IsFQDNOptions` interfaces and replace with interfaces from `@types/validator`


## [0.9.1](https://github.com/typestack/class-validator/compare/v0.9.0...v0.9.1)

### Features

* added option to pass custom context for the decorators

### Bug Fixes

* validating against a schema will validate against that one instead of every registered one

# [0.9.0](https://github.com/typestack/class-validator/compare/v0.8.5...v0.9.0) [BREAKING CHANGE]

### Features

* updated [validator.js][validator-js] from 9.2.0 to 10.4.0 (Check it's [changelog][validator-js-release-notes] for what has changed.)
  * until now fractional numbers was not allowed in the `IsNumberString` decorator, now they are allowed
  * until now Gmail addresses could contain multiple dots or random text after a `+` symbol, this is not allowed anymore 
* `IsPhoneNumber` decorator has been added which uses the [google-libphonenumber][google-libphonenumber] libary to validate international phone numbers accurately

### Bug Fixes

* update `IsURLOptions` to match underlying validator host list options
* added a console warning when no metadata decorator is found as it's possibly not intended
* the `Min` and `Max` decorator will corectly show an inclusive error message when failing
* fixed a runtime error when `validationArguments.value` is not a string

## [0.8.5](https://github.com/typestack/class-validator/compare/v0.8.4...v0.8.5)

### Bug Fixes

* remove `ansicolor` package, because it's incompatible with IE

## [0.8.4](https://github.com/typestack/class-validator/compare/v0.8.3...v0.8.4)

### Features

* `ValidatorOptions` now has a `forbidUnknownValues` key to prevent unknown objects to pass validation
  * it's highly advised to turn this option on
  * now this option defaults to `false` but will be default to `true` after the **1.0** release

## [0.8.3](https://github.com/typestack/class-validator/compare/v0.8.2...v0.8.3)

### Bug Fixes

* handle when `target` property is undefined when calling `ValidationError.toString()`

## [0.8.2](https://github.com/typestack/class-validator/compare/v0.8.1...v0.8.2)

### Features

* added `ValidationError.toString()` method for easier debugging
* added `printError` method to pretty-print errors in NodeJS or the browser

### Bug Fixes

* fixed wrong type info in `ValidatorOptions`
* fixed wrong type info in `ValidationSchema` \(the `options` key now is optional\)
* corrected `IsNumericString` to `IsNumberString` in the README
* fixed type of `host_whitelist` and `host_backlist` in `IsURLOptions`

## [0.8.1](https://github.com/typestack/class-validator/compare/v0.8.0...v0.8.1)

### Bug Fixes

* fixed wrong type info in `ValidatorOptions`

# 0.8.0 \[BREAKING CHANGE\]

### Features

* updated [validator.js][validator-js] from 7.0.0 to 9.2.0 (Check it's [changelog][validator-js-release-notes] for what has changed.)

  This caused breaking change, if you used the `IsUrl` decorator to validate `localhost` as a valid url, from now you must use the `require_tld: false` option

  ```typescript
  @IsUrl({ require_tld: false})
  url: string;
  ```

* added `@IsInstance` decorator and `validator.isInstance(value, target)` method.
* changed `@IsNumber` decorator has been changed to `@IsNumber(options: IsNumberOptions)`
* added option to strip unknown properties \(`whitelist: true`\)
* added option to throw error on unknown properties \(`forbidNonWhitelisted: true`\)
* added `@Allow` decorator to prevent stripping properties without other constraint

### Bug Fixes

* fixed issue with `@IsDateString` now it allow dates without fraction seconds to be set
* fixed issue with `@IsDateString` now it allow dates without with timezones to be set
* `@ValidateNested` correctly generates validation error on non object and non array values

## 0.6.7

### Bug Fixes

* fixed issue with `@ValidateNested` when nested property is not defined and it throw an error \(\#59\)

## 0.6.5

### Bug Fixes

* fixed bugs with `@IsUrl`, `@IsEmail` and several other decorators

## 0.6.4

### Features

* added `@IsMilitaryTime` decorator.

## 0.6.3

### Features

* added `validateOrReject` method which rejects promise instead of returning array of errors in resolved result

## 0.6.1

### Features

* added `@IsArray` decorator.

# 0.6.0 \[BREAKING CHANGE\]

### Features

* breaking change with `@ValidateNested` on arrays: Validator now groups the validation errors by sub-object, rather than them all being grouped together. See \#32 for a demonstration of the updated structure.
* added `@ValidateIf` decorator, see conditional validation in docs.

# 0.5.0 \[BREAKING CHANGE\]

### Features

* async validations must be marked with `{ async: true }` option now.

  This is optional, but it helps to determine which decorators are async to prevent their execution in `validateSync` method.

* added `validateSync` method that performs non asynchronous validation and ignores validations that marked with `async: true`.
* there is a breaking change in `registerDecorator` method. Now it accepts options object.
* breaking change with `@ValidatorConstraint` decorator. Now it accepts option object instead of single name.

## 0.4.1

### Bug Fixes

* fixed issue with wrong source maps packaged

# 0.4.0 \[BREAKING CHANGE\]

### Features

* everything should be imported from "class-validator" main entry point now
* `ValidatorInterface` has been renamed to `ValidatorConstraintInterface`
* contain can be set in the main entry point now
* some decorator's names changed. Be aware of this
* added few more non-string decorators
* validator now returns array of ValidationError instead of ValidationErrorInterface. Removed old ValidationError
* removed all other validation methods except `validator.validate`
* finally validate method is async now, so custom async validations are supported now
* added ability to validate inherited properties
* added support of separate validation schemas
* added support of default validation messages
* added support of special tokens in validation messages
* added support of message functions in validation options
* added support of custom decorators
* if no groups were specified, decorators with groups now are being ignored
* changed signature of the `ValidationError`. Now if it has nested errors it does not return them in a flat array

### Bug Fixes

* fixed all decorators that should not work only with strings

# 0.3.0

### Features

* package has changed its name from `validator.ts` to `class-validator`.
* sanitation functionality has been removed from this library. Use [class-sanitizer][1] instead.

[1]: https://github.com/typestack/class-validator/class-sanitizer
[validator-js]: https://github.com/chriso/validator.js
[validator-js-release-notes]: https://github.com/chriso/validator.js/blob/master/CHANGELOG.md
[google-libphonenumber]: https://github.com/ruimarinho/google-libphonenumber