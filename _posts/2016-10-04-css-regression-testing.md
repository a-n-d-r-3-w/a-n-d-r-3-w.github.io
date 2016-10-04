---
layout: post
title: CSS Regression Testing with BackstopJS
---
How can we detect visual regressions as early as possible? One option is to use
[BackstopJS](https://github.com/garris/BackstopJS), which I tried today. The
setup instructions were well written and I soon had a useful set of tests. The
important piece for me was to instruct BackstopJS to wait for a particular UI
element to finish loading *before* taking a screenshot. Fortunately, there is
a simple way to do this in BackstopJS by setting the `onReadyScript` configuration
property to a file that contains something like:

```
casper.waitWhileVisible('.loading-affordance', function () {
  console.log('Done loading.');
}, function () {
  console.log('Timed out.');
}, 60000); // Timeout is in milliseconds.
```

`waitWhileVisible()` is a [CasperJS function](http://docs.casperjs.org/en/latest/modules/casper.html#waitwhilevisible)
that blocks the test until the specified element disappears. Alternatively,
you can wait until a specified element appears by using `waitUntilVisible()`.
