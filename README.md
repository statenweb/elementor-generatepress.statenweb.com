Preamble
===

This is a customized [Underscores](https://underscores.me) theme. Some of the built in functionality that is part of Underscores has been removed, including registering a menu, adding customizer options and more. Feel free to add them back in a file that conforms to the autoloading pattern the project uses.

Required Tooling
===

- (npm)[https://npmjs.com]
- (composer)[https://getcomposer.org]


Backend Notes
===

- This project is to adhere to PHP Code Standards. For linting see the section **Linting** below.
- Do not pollute functions.php split out all of functionality into separate structured file path
- Use a namespaced autoloader (see **Note on Adding / Updating Composer Packages** below)
- include the code for registering a post type (and any associated code for the post type) in a file /{THEME_DIR}/project-namespace/data-structures/post-types/people.php
- include generic actions in a file /{THEME_DIR}/project-namespace/data-structures/actions.php
- include generic filters in a file /{THEME_DIR}/project-namespace/filters.php
- Use acf pro + acf-json
- if using a plugin check https://wpvulndb.com/
- Remember to use composer for plugins
- Use sanitization! https://developer.wordpress.org/themes/theme-security/data-sanitization-escaping/

Frontend Notes
===

Use bootstrap 4 (will be included in scaffolding). Use its build functionality and color pallette extensibility along with utility functions where possible. Try to write as little CSS as possible.

-   Requires [yarn](https://yarnpkg.com/lang/en/)

#### SCSS

##### Variables

Follow best practices for themeing and updating default variables where necessary see https://getbootstrap.com/docs/4.4/getting-started/theming/#modify-map). Use variables where you can for spacing (see https://getbootstrap.com/docs/4.4/utilities/spacing/#how-it-works) and colors (see https://getbootstrap.com/docs/4.4/getting-started/theming/#modify-map)

##### Utilities

-   The most important guiding principle for the markup and sass is to use almost all of the built in bootstrap functionality (bootsrap variables, utility classes, theme colors, etc)
    -   Before you create any new CSS ask yourself: are there any utility classes in bootstrap?
        -   [Borders](https://getbootstrap.com/docs/4.3/utilities/borders/)
        -   [Clearfix](https://getbootstrap.com/docs/4.3/utilities/clearfix/)
        -   [Close icon](https://getbootstrap.com/docs/4.3/utilities/close-icon/)
        -   [Colors](https://getbootstrap.com/docs/4.3/utilities/colors/)
        -   [Display](https://getbootstrap.com/docs/4.3/utilities/display/)
        -   [Embed](https://getbootstrap.com/docs/4.3/utilities/embed/)
        -   [Flex](https://getbootstrap.com/docs/4.3/utilities/flex/)
        -   [Float](https://getbootstrap.com/docs/4.3/utilities/float/)
        -   [Image replacement](https://getbootstrap.com/docs/4.3/utilities/image-replacement/)
        -   [Overflow](https://getbootstrap.com/docs/4.3/utilities/overflow/)
        -   [Position](https://getbootstrap.com/docs/4.3/utilities/position/)
        -   [Screen readers](https://getbootstrap.com/docs/4.3/utilities/screen-readers/)
        -   [Shadows](https://getbootstrap.com/docs/4.3/utilities/shadows/)
        -   [Sizing](https://getbootstrap.com/docs/4.3/utilities/sizing/)
        -   [Spacing](https://getbootstrap.com/docs/4.3/utilities/spacing/)
        -   [Stretched link](https://getbootstrap.com/docs/4.3/utilities/stretched-link/)
        -   [Text](https://getbootstrap.com/docs/4.3/utilities/text/)
        -   [Vertical align](https://getbootstrap.com/docs/4.3/utilities/vertical-align/)
        -   [Visibility](https://getbootstrap.com/docs/4.3/utilities/visibility/)
        -   or more @ [https://getbootstrap.com](https://getbootstrap.com)
        -   or check the `_utilities.scss` (or other scss files) in the project
-   look @ the `_variables.scss` to see some of the overrides I have added. Feel free to add more variables, please document any changes with comments.
-   look @ the `_utilities.scss` file I have added in a bunch of font size helpers, line height helpers and more
-   look @ the `_custom-bootstrap.scss` for typography helper classes
-   look @ `_typography.scss` file I have created a bunch of helper classes for fonts
-   Margins padding’s and spacing should be the closest to the design. If you see lots of designs differences or things that don’t match bootstrap spacing pb-2, m-1 etc let me know
-   Outside of the native bootstrap (s)css, the only custom css that should be written should be extreme edge cases and custom reusable utility classes.
-   Creating a new scss file, if it's a utility it should go int the `_utilities.scss` class and should be documented
-   If you are handling an edge case and it's not a utility class definition, add a partial and name it something that makes sense, e.g. `_book-module` or `_hero.scss` and include it in the `app.scss`


Steps to build the Frontend
===

-   run `npm install` from the theme directory
-   run `npm run build:local` or `npm run build:local:watch` from the theme directory
-   point a web server (e.g. MAMP) to the public directory and run from your browser



Note on Adding / Updating Composer Packages
===

I want to stress something of utmost importance -- handling `composer.json`, specifically versions of packages. If you want to update a theme or a plugin - this is done in the `composer.json` file. [Composer natively supports all different types of version constraints](https://getcomposer.org/doc/articles/versions.md) -- for this project we are not using any modifiers, we are using exact versions. For example see the (example) Composer file below

```
{
  "name": "webteam/sample",
  "description":"Sample",
  "authors": [
    {
      "name": "Gargano, Matthew",
      "email": "mat@statenweb.com"
    }
  ],
  "config": {
    "preferred-install": "dist",
    "disable-tls": true,
    "secure-http": false
  },
  "repositories": [
    {
      "type": "composer",
      "url": "https://wpackagist.org"
    },
    {
      "type": "composer",
      "url": "http://satis.statenweb.com/"
    },
    {
      "type": "composer",
      "url": "https://composer.deliciousbrains.com/THISISNOTREAL"
    }
  ],
  "require": {
    "php": ">=5.6",
    "mnsami/composer-custom-directory-installer": "^1.1",
    "composer/installers": "~1.0.12",
    "deliciousbrains-plugin/wp-migrate-db-pro": "1.9.5",
    "deliciousbrains-plugin/wp-migrate-db-pro-media-files": "1.4.13",
    "prh/sales-platform-white-label-theme": "5.0.31",
    "prh/sales-api": "1.0.8",
    "prh/advanced-custom-fields-pro" : "5.6.13"
    
  },
  "require-dev": {
    "squizlabs/php_codesniffer": "^2.5.1",
    "vlucas/phpdotenv": "^2.0.1",
    "roots/wordpress": "5.1.1"
  },
  "extra": {
    "installer-paths": {
      "web/app/mu-plugins/{$name}/": [
        "type:wordpress-muplugin"
      ],
      "web/app/plugins/{$name}/": [
        "type:wordpress-plugin"
      ],
      "web/app/themes/{$name}/": [
        "type:wordpress-theme"
      ]
    },
    "wordpress-install-dir": "web/wp"
  },
  "scripts": {
    "test": [
      "vendor/bin/phpcs"
    ]
  }
}


```
You will note that *besides some composer related packages*, all of the WordPress plugin versions in the `requires` key are exact versions, i.e. no modifiers `~` `^` `>` `*` etc. before any version numbers. Summarily, any plugin should be explicitly versioned by the exact version number. This will help save us from the inadvertent introduction of regressions that may cause based on a new (unexpected) plugin version.


Autoloading Pattern
===
This project's theme uses a file called `application.php` within its theme. In that file, the theme registers an autoloader for the standard PHP library (SPL) autoloader to (attempt to) autoload classes in the application namespace when they are instantiated below the call to the spl_autoload_register. 

It uses the namespace of the class to locate the class file to include - the only difference between the actual namespace and the file that it tries to include is that it translates it to all lowercase, adds a .php to the end and then replaces "_" with a "-" and "\" with the current file system's directory separator (Linux its /). 

For example, if there is class whose fully qualified namespace + class is "\Social_Impact\Settings\Site" and the application tries to new it up and the PHP application doesn't recognize it, it will try to include a file located in "social-impact/settings/site.php" if it does not find the file name it will die telling you where it expected the file to be located based on its namespace.

Below the spl_autoload_register call is where the theme initializes classes used in the application. The WordPress classes usually follow the same pattern; each class is namespaced based on its directory (see above). Each class typically has an `init` method and a `attach_hooks` method. WordPress is all about actions and filters -- collectively known as hooks. Look at the classes in the repo to get a better feel for the architecture. 


Getting Started
===

1. Check out this repo
1. Map (no pun intended) a local domain, e.g. socialimpact.tst to {REPO ROOT}/web
1. Create a local DB
1. Copy `.env.example` to `.env`
1. Update the `DB_NAME`, `DB_USER`, `DB_PASSWORD` as applicable
1. Navigate to the mapped location (from above)
1. Install WordPress and plugins by running `composer install`
1. Navigate to the mapped domain.
1. Walk through the default install of WordPress
1. The next, optional steps are, locally, to:  
    1. Activate WP Migrate DB Pro + the WP Migrate DB Pro Media Add On.
    1. Obtain the Delicious Brains WP Migrate DB Pro key and enter it
    1. Obtain the Connection Info from the live site
    1. Pull the database and media from the live site

At this point you will have a live copy of a WordPress instance without the theme.


1. The next step is to go to the theme directory and run:
    1. npm install
    2. npm run build:local:watch
    
    This will run webpack's watch functionality and will compile your JS/SCSS and run the webpack build process whenever any assets it is watching are changed.

That's all, you're set to get started.


Linting
===

There's a PHP Code Sniffer linting script that you can run by running `composer run lint.` This lints the theme directory for the site and ignores some specific locations. If you add or have code elsewhere, please update the script in composer.json to ensure your code is covered in the check.
