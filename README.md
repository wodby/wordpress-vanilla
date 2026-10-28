# Vanilla WordPress Composer boilerplate

A Composer-based WordPress project, ready to build and deploy with Wodby 2.0.

## Layout

```
composer.json        WordPress core, plugins and themes, managed by Composer
web/                 Web root
├── index.php        Front controller that loads WordPress from web/wp
├── wp/              WordPress core, installed by Composer (not committed)
└── wp-content/      Themes, plugins, must-use plugins and uploads
```

WordPress core is installed in `web/wp`, apart from `wp-content`, so Composer never touches your own code when it
installs or updates core. The site answers at the web root; core, including the admin, answers at `/wp`
(`/wp/wp-admin/`). The old `/wp-admin` and `/wp-login.php` addresses redirect there.

## Plugins and themes

Install plugins and themes from the WordPress.org directory with Composer, through [WP Packages](https://wp-packages.org):

```shell
composer require wp-plugin/akismet
composer require wp-theme/twentytwentyfour
```

They are installed in `web/wp-content/plugins` and `web/wp-content/themes`, and are not committed: the build runs
`composer install`.

Your own code is committed:

- Themes go in `web/wp-content/themes/<name>/`.
- Single-file must-use plugins go in `web/wp-content/mu-plugins/`.
- Plugins go in `web/wp-content/plugins/<name>/`. Add an exception for each to `.gitignore`, such as
  `!/web/wp-content/plugins/my-plugin/`, because the directory is otherwise left to Composer.

Update core, plugins and themes with `composer update`, commit `composer.lock` and deploy.

## Configuration

`web/wp-config.php` is not part of the project. The Wodby image generates it, with the database, salts, URLs and cache
settings of the environment.

Use WP-CLI with core's path, for example `wp plugin list --path=web/wp`.

## Use with Wodby 2.0

- This boilerplate is the build template of the Wodby 2.0 [WordPress PHP service](https://github.com/wodby/service-wordpress-php).
- A Wodby CI build pipeline is included.
- See https://wodby.com/stacks/wordpress

For local development with Docker, see [Docker4WordPress](https://github.com/wodby/docker4wordpress).
