# Introduction

While there have been other resource based programming languages in the past (such as [Plaid](http://www.cs.cmu.edu/~aldrich/plaid/)), for a long time resource based programming has been a niche, lacking applications where resource based approach would excel. However, [smart contracts](https://en.wikipedia.org/wiki/Smart_contract) and [blockchains](https://en.wikipedia.org/wiki/Blockchain) introduced software development challenges that can be answered with resource based programming.

The [Move language](https://github.com/move-language/move/) and its Move Virtual Machine were designed originally by Facebook to power their [Diem](https://en.wikipedia.org/wiki/Diem_(digital_currency)) blockchain platform providing an intuitive environment and ecosystem for resource oriented applications. Fortunately Move was adopted by multiple blockchain projects as their smart contract execution environment before Diem was discontinued, so Move continued living separately as an independent project.

Today Move and its virtual machine are powering [multiple blockchains](https://github.com/MystenLabs/awesome-move#move-powered-blockchains), most of which are still in the early development phase.

Because Move is currently the most widely developed resource based programming language for blockchains, code examples are written in Move. However it is likely that some of these patterns can be implemented also in some other resource based language and ecosystem.

## What this book is

This book is for discussing software design paradigms and best practices for resource based languages, especially Move and its flavors.

## What this book is not

This book is not a guide to Move or any other resource based language. For books on Move itself, see [this list](https://github.com/MystenLabs/awesome-move#books). Also see [awesome-move](https://github.com/MystenLabs/awesome-move) for a curated list of code and content from the Move programming language community.

## Technical disclaimer

This book is designed to be viewed digitally with hyperlink support (such as PDF or web format). For now the [full software pattern format](https://en.wikipedia.org/wiki/Software_design_pattern#Documentation) is not followed, instead the patterns are simply defined by a short summary and examples.

## License

[![CC BY 4.0 license button][cc-by-png]][cc-by]

Move Patterns: Design Patterns for Resource Based Programming © 2022 by [Ville Sundell](https://github.com/villesundell) is licensed under CC BY 4.0. To view a copy of this license, visit [http://creativecommons.org/licenses/by/4.0/](http://creativecommons.org/licenses/by/4.0/).

[cc-by-png]: https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/by.svg "CC BY 4.0 license button"
[cc-by]: https://creativecommons.org/licenses/by/4.0/ "Creative Commons Attribution 4.0 International License"