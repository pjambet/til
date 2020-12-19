# GitInfo settings

Hugo has some internal tooling to pull some info from git, such as the lastmod date for a file:

https://gohugo.io/variables/git/

It turns out it was set in my netlify conf:

```
[context.production.environment]
HUGO_VERSION = "0.70.0"
HUGO_ENV = "production"
HUGO_ENABLEGITINFO = "true"
```
