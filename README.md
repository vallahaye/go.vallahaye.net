# Go import redirector

Vanity URLs for my Go modules.

This repository contains the sources to build the static site hosted at [go.vallahaye.net](https://go.vallahaye.net/) using [Hugo](https://gohugo.io/). Most of the idea comes from [this awesome article](https://blog.jbowen.dev/2020/07/using-go-vanity-urls-with-hugo/) written by Jessica Bowen ([@nullvoidptr](https://github.com/nullvoidptr)).

## Getting started

[Install Devbox](https://www.jetify.com/devbox/docs/installing_devbox/) and launch the development environment:

```
$ devbox shell
```

Use the `hugo-new-go-module` helper script to add a new Go module to the site:

```
$ ./hugo-new-go-module foo github.com/example/foo
```

Run the following command to serve the site on localhost:

```
$ hugo server
...
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Push on `main` to automatically build and deploy the site to [Cloudflare Pages](https://pages.cloudflare.com/).

## Go module archetype

```yaml
---
module: "go.example.com/foo"
import: "go.example.com/foo git https://github.com/example/foo.git"
source: "go.example.com/foo https://github.com/example/foo https://github.com/example/foo/tree/main{/dir} https://github.com/example/foo/blob/main{/dir}/{file}#L{line}"
repoURL: "https://github.com/example/foo"
---
```

| Key       | Required     | Description                       |
|:---------:|:------------:|-----------------------------------|
| `module`  | **Yes**      | The Go module import path.        |
| `import`  | **Yes**      | The `go-import` meta tag content. |
| `source`  | No           | The `go-source` meta tag content. |
| `repoURL` | **Yes**      | The repository root URL.          |

Most of the values are automatically set by the `hugo-new-go-module` helper script but some may be missing or invalid:

- No `source` value with GitHub repositories
- Bad `import` value with GitLab subgroups

## License

This project is licensed under the [MIT No Attribution License](https://opensource.org/licenses/MIT-0) (MIT-0).
