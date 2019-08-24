---
layout: post
title: Fastest JS Loop
subtitle: Finding the fastest loop in Javascript
tags: [js]
---

There are a few different ways to do loops in JavaScript. Lets take a look at which one is the fastest.

## Setup

I'm running this on my Mac, with a 2 GHz Intel Core i5 with Node v12.1.0. Lets have an array that we just run through and do some basic operations.

Basic setup of the array
```javascript
var arr = new Array(1000)
for(var i = 0; i < arr.length; i++){
   arr[i] = i
}
```

#### For Loop
```javascript
var sum = 0
for(var i = 0; i < arr.length; i++){
   sum += arr[i] * 2
}
console.log("SUM: " + sum);
```

#### Do While Loop
```javascript
var sum = 0
var i = 0
do {
   sum += arr[i] * 2
   i++
} while ( i < arr.length )
console.log("SUM: " + sum);
```

#### While Loop
```javascript
var sum = 0
var i = 0
while (i < arr.length) {
   sum += arr[i] * 2
   i++
}
console.log("SUM: " + sum);
```

#### For Of
```javascript
var sum = 0
for(var i of arr){
   sum += i * 2
}
console.log("SUM: " + sum);
```

#### For Each
```javascript
var sum = 0
arr.forEach(i => {
   sum += i * 2
})

console.log("SUM: " + sum);
```

You can take a look at [all the code](https://gist.github.com/peterfoxflick/ab6db2fa436eb5755c748cbb4da8c813) on Github.


## The Test

So each loop got its own file and a simple Ruby program timed each one. After
ten thousand times hopefully a pattern emerges. Its entirely possible that all the loops run in the same amount of time since this is all being converted to a lower level.

## Results


![Graph of results](https://lh3.googleusercontent.com/ogvxVhCEEf00UoiWYlh25AXZGof4UdAWBoL4or1ePDZV4_pvVfc47RtUqBHsx62vaGRhx8NDqdPgj5Q8wgVge_DaAb1sGGMUy08_X3zwPFIjqdunr19C6tgtoca7VkloXrhvk5UIlmhjd-bp7jRX3QI_MQLPpa9AxD0ibPfTYW_fcfPmWneMVmWlv_aVL0SGbNfQraeG-PwWM5Dk5vColkRFPtqk22PW7fVpDKCdd2XoxXbfvUb9Zk-gjWaHxoijBoC48v4GnrD2ACQFbUJi6WOOjllw9CmidENMIy9ajz5IaOHHEncg6teSZujaZLEXMQjsuBFV03F7-sAX3BvI4PhpRcFXx33vrs5QeCJYVK3ldW_sTfFPw7-kyUoO8BlLs0hWmPq54CjVnipkFDwM_fjogbS8RZRZ-kE0XALJwM8k1ORciu0VlWC-uFPLhHLpfCnfGL9L3t5czAaJUnEIS5cCLL4xMYtBt6l0Jon61Xo0e4UL34gj8_Ml9whM2QhQbKtmCjLTFcsqlRbvNegAHnkAKt2sfwTP0f66POu3RL3Zgbo0LIA1LmuTUXccG1fE0f1fTn_yytaO0PHtTLRWU86cp9hyhLP9q7I4L-pyazV6TWs4Vh9EraC-g5xeIxNjLBpN9-wRtHbBvfn3rniHyb16HP7AEJnHuCA2PFD00RMcC9aF4bttD_jUeDB2OAGpjxlsu7XM5CGYPerVIAwDTKfggQ=w1128-h856-no){: .center-block :}

| Loop | Average (s) |
|----|---|
| For Of	| 0.0590751585999955 |
| For Loop | 0.0632383086000213 |
| Do While | 0.0814892920999774 |
| While | 0.08505968210001450 |
| For Each | 0.195300551599986 |

There you have it. For-in is the fastest but is not recommended since it can be out of order, leaving the **For loop as the best/fastest loop.** That being said for each is an easy option but terribly slow in comparison.
