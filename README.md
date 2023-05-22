# bcit-reseach-long-term-issp.github.io
Documentation for the EMA YVR Project

These docs are accessible through the URL https://bcit-reseach-long-term-issp.github.io/

This uses the [Just the Docs](https://just-the-docs.github.io/just-the-docs/) theme.

## Development

To run this repository locally in a development environment, you must use Ruby version 2.X. It is optional to use a Ruby version manager such as `rbenv` to have better control over Ruby versions across your machine and projects.

Once you have Ruby version 2.X set up on your machine, install bundler.
```
gem install bundler
```

Next, use bundler to install the necessary project dependencies.

```
bundle install
```

To start running the project locally, run:
```
bundle exec jekyll serve -lI
```
The project will start running on: http://127.0.0.1:4000//

Note that, while there is Live Reload to reflect your saved changes locally, at times, this refresh rate is slow and you may have to restart the server.

By merging your branch or changes to `master`, github will automatically run build and deploy the changes to the github.io site. Perhaps sometimes a branch is handy to manage your changes!

Happy doc'ing!
