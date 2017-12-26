# schist

![travis-ci](https://travis-ci.org/slyphon/schist.svg?branch=master)

Python script to backup shell (zsh, bash) history to a sqlite3 database via cron/launchd. Syncs, merges, and dedupes current state on each run.

## y tho

As my good friend and favorite debate partner [@bd][] asked:

<img src="https://raw.githubusercontent.com/slyphon/schist/_website/y-tho.jpg" width="50%" height="50%"/>

"shell history is precious but it's kept safe with normal backups."

I mean, sure, fair.

Back in 2013 when I switched to zsh with [oh-my-zsh][] I thought "You know what? I want all of my history!" and set `HISTSIZE` to a ludicrously large number: `1250000`. Turns out, 5 years later, this was causing my shell load times to take 7-8 seconds. This may not seem like a long time...nah, it's an eternity. After doing some experimentation, I figured out that my `.zsh_history` had grown to ~ 5.3 MB, and had roughly 120k entries in it. I could cut down `HISTSIZE`, but if you're like me, shell history is one of the critical tools for doing my job. Once I figure out a command, I want to be able to go back and find it, rather than have to dig through man pages again.

The solution: cut down on `HISTSIZE`, but back up the history file frequently, so that none of the commands that get pushed out of the file are lost.

I found a few different scripts to do this, but the one that I liked the most was based on `sqlite3`, which is included in python by default, and this is my vacation hackweek project: schist.

![galactic-brain][]


[@bd]: https://twitter.com/bd
[oh-my-zsh]: https://github.com/robbyrussell/oh-my-zsh
[galactic-brain]: https://raw.githubusercontent.com/slyphon/schist/_website/galactic-zsh-history.jpg

## Usage

Run a backup of shell history, (by default, writes the db at `~/.schist.sq3`)


```
# for zsh:

$ schist zsh backup

# for bash:

$ schist bash backup

```

Dump out the complete history in a shell compatible format with 'restore':


```
$ schist zsh restore -
```

Show some stats on the last backup time, and the number of commands over the past hour, day, and week.

```
$ schist zsh stats
```
