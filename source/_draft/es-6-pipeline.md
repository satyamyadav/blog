---
title: es6 pipelines
date: 2018-01-31 16:22
categories:
  - code
tags:
  - es6
---
{% codeblock %}
alert('Hello World!');



const pipe = functions => data => {
  return functions.reduce(
    (value, func) => func(value),
    data
  );
};

const double = a => a*2;
const increase = a => a + 5;


let pipeline = pipe([double, increase, double])

// let result = increase(double(5))
let result = pipeline(5)

console.log(result);



{% endcodeblock %}


{% jsfiddle satyamyadav/Lp93ka16/1 js,result dark %}


