# Zonkytech official blog

This is the repo for the official blog. The blog is using [Hexo](https://hexo.io/).

## Running the development server

To start the development server you need to install the theme, npm dependencies and run `hexo server`.

```
git submodule update --init
yarn install
hexo server
```

You can now access the blog server at (http://localhost:4000/).

## Adding a new post

To add a new post, use the following command:

```
hexo new post "I love blogging!" --authorId ande
```

## Deploying the blog

The blog is deployed to GitHub pages. Just run the following command to deploy the current version:

```
hexo deploy
```

**The blog will be deployed automatically when pushing to `master` branch so there is generally no need to deploy manually.**
