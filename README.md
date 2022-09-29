## GSoC 2022 - Report

<div align="center" dir="auto" style="
    display: flex;
    justify-content: space-evenly;
">
  <a href="https://summerofcode.withgoogle.com" rel="nofollow">
    <img src="https://raw.githubusercontent.com/nandahkrishna/GSoC/master/assets/GSoC.png" alt="GSoC" width="80" style="max-width: 100%;">
  </a>
  <a href="https://github.com/Homebrew">
    <img src="https://raw.githubusercontent.com/nandahkrishna/GSoC/master/assets/Homebrew.png" alt="Homebrew" width="80" style="max-width: 100%;">
  </a>
</div>


__Author__: [Mohammad Zain Abbas](https://github.com/mohammadzainabbas)

__Organisation__: [Homebrew](https://github.com/Homebrew)

__Project__: [Adding a livecheck Formula DSL and migrating Livecheckables to homebrew/core](https://github.com/Homebrew/brew/issues/7027)

__Mentors__: [Nanda H Krishna](https://github.com/nandahkrishna), [Sam Ford](https://github.com/samford), [Rui Chen](https://github.com/chenrui333), [Mike McQuaid](https://github.com/MikeMcQuaid)

## Project Description

Homebrew has a `brew livecheck` command which checks upstream sources (_web pages_, _files_, _Git repositories_) to identify the latest version of software in a formula and cask. `livecheck` uses its built-in strategies to identify versions for certain URLs and this works fine for some formulae. However, it is sometimes necessary to provide explicit information to `livecheck`, telling it where to check and how to identify versions in the fetched content.

Many Homebrew packages use resources, a special kind of package dependency. While Homebrew has tools which automatically upgrade packages to new versions, this feature doesn't work with resources. This project will enhance Homebrew's existing livecheck feature.

Prior to this GSoC project, these `livecheck` instructions were found in the homebrew/livecheck tap's `Livecheckables` folder. "Livecheckable" files were minimal substitutes for formulae and only consisted of a class with `livecheck` information inside. Throughout `livecheck`'s development, there was a desire to eventually incorporate this information into homebrew/core formulae, so the livecheckable files were merely a stopgap measure.

The `livecheck` information was originally formatted as a hash argument to a `livecheck` method. While this format was functional, it didn't follow the existing norms within formulae and would need to be modified. Homebrew uses various domain-specific languages (DSLs) when establishing formula information, so it was necessary to add a `livecheck` DSL to the `Formula` class before the `livecheck` information could be incorporated into homebrew/core formulae.

Adding the `livecheck` DSL and incorporating the livecheckables into homebrew/core formulae were two expressed goals of this GSoC project. The `livecheck` DSL was the first task that was completed and it was implemented early in the project. Due to the ongoing work on livecheckables in the homebrew/livecheck tap, we waited until close to the end of GSoC to migrate the `livecheck` blocks into homebrew/core formulae.

Outside of these initial goals, we also decided to incorporate the `brew livecheck` command into the main Homebrew/brew repository, making it a built-in developer command. Before this point, users were required to tap homebrew/livecheck to be able to use this command.

As a result of this project, the homebrew/livecheck tap is no longer needed and has been deprecated. Further work related to the `brew livecheck` command will happen in Homebrew/brew and work on `livecheck` blocks will happen in homebrew/core formulae.

## Completed Tasks

* Implemented a `livecheck` DSL in Homebrew/brew and incorporated it into the `Formula` class
* Added support for the `livecheck` DSL to the `brew livecheck` command
* Updated existing livecheckables to use the new DSL format
* Removed support for the old livecheckable format from `brew livecheck`
* Added the ability to reference certain formula URLs as `url` symbol arguments (`:head`, `:homepage`, `:stable`)
* Updated livecheckables to use URL symbols, where possible
* Added autocompletion for `brew livecheck`
* Added `url` information to the livecheckables that only contained a regex
* Added livecheckables for some of the formulae that require an explicit check to be able to identify versions
* Updated existing livecheckables to bring them closer to current standards
* Integrated the `livecheck` blocks found in livecheckable files into their respective homebrew/core formulae
* Integrated the `brew livecheck` command into Homebrew/brew as a `dev-cmd`
* Removed all files from the homebrew/livecheck tap and deprecated it

## Ongoing and Future Tasks

* Add RuboCops to enforce standards for `livecheck` block information
* Add/improve network-related `livecheck` tests
* Other improvements to `livecheck`, including adding `livecheck` blocks to formulae, adding a progress bar for JSON output, documentation, etc.

## Challenges and Takeaways

* Before GSoC, I had zero knowledge of Ruby. As an aspiring polyglot (human and programming languages), learning a new language was a fun challenge. Ruby is now one of my favourite languages and I definitely see myself brewing up projects using it.
* Homebrew has a huge codebase, it took quite some time to wrap my head around some of the internals that were central to this project.
* I had other work alongside this project, and one of the biggest challenges was time management. I identified a few strategies that worked for me, and I was able to plan ahead and complete my work efficiently.
* I was able to automate some of the work by writing scripts, something I enjoy doing. With this I was able to identify what tasks could be automated and how, complete them quickly and gain some extra Ruby knowledge.
* My code quality has definitely improved, thanks to detailed reviews from the mentors. I'm working on improving the quality of my documentation and tests.

## Acknowledgements

I'd like to thank my mentors for helping me throughout this project. A special shoutout to my primary mentor Sam for their amazing and comprehensive code reviews and guidance. I enjoyed our weekly meetings and am extremely grateful to them for taking the time to answer all my questions. The Homebrew community is welcoming and friendly, and the maintainers are just brilliant. I'm glad I got an opportunity to work closely with them thanks to GSoC, and I'm looking forward to contributing to Homebrew in the future. I'd also like to acknowledge my wonderful co-GSoCers, [rmNULL](https://github.com/rmNULL) and [Vidushee Amoli](https://github.com/VidusheeAmoli), it was great fun working with them.

## Pull Requests

### [Homebrew/brew](https://github.com/Homebrew/brew)

#### GSoC

* \#7179 - [Livecheck Formula DSL](https://github.com/Homebrew/brew/pull/7179)
* \#7578 - [livecheck: add component order rubocop](https://github.com/Homebrew/brew/pull/7578)
* \#7625 - [livecheck: modified urls cop](https://github.com/Homebrew/brew/pull/7625)
* \#7668 - [livecheck: reference Formula URLs](https://github.com/Homebrew/brew/pull/7668)
* \#7671 - [livecheck: modify regex in tests](https://github.com/Homebrew/brew/pull/7671)
* \#7748 - [Add completion for livecheck](https://github.com/Homebrew/brew/pull/7748)
* \#8180 - [livecheck migration: add `brew livecheck` developer command](https://github.com/Homebrew/brew/pull/8180)
* \#8254 - [livecheck migration: create Homebrew::Livecheck](https://github.com/Homebrew/brew/pull/8254)
* \#8255 - [livecheck migration: add strategies](https://github.com/Homebrew/brew/pull/8255)
* \#8544 - [livecheck: remove test for `livecheck_formulae`](https://github.com/brew/pull/8544)

### [Homebrew/homebrew-core](https://github.com/Homebrew/homebrew-core)

#### Pre-GSoC

* \#40791 - [anime-downloader 3.6.3 (new formula)](https://github.com/Homebrew/homebrew-core/pull/40791)
* \#45722 - [anime-downloader 4.0.1](https://github.com/Homebrew/homebrew-core/pull/45722)

#### GSoC

* \#54565 - [Add livecheck block to a52dec.rb](https://github.com/Homebrew/homebrew-core/pull/54565)
* \#54595 - [aacgain: add livecheck block](https://github.com/Homebrew/homebrew-core/pull/54595)
* \#54597 - [imap-uw: add livecheck block](https://github.com/Homebrew/homebrew-core/pull/54597)
* \#55321 - [detekt: update homepage](https://github.com/Homebrew/homebrew-core/pull/55321)
* \#55950 - [livecheck: modify Formula urls](https://github.com/Homebrew/homebrew-core/pull/55950)
* \#56290 - [ossp-uuid: update homepage](https://github.com/Homebrew/homebrew-core/pull/56290)
* \#57627 - [aacgain: update livecheck regex](https://github.com/Homebrew/homebrew-core/pull/57627)
* \#58760 - [vsts-cli: deprecate](https://github.com/Homebrew/homebrew-core/pull/58760)
* \#60324 - [livecheck: migrate livecheckables to livecheck blocks](https://github.com/Homebrew/homebrew-core/pull/60324)

