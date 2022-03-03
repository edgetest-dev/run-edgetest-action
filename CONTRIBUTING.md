# Developer Docs

Contribution guidelines
-----------------------

Keep an eye on the [issues](https://github.com/fdosani/run-edgetest-action/issues)
We are always happy for help, including such things as:

- Bug reports
- Feature requests
- Commenting on issues ("me too!" and "+1" can be helpful)
- Positive feedback (It's always lovely to hear!)
- Negative feedback (but be nice)
- Pull Requests to fix a bug
- Pull Requests to implement a feature (though we wouldn't mind discussing first)



Release guidelines
------------------

``dev`` is the default branch where most people will work with day to day.
All features must be squash merged into this branch. The reason we squash merge
is to prevent the dev branch from being polluted with endless commit messages
when people are developing. Squashing collapses all the commits into one single
new commit. It will also make it much easier to back out changes if something breaks.

``main`` is where official releases will go. Each release on ``main`` should
be tagged properly to denote a "version" that will have the corresponding artifact
in the GitHub Marketplace.

Before each release the `README.md` and `VERSION` file should be updated to reflect the latest version.


TLDR;
-----

* Each feature should have its own branch.
* Each feature branch should be squash merged into ``dev``
* Before a release, bump the version in `README.md` and `VERSION`.
* Merge  ``dev`` into ``main`` via a regular "merge commits"
* tag and publish a new release



>    ``main``, and ``dev`` should be protected in the GitHub UI, so they aren't accidentally deleted.