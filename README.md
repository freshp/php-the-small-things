# php the small things
A summary of small things a php programmer can do to improve the code and the readability of code.

*estimated reading time (without links): 15 minutes*

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

I am convinced that in a complex situation the small things makes the difference.   

1. [PHP programming](#php-programming)
    1. [Meta theses](#meta-theses)
    1. [PHP programming theses](#php-programming-theses)
1. [Learning the basics](#learning-the-basics)
1. [Blogs](#blogs)
1. [Tools](#tools)
    1. [Use web services for default tasks](#use-web-services-for-default-tasks)
    1. [Free online tools](#free-online-tools)
1. [IDE](#ide)
1. [Important composer packages](#important-composer-packages)
1. [Code reviews](#code-reviews)
    1. [Code review thesis](#code-review-theses)
1. [Documentation](#documentation)

## PHP programming

### Meta theses
Every thesis can be advice.
* Every advice has its own context, and context beats any advice.
* Use common sense for every advice; these are not rules.
* Skip any advice that doesn't bring a benefit.
* Avoid subjective perspectives in advice.
* Advice should have a real, tangible benefit.
* Advice should generally apply broadly.
* You don't have to follow all advice, but you should know they exist.
  * Comment: Don't miss any advice without understanding the reason.

### PHP programming theses
These are some theses I have developed in almost 20 years of programming in teams.
It is just a numbered list to discuss it.
New theses will be listed at the end of the list, feel free to add some.
The given list is far from complete, but I have raised these points too many times and they may help others too.
My context has always been the development of products that need to be adapted and expanded over a longer period of time. 
It was never a question of whether a line of code would be adapted, but when.
Defects in these products lead to direct financial losses or a work blocker for teams.


1. **What cannot be tested should not be programmed.**
    - *Comment:* Start with [PHPUnit](https://phpunit.de).
    - **Example:** Implementing unit tests for all public methods ensures that each function performs as expected.

2. **Use type declarations for all properties, functions (return types and parameters), and variables.**
    - *Comment:* They exist for a reason.
    - **Reference:** [PHP Type Declarations](https://www.php.net/manual/en/language.types.declarations.php)

3. **Immutability is king.**
    - *Comment:* Know the [advantages](https://hackernoon.com/immutability).
    - **Example:** Using immutable objects can prevent accidental changes to data.
      ```php
      final class ImmutableUser {
          public function __construct(private readonly string $name) {
          }
 
          public function getName(): string {
              return $this->name;
          }
      }
      ```

4. **Always check clauses with the most accurate possible value.**
    - *Comment:* Return types can change, but the clause should not.
    - **Example:** `if (true === $user->isActive())` is preferred over `if ($user->isActive())`.

5. **Avoid else statements and use early returns.**
    - *Comment:* [Reasons](https://szymonkrajewski.pl/why-should-you-return-early/).
    - **Example:**
      ```php      
        function example(bool $value): void {
            if (false === $value) {
                return;
            }
            // Rest of the code
        }
      ```

6. **Do not use arrays across class or function boundaries.**
    - *Comment:* They are not typed.
    - **Example:** Use value objects or DTOs instead of arrays.
      ```php
      final class UserDTO {
          public function __construct(public readonly string $name, public readonly string $email) {
          }
      }
 
      function createUser(UserDTO $userDTO) {
          // Use $userDTO
      }
      ```

7. **String concatenation should always use `sprintf`.**
    - *Comment:* It is safer, easier to extend and it prevents magic. It is slower than normal concatenation.
     - **Example:**
      ```php
      $name = "John";
      $greeting = sprintf("Hello, %s!", $name);
      ```

8. **Use Yoda conditions.**
    - *Comment:* [Explanation](https://knowthecode.io/yoda-conditions).
    - **Example:** `if (42 === $answer)` prevents accidental assignment.
      ```php
      if (42 === $answer) {
          // Do something
      }
      ```
    - **Reference:** [To Yoda or Not to Yoda](https://knowthecode.io/yoda-conditions-yoda-not-yoda)

9. **Use `declare(strict_types=1);` at the top of every PHP script.**
    - *Comment:* [Explanation](https://brainbell.com/php/strict-type.html).
    - **Example:** Ensures that all type declarations are strictly enforced.
      ```php
      declare(strict_types=1);
 
      function add(int $a, int $b): int {
          return $a + $b;
      }
      ```
    - **Reference:** [Strict Types in PHP](https://www.php.net/manual/en/language.types.declarations.php#language.types.declarations.strict)

10. **Use `final` for your objects.**
    - *Comment:* Inheritance is complex to manage.
    - **Example:**
      ```php
      final class User {
          // Class implementation
      }
      ```
    - **Reference:** [Final Keyword in PHP](https://www.php.net/manual/en/language.oop5.final.php)

11. **Default visibility for properties and functions should be `private`.**
    - *Comment:* Treat public functions/properties as public APIs.
    - **Example:**
      ```php
      final class User {
          public function __construct(private string $name) {}

          public function getName(): string {
              return $this->name;
          }
      }
      ```
    - **Reference:** [Visibility in PHP](https://www.php.net/manual/en/language.oop5.visibility.php)

12. **Use annotations sparingly and only when necessary.**
    - *Comment:* Prefer PHP8 attributes, return types and property types.
    - **Example:**
      ```php
      #[PHPUnit\Framework\Attributes\DataProvider('provideNotAllowedKeys')]
      public function testShowErrorWithNotAllowedKeys(string $key) 
      ```
    - **Reference:** [PHP8 Attributes](https://stitcher.io/blog/php-8-attributes)

13. **Do not use full namespaces in the code; use `use` statements.**
    - *Comment:* Highlights external dependencies.
    - **Example:**
      ```php
      use Vendor\Package\Class;

      $object = new Class();
      ```
    - **Reference:** [Namespaces in PHP](https://www.php.net/manual/en/language.namespaces.importing.php)

14. **Traits should never use traits.**
    - *Comment:* Avoid complex inheritance.
    - **Example:** Avoid nested traits to reduce complexity.
    - **Reference:** [Traits in PHP](https://www.php.net/manual/en/language.oop5.traits.php)

15. **Strings should be constants.**
    - *Comment:* Reduces errors and increases reusability.
    - **Example:**
      ```php
      public const string STATUS_ACTIVE = 'active';
      ```
    - **Reference:** [Constants in PHP](https://www.php.net/manual/en/language.constants.php)

16. **Do not check in commented or unused code.**
    - *Comment:* Use version control.
    - **Example:** Clean up code before committing.
    - **Reference:** [Best Practices for Version Control](https://www.atlassian.com/git/tutorials/comparing-workflows)

17. **Avoid abbreviations in the code.**
    - *Comment:* Leverage IDE features.
    - **Example:** Use `description` instead of `desc`.
    - **Reference:** [Clean Code Practices](https://www.oreilly.com/library/view/clean-code/9780136083238/)

18. **Use PHAR files for dev-dependency tools.**
    - *Comment:* Reduces conflicts and speeds up requirements.
    - **Example:** Use `phpunit.phar` for PHPUnit.
    - **Reference:** [PHP Archive (PHAR)](https://www.php.net/manual/en/intro.phar.php)

19. **Do not use asynchronous techniques in a synchronous language.**
    - *Comment:* Different paradigms can lead to complexity.
    - **Example:** Avoid mixing async JS techniques in PHP.

#### Shortlist:

* Use composer
  * Use [composer scripts](https://getcomposer.org/doc/articles/scripts.md) for automation
    * I have good experience with providing a static code analysis and tests with composer scripts in combination with bash scripts
* Use [githooks](https://git-scm.com/docs/githooks) like [here](https://gist.github.com/freshp/977f4b5bc67bd2426450680adb172d54) to prevent commit cascade with fix tests, static code analysis, and code style
* Use [openapi](https://www.openapis.org/) for API documentation
* Adopt [dependency injection](https://www.php.net/manual/en/language.oop5.decon.php)
* Use [value objects](https://wendelladriel.com/blog/understanding-value-objects-in-php) for domain logic
* Do not use external class directly, use a wrapper
* Use database migrations for example with [phinx](https://phinx.org/)
* Use a logger like [monolog](https://github.com/Seldaek/monolog)
* Use timestamp as exception code
  * use the current timestamp as exception code while creating the exception
  * it is better testable and the error log directly leads to the code
* Use [design patterns](https://refactoring.guru/design-patterns/php) if you have their usecases
* Use a factory for object creation
* Use a repository for database access
  * You can mock them in tests
  * You know where to find the database access
* Use [`filter_input`](https://www.php.net/manual/de/function.filter-input.php) to validate user input
* Do not reinvent the wheel
* Each repository should have a readme and the readme should be updated regularly
* Use final interfaces to collect typed constants
  * So you can bundle up contents like API date formats or other stuff.
* Know the packages of [php-fig](https://github.com/php-fig)
* Look through the packages of [phpleague](https://github.com/thephpleague)
* If you deal with money look at [moneyphp](https://github.com/moneyphp/money)
* Use [flysystem](https://github.com/thephpleague/flysystem) or [vfsStream](https://github.com/bovigo/vfsStream) to test file handling
* Use [symfony intl](https://packagist.org/packages/symfony/intl) for internationalization
* Use [symfony console](https://packagist.org/packages/symfony/console) for console applications
* Most reason why I could not write tests is because I could not mock core functions but you can [example-test-php-core-methods](https://github.com/freshp/example-test-php-core-methods)
* Working in teams is about working with API contracts. The smallest API contract are the public methods in a class.

## Learning the basics
This is just a small snapshot I can recommend.
(If you buy books please think about second hand books. The given links are more for information. 
Think twice before you order it.)

* Principles of object oriented design ([web](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod))
* The clean coder ([book](https://www.amazon.de/Clean-Coder-Conduct-Professional-Programmers/dp/0137081073) | [web](https://clean-code-developer.de/))
* Extremely defensive PHP ([video](https://www.youtube.com/watch?v=8d2AtAGJPno) | [slides](https://ocramius.github.io/extremely-defensive-php/))
* Design pattern ([web](https://designpatternsphp.readthedocs.io/en/latest/README.html))
* PHP standards recommendations [PSR](https://www.php-fig.org/psr/)
* Semantic versioning ([web](https://semver.org/))
* Refactoring ([book](https://www.amazon.de/Refactoring-Improving-Design-Existing-Technology/dp/0201485672))
* Principles of package design ([book](https://www.amazon.de/Principles-Package-Design-Creating-Components/dp/1484241185))
* A philosophy of software design ([book](https://www.amazon.de/Philosophy-Software-Design-John-Ousterhout/dp/1732102201))
* Pro git ([ebook](https://git-scm.com/book/de/v2))
* The mythical man-month ([book](https://www.amazon.de/-/en/Frederick-Brooks/dp/0201835959))

## Blogs
There are many more interesting blogs, but these selection cross up my way multiple times.
It could be beneficial to look also through old articles.

* https://blog.jetbrains.com/phpstorm/
* https://blog.cleancoder.com/
* https://matthiasnoback.nl/
* https://ocramius.github.io/
* https://www.sitepoint.com/php/
* https://www.zend.com/blog
* https://localheinz.com/articles/
* https://stitcher.io/

## Tools
* use package managers for your local requirements
    * for example in MacOS install [brew](https://brew.sh/index_de)
* install [php over brew](https://formulae.brew.sh/formula/php) on MacOS
    * *comment:* the big advantage is to have multiple versions linked by brew directly from the cellar 
* install [git over brew](https://gist.github.com/derhuerst/1b15ff4652a867391f03) on MacOS
* install [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh) bash on MacOS
* install [composer](https://getcomposer.org/download/) globally for dependency management in PHP
* install [xdebug](https://xdebug.org/docs/install) for debugging, tracing, profiling and the codecoverage

### Use web services for default tasks
* use a automation server like [jenkins](https://jenkins.io/) for continuous integration, continuous deployment or any other automation
* use a remote repository server like [gitlab](https://about.gitlab.com/) or [bitbucket](https://bitbucket.org/) or at least github 
* use a private package repository like [satis](https://github.com/composer/satis)
* use a error tracker like [sentry](https://sentry.io)

### Free online tools
* if you need regex, than use [this page](https://regex101.com/)
* you want to schedule a cronjob, than look at [this page](https://crontab.guru/)
* you are not sure with your version constraint, than look at [this page](https://jubianchi.github.io/semver-check/#/)
* communication is the key, use [showcode](https://showcode.app/) for better presentations

## IDE
* use an IDE for example [PHPStorm](https://www.jetbrains.com/phpstorm/) 
* set PHPStorm up ([jetbrains documentation](https://www.jetbrains.com/help/phpstorm/configuring-php-development-environment.html)) correctly 
    * use [inspections](https://www.jetbrains.com/help/phpstorm/code-inspection.html) 
    * use one of the default codestyles in PHPStorm for example [PSR-12](https://www.php-fig.org/psr/psr-12/)
    * use [xdebug](https://xdebug.org/) in PHPStorm ([documentation](https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html))
    * take a look at PHPStorm features like ai testing, testing, database, deployment, version control, ... [tutorials](https://blog.jetbrains.com/phpstorm/category/tutorials/)
* use plugins of PHPStorm:
    * [github-copilot](https://plugins.jetbrains.com/plugin/17718-github-copilot)
    * [.env](https://plugins.jetbrains.com/plugin/9525--env-files-support)
    * [php annotations](https://plugins.jetbrains.com/plugin/7320-php-annotations)
    * select a plugin for framework support like [symfony](https://plugins.jetbrains.com/plugin/7219-symfony-support)

## Important composer packages
The list of packages is not complete, but you can start projects from this stack.

* Composer package to handle [Security advisories](https://github.com/Roave/SecurityAdvisories). 
* Do not commit secrets and use [.env's](https://github.com/vlucas/phpdotenv) instead.
* The testing framework [PHPUnit](https://github.com/sebastianbergmann/phpunit).
   * If you reached nearly 100% of code coverage than you can go further with [infection](https://github.com/infection/infection).
* Static code analyses with [PHPStan](https://github.com/phpstan/phpstan) or [Psalm](https://github.com/vimeo/psalm).
* PHP Codesniffer with [PHPCS and PHPCBF](https://github.com/PHPCSStandards/PHP_CodeSniffer).
* Dependency injection container [PHP-DI](https://github.com/PHP-DI/PHP-DI)
* PHP library to generate [UUIDs](https://github.com/ramsey/uuid) or use [ULIDs](https://github.com/robinvdvleuten/php-ulid).
* Simple composer PHAR file handling with [tooly](https://github.com/tommy-muehle/tooly-composer-script). 

## Code reviews
Start making code reviews. If you dont know how? Read this [article](https://medium.com/palantir/code-review-best-practices-19e02780015f)

### Code review theses
> You are not your Code!
* code reviewer do not comment you, they comment your code
> If you find code you do not understand, ask.
* It is not the question if you should know, but when.

## Documentation
I only saw one approach, which seems to be suitable for software projects and this is [arc42](https://arc42.org/).

For further diagrams or graphs you can use [draw.io](https://app.diagrams.net/).
