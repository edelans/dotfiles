# dotfiles
A repo to share and keep my dotfiles versioned somwhere

# How it works
see http://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html for full source.

Abstract here :

- create the ${HOME}/dotfiles directory 
- inside it make subdirectories for all the programs whose cofigurations you want to manage. 
- Inside each of those directories, move in all the appropriate files, maintaining the directory structure of your home directory. So, if a file normally resides at the top level of your home directory, it would go into the top level of the program's subdirectory. If a file normally goes in the default ${XDG_CONFIG_HOME}/${PKGNAME} location (${HOME}/.config/${PKGNAME}), then it would instead go in ${HOME}/dotfiles/${PKGNAME}/.config/${PKGNAME} and so on. 
- Finally, from the dotfiles directory, you just run $ stow $PKGNAME and Stow will symlink all the package's configuration files to the appropriate locations. 


For example, let's say you want to manage the configuration for Bash, VIM and Uzbl. Bash has a couple files in the top-level directory; VIM typically has your .vimrc file on the top-level and a .vim directory; and Uzbl has files in ${XDG_CONFIG_HOME}/uzbl and ${XDG_DATA_HOME}/uzbl. So, your home directory looks like this:

```
home/
    brandon/
        .config/
            uzbl/
                [...some files]
        .local/
            share/
                uzbl/
                    [...some files]
        .vim/
            [...some files]
        .bashrc
        .bash_profile
        .bash_logout
        .vimrc
```
You would then create a dotfiles subdirectory and move all the files there:

```
home/
    /brandon/
        .config/
        .local/
            .share/
        dotfiles/
            bash/
                .bashrc
                .bash_profile
                .bash_logout
            uzbl/
                .config/
                    uzbl/
                        [...some files]
                .local/
                    share/
                        uzbl/
                            [...some files]
            vim/
                .vim/
                    [...some files]
                .vimrc
```
Then, perform the following commands:

```
$ cd ~/dotfiles
$ stow bash
$ stow uzbl
$ stow vim
```

And, voila, all your config files (well, symbolic links to them) are all in the correct place, however disorganized that might be, while the actual files are all neatly organized in your dotfiles directory, which is easily turned into a VCS repo. 

One handy thing is that if you use multiple computers, which may not have the same software installed on them, you can pick and choose which configurations to install when you need them. All of your dotfiles are always available in your dotfiles directory, but if you don't need the configuration for one program, you simply don't Stow it and thus it does not clutter your home directory.

