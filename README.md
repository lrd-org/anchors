# anchors

An append-only integrity log.

Some repositories of this organization are private, and their history is promised to be append-only. Each line of `anchors.log` attests: *at this time, this repository's `main` branch pointed at this commit.*

Line format:

```
<UTC time, ISO 8601>  <SHA-256 of the repository's full name, e.g. sha256("lrd-org/example")>  <git commit SHA of main's HEAD>
```

Repository names are hashed so that this log discloses nothing about private repository structure. Anyone who knows a repository's name can compute its hash and verify its entries; inside the organization, verification means checking that every anchored commit is still reachable from `main`'s history (`git merge-base --is-ancestor <anchored-sha> main`).

One honest caveat: this log is operated by the same organization it checks. Its protection is public visibility — clones, caches, and observers make silent rewriting hard to hide — not independence. Stronger anchoring (for example, OpenTimestamps) may be added later.
