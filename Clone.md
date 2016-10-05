


git clone <url>

But To Install Submodules (which should be usually the case)

* With Version 1.9 of Git and later you can even download the submodules simultaneously <br/>
`git clone --recursive -j8 git://github.com/foo/bar.git` <br/>
cd bar

* With version 1.6.5 of Git and later, you can use: <br/>
`git clone --recursive git://github.com/foo/bar.git` <br/>
cd bar

* For already cloned repos, or older Git versions, just use: <br/>
`git clone git://github.com/foo/bar.git` <br/>
cd bar <br/>
`git submodule update --init --recursive <br/>`























