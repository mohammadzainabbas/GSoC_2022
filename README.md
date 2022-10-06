# GSoC 2022 - Report

<div align="center">
  <a href="https://summerofcode.withgoogle.com" rel="nofollow">
    <img src="assets/GSoC.png" alt="GSoC" width="80" style="max-width: 100%;">
  </a>
  <a href="https://github.com/Homebrew">
    <img src="assets/Homebrew.png" alt="Homebrew" width="80" style="max-width: 100%;">
  </a>
</div>

__Author__: [Mohammad Zain Abbas](https://github.com/mohammadzainabbas)

__Organisation__: [Homebrew](https://github.com/Homebrew)

__Project__: [Autobumping resources in Formulae](https://github.com/Homebrew/gsoc/issues/49)

__Mentors__: [Nanda H Krishna](https://github.com/nandahkrishna), [Sam Ford](https://github.com/samford), [Rui Chen](https://github.com/chenrui333), [Mike McQuaid](https://github.com/MikeMcQuaid)

## Project Description

Homebrew has a `brew livecheck` command which checks upstream sources (webpages, files, repositories) to identify the latest version of software in a Formula or Cask. Many Homebrew packages also contain resources, a special kind of package dependency which is usually not available as a Formula. While Homebrew has tools to automatically upgrade packages to new versions, this feature doesn't work with resources. The main aim of this project was to enhance Homebrew's existing `livecheck` feature to work for resources as well.

Resources in Formulae need to be bumped manually, i.e, contributors need to spend time in identifying the latest version of the resource as Homebrew doesn't have tooling to automate this process. It was [suggested earlier](https://github.com/Homebrew/gsoc/issues/49#issue-1124437013) to have `livecheck` or `bump`-like tooling to help automate this, as most resource updates have a clear strategy. Something similar exists for many PyPI resources -- the `brew update-python-resources` command. 

The following objectives were [defined](https://github.com/Homebrew/gsoc/issues/49#issuecomment-1040520006) to be achieved during GSoC:

- [ ] Extend the Livecheck DSL to work for resources
- [ ] Add default strategies meant for resources from specific sources (such as RubyGems, CPAN, etc.)
- [ ] Add `livecheck` blocks for resources in homebrew/core
- [ ] Augment `brew livecheck` with a option to retrieve resource versions

Extending the `livecheck` DSL and augmenting the `brew livecheck` command to work for resources were the two main goals of this GSoC project. Earlier in the project, a PR to extend the `livecheck` DSL for resources was merged. Following this, the `brew livecheck` command was modified to work for resources. This PR was the most important contribution during GSoC and it was merged after a few iterations of feedback to ensure that the feature was implemented correctly.

As a result of this project, the `brew livecheck` command now retrieves version information for resources as well (for a given Formula). For example,

```bash
brew livecheck influxdb --resources
```

will show the `livecheck` output for the `influxdb` Formula and its resources.

## Completed Tasks

- [x] Extended the `livecheck` DSL to work for resources
- [x] Augmented `brew livecheck` with an option to retrieve resource versions
- [x] Added tests for new changes to `brew livecheck` command in Homebrew/brew
- [x] Updated documentation for `brew livecheck`
- [x] Added `livecheck` blocks to resources in a few Homebrew/core Formulae

## Ongoing and Future Tasks

- [ ] Add more `livecheck` blocks to resources in several other Formulae
- [ ] Enhance `brew bump` to work for resources
- [ ] Add default strategies meant for resources from specific sources (such as RubyGems, CPAN, etc)

## Challenges and Takeaways

* Before GSoC, I had no knowledge of meta-programming in Ruby. Now, I am more comfortable with Ruby, and I have even started to use it for some personal projects.
* Homebrew has a huge codebase. It was a bit overwhelming for me at first since I had limited Ruby knowledge, but it got easier for me to understand the code once I had grasped Ruby concepts.
* While I initially struggled to debug code and test out features, I extensively used interactive Ruby (`brew irb`) to debug and to gain some extra Ruby knowledge.
* Time management was one of my biggest issues because I was working on other things in addition to this project. I told my mentor in advance about the engagements, which allowed us to plan ahead and accomplish the tasks.
* Sometimes, getting feedback on PRs took more time than I expected because the changes were large. My main takeaway here was to remain patient and engage in communication with the mentors frequently. 
* Thanks to the mentors' thorough reviews, I have learned a lot during my GSoC period.

## Acknowledgements

I would like to thank my mentors for their support during this project, especially my main mentor [Nanda H Krishna](https://github.com/nandahkrishna) and co-mentor [Sam Ford](https://github.com/samford). They were really comprehensive with their code reviews and guidance. I also appreciated their taking the time to address all of my questions during our weekly meetings.

I would also like to thank GSoC for providing me the opportunity to work with Homebrew. All the maintainers that I got to work with were incredibly helpful. I am glad that I got an opportunity to work closely with them, and I am looking forward to contributing to Homebrew in the future as well.

## Pull Requests

### [Homebrew/brew](https://github.com/Homebrew/brew)

#### GSoC

- [x] [Extend the `livecheck` DSL to work for resources brew#13496](https://github.com/Homebrew/brew/pull/13496)
- [x] [Augment `brew livecheck` with a `--resources` option to check resources brew#13613](https://github.com/Homebrew/brew/pull/13613)
- [x] [Update documentation for `brew livecheck` brew#13933](https://github.com/Homebrew/brew/pull/13933)

### [Homebrew/homebrew-core](https://github.com/Homebrew/homebrew-core)

#### GSoC

- [x] [influxdb: added livecheck block for resource `pkg-config-wrapper` homebrew-core#112155](https://github.com/Homebrew/homebrew-core/pull/112155)
- [x] [flux: added livecheck block for resource `pkg-config-wrapper` homebrew-core#112156](https://github.com/Homebrew/homebrew-core/pull/112156)
- [x] [v8 10.5.218.8 homebrew-core#111013](https://github.com/Homebrew/homebrew-core/pull/111013)
- [x] [luvit: added livecheck block for resource `luvi` homebrew-core#112158](https://github.com/Homebrew/homebrew-core/pull/112158)
- [x] [luvit: added livecheck block for resource `lit` homebrew-core#112157](https://github.com/Homebrew/homebrew-core/pull/112157)
- [x] [Add livecheck block for resource `pkg-config-wrapper` for Formulae `influxdb` and `flux` homebrew-core#111257](https://github.com/Homebrew/homebrew-core/pull/111257)
- [x] [template-glib 3.36.0 homebrew-core#111021](https://github.com/Homebrew/homebrew-core/pull/111021)

### [Homebrew/homebrew-cask](https://github.com/Homebrew/homebrew-cask)

#### Pre-GSoC

- [x] [Updated postman from 9.0.7 to 9.1.1 homebrew-cask#112984](https://github.com/Homebrew/homebrew-cask/pull/112984)
