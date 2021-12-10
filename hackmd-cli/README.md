# HackMD CLI

[![Docker Repository on Quay](https://quay.io/repository/komish/hackmd-cli/status "Docker Repository on Quay")](https://quay.io/repository/komish/hackmd-cli)

This is the commandline interface for interacting with HackMD at
https://hackmd.io.

This Containerfile packages up the CLI for execution as a container,
for folks who may not have any NPM toolchain on their workstation.

Upstream: https://github.com/hackmdio/hackmd-cli

## Building

```
containertool=podman
$containertool build -t hackmd-cli:latest -f Containerfile .
```

Swap out any configuration such as `containertool` or the image path as necessary.

## Running

The container runtime command looks something like this:

```
$containertool run --rm -v /home/yourusername/.config/hackmd:/opt/app-root/src/.hackmd:z  hackmd-cli:latest
```

The mounted volume allows for `hackmd-cli` to store authentication cookies on your host across executions.
Swap out your username or desired path as you see fit.

You can run this as an alias.

```
alias hackmd-cli="$containertool run --rm -v /home/yourusername/.config/hackmd:/opt/app-root/src/.hackmd:z  hackmd-cli:latest"
```

For importing files using the STDIN, you'll need the interactive mode enabled using the `-i` flag. For this
reason, we suggest two aliases.

```
alias hackmd-cli-import="$containertool run -i --rm -v /home/yourusername/.config/hackmd:/opt/app-root/src/.hackmd:z  hackmd-cli:latest"
```

## Samples

```
hackmd-cli login --id yourusername@example.com
<password prompt>

hackmd-cli whoami
<You are logged in hackmd.io as {YOUR NAME} [user-id]>

hackmd-cli list
<your notes>

cat /path/to/note/on/host.md | hackmd-cli-import
<Your note is available at https://hackmd.io/note-url>
```

## Known Issues

Due to the usage of this tool as a container, the `hackmd-cli import` function does not
work out of the box. References to note paths used in `hackmd-cli import` are local paths
to the container, and not the host.

To workaround this, you could mount your local note path on your filesystem to a path within
the container using the `-v` flag to your container tool. Alternatively, utilize the piping
approach described in the samples.

## Public Image

I make no express guarantees as to the availability or updating of this container image. Use at
your own risk.

https://quay.io/komish/hackmd-cli
