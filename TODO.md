# TODO

The m68k module works with the binary I have, but has issues that
someone (maybe even me) should fix. The information below was gleaned
from @rss in binja's slack

June 26, 2019:

```rss [11:56 AM]```

okay, I see a couple of problems that are easy to fix. indirect branches should be reported as `UnresolvedBranch` in `get_instruction_info`, and the code for `jmp` and `bra` should check for a label at the destination (and use `il.goto` if it exists) before using `il.jump` as a fallback.

@Jason Wright here's an example of unconditional branch lifted ideally: [clipper.py:440](https://github.com/pmackinlay/binaryninja-clipper/blob/master/clipper.py#L440)

and for `get_instruction_info`:
[clipper.py:1176](https://github.com/pmackinlay/binaryninja-clipper/blob/master/clipper.py#L1176)

NOTE: the il.goto/il.jump using labels is done, but the UnresolvedBranch
comment has not been dealt with.
