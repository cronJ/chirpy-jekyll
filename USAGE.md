# Usage information

## Docker image serve

For `jekyll serve` in a PowerShell use in the repository folder:

```
docker run -p 4000:4000 -v ${PWD}:/site ghcr.io/bretfisher/jekyll-serve
```

## Docker image build

Run the following command in the repository folder:

```
docker run -v ${PWD}:/site -it --entrypoint bash ghcr.io/bretfisher/jekyll
```

After the docker image is running, run the following command to build the image:

```
bundle install
bundle exec jekyll build
```

## Image size

Widest side is 800px.
