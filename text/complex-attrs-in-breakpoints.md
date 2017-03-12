- Start Date: 2017-03-06
- RFC PR: (leave this empty)

# Summary

Support complex attributes in breakpoints, such as the `align` and `justify` attriutes.

# Motivation

Complex attributes in breakpoints!

# Detailed design

Complex attributes in breakpoints will be used as before, but without quotes around the attribute value:

`<box sm="justify=end align=start"></box>`

# How We Teach This

Document that all properties can be used within breakpoints. Specify the ommission of quotes when used within breakpoints.

# Drawbacks

Using an `=` as the seperator has the potential to cause some confusion, though I belive it to be straightforward enough, especially over the pitfalls of the alternatives. Using a `=` as the seperator has the benefit of keeping our DSL consistent.

# Alternatives

Dasherized attributes: `<box sm="justify-end"></box>`

Drawbacks:
- We plan to support justify-self and align-self. Not having a unique seperator for attribute name and attribute value makes implementation more difficult.
- Dasherized attributes have the potential for collisions. Other libs or browsers might do something with these relatively common attributes
- We would now have to support two forms of attribute: dasherized and seperated-by-`=`.

`:` seperator instead of `=`: `<box sm="justify:end></box>`

Drawbacks:
- Looks similar to CSS, potential for confusion
- Inconsistent with the current complex attribute format.
