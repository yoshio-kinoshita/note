# jenkins$B$G(BthinBackup$B%W%i%0%$%s$r;n$7$F$_$k(B
jenkins$B$G$I$N$h$&$K%P%C%/%"%C%W<h$k$N$,3Z$+$rD4$Y$F$_$^$7$?!#(B

$B>r7o$H$7$F(B

* $B%9%1%8%e!<%k$G%P%C%/%"%C%W(B
* $B%j%9%H%"4JC1!#(B
* $B%P%C%/%"%C%WBP>]$O@_Dj$@$1!#%j%=!<%9$O$$$i$J$$!#(B

$B$G$9!#(Bbackup$B%W%i%0%$%s$,$"$C$?$N$G$9$,!"$=$l$G$O%9%1%8%e!<%j%s%0$G$-$:!#(Bant$B$@$H%j%9%H%"4JC1$H$O8@$($J$5$=$&$G$7$?!#(B
$B$G!"?'!9D4$Y$F$_$?$i(BthinBackup$B$H$$$&%W%i%0%$%s$rH/8+!#NI$5$=$&$J$N$G;n$7$F$_$^$9!#(B

# thinBackup
$B%Z!<%8$O(B[$B$3$3(B](https://wiki.jenkins-ci.org/display/JENKINS/thinBackup)
$B%$%s%9%H!<%k$7$F!"%Q%i%a%?$r@_Dj$7$F$$$-$^$9!#(B

## Backup directory
jenkins$B%W%m%;%9$,FI$_=q$-$G$-$k%G%#%l%/%H%j$r;XDj$7$^$9!#(B

## Backup schedule for full backups
cron$B7A<0$G5-=R$7$^$9!#7n(B-$B6b$G(B12$B;~%P%C%/%"%C%W$K$7$^$9!#(B

    0 12 * * 1-5

## Backup schedule for differential backups
$B:9J,%P%C%/%"%C%W$G$9!#;H$o$J$$$N$G2?$b=q$-$^$;$s!#(B

## Max number of backup sets
$B%P%C%/%"%C%W$r2?@$BeA0$^$GJ];}$9$k$+$G$9!#$J$s$H$J$/(B5$B$K$7$F$_$^$9!#(B

## Files excluded from backup (regular expression)
$B%P%C%/%"%C%WBP>]30!#(B

# $B<jF0$G%P%C%/%"%C%W(B
backup$B$r2!$;$P<jF0$G%P%C%/%"%C%W<h$l$^$9!#(B

# $B%j%9%H%"(B
$B%j%9%H%"%\%?%s$r2!$7$F%j%9%HBP>]$rA*$Y$P(Bok$B$G$9!#(B

# $B:G8e$K(B
$B%P%C%/%"%C%W!"%j%9%H%"$,3Z$K$G$-$k$N$GNI$$%W%i%0%$%s$@$H;W$$$^$9!#(B
$B$3$l$G2?$+$"$C$F$b@_Dj$OI|3h$G$-$^$9!#(B


