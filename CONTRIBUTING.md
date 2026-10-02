# Developer Docs

Contribution guidelines
-----------------------

Keep an eye on the [issues](https://github.com/edgetest-dev/run-edgetest-action/issues)
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

``main`` is the single long-lived branch. All work lands on it via pull requests
from short-lived feature branches.

We squash merge every PR into ``main``. The reason is to prevent the branch
from being polluted with endless commit messages when people are developing.
Squashing collapses all the commits into one single new commit. It will also
make it much easier to back out changes if something breaks.

Each release on ``main`` should be tagged properly to denote a "version" that
will have the corresponding artifact in the GitHub Marketplace.

To cut a release:

1. Run the **Bump version** workflow (workflow_dispatch) with the desired
   bump type. It opens a PR that updates ``VERSION`` and the README pin.
2. Squash merge that PR once CI is green.
3. Tag the merge commit on ``main`` as ``vX.Y`` and publish a GitHub release.

TLDR;
-----

* Each feature should have its own branch.
* Each feature branch should be squash merged into ``main``
* To release: run the bump-version workflow, squash merge, then tag and
  publish a new release.


>    ``main`` should be protected in the GitHub UI, so it isn't accidentally
>    deleted.
