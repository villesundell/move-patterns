# Introduction

While there have been other resource based programming languages in the past (such as [Plaid](http://www.cs.cmu.edu/~aldrich/plaid/)), resource based programming is still a niche, largely because of lack of real world use cases. The [Move smart contract programming language](https://github.com/move-language/move/) and blockchains changes the game, providing an ecosystem and intuitive environment for resource oriented designs.

Move language (and its MoveVM virtual machine) was designed originally by Facebook to power their [Diem](https://en.wikipedia.org/wiki/Diem_(digital_currency)) blockchain project. Fortunately Move was adopted by multiple blockchain projects as their smart contract execution environment before Diem was discontinued, so Move continued living separately as an independent project.

Today Move, and its virtual machine are powering [multiple blockchains](https://github.com/MystenLabs/awesome-move#move-powered-blockchains), most of which are still in early development phase.

Move is currently the most mature resource based ecosystem (especially for blockchains), so code examples are written in Move. However it is likely that some of these concepts can be implemented also in some other resource based language and ecosystem.

## What this book is

This book is for discussing software design paradigms and best practices for resource based languages, especially Move.

## What this book is not

This book is not a guide to Move or any other resource based language. For books on Move itself, see [this list](https://github.com/MystenLabs/awesome-move#books). Also see [awesome-move](https://github.com/MystenLabs/awesome-move) for a curated list of code and content from the Move programming language community.

## Technical disclaimer

Due to excessive hyperlink usage, this book is not optimized for printing as-is, at least for now. However, the book can be viewed in any digital format supporting hyperlinks, including PDF.

## License

[![CC BY 4.0 license button][cc-by-png]][cc-by]

Move Patterns: Design Patterns for Resource Based Programming © 2022 by [Ville Sundell](https://github.com/villesundell) is licensed under CC BY 4.0. To view a copy of this license, visit [http://creativecommons.org/licenses/by/4.0/](http://creativecommons.org/licenses/by/4.0/).

[cc-by-png]: https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/by.svg "CC BY 4.0 license button"
[cc-by]: https://creativecommons.org/licenses/by/4.0/ "Creative Commons Attribution 4.0 International License"