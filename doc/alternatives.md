# Alternatives

The following table tries to give an overview *from `bat`s perspective*, i.e. we only compare
categories which are relevant for `bat`. Some of these projects have completely different goals and
if you are not looking for a program like `bat`, this comparison might not be for you.

|                                              | bat                                                                 | [pygments](http://pygments.org/) | [highlight](http://www.andre-simon.de/doku/highlight/highlight.php) | [ccat](https://github.com/jingweno/ccat) | [source-highlight](https://www.gnu.org/software/src-highlite/) | [hicat](https://github.com/rstacruz/hicat)          | [coderay](https://github.com/rubychan/coderay)      | [rouge](https://github.com/jneen/rouge)             | [clp](https://github.com/jpe90/clp)      |
|----------------------------------------------|---------------------------------------------------------------------|----------------------------------|---------------------------------------------------------------------|------------------------------------------|----------------------------------------------------------------|-----------------------------------------------------|-----------------------------------------------------|-----------------------------------------------------|-----------------------------------------------------|
| Drop-in `cat` replacement                    | :heavy_check_mark: [*](https://github.com/sharkdp/bat/issues/134)   | :x:                              | :x:                                                                 | (:heavy_check_mark:)                     | :x:                                                            | :x: [*](https://github.com/rstacruz/hicat/issues/6) | :x:                                                 | :x:                                                 | :x:                                                                 |
| Git integration                              | :heavy_check_mark:                                                  | :x:                              | :x:                                                                 | :x:                                      | :x:                                                            | :x:                                                 | :x:                                                 | :x:                                                 | :x:                                                                 |
| Automatic paging                             | :heavy_check_mark:                                                  | :x:                              | :x:                                                                 | :x:                                      | :x:                                                            | :heavy_check_mark:                                  | :x:                                                 | :x:                                                 | :x:                                                                 |
| Languages (circa)                            | 150                                                                 | 300                              | 200                                                                 | 7                                        | 80                                                             | 130                                                 | 30                                                  | 130                                                 | 150                                                 |
| Extensible (languages, themes)               | :heavy_check_mark:                                                  | (:heavy_check_mark:)             | (:heavy_check_mark:)                                                | :x:                                      | (:heavy_check_mark:)                                           | :x:                                                 | :x:                                                 | :x:                                                 | :heavy_check_mark:                                                 |
| Advanced highlighting (e.g. nested syntaxes) | :heavy_check_mark:                                                  | :heavy_check_mark:               | (:heavy_check_mark:) ?                                              | :x:                                      | :heavy_check_mark:                                             | :heavy_check_mark:                                  | :heavy_check_mark:                                  | :heavy_check_mark:                                  | :heavy_check_mark:                                  |
| Execution time [ms] (`jquery-3.3.1.js`)      | 422                                                                 | 455                              | 299                                                                 | 39                                       | 208                                                            | 287                                                 | 128                                                 | 740                                                 | 22                                          |
| Execution time [ms] (`miniz.c`)              | 27                                                                  | 169                              | 19                                                                  | 4                                        | 36                                                             | 131                                                 | 58                                                  | 231                                                 | 4                                          |
| Execution time [ms] (957 kB XML file)        | 215                                                                 | 296                              | 236                                                                 | 165                                      | 83                                                            | 412                                                 | 135                                                 | 386                                                 | 127                                          |

If you think that some entries in this table are outdated or wrong, please open a ticket or pull
request.

Some other alternatives that are also related, but not yet included in the table:
- [lesspipe](https://github.com/wofr06/lesspipe)
- [vimpager](https://github.com/rkitover/vimpager)

## Benchmarks

The benchmarks above have been created with this script:
```bash
#!/usr/bin/env bash

cd "$(dirname "${BASH_SOURCE[0]}")" || exit

if ! command -v hyperfine > /dev/null 2>&1; then
    echo "'hyperfine' does not seem to be installed."
    echo "You can get it here: https://github.com/sharkdp/hyperfine"
    exit 1
fi

SRC="test-src/jquery-3.3.1.js"


cmd_bat="bat --style=full --color=always --paging=never '$SRC'"
cmd_bat_simple="bat --plain --wrap=never --tabs=0 --color=always --paging=never '$SRC'"
cmd_pygmentize="pygmentize -g '$SRC'"
cmd_highlight="highlight -O truecolor '$SRC'"
cmd_ccat="ccat --color=always '$SRC'"
cmd_source_highlight="source-highlight --failsafe --infer-lang -f esc -i '$SRC'"
cmd_hicat="hicat '$SRC'"
cmd_coderay="coderay '$SRC'"
cmd_rouge="rougify '$SRC'"
cmd_clp="clp '$SRC'"

hyperfine --warmup 3 \
    "$cmd_bat" \
    "$cmd_bat_simple" \
    "$cmd_pygmentize" \
    "$cmd_highlight" \
    "$cmd_ccat" \
    "$cmd_source_highlight" \
    "$cmd_hicat" \
    "$cmd_coderay" \
    "$cmd_rouge" \
    "$cmd_clp" \
```
