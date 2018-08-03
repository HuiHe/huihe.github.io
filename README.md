# blog-hexo

This is my personal blog using hexo hosted on github. [It was migrated from Ghost](source/_posts/migrate-ghost-to-hexo.md)

## How to write

https://hexo.io/docs/writing

```
$ hexo new [layout] <title>
```

post is the default layout, but you can supply your own. You can change the default layout by editing the default_layout setting in \_config.yml.

## Generating

```
$ hexo generate
```

Generating static files

## How to deploy

https://hexo.io/docs/deployment

```
$ hexo deploy
```

I'm using hexo-deployer-git, check the deploy section in \_config.yml

## Deploy After Generating

To deploy after generating, you can run one of the following commands. There is no difference between the two.

```
$ hexo generate --deploy
$ hexo deploy --generate
```
