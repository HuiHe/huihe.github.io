# A Developer's Blog

This is my personal blog using hexo hosted on github. [It was migrated from Ghost](source/_posts/migrate-ghost-to-hexo.md)

## How to write

```
$ yarn hexo new [layout] <title>
```

post is the default layout, but you can supply your own. You can change the default layout by editing the default_layout setting in \_config.yml.

## Generate local static files

```
$ yarn generate
```

## How to deploy

```
$ yarn deploy
```

I'm using hexo-deployer-git, check the deploy section in \_config.yml
