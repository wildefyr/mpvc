# 🎧 mpvc

![GitHub](https://img.shields.io/github/license/lwilletts/mpvc)
![GitHub Release Date](https://img.shields.io/github/release-date/lwilletts/mpvc)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/lwilletts/mpvc)
![GitHub top language](https://img.shields.io/github/languages/top/lwilletts/mpvc)
![GitHub lines of Code](https://sloc.xyz/github/lwilletts/mpvc/?category=code)

Music player in POSIX-sh interfacing mpv from the shell + extras/goodies [^install] 🚀.

A fork of [lwillets/mpvc](https://github.com/lwilletts/mpvc) evolving on its own adding features such as: improved interfaces to CLI, TUI, FZF, WEB, EQZ, & play streaming services as YouTube/Invidious.
For more on the features of this fork check: [Git](#git) QuickStart, [Wiki](../../wiki), [LogBook](../../wiki#logbook) & [Casts](../../wiki#screencasts).

⏩ Skip directly to [Installation](#Installation) to try mpvc!

<details open>
<summary>mpvc-tui -T: running the mpvc TUI <i>(click to view screenshot)</i></summary>

![mpvc-tui -T screenshot](../../blob/master/docs/assets/mpvc-tui.png)
</details>

<details>
<summary>mpvc-fzf -f: running with fzf to manage the playlist <i>(click to view screenshot)</i></summary>

![mpvc-fzf screenshot](../../blob/master/docs/assets/mpvc-tui-arch.png)
</details>

<details>
<summary>mpvc-tui -n: running with mpvc-fzf and desktop notifications on the upper-right corner <i>(click to view screenshot)</i></summary>

![mpvc tui+fzf+notifications screenshot](../../blob/master/docs/assets/mpvc-tui-fzf.png)
</details>

## ▶️ Overview [^install]

[mpvc](../../) is a collection of POSIX shell scripts:

- [mpvc](../../blob/master/mpvc): provides the core CLI commands to control mpv
- [extras/mpvc-tui](../../blob/master/extras/mpvc-tui): provides a console TUI, using mpvc underneath
- [extras/mpvc-fzf](../../blob/master/extras/mpvc-fzf): provides FZF integration to mpvc.
- [extras/mpvc-web](../../blob/master/extras/mpvc-web): a hack to remotely control mpvc from web (handy on mobile)
- [extras/mpvc-mpris](../../blob/master/extras/mpvc-mpris): speaks MPRIS to control mpv player through key-bindings.
- [extras/mpvc-equalizer](../../blob/master/extras/mpvc-equalizer): provides a basic mpv equalizer for the CLI.
- [extras/mpvc-autostart](../../blob/master/extras/mpvc-autostart): automatic mpv start/stop based on presence.
- [extras/mpvc-installer](../../blob/master/extras/mpvc-installer): provides an installer to install/update mpvc.

For more details on how to use the above tools have a look at the [Git](#git) QuickStart Guide, [LogBook](../../wiki#logbook).
In addition, the [casts/](../../wiki#screencasts) directory to shows some screencasts of mpvc in action.

## Requirements

Required:
- `sh`: a POSIX compliant shell (`/bin/sh` works)
- `mpv`: the mpv media player (see https://mpv.io)
- `socat`: is preferred due to the differing implementations of `netcat` across UNIXes.
- `awk`: a sane version of `awk` for the same reason (GNU/BSD `awk` works)

Recommended extras:

- `curl`
- `fzf`
- `jq`
- `notify-send`
- `yt-dlp`

## Installation

- [Manual](#manual)
- [Git](#git)
- [Debian](#debian)
- [Arch](#arch-mpvc-git)
- [BSD](#bsd)
- [MacOS](#macos)
- [Gentoo](#gentoo-mpvc)
- [Nix](#nix-mpvc)

Installing is just a matter of fetching the scripts either via [Git](#git)/Curl/etc., scripts can be used directly from the repo, the `mpvc-installer` bit is just there for easiness, to fetch & link them into your `BINDIR=~/bin/` that [mpvc-installer](../../blob/master/extras/mpvc-installer) does by default.

The easiest for a onetime install is the [Manual](#manual), however for @latest version a [Git](#git) install is recommended.
Remember to check your installation for missing dependencies/requirements using `mpvc-installer check-reqs`, and, if you encounter any issue file an [Issue](../../issues).

### Manual

```console
curl -LO https://github.com/lwilletts/mpvc/raw/master/extras/mpvc-installer \
  && BINDIR=$HOME/bin sh ./mpvc-installer fetch-user
```

### Git

Below is a **Quick Start** guide showcasing mpvc git install and usage.
This does git clone, and symlinks the mpvc scripts to `BINDIR` (default `~/bin`), so updating becomes a matter of just running `git pull`.

```sh
 # fetch a local copy of the github repo
 git clone https://github.com/lwilletts/mpvc/
 # use extras/mpvc-installer: just copy/link to BINDIR=$HOME/bin (by default)
 (cd mpvc; extras/mpvc-installer link-user)
 (cd mpvc; extras/mpvc-installer check-reqs)

 # use mpvc to add/load/save media files or online YT URLs
 mpvc add /path/to/your/*.mp3 # or your URLs
 find . -type f -name | mpvc load
 mpvc save my-playlist

 # use mpvc stash to store/recover current mpv state (see the logbook for more)
 mpvc stash ls
 mpvc stash push current
 mpvc stash apply current

 # use mpvc-fzf to manage mpvc stash (see mpvc-fzf -h for more)
 mpvc-fzf -a
 # use mpvc-fzf to search and play youtube media
 mpvc-fzf -p 'kupla mirage'
 # use mpvc-fzf to browse & play lofi girl music
 mpvc-fzf -b https://lofigirl.com/wp-content/uploads/2023/06
 # use mpvc-fzf to manage the playlist
 mpvc-fzf -f
 # use mpvc-tui to start the tui + desktop notifications
 mpvc-tui -T
```

For more  check the  [LogBook](../../wiki#logbook) (remeber your best chance is to try, play, and have fun).

### Debian

Debian (and APT derivatives such as Ubuntu):

```console
apt install mpv gawk curl socat fzf rlwrap jq libnotify-bin
```

### Arch [mpvc-git](https://aur.archlinux.org/packages/mpvc-git)

Arch (and derivatives):

```console
pacaur -y mpvc-git
pacman -Sy mpv gawk curl socat fzf rlwrap jq libnotify
````

### BSD

BSD (and pkg(1) based derivatives as FreeBSD, see [FAQ](../../wiki/FAQ)):

```console
pkg install -y mpv curl socat fzf rlwrap jq libnotify # mpv-mpris
```

### MacOS

MacOS (and brew(1) based derivatives see [FAQ](../../wiki/FAQ)):

```console
brew install mpv curl socat fzf rlwrap jq libnotify yt-dlp
```

### Gentoo [mpvc](https://gitlab.com/xy2_/osman)

```console
emerge mpvc
```

### Nix [mpvc](https://github.com/NixOS/nixpkgs/blob/master/pkgs/by-name/mp/mpvc/)

```console
nix-env -i mpvc
```

## Usage

### mpvc

```console
usage: mpvc opts # @version v1.6 (c) gmt4 https://github.com/gmt4/mpvc
 -a | --add | add         : Add media to playlist (see --load for stdin).
 -r | --remove | rm       : Remove media by id from playlist (see searchrm for rm by title)
 -s | --stop | stop       : Always stop playback.
 -P | --play | play       : Always start playback.
 -p | --toggle            : Toggle playback.
    | --next              : Jump to next entry in the playlist
    | --prev              : Jump to previous entry in the playlist
 -i | --playlist          : Print filenames of tracks to fit within terminal.
 -I | --fullplaylist      : Print all filenames of tracks in current playlist.
 -v | --vol               : Increase/decrease volume relative to current volume.
 -h | --help              : Prints the short help.
 -H | --help-long         : Prints the long help.
*tips: If unsure about where to begin, have a look at https://gmt4.github.io/mpvc
```

### mpvc-tui

```console
usage: mpvc-tui opts # @version v1.6 (c) gmt4 https://github.com/gmt4/mpvc
 -d|dir     : Set the WD to the media directory given as argument
 -n|notify  : Desktop notification using notify on mpvc events (notify-send*)
 -s|suggest : Suggest a random media to play based on previous media played
 -S|scrobler: Starts the mpvc-tui scrobbler
 -H|history : Starts the mpvc-tui history
 -t|tui     : Starts the mpvc-tui to manage the mpv playlist (rlwrap*)
 -T|Tui     : Combo that starts mpvc-tui -t -n, and adds media given as args
 -x|launch  : Starts mpvc-tui in a new xterm ($MPVC_TUI_TERM) # combine with <opts>
 -v|version : Prints the mpvc-tui version.
*tips: If unsure about where to begin, start with: mpvc-tui -d /path/to/media/ -T
````

### mpvc-fzf

```console
usage: mpvc-fzf opts # @version v1.6 (c) gmt4 https://github.com/gmt4/mpvc
 -b|browse   : Browse the provided ytdl-archive URL with fzf
 -c|chapters : Start fzf to manage the current mpv chapterlist
 -d|dir      : Set the WD to the media directory given as argument
 -e|eqz      : Start fzf to manage the equalizer settings
 -f|playlist : Start fzf to manage the current mpv playist
 -g|fetch    : Fetch the given YT URL, and store locally
 -G|Fetch    : Search on Invidious, fetch, and store locally
 -i|lyrics   : Search given media lyrics on Invidious
 -k|dplay    : Search & play DuckDuckGo videos
 -K|dsearch  : Search DuckDuckGo videos
 -l|local    : Search & play local media
 -s|search   : Search on Invidious
 -p|splay    : Search & play media found using Invidious
 -y|related  : Search related media on Invidious
 -Y|Related  : Search & play related media using Invidious
 -x|launch   : Starts mpvc-fzf in a new xterm (config $MPVC_TERM) [combine -x with other opts]
 -v|version  : Return the mpvc-fzf version.
 now         : Return a shareable URL to the now listening playlist
 lofi        : Search & play Lo-Fi channels
 somafm      : Search & play SomaFM channels
 radioapi    : Search & play Radio-Browser API channels
*tips: If unsure about where to begin, start: mpvc-fzf -p 'kupla mirage'
```

[^install]: Skip directly to [Installation](#Installation) to try mpvc

