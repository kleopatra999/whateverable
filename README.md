# bisectbot
IRC bot for a lightning fast git bisect

This bot runs as ``bisectable`` on ``#perl6``.
Currently ``AlexDaniel`` is maintaining it.

## Usage examples
```
<AlexDaniel> bisect: exit 1 if (^∞).grep({ last })[5] // 0 == 4 # RT 128181
<bisectable> AlexDaniel: (2016-03-18) https://github.com/rakudo/rakudo/commit/6d120ca
```

Garbage in, rainbows out. Attempts to guess what you have meant:
```
<AlexDaniel> say (^∞).grep({ last })[5] # same but without proper exit codes
<bisectable> AlexDaniel: exit code is 0 on both starting points, bisecting by using the output
<bisectable> AlexDaniel: (2016-03-18) https://github.com/rakudo/rakudo/commit/6d120ca
```

```
<AlexDaniel> bisect: class A { has $.wut = [] }; my $a = A.new; $a.wut = [1,2,3]
<bisectable> AlexDaniel: exit code on a “good” revision is 1 (which is bad), bisecting with inverted logic
<bisectable> AlexDaniel: (2016-03-02) https://github.com/rakudo/rakudo/commit/fdd37a9
```

```
<AlexDaniel> bisect: exit 42
<bisectable> AlexDaniel: on both starting points the exit code is 42 and the output is identical as well
```

You can use ``␤`` characters instead of newlines:
```
<AlexDaniel> bisect: # newline test␤exit 42
<bisectable> AlexDaniel: on both starting points the exit code is 42 and the output is identical as well
```

It also supports URLs, but note that you have to provide a direct link to the “raw” version:
```
<AlexDaniel> bisectable: https://gist.githubusercontent.com/atweiden/9d1dfe825ade18a7db54d8e0733ca2e4/raw/16b7c39cfd12fef6eb74851c872097e0c655cff3/pkginfo.p6
<bisectable> successfully fetched the code from the provided URL
<bisectable> exit code is 1 on both starting points, bisecting by using the output
<bisectable> AlexDaniel: (2016-02-18) https://github.com/rakudo/rakudo/commit/9983c2c
```

More examples:
```
<moritz> bisect: try { NaN.Rat == NaN; exit 0 }; exit 1
<bisectable> moritz: (2016-05-02) https://github.com/rakudo/rakudo/commit/e2f1fa7
```

```
<AlexDaniel> bisect: for ‘q b c d’.words -> $a, $b { }; CATCH { exit 0 }; exit 1
<bisectable> AlexDaniel: (2016-03-01) https://github.com/rakudo/rakudo/commit/1b6c901
```

```
<AlexDaniel> bisectable: help
<bisectable> AlexDaniel: Like this: bisect: good=2015.12 bad=HEAD exit 1 if (^∞).grep({ last })[5] // 0 == 4 # RT 128181
```

```
<AlexDaniel> bisect: good=2016.03 bad 2016.02 say (^∞).grep({ last })[5] # swapped good and bad revisions
<bisectable> AlexDaniel: exit code is 0 on both starting points, bisecting by using the output
<bisectable> AlexDaniel: “bisect run” failure
```

```
<AlexDaniel> bisectable: http://github.org/sntoheausnteoahuseoau
<bisectable> AlexDaniel: it looks like an URL but for some reason I cannot download it (HTTP status-code is 404)
```

```
<AlexDaniel> bisect: https://gist.github.com/atweiden/9d1dfe825ade18a7db54d8e0733ca2e4
<bisectable> AlexDaniel: it looks like an URL, but mime type is “text/html; charset=utf-8” while I was expecting “text/plain; charset=utf-8”. I can only understand raw links, sorry.
```


Defaults to ``good=2015.12`` and ``bad=HEAD``.

# commitbot
IRC bot to run code at a given commit of Rakudo

This bot runs as ``committable`` on ``#perl6-dev``.
Currently ``AlexDaniel`` and ``MasterDuke`` are maintaining it.

## Usage examples
```
<MasterDuke> committable: f583f22 say $*PERL.compiler.version
<committable> MasterDuke: v2016.06.183.gf.583.f.22
```

## Installation
Run ``new-commits`` script periodically to process new commits.
Basically, that's it.

Some of these scripts are sensitive to the current working directory.
Use with care.
