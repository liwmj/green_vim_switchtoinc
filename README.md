# vim-switchtoinc

这是一款vim插件，用于头文件和源文件间快速切换。注：在a.vim插件基础上修改的。

## 特性

* 支持多种语言（所有具备头文件的语言），主要支持为c, cpp, objective-c, objective-cpp等
* 支持绝对路径进行查找
* 支持源文件为基准的相对路径查找
* 支持regex替换路径
* 支持自定义项目目录，批量初始化目录后使用（推荐）

## 安装

可以直接克隆下来丢在vim的插件目录，但我推荐用插件管理器进行管理，下面是各种插件管理器：

*  [Pathogen](https://github.com/tpope/vim-pathogen)
  * `git clone https://github.com/liwangmj/vim-switchtoinc.git ~/.vim/bundle/vim-switchtoinc`
*  [vim-plug](https://github.com/junegunn/vim-plug)
  * `Plug 'liwangmj/vim-switchtoinc'`
*  [NeoBundle](https://github.com/Shougo/neobundle.vim)
  * `NeoBundle 'liwangmj/vim-switchtoinc'`
*  [Vundle](https://github.com/gmarik/vundle)
  * `Plugin 'liwangmj/vim-switchtoinc'`

## 使用

切换到当前文件的源文件或则头文件：
```
:A
```

同上，但在上面基础上会水平分栏进行打开：
```
:AV
```

打开当前文件的源文件或头文件，并会垂直分栏进行打开：
```
:AS
```

多个重名文件之间的切换：
```
:AN
```

初始化查找目录（只在用最后一种方式前使用，其他方法不用）：
```
:SearchIncAndSrcPath
```

## 设置

需要设置源文件和头文件的查找目录，通过 `g:alternateSearchPath` 来设置。

基于源文件的相对路径查找（如下是默认值）：
```
let g:alternateSearchPath = 'sfr:../source,sfr:../src,sfr:../include,sfr:../inc'
```

基于绝对路径查找（例子）：
```
let g:alternateSearchPath = 'abs:/home/my/myporject/inc,abs:/home/my/myproject/src'
```

基于vim正则表达式查找（例子）：
```
let g:alternateSearchPath = 'reg:/inc/src/g/, reg:/src/inc/g/'
```

以上方法都比较有局限性，因为只能针对单条路径（正则）或单个目录进行查找，下面的方法相对麻烦一点，但一劳永逸，不用担心可恶的目录问题：

* 先设置项目的根目录（例子）：
```
let g:iSearchProjectPath = '/home/my/myproject'
let g:iSearchPathName = [
            \'src', 'Src', 'SRC',
            \'inc', 'Inc', 'INC',
            \'source', 'Source', 'SOURCE',
            \'include', 'Include', 'INCLUDE',
            \'my_inc', 'my_inc'
\]
```

* 再调用 `SearchIncAndSrcPath` 进行初始化查找目录：
```
:SearchIncAndSrcPath
```

* 然后可以用`:A` `:AV` `:AS` 进行切换了。

* 最后说一下，最新版本更新：
```
*第一次调用`:A` `:AV` `:AS`，插件内部会自动执行一次 `SearchIncAndSrcPath`，只需直接切换即可，不用单独执行。
```
```
*另外，如果在使用vim过程中相关文件目录有更改，可以通过执行一次 `SearchIncAndSrcPath`来更新，但值得注意的是：之前打开过的文件切换信息由于存在缓存无法更新，需要重启vim才能生效！
```

## 谢谢

欢迎使用，祝使用愉快

* http://liwangmj.com
* liwangmj@gmail.com


