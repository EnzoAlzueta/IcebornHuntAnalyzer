# Roadmap

## First milestone: safe archive reader, then a small desktop browser

This project can advance immediately, independently of the common runtime.
Input is nativePC/plugins/iceborne_damage_meter_hunts.bin, IDMHARC1, produced by
the meter from 0.6.12. Read [the hunt archive specification](https://github.com/EnzoAlzueta/IcebornDamageMeter/blob/main/docs/HUNT-ARCHIVE.md)
and its checksum record. Do not alter the meter to simplify the analyzer.

1. Choose the smallest suitable Windows desktop implementation after documenting
   startup/memory/distribution tradeoffs. Do not add a game plugin, web service,
   network upload, always-running monitor or an install-time runtime dependency
   without first assessing portable distribution options.
2. Build a bounded streaming decoder with header/schema/build/length/CRC checks,
   correct UTF-16LE, empty slots, partial observations and damaged input handling.
   Create synthetic golden fixtures and compare with the meter codec fixtures.
3. Treat the input as read-only even when corrupt. A writer may append while it
   is open: read only complete verified frames and tolerate an incomplete tail.
   Distinguish corruption from a file still being written. Do not repair it.
4. MVP UI: choose archive, hunt list, selected hunt details and date/quest/weapon
   filters. Keep the interface responsive for 1k/10k/100k synthetic hunts. Use
   streaming/paging and, if warranted, an external cache/index in your own folder.
5. Later milestone: personal trends and comparable-weapon views. No universal
   weapon tier list from biased local hunts, invented build/monster metadata or
   global player identity inferred from transient IDs.

Use (damage - baselineDamage)/participation time for derived observed DPS, with
zero-time handling. Party size means peak simultaneous players, not nonempty
slots. Exclude/flag partial hunts, weapon changes and generic investigation ID
30000 for like-for-like comparisons. Never silently discard these records from
the basic browser. Old data discarded by the ten-hunt history is unrecoverable.

Complete with portable local artifact, decoder tests, large-file measurements,
data-limit explanations and clear English primary docs. No loader/SDK dependency.
Do not copy a real personal archive into source fixtures or publish player names.
