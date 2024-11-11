# Install

Add a new repository to `composer.json`:

```json
 "drupal-qa": {
    "type": "vcs",
    "url": "https://github.com/lussoluca/drupal-qa"
}
```

Install the package:

```shell
composer require lussoluca/drupal-qa:dev-main
```

When asked for `Do you want to create a grumphp.yml file?` answer `No`.

Add a `grumphp.yml` file to `src/drupal` with those lines:

```yml
imports:
  - { resource: vendor/lussoluca/drupal-qa/grumphp.yml }
```

Try to commit something and see GrumPHP runs the configured tools.

# Override

Some configurations can be overridden in the local `grumphp.yml` file:

* convention.phpstan.configuration
* convention.phpstan.level
