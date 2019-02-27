# NPM notes

## Initiate a project

Working with NPM can be very usefull in your project. There are some handy commands to initiate NPM in your project.

This will initiate a package.json. After the command NPM wil ask you some question to fill in some details.

```sh
npm init
```

If you don't want to answer those question attach the `--yes` flag.

```sh
npm init --yes
```

## node_modules

When installing packages NPM will create a folder in your project that is called `node_modules`. These package are dependencies in your project and will be registerd in your package.json. By requiring the package in your `app.js` file Node.js will now that it has to look for the `node_modules` folder.

## Semantic versioning

Sementaic versioning or SamVer is a method to label versions of packages. A version number looks like this `"4.13.6"`. The structure of this number has a certain logic. They name it as Major.Minor.Patch.

- `Major` - When a new version is released and the original API will break.
- `Minor` - When new features are added but the API I won't break.
- `Patch` - When a bug has been fixed that had apeared only on the current version.

This is how it works: when you update from for example `"4.13.6"` with a minor update the version wil be `"4.14.0"`. This also applies on major updates and will look like this: `"5.0.0"`.

You can be flexible with using versions specifications like the carrot character `^` and the tilde `~`.

- `"^4.13.6"` - Will use any version as long as it is higher then `4.x.x`.
- `"~4.13.6"` - This will only use version `4` with a minimum of `"4.13.x"`.

Another neat thing to check your exact depencies versions is by the following comand:

```sh
npm list
```

But this list will show a list of your dependencies and its sub dependencies. But that can be pretty dence. If you want to see just the dependencies that you use, use this:

```sh
npm list --depth=0
```

If you want to check some information about dependecies about a package before installing write the following command:

```sh
npm view <package>
```

This command wil return the `package.json` file. You can add an extra parameter to the command to just see one single property of the file.

```sh
npm view mongoose dependencies
```

## Downgrading and upgrading packages

If you want to install a specific version or downgrading of a package then you can do that by adding `@version`.

```sh
npm i mongoose@2.4.2
```

After a while some packages might be updated a few times. To check that use:

```sh
npm outdated
```

To update the packages use:

```sh
npm update
```

Remember, this will not work for major updates. Only for minor and patches. This is beceause major updates could break your project. This will save a lot of headaches.

If you do want to update you project with the newest major updates then the package [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) can help you.

## Install dev dependencies

In order to install packages that are not used for bundles or the project itself use the `--save-dev`.

```sh
npm i jshint --save-dev
```

## Uninstalling dependencies

If you want to uninstall a package you can go for two options. With the `un` or `uninstall` commands.

```sh
npm un mongoose
```
