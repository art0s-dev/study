# Worktrees
Hast du dich jemals gefragt, wie man in Git "mal ebend schnell" zwischen branches wechseln kann oder unterschiedlichen
Versionsständen welchseln kann, ohne irdendwas zu stashen ohne "unschönheiten"?
Die Antwort heißt worktrees. Ich stelle das mal am besten schematisch dar:

hauptverzeichnis
- worktrees/branchB
- worktrees/branchA
- src/
- config/
- deineGanzenDateien/
- .gitignore

im ordner Worktrees/branchB findest du eine laufende Kopie des gesamten Repos mitsamt eines ausgechecktem branch.
Der Main bleibt unberührt und bekommt nur unterrepos, sodass man in den einzelnen ausgebranchten repos arbeiten kann.
Sobald das von erfolg gekrönt ist, kann man in das hauptrepo mergen und die änderungen aus den worktrees übernehmen (wenn mann denn will)

## So geht's

Füge ein worktree hinzu
`git worktree add nameDesOrdners/nameDesBranch`

Entferne ein worktree
`git worktree remove nameDesOrdners/nameDesBranch`

>Wichtig: Sobald die Worktrees gelöscht sind bleiben für den main
>die branches erhalten. Das heißt, ab und zu sollte man da nochmal 
>feucht durchwischen ;)
