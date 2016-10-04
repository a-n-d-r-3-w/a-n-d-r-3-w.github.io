---
layout: post
title: Over-constrained CSS
---
Here's a bug where the solution is to delete CSS code. My team replaced the string
in a UI element with a much longer string, and the longer string now extends past the bottom
border of the element. In the giant CSS file (400+ lines, another problem for
another time), I found this:

{% highlight css %}
.custom-element {
  width: 100px;
  height: 20px;
  ...
}
{% endhighlight %}

Simply deleting the `height` rule fixed the problem. Now the browser takes
care of setting the height of the element to fit its content, and the next time we
make the string longer or shorter, the element height will be just right.
The lesson is to avoid using fixed values where possible, because otherwise it
needlessly constrains your UI and makes it brittle.
