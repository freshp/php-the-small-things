# php the small things
A summary of small things a php programmer can do to improve the code and the readability of code.

*estimated reading time (without links): 10 minutes*

There are so brilliant programming concepts and paradigms in the PHP community. I don't want to chew them again and again. 
But I think everybody needs some easy small things we can improve in our everyday's work. 
There are so many books, conferences, videos and so on, where you can learn great new or old architectures. 
But most of the time you have to start from scratch or read thick books before you can start. 
That is fine, but IMO there are so many small things you can improve and start now. 
I saw many developer doing great work in general, but no one understands the goal of their software or the way to the goal. 
There will be the day they dont support their fancy tools any more. 
And a new developer starts from scratch, because he or she do not understands the code at all. 
Everybody can produce legacy code. (legacy code is code that works) So IMO the best code is code that everybody can understand by reading it. 
This repository should help to see, that there are so many small things we can improve from now on.     

1. [Tools](#tools)
    1. [Build your own webservices](#build-your-own-webservices)
    1. [Free online tools](#free-online-tools)
1. [IDE](#ide)
1. [PHP programming](#php-programming)
    1. [Meta theses](#meta-theses)
    1. [PHP programming theses](#php-programming-theses)
1. [Learning the basics](#learning-the-basics)
1. [Blogs](#blogs)
1. [Important composer packages](#important-composer-packages)
1. [Code reviews](#code-reviews)
    1. [Code review thesis](#code-review-theses)

## Tools
* use package managers for your local requirements
    * for example in MacOS install [brew](https://brew.sh/index_de)
* install [php over brew](https://formulae.brew.sh/formula/php) on MacOS
    * *comment:* the big advantage is to have multiple versions linked by brew directly from the cellar 
* install [git over brew](https://gist.github.com/derhuerst/1b15ff4652a867391f03) on MacOS
* install [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh) bash on MacOS
* install [composer](https://getcomposer.org/download/) globally for dependency management in PHP
* install [xdebug](https://xdebug.org/docs/install) for debugging, tracing, profiling and the codecoverage

### Build your own webservices
* use a automation server like [jenkins](https://jenkins.io/) for continuous integration, continuous deployment or any other automation
* use a remote repository server like [gitlab](https://about.gitlab.com/) or [bitbucket](https://bitbucket.org/) or at least github 
* use a private package repository like [satis](https://github.com/composer/satis)

### Free online tools
* if you need regex, than use [this page](https://regex101.com/)
* you want to schedule a cronjob, than look at [this page](https://crontab.guru/)
* you are not sure with your version constraint, than look at [this page](https://jubianchi.github.io/semver-check/#/)  

## IDE
* use an IDE for example [PHPStorm](https://www.jetbrains.com/phpstorm/) 
* set PHPStorm up ([jetbrains documentation](https://www.jetbrains.com/help/phpstorm/configuring-php-development-environment.html)) correctly 
    * use [inspections](https://www.jetbrains.com/help/phpstorm/code-inspection.html) 
    * use one of the default codestyles in PHPStorm for example [PSR-12](https://www.php-fig.org/psr/psr-12/)
    * use [xdebug](https://xdebug.org/) in PHPStorm ([documentation](https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html))
    * take a look at PHPStorm features like database, deployment, version control, ...
* use plugins of PHPStorm:
    * PHP Inspections - EA [Extended](https://plugins.jetbrains.com/plugin/7622-php-inspections-ea-extended-) und [Ultimate](https://plugins.jetbrains.com/plugin/10215-php-inspections-ea-ultimate-)
    * [composer](https://plugins.jetbrains.com/plugin/index?xmlId=org.psliwa.idea.composer)
    * [.env](https://plugins.jetbrains.com/plugin/9525--env-files-support)
    * [php annotations](https://plugins.jetbrains.com/plugin/7320-php-annotations)
    * [bash support](https://plugins.jetbrains.com/plugin/4230-bashsupport)
    * select a plugin for framework support like [symfony](https://plugins.jetbrains.com/plugin/7219-symfony-support)

## PHP programming
In the future I want to write a short abstract on the how and why I write these theses down. 
Maybe there will be some Sniffs to check them.

### Meta theses
Every thesis can be an advise.
* Every advice has its own context and the context beats every advice.
* Please use common sense for every advice, because they are no rules.
* Every advice which does not bring any benefit should be skipped.
* Never create advices from subjective perspectives.
* A advice should ever have a real benefit.
* A advice should apply generally.
* You don't have to follow them all, but you should know that they exist. 
    * *comment*: You should not miss out any advice, if you dont know the reason. *rework

### PHP programming theses
> What cannot be tested should not be programmed.
* *comment:* There are many tools for automated testing, but start with [PHPUnit](https://phpunit.de/).
> Use type declarations for all properties, functions and variables in your code.
* *comment:* They didn't come in for nothing.
> Immutability is king.
* *comment:* Know the [advantages](https://hackernoon.com/5-benefits-of-immutable-objects-worth-considering-for-your-next-project-f98e7e85b6ac).  
> Always check clauses (e.g. in IFs) with the most accurate possible value.
* *comment:* Return types can change, but the clause should not. (core methods can also be changed.)
> Avoid else and try early returns.
* *comment:* Read some [why's](https://szymonkrajewski.pl/why-should-you-return-early/).
> Do not use arrays across class (or function) boundaries.
* *comment:* They are not typed.
> String concatenation always with `sprintf`.
* *comment:* It is easier to extend and it prevents magic.
> Use yoda comparison.
* *comment:* [Explanation](https://knowthecode.io/yoda-conditions-yoda-not-yoda). 
You can look at the same position for every clause and you prevent to assign a variable. 
> Use `declare(strict_types=1);` at the top of every PHP script
* *comment:* [Explanation](https://www.brainbell.com/php/strict-type.html)  
> Use `final` for your objects.
* *comment:* Our brain is not designed to understand inheritance (like exponential function).
> The default visibility `private` applies to properties and functions.
* *comment:* You have to take care about every public function.
> As long as annotations are not a language construct in PHP use them sparingly and only for inevitable process control
> or external packages where the maintainers know what they are doing.
* *comment:* Writing your own annotations is for pro's.
> Do not use full namespaces in the code, `use` even if only `\` has to be specified
* *comment:* You can see how many external dependencies your class have. 
> Traits should never use traits. I think you should prevent traits at all. 
* *comment:* It is nearly impossible to get out of this inheritance tree. And think at exponential functions.
> Do not check in commented or unused code.
* *comment:* You have a version control system, use it.
> No abbreviations in the code.
* *comment:* You use an IDE, use it.

## Learning the basics
* Principles of object oriented design ([web](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod))
* The Clean Coder ([book](https://www.amazon.de/Clean-Coder-Conduct-Professional-Programmers/dp/0137081073) | [web](https://clean-code-developer.de/))
* Extremely defensive PHP ([video](https://www.youtube.com/watch?v=8d2AtAGJPno) | [slides](https://ocramius.github.io/extremely-defensive-php/))
* Design Pattern ([web](https://designpatternsphp.readthedocs.io/en/latest/README.html))
* PHP Standards Recommendations [PSR](https://www.php-fig.org/psr/)
* Semantic Versioning ([web](https://semver.org/))
* Refactoring ([book](https://www.amazon.de/Refactoring-Improving-Design-Existing-Technology/dp/0201485672))
* Principles of package design ([book](https://www.amazon.de/Principles-Package-Design-Creating-Components/dp/1484241185))

## Blogs
* https://matthiasnoback.nl/
* https://ocramius.github.io/
* https://stitcher.io/ 
* https://blog.jetbrains.com/phpstorm/

## Important composer packages
The list of packages is not complete, but you can start from this stack.
* Composer package to handle [Security advisories](https://github.com/Roave/SecurityAdvisoriesBuilder) 
* Testing framework [PHPUnit](https://github.com/sebastianbergmann/phpunit)
* Static code analyses with [PHPStan](https://github.com/phpstan/phpstan) or [Psalm](https://github.com/vimeo/psalm)
* PHP Codesniffer [PHPCS and PHPCBF](https://github.com/squizlabs/PHP_CodeSniffer)
* PHP library to generate [UUIDs](https://github.com/ramsey/uuid) 
* Simple composer PHAR file handling with [tooly](https://github.com/tommy-muehle/tooly-composer-script) 
* Simple [Enum](https://github.com/freshp/php-enumeration) abstraction inspired by MySQL 

## Code reviews
Start making code reviews. If you dont know how? Read this [article](https://medium.com/palantir/code-review-best-practices-19e02780015f)

### Code review theses
> You are not your Code!
* code reviewer do not comment you, they comment your code
> If you find code you do not understand, ask.
