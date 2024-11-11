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

When asked for `Do you want to create a grumphp.yml file?`, answer `No`.

Add a `grumphp.yml` file to `src/drupal` with those lines:

```yml
imports:
  - { resource: vendor/lussoluca/drupal-qa/grumphp.yml }
```

# Override

Some configurations can be overridden in the local `grumphp.yml` file:

* convention.phpstan.configuration
* convention.phpstan.level

# Run outside of a commit

To run the tool before creating a commit, add those lines to `Makefile.project`:

```make
.PHONY: grumphp
grumphp:
  docker run --rm -it \
    -v ${PWD}:/app -w /app \
    ghcr.io/sparkfabrik/drupal-qa:2.5.0 sh -c "cd src/drupal && php bin/grumphp git:pre-commit"
```

Run `make grumphp` to start the tool.

*Disclaimer*: Docker image `ghcr.io/sparkfabrik/drupal-qa` is used here just because it contains both PHP and GIT executables;
any images with those tools will be OK. We should use an image that has the same PHP version of the project.

# Run for all commits

Run this command:

```shell
docker run --rm -it -v ${PWD}:/app -w /app ghcr.io/sparkfabrik/drupal-qa:2.5.0 sh -c "cd src/drupal && php bin/grumphp git:init"
```

This will update the `pre-commit` and `commit-msg` GIT hooks to run GrumPHP.

Now try to commit something and see GrumPHP runs the configured tools.

*Disclaimer*: Docker image `ghcr.io/sparkfabrik/drupal-qa` is used here just because it contains both PHP and GIT executables;
any images with those tools will be OK. We should use an image that has the same PHP version of the project.