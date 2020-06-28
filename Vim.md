## Vim navigation

- `<c-b>`: page up
- `<c-f>`: page down
- `<c-o>`: previous location
- `<c-i>`: next location


## scrollbind

When enabled, make each window in Vim scroll simultaneously.

`:set scrollbind`

`:set noscrollbind`

toggle the option with:

`:set scb!`

## Ranges:

Certain commands allow a range in the form

```
<start address><separator><end address>
```

The range is always placed before the command


### Separator

When separator is `;` the cursor position will be set to that line
before interpreting the next line specifier.  This doesn't happen for `,`.


### Aliases

- `1` is the first line
- `$` is the last line
- `.` is the current line (default except for a few commands like :write and :global which have the whole file as default range
- `%` is the whole file (short for 1,$)

### adresses format

- a number (inclusive)
- a pattern
  - `?pattern?` searches backwards
  - /pattern/ searches forwards
- a mark
- `\/`		the next line where the previously used search pattern matches
- `\?`		the previous line where the previously used search pattern matches
- `\&`		the next line where the previously used substitute pattern matches

You can add and subtract lines count from either the start of the end of the range simply adding -n or +n

Pattern can be preceded with another address (number, pattern, ...) and search will begin from here.

### Tips

If you type a number before the colon beginning a command, vim will transform it to a range containing this number of lines from current line 

For example, `5:`, will be transformed into `:.,.+4`


Some commands work on the whole file when you do not specify a range.  To make
them work on the current line explicitly use the "." address

For example:

```vimscript
:.write otherfile
```

### visual mode

If you select text with Visual mode and  you then press ":" to start a colon command, you will see this:

`:'<,'>`

The '< and '> are marks, placed at the start and end of the Visual selection and they remain at their position until another Visual selection is made

## search

`/some_pattern<CR>`

Hitting `<CR>` exits search mode

refining the 

- `/` followed by the up arrow allowing refinements to the search.

`<C-g>`, `<C-t>`
- jump to the next occurrence of the current pattern while focus is still in the search box.
