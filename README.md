PHP Coding Standards Fixer
==========================

The PHP Coding Standards Fixer tool fixes *most* issues in your code when you
want to follow the PHP coding standards as defined in the PSR-1 and PSR-2
documents.

If you are already using `PHP_CodeSniffer` to identify coding standards
problems in your code, you know that fixing them by hand is tedious,
especially on large projects. This tool does the job for you.

Installation
------------

Download the
[`php-cs-fixer.phar`](http://cs.sensiolabs.org/get/php-cs-fixer.phar) file and
store it somewhere on your computer.

Usage
-----

The `fix` command tries to fix as much coding standards
problems as possible on a given file or directory:

    php php-cs-fixer.phar fix /path/to/dir
    php php-cs-fixer.phar fix /path/to/file

You can limit the fixers you want to use on your project by using the
`--level` option:

    php php-cs-fixer.phar fix /path/to/project --level=psr1
    php php-cs-fixer.phar fix /path/to/project --level=psr2
    php php-cs-fixer.phar fix /path/to/project --level=all

When the level option is not passed, all PSR-2 fixers and some additional ones
are run.

You can also explicitly name the fixers you want to use (a list of fixer names
separated by a comma):

    php php-cs-fixer.phar fix /path/to/dir --fixers=linefeed,short_tag,indentation

Here is the list of built-in fixers:

 * **indentation**     [PSR-2] Code must use 4 spaces for indenting, not tabs.

 * **linefeed**        [PSR-2] All PHP files must use the Unix LF (linefeed)
                   line ending.

 * **trailing_spaces** [PSR-2] Remove trailing whitespace at the end of lines.

 * **return**          [all] An empty line feed should precede a return
                   statement.

 * **short_tag**       [PSR-1] PHP code must use the long <?php ?> tags or the
                   short-echo <?= ?> tags; it must not use the other tag
                   variations.

 * **unused_use**      [all] Unused use statements must be removed.

 * **braces**          [PSR-2] Opening braces for classes and methods must go on
                   the next line, and closing braces must go on the next
                   line after the body. Opening braces for control
                   structures must go on the same line, and closing braces
                   must go on the next line after the body.

 * **visibility**      [PSR-2] Visibility must be declared on all properties and
                   methods; abstract and final must be declared before the
                   visibility; static must be declared after the visibility.

 * **phpdoc_params**   [all] All items of the @param phpdoc tags must be aligned
                   vertically.

 * **eof_ending**      [all] A file must always ends with an empty line feed.

 * **controls_spaces** [all] A single space should be between: the closing brace
                   and the control, the control and the opening parenthese,
                   the closing parenthese and the opening brace.

 * **elseif**          [PSR-2] The keyword elseif should be used instead of else
                   if so that all control keywords looks like single words.

You can also use built-in configurations, for instance when ran for Symfony:

    # For the Symfony 2.1 branch
    php php-cs-fixer.phar fix /path/to/sf21 --config=sf21

Here is the list of built-in configs:

 * **default** A default configuration

 * **magento** The configuration for a Magento application

 * **sf20**    The configuration for the Symfony 2.0 branch

 * **sf21**    The configuration for the Symfony 2.1 branch

Instead of using the command line arguments, you can save your configuration
in a `.php_cs` file in the root directory of your project. It
must return an instance of `Symfony\CS\ConfigInterface` and it lets you
configure the fixers and the files and directories that need to be analyzed:

    <?php

    $finder = Symfony\CS\Finder\DefaultFinder::create()
        ->exclude('somefile')
        ->in(__DIR__)
    ;

    return Symfony\CS\Config\Config::create()
        ->fixers(array('indentation', 'elseif'))
        ->finder($finder)
    ;

Helpers
-------

If you are using Vim, install the dedicated
[plugin](https://github.com/stephpy/vim-php-cs-fixer).

Contribute
----------

The tool comes with quite a few built-in fixers and finders, but everyone is
more than welcome to [contribute](https://github.com/fabpot/php-cs-fixer) more
of them.

### Fixers

A *fixer* is a class that tries to fix one CS issue (a `Fixer` class must
implement `FixerInterface`).

### Configs

A *config* knows about the CS level and the files and directories that must be
scanned by the tool when run in the directory of your project. It is useful
for projects that follow a well-known directory structures (like for Symfony
projects for instance).
