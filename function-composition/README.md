## Problem

Consider that you have a price for your customer:

```
const price = 1000
```

You want to add `10%` tax to it:

```
const priceAfterApplyingTax = price * (1 + 10/100)
```

Now You want to add `400` for shipping to it:

```
const priceAfterApplyingTaxAndShipping = priceAfterApplyingTax + 400
```

And at last, you want to apply `20%` discount:

```
const priceAfterApplyingTaxAndShippingAndDiscount = priceAfterApplyingTaxAndShipping * (1 - 20/100)
```


We get the final result, but actually it's not clear what's going on, a lot of variable declaration,
a lot of mathematics expressions. And the most important problem, is that what if we want to do
the same process for another price? We have to write all this codes again:


```
const price2 = 1000
const price2AfterApplyingTax = price2 * (1 + 10/100)
const price2AfterApplyingTaxAndShipping = price2AfterApplyingTax + 400
const price2AfterApplyingTaxAndShippingAndDiscount = price2AfterApplyingTaxAndShipping * (1 - 20/100)
```

## Define functions

It's better to create functions for our logic:

```
const applyShippingBy400 = amount => amount + 400
const applyTaxBy10percent = amount => amount * (1 + 10 / 100)
const applyDiscountBy20percent = amount => amount * (1 - 20 / 100)

const price = 1000
const priceAfterApplyingTax = applyTaxBy10percent(price)
const priceAfterApplyingTaxAndShipping = applyShippingBy400(priceAfterApplyingTax)
const priceAfterApplyingTaxAndShippingAndDiscount = applyDiscountBy20percent(priceAfterApplyingTaxAndShipping)
```

## Function Composition

Instead of creating variables, you can pass the value of first function, to the next function:

```
const applyTaxBy10percent = amount => amount * (1 + 10 / 100)
const applyShippingBy400 = amount => amount + 400
const applyDiscountBy20percent = amount => amount * (1 - 20 / 100)

const price = 1000
const finalPrice = (
  applyDiscountBy20percent(
    applyShippingBy400(
      applyTaxBy10percent(price)
    )
  )
)
```

## Ramda

[Ramda](http://ramdajs.com/) is a practical functional library for JavaScript programmers.
So your code will become more functional style and so more readable. The above example will be 
code in Ramda like this:

```
const applyTaxBy10percent = amount => amount * (1 + 10 / 100)
const applyShippingBy400 = amount => amount + 400
const applyDiscountBy20percent = amount => amount * (1 - 20 / 100)

const price = 1000
const finalPrice = R.pipe(
  applyTaxBy10percent,
  applyShippingBy400,
  applyDiscountBy20percent
)(price)
```

## Function Creation

We could make the code better. What if we want to apply this rules to another price, but
with different tax and discount.

```
const applyTaxPercent = tax => amount => amount * (1 + tax / 100)
const applyShipping = shipping => amount => amount + shipping
const applyDiscountPercent = discount => amount => amount * (1 - discount / 100)

const price = 1000
const priceFinal = R.pipe(
  applyTaxPercent(10),
  applyShipping(400),
  applyDiscountPercent(20)
)(price)

const price2 = 2000
const price2Final = R.pipe(
  applyTaxPercent(20),
  applyShipping(800),
  applyDiscountPercent(50)
)(price2)
```

As you can see, coding functional programming is more readable and all parts are
small enough to test and debug easily.