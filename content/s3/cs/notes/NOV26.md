[up](../index.md)

# Housekeeping

Due to power outages, project has been extended.

Normal due date Tuesday night (tomorrow)

Late submission Wednesday night.

No submissions for any points for any reason after Wednesday.

# Build the data path!

Before we can do that... 2 major things

Handout - puts RTL things from last class onto paper

single-cycle CPU

Fetch component feeds directly into Decode, into execute, to memory, to writeback.

This linear sequence happens entirely within a single clock cycle. This works because the input to fetch is stable, and therefore can propagate forwards up to the writeback. We stop after writeback so that the input to fetch does not change.

One at a time - building hardware for mips RTL

Registers are not needed for temporaries, except PC.

> Draw along with Phil! Moving to paper.
