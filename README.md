# php the small things
A summary of small things a php programmer can do to improve the code and the readability of code.

## quickwins

### Tools
* use package managers for your local requirements
    * for example in MacOS install [brew](https://brew.sh/index_de)
* install [php over brew](https://formulae.brew.sh/formula/php)
    * *comment:* the big advantage is to have multiple versions linked by brew directly from the cellar 
* install [git over brew](https://gist.github.com/derhuerst/1b15ff4652a867391f03)
* install [composer](https://getcomposer.org/download/) globally for dependency management in PHP
* install [xdebug](https://xdebug.org/docs/install) for debugging, tracing, profiling and the codecoverage
    
### IDE
* use an IDE for example [PHPStorm](https://www.jetbrains.com/phpstorm/) 
* set it up ([jetbrains documentation](https://www.jetbrains.com/help/phpstorm/configuring-php-development-environment.html)) correctly 
    * use [inspections](https://www.jetbrains.com/help/phpstorm/code-inspection.html) 
    * use one of the default codestyles in PHPStorm for example [PSR-12](https://www.php-fig.org/psr/psr-12/)
    * use [xdebug](https://xdebug.org/) in PHPStorm ([documentation](https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html))
    * take a look at PHPStorm features like database, deployment, version control, ...
* use plugins of your IDE:
    * PHP Inspections - EA [Extended](https://plugins.jetbrains.com/plugin/7622-php-inspections-ea-extended-) und [Ultimate](https://plugins.jetbrains.com/plugin/10215-php-inspections-ea-ultimate-)
    * [composer](https://plugins.jetbrains.com/plugin/index?xmlId=org.psliwa.idea.composer)
    * [.env](https://plugins.jetbrains.com/plugin/9525--env-files-support)
    * [php annotations](https://plugins.jetbrains.com/plugin/7320-php-annotations)
    * [bash support](https://plugins.jetbrains.com/plugin/4230-bashsupport)
    * select a plugin for framework support like [symfony](https://plugins.jetbrains.com/plugin/7219-symfony-support)

### Easy programming guidelines
* Every rule has its own context and the context beats every rule.
* Please use common sense for every rule.
* Every rule which does not bring any benefit should be skipped.

#### rules
* No abbreviations in the code.
    * *comment:* You use an IDE, use it.
* Do not use arrays across class (or function) boundaries.
    * *comment:* They are not typed.
* Do not check in commented or unused code.
    * *comment:* You have a version control system, use it.
* As long as annotations are not a language construct in PHP use them sparingly and only for
inevitable process control or external packages where the maintainers know what they are doing.
    * *comment:* Writing your own annotations is for pro´s.   
* String concatenation always with `sprintf`.
    * * *comment:* It is easier to extend and it prevents magic.
* Use type declarations for all properties, functions and variables in your code.
    * *comment:* You didn't come in for nothing
* Use `declare(strict_types=1);` in your
    * *comment:* [explanation](https://www.brainbell.com/php/strict-type.html)  
* Use `final` for your objects.
    * *comment:* Our brain is not designed to understand inheritance (like exponential function).
* The default visibility `private` applies to properties and functions.
    * *comment:* You have to take care about every public function.
* Do not use full namespaces in the code, `use` even if only `\` has to be specified
    * *comment:* You can see how many external dependencies your class have. 
* Immutability is king.
    * *comment:* know the [advantages](https://hackernoon.com/5-benefits-of-immutable-objects-worth-considering-for-your-next-project-f98e7e85b6ac)  
* Always check clauses (e.g. in IFs) with the most accurate possible value.
    * *comment:* Return types can change, but the clause should not. (core methods can also change.)
* Avoid else and try early returns.
    * *comment:* read some [why´s](https://szymonkrajewski.pl/why-should-you-return-early/)
* Use yoda comparison.
    * *comment:* [explanation](https://knowthecode.io/yoda-conditions-yoda-not-yoda). 
    You can look at the same position for every clause and you prevent to assign a variable. 
* What cannot be tested should not be programmed.
    * *comment:* There are many tools for automated testing, but start with [PHPUnit](https://phpunit.de/)

### Basics
* Extremly Defensiv Programming ([video](https://www.youtube.com/watch?v=8d2AtAGJPno) | [slides](https://ocramius.github.io/extremely-defensive-php/))
* The Clean Coder ([book](https://www.amazon.de/Clean-Coder-Conduct-Professional-Programmers/dp/0137081073) | [web](https://clean-code-developer.de/))
* Design Pattern ([web](https://designpatternsphp.readthedocs.io/en/latest/README.html))
* Refactoring ([book](https://www.amazon.de/Refactoring-Improving-Design-Existing-Technology/dp/0201485672))

### Code Reviews
* "You are not your Code!"
    * code reviewer do not comment you, they comment your code
* If you find code you do not understand, remark it.

### Do´s
* Semantic Versioning ([web](https://semver.org/))
* PHP Standards Recommendations [PSR](https://www.php-fig.org/psr/) 
