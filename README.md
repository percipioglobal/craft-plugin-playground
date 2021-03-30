## About percipioglobal/craft-plugin-playground

This is a project scaffolding package for Craft 3 CMS plugin development.

## Using percipioglobal/craft-plugin-playground

This project package works exactly the way Pixel & Tonic's [craftcms/craft](https://github.com/craftcms/craft) package works; you create a new project by first creating & installing the project:

    composer create-project percipioglobal/craft-plugin-playground --no-install

This will create a project named `craft-plugin-playground` which is a turnkey Craft CMS install for developing plugins.

We use `--no-install` so that the composer packages for the root project are not installed.

## Setting Up Local Dev

You'll need Docker desktop for your platform installed to run the project in local development

* Composer will have already created a `.env` file in the `cms/` directory, based off of the provided `example.env`
  
* Edit the `cms/composer.json` file and change the line `"url": "/Users/percipio/dev/craft-plugins/*",` in `repostories` to point to your local plugin Git repositories
* Edit the `docker-composer.yaml` file and change the line `- /Users/percipio/dev/craft-plugins:/Users/percipio/dev/craft-plugins` to point to your local plugin Git repositories
* Start up the site with `docker-compose up` (the first build will be somewhat lengthy)
* Navigate to `http://localhost:8001` to use the site

### Login

The default login is:

**User:** `development@percipio.london` \
**Password:** `letmein`

### Updating

To update to the latest Composer packages (as constrained by the `cms/composer.json` semvers), do:
```
rm cms/composer.lock
docker-compose up
```

### External Access

The ports are bound as follows if you want to connect with eg. Sequel Ace, Tableplus, DataGrip, ...:

**Mysql:** `5306`
**PostgreSQL:** `6432`

### Switching between MySQL & Postgres

The plugindev project supports both MySQL and Postgres out of the box. It spins up a container for each database, and seeds them with a starter db.

To use MySQL (the default) just type:
```bash
make mysql
```

To use Postgres just type:
```bash
make postgres
```

...and then just reload the page.

This is great for ensuring your db queries work properly on both MySQL and Postgres, without having to set up two separate environments.

### Dual PHP Containers for Xdebug

By default, all of your requests will be routed through the production PHP container, for speedy local development and testing.

However, there is a second Xdebug PHP container that's always running too, for the time that you need to use Xdebug on the really tough problems.

What happens is a request comes in, Nginx looks to see if there's an `XDEBUG_SESSION` cookie set. If there's no cookie, it routes the request to the regular php container.

If however the `XDEBUG_SESSION` cookie is set (with any value), it routes the request to the php_xdebug container.

You can set this cookie with a [browser extension, your IDE](https://xdebug.org/docs/step_debug), or via a number of other methods. Here is the Xdebug Helper browser extension for your favorite browsers: [Chrome](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc) - [Firefox](https://addons.mozilla.org/en-GB/firefox/addon/xdebug-helper-for-firefox/) - [Safari](https://apps.apple.com/app/safari-xdebug-toggle/id1437227804?mt=12)

You can read more about it in the Dual [An Annotated Docker Config for Frontend Web Development](https://nystudio107.com/blog/an-annotated-docker-config-for-frontend-web-development#xdebug-performance) article.

### Makefile Project Commands

This project uses Docker to shrink-wrap the devops it needs to run around the project.

To make using it easier, we're using a Makefile and the built-in `make` utility to create local aliases. You can run the following from terminal in the project directory:

- `make dev` - starts up the local dev server listening on `http://localhost:8000/`
- `make clean` - shuts down the Docker containers, removes any mounted volumes (including the database), and then rebuilds the containers from scratch
- `make mysql` - switches the project to use the MySQL database container; just reload the browser
- `make postgres` - switches the project to use the Postgres database container; just reload the browser
- `make composer xxx` - runs the `composer` command passed in, e.g. `make composer install`

### XDebug with VScode

To use Xdebug with VSCode install the [PHP Debug extension](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug ) and use the following configuration in your `.vscode/launch.json`:
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003,
            "log": true,
            "externalConsole": false,
            "pathMappings": {
                "/var/www/project/cms": "${workspaceRoot}/cms"
            },
            "ignore": ["**/vendor/**/*.php"]
        }
    ]
}
```


Below is the entire intact, unmodified `README.md` from Pixel & Tonic's [craftcms/craft](https://github.com/craftcms/craft):

.....

<p align="center"><a href="https://craftcms.com/" target="_blank"><img width="312" height="90" src="https://craftcms.com/craftcms.svg" alt="Craft CMS"></a></p>

## About Craft CMS 

Craft is a flexible and scalable CMS for creating bespoke digital experiences on the web and beyond.

It features:

- An intuitive Control Panel for administration tasks and content creation.
- A clean-slate approach to content modeling and [front-end development](https://docs.craftcms.com/v3/dev/).
- A built-in Plugin Store with hundreds of free and commercial [plugins](https://plugins.craftcms.com/).
- A robust framework for [module and plugin development](https://docs.craftcms.com/v3/extend/).

Learn more about it at [craftcms.com](https://craftcms.com).

## Tech Specs

Craft is written in PHP (7+), and built on the [Yii 2 framework](https://www.yiiframework.com/). It can connect to MySQL (5.5+) and PostgreSQL (9.5+) for content storage.

## Installation

See the following documentation pages for help installing Craft 3:

- [Server Requirements](https://docs.craftcms.com/v3/requirements.html)
- [Installation Instructions](https://docs.craftcms.com/v3/installation.html)
- [Upgrading from Craft 2](https://docs.craftcms.com/v3/upgrade.html)

## Popular Resources

- **[Documentation](http://docs.craftcms.com/v3/)** – Read the official docs.
- **[Guides](https://craftcms.com/guides)** – Follow along with the official guides.
- **[#craftcms](https://twitter.com/hashtag/craftcms)** – See the latest tweets about Craft.
- **[Discord](https://craftcms.com/discord)** – Meet the community.
- **[Stack Exchange](http://craftcms.stackexchange.com/)** – Get help and help others.
- **[CraftQuest](https://craftquest.io/)** – Watch unlimited video lessons and courses.
- **[Craft Link List](http://craftlinklist.com/)** – Stay in-the-know.
- **[Percipio Blog](https://percipio.london/blog)** – About Craft / modern web development and other takes

Major thanks to [nystudio107](https://nystudio107.com/) for all the great work on this boilerplate!