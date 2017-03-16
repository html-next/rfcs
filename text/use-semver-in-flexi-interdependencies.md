- Start Date: 2017-03-16
- RFC PR: (leave this empty)

# Summary

Use semver for version control of the flexi addons (as opposed to lock-step).

# Motivation

* We no longer have to bump versions in every addon because of a tiny change in
  one addon.
  - Encourages us to release more often by lowering the effort involved
  - Allows bug fixes to be rolled out faster/more easily
* Easier upgrade path: users don't have to re-download unchanged addons
* Users aren't forced to update all flexi addons when they only want changes
  from one
  - Example:
    * We add a feature to addon A and make a breaking change to addon B.
    * Release
    * User wants the feature from addon A, but doesn't care about the new
      features in addon B.
    * User either has to deal with the breaking changes from addon B, or ignore
      the version warnings until they do. We needlessly annoy the user with said
      warnings.

# Detailed design

Use [the semver package](https://www.npmjs.com/package/semver) in the main flexi
repo to do interdependency checks between versions. Warn the user when there is
a minor version mismatches, error when there is a major version mismatch.

### Example

* flexi-dsl adds a new attribute, gets a minor version bump to v2.5.0
* flexi-default-styles adds a CSS class for said attribute, gets a minor version
  bump to v2.2.0
* flexi repo warns the user if they have flexi-dsl >= v2.5.0 but
  flexi-default-styles <= v2.2.0

* flexi-layouts changes the name of components, major version bump to v3.0.0
* flexi-dsl accommodates the change, major version bump to v3.0.0
* flexi errors if the user has flexi-dsl >= 3.0.0 but flexi-layouts <= 3.0.0, or
  vice versa.

### Initial spike

https://github.com/html-next/flexi/pull/122

# How We Teach This

Since this would become the primary responsibility of the flexi addon (besides
actually installing the dependencies) add a description of this feature to the
README.md.

Consider adding a section to the http://readme.io docs describing the
functionality of each addon from a high level, including the main flexi addon.

# Drawbacks

We would have to maintain a growing list of semver compatibility checks.

I believe this would be OK since the checks would be very straightforward (see
the examples under Detailed Design).

# Alternatives

The alternative is to continue doing lock-step upgrades. This has the benefit of
keeping things simple for us but, as mentioned in Motivation, has a major
drawback for users desiring to upgrade any flexi addon, and hinders our
ability/motivation to roll out releases.

# Unresolved questions

Is there some way to get NPM to do this for us, or an NPM package designed for
this purpose? It seems like optional-dependency management is a common need that
has likely been solved in the past.
