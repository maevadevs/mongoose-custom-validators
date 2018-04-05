# Custom Validators for Mongoose Schema

This repository contains some custom validators for Mongoose Schema. It complements the validators that are already found within [Mongoose](http://mongoosejs.com/docs/validation.html) itself *AND* the [`validator`](https://www.npmjs.com/package/validator) package.

## List of Custom Validators

- [isValidPassword](#isValidPassword)

### `isValidPassword`<a name="isValidPassword"></a>

#### Signature: `(String, require = defaultRequire) => Boolean`

Validates password string against the requirements properties. By default, we opt for a strong password the must meet the following criterias:

    defaultRequire = {
      minlength: 10,   // <Number>   At least 10 characters long (optional)
      uppercase: true, // <Boolean>  Have at least 1 uppercase character
      lowercase: true, // <Boolean>  Have at least 1 lowercase character
      number: true,    // <Boolean>  Have at least 1 number
      nonalpha: true   // <Boolean>  Have at least 1 Nonalpha character
    }

#### Usage

    const { isValidPassword } = require('./customValidators.js')

To override some or all of the defaults, pass in an object with the criterias properties to override. **Non-overriden criterias will be using the `defaultRequire`.** The only acceptable properties are the ones listed above under the `defaultRequire`

If using just the `defaultRequire`, simply pass the function as the validator

    validate: {
      validator: isValidPassword,
      message: 'Password must have at least: 1 uppercase letter, 1 lowercase letter, 1 number, and 1 special character.'
    }

If using with custom `userRequire`, pass validator through an anonymous function that takes the password string

    validate: {
      validator: (str) => isValidPassword(str, { uppercase: false }),
      message: 'Password must have at least: 1 lowercase letter, 1 number, and 1 special character.'
    }