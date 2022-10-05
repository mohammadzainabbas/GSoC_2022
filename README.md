## GSoC 2022 - Report

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

#
## Project Description

Homebrew has a `brew livecheck` command which checks upstream sources (_web pages_, _files_, _Git repositories_) to identify the latest version of software in a _formula_ and _cask_. Many Homebrew packages use _resources_, a special kind of package dependency. While Homebrew has tools which automatically upgrade packages to new versions, this feature doesn't work with _resources_. The main aim of this project was to enhance Homebrew's existing `livecheck` feature to work for _resources_ as well.

Prior to this GSoC project, many Formulae have resources that need to be bumped manually, which requires some searching. It was [suggested earlier](https://github.com/Homebrew/gsoc/issues/49#issue-1124437013) to have `livecheck` or `bump` like tooling to help automate this, as most resource updates have a clear _strategy_. (Something, similar to what already exists for many Formulae with _PyPI resources_ using `brew update-python-resources`). 

However later on, following objectives were [defined](https://github.com/Homebrew/gsoc/issues/49#issuecomment-1040520006) to be achieved during GSoC:

- [ ] Extend the livecheck DSL to work for resources.
- [ ] Add default strategies meant for resources from specific sources (such as RubyGems, CPAN, etc.).
- [ ] Add livecheck blocks for resources in homebrew/core.
- [ ] Implement a brew update-resources command and augment brew livecheck with an option to retrieve resource versions.

Homebrew uses various domain-specific languages (_DSLs_) when establishing `formula`, `cask` and `resource` information, so it was necessary to extend the `livecheck` DSL for the `Resource` class before the `brew livecheck` command could be used to retrieve resources versions for a given formulae in `homebrew/core`.

Extending the `livecheck` DSL and augmenting `brew livecheck` command to work for resources were two main goals of this GSoC project. Extending `livecheck` DSL was the first task that was completed and it was implemented earlier in the project. Several modifications were done to allow `brew livecheck` command to be work for resources (and keeping it consistent with the already existing workflow). This part was the main part of the GSoC, thus it took a while to get it reviewed by the mentors and other maintainers.
<!-- 
Since the last GSoC, the _homebrew/livecheck_ tap was no longer needed, and thus was deprecated. All the work related to the `brew livecheck` command was done in _Homebrew/brew_, and work on `livecheck` blocks was done in _homebrew/core_ formulae. -->

As a result of this project, now `brew livecheck` command retrieves `livecheck` information for resources as well (for a given formula). i.e:

```bash
brew livecheck influxdb --resources
```

will show livecheck output for `influxdb` formula and it's _resources_.

#
## Completed Tasks

- [x] Extended the `livecheck` DSL to work for resources.
- [x] Added support for extended `livecheck` DSL to the `brew livecheck` command.
- [x] Augmented `brew livecheck` with an option to retrieve resource versions.
<!-- - [x] Updated output format (_debug_, _json_, _verbose_) for `brew livecheck` command when given new `--resources` flag. -->
- [x] Added tests for new changes to `brew livecheck` command in _homebrew/brew_. 
- [x] Updated documentation for `brew livecheck` to incorporate the changes being made.
- [x] Added resource `livecheck` blocks in few Formulae in _homebrew/core_.
<!-- - [x] Added autocompletion for `brew livecheck` (automatically done for resource) -->

## Ongoing and Future Tasks

- [ ] Add more resource `livecheck` blocks to several other Formulae in _homebrew/core_.
- [ ] Enhance `brew bump` to work for livecheck resources.
<!-- - [ ] Implement a wrapper `brew update-resources` command on top of `brew livecheck`. -->
- [ ] Add default strategies meant for resources from specific sources (such as _RubyGems_, _CPAN_, etc).

## Challenges and Takeaways

* Before the GSoC, I had no knowledge of meta-programming in Ruby. Now, I am more comfortable with Ruby, and I have even started to use it for some personal projects.
* __Homebrew__ has a huge codebase. It was bit overwhelming for me at first, since I had limited Ruby knowledge. But it got easier once I grasp more understanding of Ruby.
* One of the diffculity that I faced was about debugging a Ruby code, I extensively used interactive Ruby (`brew irb`) to debug and to gain some extra Ruby knowledge.
* Time management was one of my biggest issues because I was working on other things in addition to this project. I told my mentor in advance about the engagements, which allowed us to plan ahead and accomplish the tasks.
* Sometimes, getting feedback/review on PRs took more time than what I expected, and it became an issue for other things in the project. My main takeaway here was to remain patient and keep asking for feedback/review on the communication channels. 
* Thanks to the mentors' thorough reviews, I have learned a lot during my GSoC period.

<!-- * Prior to GSoC, I had zero knowledge of Ruby (or meta-programming in Ruby). As an enthusiastic polyglot (human and programming languages), learning a new language was a fun challenge. Now, I am more comfortable with Ruby, and I have even started to use it for some personal projects.
* __Homebrew__ has a huge codebase, it took quite some time to wrap my head around some of the internals that were central to this project.
* One of the diffculity that I faced was about debugging a Ruby code, I extensively used interactive Ruby (`brew irb`) to debug and to gain some extra Ruby knowledge.
* I had other work alongside this project, and one of the biggest challenges was time management. I kept my mentor well informed about the engagements in advanced, this helped us to plan ahead and complete the work efficiently.
* My ruby code quality has definitely improved, thanks to detailed reviews from the mentors. I'm working on further improving the quality of my work. -->

## Acknowledgements

I would like to thank my mentors for their support during this project, esp. to my main mentor [Nanda H Krishna](https://github.com/nandahkrishna) (and co-mentor [Sam Ford](https://github.com/samford)). They were really keen with their comprehensive code reviews and guidance. I also appreciated their taking the time to address all of my questions/ambiguities during our weekly meetings.

I would also like to thank GSoC which provided me an opportunity to work with __Homebrew__ community, which I found to be quite helpful and humble. All the maintainers that I got to work with are simply great and incredibly helpful. I am glad that I got an opportunity to work closely with them, and I am looking forward to contributing to __Homebrew__ in the future as well.

<!-- I'd like to thank my mentors for helping me out throughout this project. A special shoutout to my primary mentor [Nanda H Krishna](https://github.com/nandahkrishna) (and co-mentor [Sam Ford](https://github.com/samford)) for their amazing and comprehensive code reviews and guidance. I enjoyed our weekly meetings and am extremely grateful to them for taking the time to answer all my questions. The __Homebrew__ community is welcoming and friendly, and the maintainers are just brilliant and really helpful. I'm glad that I got an opportunity to work closely with them thanks to GSoC, and I'm looking forward to contributing to __Homebrew__ in the future as well. -->

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
