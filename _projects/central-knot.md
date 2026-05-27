---
layout: post
title: Central Knot
excerpt_separator: <!--excerpt-end-->
---

<div class="muted">
    HTTP BitTorrent tracker.
</div>
<!--excerpt-end-->

# Central Knot
---
Codeberg Repo: [Central Knot](https://codeberg.org/efournierrobert/central-knot)

BitTorrent protocol: [Back to basics: BitTorrent](/2026/05/07/torrent.html)

---
Central Knot is a HTTP tracker for the BitTorrent protocol. It follows
the specifications described in [BEP 3](https://bittorrent.org/beps/bep_0003.html) and [BEP 23](https://bittorrent.org/beps/bep_0023.html) of the protocol.

The tracker exposes the endpoint `/announce` on the port 9000. This can be added to a list of
trackers for a torrent and it will start tracking the swarm. This was tested with the [qBittorrent](https://www.qbittorrent.org/) client and will work when downloading a torrent with it, but any client that respects the specifications should work out of the box.
