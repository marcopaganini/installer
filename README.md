# A simple github releases installer.

This is a simple one-liner installer for github releases. It allows your users
to download and install the latest release of your program, for their specific
OS and architecture, with a simple command.

## Repository Setup

To use this program, your github releases should be named
`reponame-<OS>-<ARCH>.tar.gz` under your releases directory.  Note that OS and
ARCH are your OS name and Architecture name, respectively. This program uses
the Go standard names for OS and architecture (look at the source and it should
become very clear). For an example of how things should look, see this release
for another of my projects, [https://github.com/marcopaganini/termotp/releases/tag/v0.0.4].

Your distribution files must go in a directory named `<OS>-<ARCH>` inside the
tarfile. This directory must contains, beside all files necessary to run your
program, a shell script called `install.sh` that makes sure your program is
properly installed in `/usr/local/bin` for example.

You can see examples of this in action in another of my repositories: [termotp](https://github.com/marcopaganini/termotp).

## Usage

To use, direct your users to type one of the following commands (wget or curl):

wget:

```
wget -q -O/tmp/install \
  'https://raw.githubusercontent.com/YOUR-USER/YOUR-REPO/master/install.sh' && \
  sudo sh /tmp/install YOUR-USER/YOUR-REPO
```

curl:

```
curl -s \
  'https://raw.githubusercontent.com/YOUR-USER/YOUR-REPO/master/install.sh' >/tmp/install && \
  sudo sh /tmp/install YOUR-USER/YOUR-REPO
```

The commands above can be copied into a single line, naturally.

## Restrictions

Many. This is simple program in shell that I moved to this repo, since I kept different versions
of it inside my personal projects. Some notables issues.

- The program requires your release tarballs to have the same name as your repository.
- The program uses Go's OS and Architecture names (see Appendix for an example).
- The shell does some very basic heuristics to translate the output of `uname -m` and
  `uname -o` to Go's OS and architecture names. Feel free to email me if you find errors there.
- There's no provision to uninstall things. An easy way would be to include an "uninstall"
  program with your distribution, like "uninstall-yourrepo.sh" that would be copied
  to `/usr/local/bin` (by default) during installation.

## Appendix

Go OS and Architecture names:

```
aix/ppc64        freebsd/amd64   linux/mipsle   openbsd/386
android/386      freebsd/arm     linux/ppc64    openbsd/amd64
android/amd64    illumos/amd64   linux/ppc64le  openbsd/arm
android/arm      js/wasm         linux/s390x    openbsd/arm64
android/arm64    linux/386       nacl/386       plan9/386
darwin/386       linux/amd64     nacl/amd64p32  plan9/amd64
darwin/amd64     linux/arm       nacl/arm       plan9/arm
darwin/arm       linux/arm64     netbsd/386     solaris/amd64
darwin/arm64     linux/mips      netbsd/amd64   windows/386
dragonfly/amd64  linux/mips64    netbsd/arm     windows/amd64
freebsd/386      linux/mips64le  netbsd/arm64   windows/arm
```
