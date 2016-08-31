# Git stuff
## Problem: when creating a new branch from a remote repo, its not set to automatically push to the remote.
### Solution: Config git to auto push new branch to repo on push.

```
git config --global push.default current
git checkout -b my-new-branch
git push -u
```

# Drupal 8:
## Problem: Find and then set settings in PHP
### Solution: Use Drush config-list
`drush config-list`
`drush config-get system.file`
#### View overridden settings:
`drush config-get system.file --include-overridden`

## Settings.php changes
### Trusted Hosts
```
$settings['trusted_host_patterns'] = array(
  '^vm-try-udevintra\.oag.lawnet$',
  '^vm-try-udevintra$',
  '^vm-try-uintra\.oag.lawnet$',
  '^vm-try-uintra$',
  '^nymatters\.vm$',
  '^.+\.nymatters\.vm$',
);
```

## Enable Local Settings.php
```
if (file_exists(__DIR__ . '/settings.local.php')) {
  include __DIR__ . '/settings.local.php';
}
```

## Set settings in local PHP
`$config['system.file']['path']['temporary'] = '/var/www/drupal-temporary-path';`

## Enable Local Development services:
`$settings['container_yamls'][] = DRUPAL_ROOT . '/sites/development.services.yml';`

## Enable TWIG Debugging
`development.services.yml`

## Theming Guide:
https://sqndr.github.io/d8-theming-guide/index.html

Need to uninstall and re-install theme to apply new settings.

## Wrapping JS behaviors:
https://sqndr.github.io/d8-theming-guide/javascript/behaviors.html

## Blocks:
Placing Blocks now instead of them all showing in the list.

Blocks are per theme

## Modules:
Modules are not disabled, they are uninstalled completely now.

## Drupal 8 complaining about missing modules?
https://www.drupal.org/node/2487215
run drush and also can do PHP for D8 stuff:

```
drush php
Drupal::configFactory()->getEditable('custom_search.settings')->delete();
Drupal::configFactory()->getEditable('custom_search.settings.results')->delete();
```

*Do not remove module from system without uninstalling it.*

# Drupal 8 make a custom library:
```
THEME.libraries.yml
library-name:
  js:
    scripts/myscript.js: {}
  dependencies:
  - core/jquery
```

## then in your twig template
`{{ attach_library('THEME/library-name') }}`

## Twig templates have extra filters in Drupal 8:
https://www.drupal.org/node/2357633
used |clean_id

# Views:
Want to group view rows based on a field? but want to also keep the view to display your perfectly crafted content display instead of every field individually? Follow this tutorial (D7 & D8 Compatible, D8 requires no additional modules though) https://www.webomelette.com/drupal-views-grouping-field-content-display-modes (edited)

[11:15]
TL;DR Display Fields, include grouping field, group by that field, include another field that is "Rendered content" and the display type and BOOM GOES THE :dynamite:

CMI
will be powerful
export configuration from one to another.
