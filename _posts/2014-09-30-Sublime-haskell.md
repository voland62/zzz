---
layout: post
title: Sublime Haskell
comments: true 
---

Для того чтоб попробовать хаскель - есть несколько разных способов, - установить [Haskell Platform](https://www.haskell.org/platform/), и запустить ghci, ещё проще - войти в онлайн IDE [FPComplete](https://www.fpcomplete.com) и начать кодить там.

Здесь же я описываю как настроить Sublime text 3 для этих целей. Я делал под виндой, под линуксом - думаю что будет в общих чертах - очень схоже.

1. Ставим [Haskell Platform](https://www.haskell.org/platform/).


2. Настроить cabal
  -меняем порядок в path - чтобы C:\Users\Batman\AppData\Roaming\cabal\bin был выше C:\dev\bin\hask\bin. Это потому что после установки у нас будет два бинарника cabal.exe и нам нужет тот что лежит в HOME/cabal/bin.
  -затем cabal update, cabal install cabal-install
  -перенаправить на [stackage](http://www.stackage.org/) - дело в том что стандартный Haskell репозиторий, как я понимаю - не проверяется на совместимость пакетов между собой, и вот stackage - альтернативный репозиторий, который такую проверку делает. Подробности, и инструкцию, можно почитать на сайте проекта.
  Нам нужна инклюзив версия:
  remote-repo: http://www.stackage.org/stackage/92c5686ff52b79d727431993e2f21b1b7b869d1b
  cabal update
  
3. Ставим [Sublime haskell](https://github.com/SublimeHaskell/SublimeHaskell)
    тут всё нормально по-дефолту, но в
    c:\Users\Batman\AppData\Roaming\Sublime Text 3\Packages\User\cabal-my-custom.sublime-build
    меняем:

    ```json
    {
        "cmd": ["cabal build --ghc-options='-O0 -hidir o0 -odir o0'"],
        "shell": true,
         "file_regex": "^(\\S*?):(\\d+):(\\d+):$"
    }
     ```

4. Ставим [Sublime REPL](https://github.com/wuub/SublimeREPL) в 
    c:\Users\Batman\AppData\Roaming\Sublime Text 3\Packages\SublimeREPL\config\Haskell\Main.sublime-menu меняем:

    ```
    "cmd": ["cabal", "repl"],
    "cwd": "$folder",
    ```

5. Cтавим [LoadFileToRepl](https://sublime.wbond.net/packages/Load%20file%20to%20REPL)
  (Здесь есть нюанс - если у вас есть в проекте две папки с двумя cabal файлами в каждом - то этот плагин будет запускать репл для первого в списке проекта. Надо просто переместить наверх требуемую папку.)
