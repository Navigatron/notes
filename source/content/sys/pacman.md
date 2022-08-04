pacman
-Q = query the database
-c = shows changelog of packages, if they exist.
-d = show installed as dependency. Combine with t to see deps with no parent
-e = explicitly installed packages. combine with -t for those with no need.
-g groupname = show packages in a group
-i = show info on packages printed.
-k = check = make sure that, the files a package says it owns, exist.
-l = list = show me the files this package owns
-m = foreign = packages that are here, but not in the syncdb
-n = native = they Dooo exist in the syncdb. Good job.
-o file = owns = gimme the pac responsible for this shit
-t = unrequired. Nobody needs this.
-u = upgrades = show me the ones that need to be updated.

What about removing those packs that I don't like?
-R = remove
-c = cascade = yeet everything that depends on this
-s = recursive = Yeet all things this depends on, as long as nobody else needs em
