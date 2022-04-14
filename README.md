<div align="center">
    <img src="https://github.com/1inch/farming/blob/master/.github/1inch_github_w.svg#gh-light-mode-only">
    <img src="https://github.com/1inch/farming/blob/master/.github/1inch_github_b.svg#gh-dark-mode-only">
</div>

# Utils library for contracts and tests

[![Build Status](https://github.com/1inch/solidity-utils/workflows/CI/badge.svg)](https://github.com/1inch/solidity-utils/actions)
[![Coverage Status](https://coveralls.io/repos/github/1inch/solidity-utils/badge.svg?branch=master)](https://coveralls.io/github/1inch/solidity-utils?branch=master)
[![NPM Package](https://img.shields.io/npm/v/@1inch/solidity-utils.svg)](https://www.npmjs.org/package/@1inch/solidity-utils)

### About

This repository contains frequently used smart contracts, libraries and interfaces. Also it contains utils which are used in tests.

### Solidity

|directory|.sol|description|
|--|--|--|
|contracts|`EthReceiver`||
|contracts|`Permitable`||
|contracts|`GasChecker`||
|contracts/interfaces|`IDaiLikePermit`|Interface of token which has `permit` method like DAI token|
|contracts/interfaces|`IWETH`|WETH token interface|
|contracts/libraries|`AddressArray`|library for work with array of addresses|
|contracts/libraries|`AddressSet`|library for work with set of addresses|
|contracts/libraries|`RevertReasonParser`|library parse the message from reverted method to readble format|
|contracts/libraries|`StringUtil`|optimized methods to convert data to hex|
|contracts/libraries|`UniERC20`||

### JS

|module|function|descrption|
|--|--|--|
|asserts|`assertThrowsAsync(action, msg)`|checks the async function `action()` thrown with message `msg`|
|asserts|`assertRoughlyEqualValues(expected, actual, relativeDiff)`|checks the `expected` value is equal to `actual` value with `relativeDiff` precision|
|utils|`timeIncreaseTo(seconds)`|increases blockchain time to `seconds` sec|
|utils|`trackReceivedToken(token, wallet, txPromise, ...args)`|returns amount of `token` which recieved the `wallet` in async method `txPromise` with arguments `args`|
|utils|`trackReceivedTokenAndTx(token, wallet, txPromise, ...args)`|returns transaction info and amount of `token` which recieved the `wallet` in async method `txPromise` with arguments `args`|
|utils|`fixSignature(signature)`|patchs ganache's signature to geth's version|
|utils|`signMessage(signer, messageHex) `|signs `messageHex` with `signer` and patchs ganache's signature to geth's version|
|utils|`countInstructions(txHash, instruction)`|counts amount of `instruction` in transaction with `txHash` hash|
|profileEVM|`profileEVM(txHash, instruction, optionalTraceFile)`|the same as the `countInstructions()` with option of writing all trace to `optionalTraceFile`|
|profileEVM|`gasspectEVM(txHash, options, optionalTraceFile)`|returns all used operations in `txHash` transaction with `options` and their costs with option of writing all trace to `optionalTraceFile`|

### UTILS

#### Docify

Generates documentation in markdown format from natspec docs

##### Usage
Add to `package.json` file solidity compiler version and shortcut to run command

`devDependencies` section

```
"solc": "0.8.12",
```

`scripts` section
```
"docify": "npx solidity-utils-docify"
```

...

#### Test documentation generator (test-docgen)
Script generates documentation for tests in markdown format.
Give descriptions for `describe` and `it` sections and build documentation using these descriptions.

##### Example
Test described as shown below

```JavaScript
// Test suite
describe('My feature', function() {
    // Nested test suite 
    describe("My subfeature", function() {
        /*
            **Test case 1**
            Test case should work
         */
        it("My case", function() {
        // code here
        })
    })
})
```
will generated the following output
```Markdown

# My feature

Test suite

## My subfeature

Nested test suite 

### My case

**Test case 1**
Test case should work
```

##### Installation
- Before use install documentation parser
```
yarn add acquit --dev
```
- Optionally configure script for default usage. Add to `script` section in `package.json` 
```
"test:docs": "npx test-docgen"
```
- Optionally configure script for generating test list only. Add to `script` section in `package.json` 
```
"test:docs": "npx test-docgen -l"
```

##### Usage
If script configured
```
yarn test:docs
```
or
```
npx test-docgen
```

Available parameters
```
Options:
  -i, --input <input>      tests directory (default: "test")
  -x, --exclude [exclude]  exclude directories and files. omit argument to exclude all subdirectories (default: false)
  -o, --output <output>    file to write output (default: "TESTS.md")
  -c, --code               include code (default: false)
  -l, --list               list tests only, do not include description (default: false)
  -d, --debug              debug mode (default: false)
  -h, --help               display help for command
```
##### Examples
Generate docs with default input and output
```
npx test-docgen
```

Generate docs for files in folders `tests/mocks` and `tests/utils`
```
npx test-docgen -i "tests/mocks;tests/utils"
```
Exclude from docs file `test/mock-exclude.js` and `test/utils folder`
```
npx test-docgen -x "tests/mock-exclude.js;tests/utils"
```
Generate list of tests only
```
npx test-docgen -l
```