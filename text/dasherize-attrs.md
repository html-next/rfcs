- Start Date: 2017-03-06
- RFC PR: (leave this empty)

# Summary

I think it would be nice to enable dasherized use of attrs, so that `justify="between"` could also be written as `justify-between`.

# Motivation

The reason I think this would be useful, is we could then define all attributes without the need for `=` and it would allow us to use
every attribute in size specific ways. For example, you can do something like `lg="fill"` now, but there is no way to define something
for `lg="justify="between""` This change would allow `lg="justify-between"`.

# Detailed design

This should be as simple as looking at how the current set of attributes are implemented, and adding cases for each `foo="bar"` case
in a dasherized form as well.

# How We Teach This

I think we would just document that all properties can be used in a `foo="bar"` fashion or alternatively as `foo-bar`.
We could support both syntaxes fairly easily, so I don't think there is a real need to switch completely to one or the other.
I do think it would be nice to prefer dasherized everywhere though, which would require reworking the docs a bit.

# Drawbacks

I don't really see any drawbacks, but perhaps @runspired or @kybishop might have some insight into potential pitfalls.

# Alternatives

We could alternatively support some sort of complex nested logic like `foo="bar='baz'"`, but that does not feel as clean.
