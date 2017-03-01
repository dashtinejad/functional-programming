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
console.log(price2AfterApplyingTaxAndShippingAndDiscount)
```

