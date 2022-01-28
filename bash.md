# bash

For some examples see [powercontrol-client](https://github.com/s4b7r/powercontrol-client/blob/main/reset-clienstate.sh).

## Process substitution

https://tldp.org/LDP/abs/html/process-sub.html

```bash
cat $(./command)
```

Can also return file descriptors for stdin and stdout with `>(COMMAND)` and `<(COMMAND)`.

## tee

Can use `tee` to "multiplex" streams, see e.g. https://unix.stackexchange.com/a/47514

https://www.man7.org/linux/man-pages/man1/tee.1.html

## Everything except X "wildcard"

```bash
rm !(dontdeletethis.md)
```

https://www.putorius.net/run-rm-command-but-exclude-one-file.html
