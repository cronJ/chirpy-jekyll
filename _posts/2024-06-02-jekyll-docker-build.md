---
title: Jekyll Docker Build
date: 2024-06-02 16:15:00 +0200
categories: [Jekyll, Software]
tags: [jekyll, docker, build]
---

After using a static site generator (Pelican) in the past and not being happy with WordPress, I decided to try Jekyll.

I found a really nice theme which comes with a complete starter repository as a template.
So, I hadn't to start from scratch.
The theme is called chirpy and is available on GitHub [here](https://github.com/cotes2020/chirpy-starter).

I had most of my posts already as Markdown files on my local machine.
Only the front matter needed some adjustments to make it work with Jekyll.

At first, I used WSL for running Ruby and Jekyll.
But I wanted to use Docker instead of WSL, so that in the future it will still work.

## Pre-configured Docker images

I found the following repository which provides two different Docker images: [BretFisher/jekyll-serve](https://github.com/BretFisher/jekyll-serve)

When writing locally, I can run a Jekyll serve image with `docker run -p 4000:4000 -v ${PWD}:/site ghcr.io/bretfisher/jekyll-serve` from inside my local repository.
This will auto-generate the site and serve it on port 4000.

But, when I have finished everything and pushed it to GitHub, I want to release a new site with Jekyll.

For this I created a workflow which uses GitHub Actions and attaches the build to a release.

## Workflow

For the local build I used the command `docker run -v ${PWD}:/site -it --entrypoint bash ghcr.io/bretfisher/jekyll` followed by `bundle install` and `bundle exec jekyll build`.

In an automated workflow we can remove the `-it` because we have no terminal.
After the build is done we can also remove the container, so we add the `--rm` flag.

This gives us the new Docker command:

```
docker run --rm -v ${PWD}:/site --entrypoint bash ghcr.io/bretfisher/jekyll -c "bundle install && bundle exec jekyll build"
```

But to use it in an GitHub Actions workflow we have to adapt it a little further.

{% raw %}

```
docker run --rm -v ${{ github.workspace }}:/site --entrypoint bash ghcr.io/bretfisher/jekyll -c "git config --global --add safe.directory /site && bundle install && bundle exec jekyll build"
```

{% endraw %}
{% raw %}
The `${PWD}` is replaced with `${{ github.workspace }}`.
And we add `git config --global --add safe.directory /site` to avoid permission problems.
{% endraw %}
So, we can now write a workflow file which looks like this:

{% raw %}

```yml
name: Build Jekyll Site and Attach to Release

on:
  release:
    types: [created]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2

      - name: Run Docker container and build site
        run: |
          docker run --rm \
          -v ${{ github.workspace }}:/site \
          --entrypoint bash ghcr.io/bretfisher/jekyll \
          -c "git config --global --add safe.directory /site && bundle install && bundle exec jekyll build"

      - name: Zip the site
        run: zip -r "chirpy-jekyll-${{ github.ref_name }}.zip" _site

      - name: Upload release asset
        uses: actions/upload-release-asset@v1
        with:
          upload_url: ${{ github.event.release.upload_url }}
          asset_path: ./chirpy-jekyll-${{ github.ref_name }}.zip
          asset_name: chirpy-jekyll-${{ github.ref_name }}.zip
          asset_content_type: application/zip
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

{% endraw %}

The workflow has only one job, which uses the following steps:

1. Trigger when a GitHub release is created
2. Checkout the repository
3. Set up `Docker Buildx`
4. Run the Docker container
5. Build the Jekyll site
6. Zip the site with the version tag in the file name
7. Upload the release asset

<!-- prettier-ignore-start -->
> Check the GitHub repository settings. This workflow needs to have write permission.
{: .prompt-warning }
<!-- prettier-ignore-end -->

## Conclusion

Over all, it was a little trial and error to get the Jekyll build working.
But now I have two easy ways to work on posts and generate a new site version.
