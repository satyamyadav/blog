---
title: understanding es6 pipeline O|>erator
cover: /img/screenshots/es6-pipeline.png
date: 
categories:
  - code
tags:
  - lodash
  - es6
  - javascript
  - experimental
  - ESNext
---

Pipeline operator `|>` is a readable way of writing chained functions. The operator is currently at stage 1 of tc39 proposal (ESNext Proposal).

<!-- more  -->

The pipeline operator provides a syntactic sugar to call a function with single argument.

`expression |> function` 

or call multiple functions as 

`expression |> fn1 |> fn2 |> fn3`

each function gets the result from its preceeding function as input and passes the result to next function i.e. input (argument/expression) is piped through and complete pipeline.

Let's look at some examples :


Lets define the `double` and `increment` functions used in each example.

{% codeblock %}

const double = n => n * 2; 
const increment = n => n + 1;

{% endcodeblock %}

**The function(argument) way:**


{% codeblock %}

// without chaining

double(increment(double(10)));  //42

{% endcodeblock %}


**using lodash**

{% codeblock %}

const _ = require('lodash');

_.mixin({'double': double, 'increment': increment});

_(10).double().increment().double().value(); //42

{% endcodeblock %}


**es5 utility function**

{% codeblock %}

//  pipeline utility

const pipe = functionList => (data) => {
  return functionList.reduce((value, func) => {
    return func(value)
  }, data);
}

pipe([double, increment, double])(10); //42

{% endcodeblock %}


**ESNext pipeline operator**

{% codeblock %}

// es6 pipeline operator

10 |> double |> increment |> double; //42

{% endcodeblock %}

References :

  [ESNext Proposal tc39](https://github.com/tc39/proposal-pipeline-operator)

  [MDN web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Pipeline_operator)

  [Raw code](https://gist.githubusercontent.com/satyamyadav/27723528a35e3d7b4cd80b198ec8f792/raw/e7eb9d3e80ea454d54f17738c0343a9f911d188a/pielinejs.js)

**Gist**

<script src="https://gist.github.com/satyamyadav/27723528a35e3d7b4cd80b198ec8f792.js"></script>


