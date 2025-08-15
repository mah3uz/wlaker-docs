---
title: Plugins
nextjs:
  metadata:
    title: Plugins
    description: Extend Walker with custom sources and actions using raw, JSON, or key–value parsers, plus output mode examples and Node helpers.
---

Plugins let you add custom sources and actions. Define them under `[[plugins]]` in your config.

## Fields

- name: module name shown in UI
- prefix: optional prefix to trigger this module
- src: command to produce entries (reads query from stdin unless `%TERM%` is in `src`)
- src_once: run once and cache output
- output: if true, show a single entry that displays the command output
- parser: `raw` | `json` | `kv` (defaults to `raw`)
- separator: column separator for `raw` (e.g., `;`)
- label_column / result_column: 1-based indices for raw columns
- kv_separator: default `;` for `kv` parser
- cmd / cmd_alt: activation commands; `%RESULT%` will be replaced with the selected value
- keywords: extra fuzzy triggers for output mode
- terminal: run in a terminal
- theme, theme_base, icon, weight, typeahead, history, etc. (general module fields)

## RAW parser example

```toml
[[plugins]]
name = "rg"
prefix = "rg "
src = 'rg --vimgrep --color=never "%TERM%"'
parser = "raw"
separator = ":"
# columns: file:line:col:text
label_column = 0  # text
result_column = 1 # file
cmd = 'xdg-open "%RESULT%"'
```

Input lines are URL-unescaped before labeling. `%TERM%` is replaced in `src`.

## JSON parser example

```toml
[[plugins]]
name = "notes"
prefix = "note "
src = 'jq -c ".[]" ~/notes/index.json'
parser = "json"
cmd = 'wl-copy "%RESULT%"'
```

`json` must output an array of entries matching Walker’s Entry shape: `{ label, sub?, exec?, exec_alt?, icon?, value?, categories?, matching? }`.

## KV parser example

```toml
[[plugins]]
name = "kv-ex"
src = 'some-cmd'
parser = "kv"
kv_separator = ";"
cmd = 'echo "%RESULT%" | wl-copy'
```

Each line has `key=value` pairs joined by `;`, e.g.: `label=Hello;value=Hello;icon=face-smile`.

## Output mode example

```toml
[[plugins]]
name = "sys"
src_once = 'uname -a'
output = true
cmd = 'wl-copy "%RESULT%"'
keywords = ["sys", "uname"]
```

Shows a single entry whose label is the captured output and copies it on activation.

## Node/JS helpers

Set `js_runtime = "node"` at the top level if you rely on Node-based scripts.

Here is a working example using `rink`:

```javascript
"use strict";
const os = require("os");

const args = process.argv.slice(2);
const term = args.join(" ");

if (term.length < 3) {
  console.log([]);
  return;
}

const { spawnSync } = require("child_process");
const { stderr } = require("process");
const ls = spawnSync("rink", [term]);

if (ls.stderr.toString() !== "") {
  return [{}];
}

const res = ls.stdout.toString();
const lines = res.split(os.EOL);

if (lines[1].includes("No such unit")) {
  console.log([]);
  return;
}

if (lines[1].includes("Expected")) {
  console.log([]);
  return;
}

console.log(
  JSON.stringify([
    {
      label: lines[1],
      sub: "rink",
      exec: `echo '${lines[1]}' | wl-copy`,
      class: "calc",
      matching: 1,
    },
  ]),
);
```

```bash
node assets/rink.example.plugin.cjs "2 m in cm"
```

Then wire it as a plugin using the `json` parser.

