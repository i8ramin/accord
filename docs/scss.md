# SCSS
This adapter uses [node-sass](https://github.com/andrew/node-sass), an incredibly fast C binding to libsass. It is however limited in that it does not include ways to work with plugins and extensions that are as robust as the main ruby version, and that it only supports the scss syntax, and not sass.

## Supported Methods
 - render

## Source Maps

Libsass does not yet support source maps, although at the time of writing there is [an open pull request](https://github.com/sass/libsass/pull/591) to work on this.

## Additional Options
It has a pretty standard API, and uses the [options documented here](https://github.com/andrew/node-sass#options). Do not pass through `data` or `file`, as this will be overridden by accord's wrapper - everything else is fair game.

If you do want to include plugins, you can start moving towards this type of functionality using the `importPaths` option - by adding a folder to this path, you will make all its contents available for `@import`s into your scss files. While not quite as robust as Stylus' options or sass-ruby's options, it will get the job done.

## Compile time included imports

The scss adapter returns an array of files included via `@import`. This array will be available as `imports` on the response object.

## Build meta information

Meta information about the build will be available as `meta` on the response object.
