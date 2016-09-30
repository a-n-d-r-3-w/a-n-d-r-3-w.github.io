---
layout: post
title: Over-constrained CSS
---
Here's a bug where the solution is to delete CSS code.
(I like less code as long as it's still readable.) My team replaced the string
in a tab with a much longer string, and now the string extends past the bottom
border of the tab. In the giant CSS file (400+ lines, another problem for
another time), I found this:
~~~~
.tab {
  width: 100px;
  height: 20px;
  ...
}
~~~~
Simply deleting the `height` rule fixed the problem. Now the browser takes
care of setting the height of the tab to fit its content, and the next time we
make the string longer or shorter, the tab height will be just right. The lesson is to avoid using fixed
values where possible, because otherwise it needlessly constrains your UI and
makes it brittle.
