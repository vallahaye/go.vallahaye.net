# modsite

Vanity URLs for my Go modules.

This repository contains the sources to build the static site hosted at [go.vallahaye.net](https://go.vallahaye.net/) using [Hugo](https://gohugo.io/). Most of the idea comes from [this awesome article](https://blog.jbowen.dev/2020/07/using-go-vanity-urls-with-hugo/) written by Jessica Bowen ([@nullvoidptr](https://github.com/nullvoidptr)).

## Getting started

[Install Devbox](https://www.jetify.com/devbox/docs/installing_devbox/) and launch the development environment:

```
$ devbox shell
```

Use the `hugo-new-module` helper script to add a new module to the site:

```
$ ./hugo-new-module foo github.com/example/foo
```

Run the following command to serve the site on localhost:

```
$ hugo server
...
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Merge on `main` branch to automatically build and deploy the site to [Cloudflare Pages](https://pages.cloudflare.com/).

## Modules archetype

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
| `module`  | **required** | The Go module import path.        |
| `import`  | **required** | The `go-import` meta tag content. |
| `source`  | *optional*   | The `go-source` meta tag content. |
| `repoURL` | **required** | The repository root URL.          |

Most of the values are automatically set by the `hugo-new-module` script but some may be missing (no `source` value with GitHub repositories) or invalid (invalid `import` value with GitLab subgroups).

## License

This project is licensed under the [MIT No Attribution License](https://opensource.org/licenses/MIT-0) (MIT-0).
