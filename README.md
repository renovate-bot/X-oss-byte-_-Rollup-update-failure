# Rollback Update Failure

* Plugin Name: Rollback Update Failure
* Contributors: afragen
* Tags: feature plugin, update, failure
* License: MIT
* Requires PHP: 5.6
* Requires at least: 5.2
* Stable Tag: main

Feature plugin for testing automatic rollback of a plugin or theme update failure.

## Description

This is a feature plugin based on the [PR](https://github.com/WordPress/wordpress-develop/pull/860) for [#51857](https://core.trac.wordpress.org/ticket/51857).

The assumption is that most of the errors in large plugins/themes occur during the `copy_dir()` part of `WP_Upgrader::install_package()`. There is at least one additional Trac ticket that is needed as well, [#52342](https://core.trac.wordpress.org/ticket/52342).

It is during the `WP_Upgrader::install_package()` that the currently installed plugin is deleted in anticipation of copying the new update into that location. Having an empty plugin/theme folder or an incompletely copied update seems to be the most common issue.

Requires Trac ticket [#52831](https://core.trac.wordpress.org/ticket/52381) in order to do the acutal rollback in the event of a plugin/theme update failure.

There will be messaging in the event of an error and successful or unsuccessful rollback.

## Testing

There was much discussion regarding the thought that adding additional IO processes for the zip and unzip process could result in server timeout issues on resource starved shared hosts. Activating the feature plugin will result in the creation of a zipfile of the installed plugin/theme being updated.

For the sake of testing assume any server timeout occurring during the update process might be releated to the additional IO processes creating the zipfile. Please report these in [GitHub Issues](https://github.com/afragen/rollback-update-failure/issues) and report your server details. ( Host, RAM, OS, etc. )

To simulate a failure, use the filter `add_filter( 'rollback_update_testing', '__return_true' );`

## Reporting

Please submit [issues](https://github.com/afragen/rollback-update-failure/issues) and [PRs](https://github.com/afragen/rollback-update-failure/pulls) to GitHub.

## Changelog

Please see the Github repository: [CHANGELOG.md](https://github.com/afragen/rollback-update-failure/blob/main/CHANGELOG.md).
