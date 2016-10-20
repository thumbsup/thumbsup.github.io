# thumbsup website

## Setup

- Install [Jekyll](https://jekyllrb.com/)
- Run `bundle install`

## Making changes

- Start Jekyll with `bundle exec jekyll serve`
- Make changes
- Browse to http://localhost:4000
- When you're happy, commit &amp; push
- Github will publish the results to https://thumbsup.github.io

## Rebuilding the demo galleries

To avoid dependencies on `ffmpeg` etc, building the demo sites requires [Docker](https://www.docker.com).
Verify it's working by running `docker pull thumbsup/thumbsup`.

The following command will rebuild all demo sites, using different templates and config settings:

```bash
./build-demos
```
