:tocdepth: 1

.. Please do not modify tocdepth; will be fixed when a new Sphinx theme is shipped.

.. sectnum::

Source Code
===========

All source code used must either be in the form of a puppet module published on
the `puppetforge <https://forge.puppet.com/>`_ or in a repository within the
github `lsst-it <https://github.com/lsst-it/>`_ organization.

Key Repos
---------

* control repo: https://github.com/lsst-it/lsst-control
* hieradata: https://github.com/lsst-it/lsst-puppet-hiera
* "private" hieradata: https://github.com/lsst-it/lsst-puppet-hiera-private

Git / Github Workflow
---------------------

The lsst-it puppet repos follow the common pattern of changes being developed on feature branches, which then SHALL merged into the `production` branch, using Github's pull-request feature.
Commit(s) SHALL NOT be directly pushed onto the `production` branch. All changes to this branch MUST be made via a pull-request.

The `production` ref is then branched to a site specific production branch using the pattern `<site>_production`. E.g.

* `cp_production`

.. note::

   **Currently, only a site specific branch is used for `cp`/summit. These branches have been retired for all other sites.**

A `<site>_production` branch functions much the same as a tag placed on a commit on the `production` branch, which is periodically "moved forward" to point to newer commits.
A production branch SHALL NOT ever contain commits which are not already part of the `production`.

The function of the production branch(es) is to control when change, any change at all, is allowed to happen for a site.
A feature branch SHOULD be merged into `production` when that work is deemed complete enough for deployment.
However, when a feature is ready for deployment does not mean that it is convenient time in terms of operations to roll that feature out.
For example, 1659 on a Friday afternoon may not be the best time to roll out a new feature to the summit during an observing campaign.
The alternative would be to not allow feature branches to be merged until they are considered complete and it is a convenient time to roll out those changes across all sites.
The major downside to that approach is that it encourages large, monolithic, and long lived feature branches that are prone to merge conflicts and are more difficult to review relative to a multiple small, inter-related pull-requests.

Testing
-------

Work-In-Progress Pull-requests
-------------------------------

A pull-request which is opened for the purpose of observing CI runs, keeping track of work in progress which is being set aside, or to gather informal review MUST BE marked as a `draft` and have the PR title prepended with the string `(WIP)`.

Pull-request Review Critera
---------------------------

* Does the source branch of the PR contain a Jira issue slug?
  All non-trivial changes should be attached to a Jira issue.
  An example of a trivial change would be fixing a typo in a code comment.
* Does the title of the PR sufficiently explain the scope of the change?
* Does the PR description explain why this change is necessary?
  What problem is being solved?
* Are the titles of the commit message(s) descriptive and in imperative mood?
  https://cbea.ms/git-commit/
* Do the individual commits within the PR break the change up into discrete isolated changes?
  Does each individual commit contain the relevant unit tests and comments?
* Do *YOU* as the reviewer understand why the change is necessary and how it is being accomplished?
* Is there a puppet forge module that provides the same functionality or could be used with modifications?
* Are there code comments explaining anything "tricky" or unusual?
  Is the code over commented?
* Is the unit test coverage sufficient?
  Do existing unit tests sufficiently over the change?
  Are the unit tests too sensitive / brittle?
