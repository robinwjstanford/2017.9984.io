# 2017.9984.io

> The 9984 >> SUMMIT 2017 site
>
> Blockchain Futures for Developers, Enterprises &amp; Society
> October 5 - 6, 2017
> https://2017.9984.io

[![Build Status](https://travis-ci.org/9984/2017.9984.svg?branch=master)](https://travis-ci.org/9984/2017.9984)
[![css bigchaindb](https://img.shields.io/badge/css-bigchaindb-39BA91.svg)](https://github.com/bigchaindb/stylelint-config-bigchaindb)
[![Greenkeeper badge](https://badges.greenkeeper.io/9984/2017.9984.io.svg)](https://greenkeeper.io/)

---

**[Live](http://2017.9984.io) | [Beta](http://beta.2017.9984.io)**

---

# Content editing

The following instructions apply to adding / editing speakers & talks.

## Adding / editing speakers & talks

- Each content item is represented as a Markdown file with YAML at the top. The data should look something like this:
  ```
  ---
  property: "value"
  other_property:
    - "list"
    - "of"
    - "values"
  ---
  ```

### Add new content through GitHub

  1. Click into the appropriate directory ([/_src/_speakers](_src/_speakers), [/_src/_talks](_src/_talks)
  1. Copy the data from an existing `.md` file
  2. In the parent folder, click `Create new file`
  3. Paste the data into GitHub and edit
  4. Edit to your heart’s content!
     - The filename you choose may determine the content page URL
     - The `id` property should be the same as the filename
  5. When finished, fill in a commit description and select `Create a new branch for this commit and start a pull request`.
  6. Wait to see if the created pull request passes the build. If it does, click merge and your changes will be live

# Development

You need to have the following tools installed on your development machine before moving on:

- [node.js](http://nodejs.org/) & [npm](https://npmjs.org/)
- (optional) use [Yarn](https://yarnpkg.com) instead of npm for faster dependency installations
- [Ruby](https://www.ruby-lang.org) (for sanity, install with [rvm](https://rvm.io/))
- [Bundler](http://bundler.io/)

## Install dependencies

Run the following command from the repository's root folder to install all dependencies.

```bash
npm i && bundle install
```

or

```bash
yarn && bundle install
```

## Development build

Spin up local dev server and livereloading watch task, reachable under [https://localhost:1337](https://localhost:1337):

```bash
gulp
```

# Continuous deployment: always be shipping

![shipping](https://cloud.githubusercontent.com/assets/90316/26559768/e21e9724-44b1-11e7-90cf-6ef6ebb06d09.gif)

The site gets built & deployed automatically via Travis. This is the preferred way of deployment, it makes sure the site is always deployed with fresh dependencies and only after a successful build.

Build & deployment happens under the following conditions on Travis:

- every push builds the site
- **live deployment**: every push to the master branch initiates a live deployment
- **beta deployment**: every new pull request and every subsequent push to it initiates a beta deployment

# Manual deployment

For emergency live deployments or beta & gamma deployments, the manual method can be used. The site is hosted in an S3 bucket and gets deployed via a gulp task.

## Prerequisite: authentication

To deploy the site, you must authenticate yourself against the AWS API with your AWS credentials. Get your AWS access key and secret and add them to `~/.aws/credentials`:

```
[default]
aws_access_key_id = <YOUR_ACCESS_KEY_ID>
aws_secret_access_key = <YOUR_SECRET_ACCESS_KEY>
```

This is all that is needed to authenticate with AWS if you've setup your credentials as the default profile.

If you've set them up as another profile, say `[9984]` you can grab those credentials by using the `AWS_PROFILE` variable like so:

```bash
AWS_PROFILE=9984 gulp deploy --live
```

In case that you get authentication errors or need an alternative way to authenticate with AWS, check out the [AWS documentation](http://docs.aws.amazon.com/AWSJavaScriptSDK/guide/node-configuring.html).

## Staging build & beta deployment

The staging build is a full production build but prevents search engine indexing & Google Analytics tracking.

```bash
# make sure your local npm packages & gems are up to date
npm update && bundle update

# make staging build in /_dist
# build preventing search engine indexing & Google Analytics tracking
gulp build --staging

# deploy contents of /_dist to beta
gulp deploy --beta
```

## Production build & live deployment

```bash
# make sure your local npm packages & gems are up to date
npm update && bundle update

# make production build in /_dist
gulp build --production

# deploy contents of /_dist to live
gulp deploy --live
```

# Coding conventions

## (S)CSS

Follows [stylelint-config-bigchaindb](https://github.com/bigchaindb/stylelint-config-bigchaindb) which itself extends [stylelint-config-standard](https://github.com/stylelint/stylelint-config-standard).

Lint with [stylelint](https://stylelint.io) in your editor or run:

```bash
npm test
```

# Authors

- Matthias Kretschmann ([@kremalicious](https://github.com/kremalicious)) - [BigchainDB](https://www.bigchaindb.com)
