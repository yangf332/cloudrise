SVN Command
===============

### Command
    svn checkout [path]
    svn add [file]
    svn commit -m '[commit]'       // svn ci
    svn update                     // svn up
    svn update -r 200 test.php
    svn lock -m '[lock message]' [path]
    svn unlock [path]
    svn status [path]              // svn st
    svn status -v [path]
    svn delete [path] -m '[delete message]'
    svn log [path]
    svn info [path]
    svn diff [path]
    svn diff -r m:n [path]
    svn merge -r m:n [path]
    svn help
    svn help ci
    svn list [path]                // svn ls
    svn mkdir [path]
    svn revert [path]
    svn resolved [path]
    


### 链接
    [SVN command](http://www.cnblogs.com/wblade/archive/2010/10/27/1862840.html "SVN command")
