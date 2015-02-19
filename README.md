# rules-when
Simple When Rule Construction

[W I P Initial Feb 18th, 2015]


## BizRez When Rules

A simple way to dynamically create when rules - A great example how to use the new Function instead of the 'evil' eval.

<img src="http://upload.wikimedia.org/wikipedia/commons/d/dc/Magneto,_longitudinal_section_(Rankin_Kennedy,_Modern_Engines,_Vol_II).jpg" align="right" width="200px" />

## Intro

Simplicity is elegance.

What we need is a descriptive way to tag Biz(i)ness Rules and catalog, inventory, usage, and change dynamically.
Javascript provides a simple way of dynamically creating functions on the fly.


Prime directives, and ables ...
- Easy to understand the code
- Thin
- Self documenting
- Pattern - not an enforcement
- Crazy fast
- Secure from XXS


## Dependencies

-  Mocha.js for for test infecting the code (good infection)

## A few Use Cases for Usage

- Validations
- Calculations
- Automated business rules - decision engine
- Home security, sprinkler systems, and darn maybe your car...

## Benefits

- Repository of rules
- Traceability
- Modify the rule not the code
- Dynamic changeability - conditions change so do the execution
- Easy to understand and modify
- Extensible
- Maintainable
- Reusable
- Chainable
- Micro foot print and scalable

## Example Setup

```

//Example Setup

var when = {

    isPerson: "return object.isPerson === true //Comment",
    hasLicense: "return object.license === true //Comment",
    isPersonAndHasLicense: "return when['isPerson'](object) && when['hasLicense'](object)",
    payTax: "return object.payTax === true",
    doHula: "return when['isPerson'](object) && when['hasLicense'](object) && when['payTax'](object)"

}

var calculate = {

    adder: "return object.a + object.b //Comment",
    calculateTax: "return object.amount * 1.8",
    addTax: "if (when['payTax'](object)) {return calculate['calculateTax'](object)}; return 0",
    mutate: "object.tada = 'hello Moto'; return true"

}

//Describe Decision Table
var decisionTable = {

    calcNumber: [["return when['isPerson'](object)", "return calculate['adder'](object)", "return true"],
        ["return when['isPerson'](object)", "return calculate['calculateTax'](object)", "return true"],
        ["return when['isPerson'](object)", "return calculate['calculateTax'](object)", "return true"]
    ]

}

```

## Example Run

```
rules.loadWhenRules(when);
rules.loadCalcualtions(calculate);
rules.loadDecisionTable(decisionTable);

var person = {isPerson: true, license: true, a: 5, b: 10, amount: 500, payTax: true};

console.log("isPerson:" + rules.when('isPerson', person));
console.log("hasLicense:" + rules.when('hasLicense', person));
console.log("adder:" + rules.calculate('adder', person));
console.log("addTax:" + rules.calculate("addTax", person));
console.log("isPersonAndHasLicense:" + rules.when('isPersonAndHasLicense', person));
rules.calculate('mutate',person);
console.log(person.tada);
console.log("decisiontable result:" + rules.decisionTable('calcNumber', person));
console.log("doHula:" + rules.when('doHula',person));

```

## Mocha Test

mocha ./lib/test
