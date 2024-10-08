## 1. Перенос изменений между ветками
`git rebase <целевая_ветка>` — это команда, которая позволяет взять изменения текущей ветки и "перенести" их на другую ветку, создавая иллюзию, что они были сделаны на основе её последних коммитов. Это альтернатива команде `git merge`, но она перезаписывает историю коммитов.

Когда вы выполняете rebase, изменения вашей текущей ветки применяются поверх указанной ветки, сохраняя линейную историю.

### Пример: 
Предположим, у нас есть две ветки:
- Ветка `main` с коммитами A → B → C
- Ветка `new_branch` с коммитами D → E

```
A -- B -- C  (main)
          \
           D -- E  (new_branch)
```

### 1.1 Слияние с помощью git merge
При слиянии ветки `new_branch` в `main` с помощью `git merge`, Git создаст новый коммит слияния, сохранив историю двух веток.

```
A -- B -- C ---- M  (main)
           \   /
            D -- E  (new_branch)
```

- M — это новый коммит слияния. 
В истории останется информация о том, что изменения пришли из разных веток.

### 1.2 Перенос с помощью git rebase
При выполнении `git rebase` ветки `new_branch` на ветку `main`, Git "переносит" изменения D и E поверх коммитов на ветке `main`, делая историю линейной.

```
A -- B -- C -- D' -- E'  (new_branch)
```

В результате ветка feature выглядит так, как будто коммиты D и E были сделаны после C, а не параллельно. История становится чище и линейной, без коммитов слияния.
