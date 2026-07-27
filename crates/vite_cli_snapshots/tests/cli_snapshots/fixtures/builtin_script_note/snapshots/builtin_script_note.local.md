# builtin_script_note

## `vp dev --port 12312312312`

`vp dev` points at the `dev` script (invalid port exits the server immediately)

**Exit code:** 1

```
note: You are running `vp dev` as a Vite+ built-in command. If you meant to run the dev npm script, use `vpr dev` instead.
error when starting dev server:
Error: No available ports found between 12312312312 and 65535
```

## `vp lint src/`

every built-in that can be mistaken for a script gets the same note

```
note: You are running `vp lint` as a Vite+ built-in command. If you meant to run the lint npm script, use `vpr lint` instead.
Found 0 warnings and 0 errors.
Finished in <duration> on 1 file with <n> rules using <n> threads.
```

## `cd src && vp lint .`

note reaches the enclosing package from a subdirectory, like `vpr` does

```
note: You are running `vp lint` as a Vite+ built-in command. If you meant to run the lint npm script, use `vpr lint` instead.
Found 0 warnings and 0 errors.
Finished in <duration> on 1 file with <n> rules using <n> threads.
```

## `vp format src/`

the `format` alias reaches the local CLI as typed, so its own script gets the note

```
note: You are running `vp format` as a Vite+ built-in command. If you meant to run the format npm script, use `vpr format` instead.
Finished in <duration> on 1 files using <n> threads.
```

## `vp fmt src/`

no note: only `format` is a script here, and that is not the name this ran under

```
Finished in <duration> on 1 files using <n> threads.
```

## `vp help dev`

no note: a help request runs nothing, and reaches the local CLI as `dev --help`

```
vp/<version>

Usage:
  $ vp [root]

Commands:
  [root]           start dev server
  build [root]     build for production
  optimize [root]  pre-bundle dependencies (deprecated, the pre-bundle process runs automatically and does not need to be called)
  preview [root]   locally preview production build

For more info, run any command with the `--help` flag:
  $ vp --help
  $ vp build --help
  $ vp optimize --help
  $ vp preview --help

Options:
  --host [host]            [string] specify hostname
  --port <port>            [number] specify port
  --open [path]            [boolean | string] open browser on startup
  --cors                   [boolean] enable CORS
  --strictPort             [boolean] exit if specified port is already in use
  --force                  [boolean] force the optimizer to ignore the cache and re-bundle
  --experimentalBundle     [boolean] use experimental full bundle mode (this is highly experimental)
  -c, --config <file>      [string] use specified config file
  --base <path>            [string] public base path (default: /)
  -l, --logLevel <level>   [string] info | warn | error | silent
  --clearScreen            [boolean] allow/disable clear screen when logging
  --configLoader <loader>  [string] use 'bundle' to bundle the config with Rolldown, or 'runner' (experimental) to process it on the fly, or 'native' (experimental) to load using the native runtime (default: bundle)
  -d, --debug [feat]       [string | boolean] show debug logs
  -f, --filter <filter>    [string] filter debug logs
  -m, --mode <mode>        [string] set env mode
  -h, --help               Display this message
  -v, --version            Display version number
```

## `vp preview --port 12312312312`

no note: this project has no `preview` script

**Exit code:** 1

```
error when starting preview server:
Error: No available ports found between 12312312312 and 65535
```

## `vp lint src/`

the note still reaches piped output, such as an AI agent capturing the command; it goes to stderr, so parsed stdout stays intact

```
Found 0 warnings and 0 errors.
Finished in <duration> on 1 file with <n> rules using <n> threads.
[1m[2mnote:[0m[0m You are running [94m`vp lint`[39m as a Vite+ built-in command. If you meant to run the lint npm script, use [94m`vpr lint`[39m instead.
```
