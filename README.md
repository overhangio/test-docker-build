# Docker image building tests

Try out different strategies on Github Actions to accelerate Docker image building with [Tutor](https://docs.tutor.overhang.io/).

* Related conversation: https://discuss.openedx.org/t/is-building-docker-images-taking-too-long-for-you/9451
* Related GitHub issue: https://github.com/openedx/wg-devops/issues/6

## Results

Build "openedx" Docker image from scratch:

* Baseline: 35.8 minutes (2150s) ([source](https://github.com/overhangio/test-docker-build/actions/runs/4447024271/jobs/7847560759)). This is the build time that everyone experiences when they build the openedx Docker image for the first time locally.
* With registry cache: 9.1 minutes (546s) ([source](https://github.com/overhangio/test-docker-build/actions/runs/4447024271/jobs/7847560948)).

Re-build the "openedx" Docker image with an edx-platform fork:

* Baseline: 14.86 min (892s) ([source](https://github.com/overhangio/test-docker-build/actions/runs/4691689809/jobs/8316474039)). This is the build time that everyone experiences when they need to re-build with an edx-platform fork.
* Build from scratch but with a registry cache: TODO ([source](https://github.com/overhangio/test-docker-build/actions/runs/4692242266/jobs/8317714078))
* Build with a mount cache: 19.16 min (1150s) ([source](https://github.com/overhangio/test-docker-build/actions/runs/4691689809/jobs/8316473640)). This is higher than the baseline, but that benchmark did not leverage the mount cache: it appears that the `pip install` and `npm clean-install` steps are cached anyway. We should make another test where we modify the edx-platform requirements.
