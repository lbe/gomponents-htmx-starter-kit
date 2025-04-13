# Work In Progress
I have been searching for a web application starting template based upon Go `stdlib` and `gomponents-htmx`.  The closest that I have found was [maragudk/gomponents-starter-kit](https://pkg.go.dev/github.com/maragudk/gomponents-starter-kit) which uses `chi` and several of maragudk's own development modules.  My goals for this repo are:

1. Replace `chi` with  `ServeMux`
2. Replace maragudk's custom models with `stdlib`
3. Add DaisyUI

## Motivation

In 2023, I experimented with writing data analysis applications in Go. Previously, For the two previous decades, I wrote these types of applications in Perl. Many dump on Perl because it is so expressive that one can write what looks like gibberish and it does what it was written to do. I was initially attracted to Perl because it is a simple garbage collected language with a batteries include stdlib. Sound familiar? Additionally, Perl has a rich set of publicly available modules on [CPAN](https://metacpan.org). Many of these contain C code that in turn make Perl much more performant that many scripted languages. Additionally, a primary focus of Perl from its start has been text processing.  Many of my data analysis applications consume unstructured text as their source.  So Perl has been a perfect fit.

I started the Go experiment in 2023 because I was reaching the performance limitations of what I could achieve in Perl without resorting to writing my Perl modules in C. My C skills were and are insufficient to do this and I did not want to spend the time required to address this problem. I spent a little time and evaluated compiled languages available with automated memory management. I excluded anything that required a separate virtual machine like Java's JVM or C#'s CLR. My short list was Go, Julia and Swift. After some quick and admittedly insufficent testing of the three, I selected Go.  I selected Go because I liked the simple language, rich stdlib and built-in concurrency. I found that i could approach the performance of C or Rust made possible by data found in Go's profiler `pprof`. Additionally, the development tools and experience were great!

My initial efforts were focused on the portions of my application that were performance related.  I have kept the web application for viewing and visualizing data in Perl. The Perl web application is built in HTMX using code to generate the HTML. I would not like to move this over to Go.

# gomponents-starter-kit

<img src="logo.png" alt="Logo" width="300" align="right">

[![GoDoc](https://pkg.go.dev/badge/github.com/maragudk/gomponents-starter-kit)](https://pkg.go.dev/github.com/maragudk/gomponents-starter-kit)
[![Go](https://github.com/maragudk/gomponents-starter-kit/actions/workflows/ci.yml/badge.svg)](https://github.com/maragudk/gomponents-starter-kit/actions/workflows/ci.yml)
[![Go](https://github.com/maragudk/gomponents-starter-kit/actions/workflows/cd.yml/badge.svg)](https://github.com/maragudk/gomponents-starter-kit/actions/workflows/cd.yml)

A starter kit for building a web app with gomponents, HTMX, and TailwindCSS in Go.

Made with ✨sparkles✨ by [maragu](https://www.maragu.dev/).

Does your company depend on this project? [Contact me at markus@maragu.dk](mailto:markus@maragu.dk?Subject=Supporting%20your%20project) to discuss options for a one-time or recurring invoice to ensure its continued thriving.

## Getting started

The easiest way to get started is to [Use this template](https://github.com/new?template_name=gomponents-starter-kit&template_owner=maragudk) to create a new repository. Or you could clone this repository the traditional way:

```shell
git clone git@github.com:maragudk/gomponents-starter-kit.git your-app-name
```

After that, you can start the app with:

```shell
make start
```

If you make style changes, watch the CSS with:

```shell
make watch-css
```

You can run tests and linting with:

```shell
make test lint
```

### Enabling TailwindCSS auto-complete in your IDE

[TailwindCSS has auto-complete of classnames (and more) through IDE plugins](https://tailwindcss.com/docs/editor-setup).

After you've installed the TailwindCSS plugin for your IDE, it needs some configuration to work with gomponents. Here's the config for VS Code and JetBrains IDEs:

<details>
<summary>VSCode</summary>

Edit `vscode-settings.json` and add the following:

```json
{
	"tailwindCSS.includeLanguages": {
		"go": "html",
	},
	"tailwindCSS.experimental.classRegex": [
		["Class(?:es)?[({]([^)}]*)[)}]", "[\"`]([^\"`]*)[\"`]"]
	],
}
```

[See the official plugin page for more info](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)
</details>

<details>
<summary>JetBrains/GoLand</summary>

Go to `Settings` -> `Languages & Frameworks` -> `Style Sheets` -> `Tailwind CSS` and add the following (don't delete the other config):

```json
{
	"includeLanguages": {
		"go": "html"
	},
	"experimental": {
		"classRegex": [
			["Class(?:es)?[({]([^)}]*)[)}]", "[\"`]([^\"`]*)[\"`]"]
		]
	}
}
```

[See the official plugin page for more info](https://plugins.jetbrains.com/plugin/15321-tailwind-css)
</details>

## Deploying

The [CD workflow](.github/workflows/cd.yml) automatically builds a multi-platform Docker image and pushes it to the Github container registry GHCR.io, tagged with the commit hash as well as `latest`.

You can try building the image locally with:

```shell
make build-docker
```

Note that [you need the containerd image store enabled](https://docs.docker.com/desktop/containerd/#enable-the-containerd-image-store) for this to work.
