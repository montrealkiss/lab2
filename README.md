## Національний технічний університет України<br>“Київський політехнічний інститут ім. Ігоря Сікорського”

## Факультет прикладної математики<br>Кафедра системного програмування і спеціалізованих комп’ютерних систем


# Лабораторна робота №2<br>"Розширена робота з git"

## КВ-21 Юдін Дмитро

## Хід виконання роботи

### 1. Зклонувати репозиторій для цієї роботи використавши локальний репозиторій від lab1 в якості "віддаленого".
Локальний репозиторій знаходиться за шляхом F:\KPI\tirpz\lab1\branch_1
```
$ git clone file:///f/KPI/tirpz/1lab/branch_1/
Cloning into 'branch_1'...
remote: Enumerating objects: 694, done.
remote: Counting objects: 100% (694/694), done.
remote: Compressing objects: 100% (634/634), done.
remote: Total 694 (delta 38), reused 678 (delta 31), pack-reused 0 (from 0)
Receiving objects: 100% (694/694), 8.56 MiB | 6.20 MiB/s, done.
Resolving deltas: 100% (38/38), done.

```
Репозиторій було успішно зклоновано.
Виконаємо перевірку, подивимось зміст гілки branch_1 в теці 2lab:
```
$ git branch -a
* branch_1
  remotes/origin/HEAD -> origin/branch_1
  remotes/origin/branch_1
  remotes/origin/branch_2
  remotes/origin/branch_3
  remotes/origin/tonai-addons
```
Клонування пройшло вірно.
### 2. Робота з ремоутами
Перевіримо куди "дивиться" наш поточний ремоут origin:
```
$ git remote -v
origin  file:///f/KPI/tirpz/1lab/branch_1/ (fetch)
origin  file:///f/KPI/tirpz/1lab/branch_1/ (push)
```
# 2.1 Додати новий ремоут використавши URI на інтернет-джерело вашого репозиторію.
Інтернет-джерело репозиторію використаного в першій Лабораторній роботі має наступне посилання:
https://github.com/slidevjs/slidev.
Додаємо новий ремоут використавши це посилання:
```
$ git remote add upstream https://github.com/slidevjs/slidev
```
Виконаємо перевірку додавання нового ремоута:
```
$ git remote -v
origin  file:///f/KPI/tirpz/1lab/branch_1/ (fetch)
origin  file:///f/KPI/tirpz/1lab/branch_1/ (push)
upstream        https://github.com/slidevjs/slidev (fetch)
upstream        https://github.com/slidevjs/slidev (push)
```
# 2.2 Показати список віддалених гілок, так щоби було видно гілки з різних ремоутів.
Спочатку завантажимо нові гілки використовуючи `git fetch upstream`.
Далі виконуємо команду `git branch -a` аби показати що було додано новим ремоутом, і тим самим будемо транслювати нові гілки з нового ремоуту
та старі з першого:
```
$ git branch -a
* branch_1
  remotes/origin/HEAD -> origin/branch_1
  remotes/origin/branch_1
  remotes/origin/branch_2
  remotes/origin/branch_3
  remotes/origin/tonai-addons
  remotes/upstream/docs-legacy
  remotes/upstream/feat/hookable
  remotes/upstream/feat/light-or-dark-component
  remotes/upstream/feat/try-prettier
  remotes/upstream/main
```
# 2.3 Створити нову гілку і додати до неї декілька комітів.
Створюємо нову гілку:
```
$ git checkout -b lab2_1_branch
Switched to a new branch 'lab2_1_branch'
```
Створюємо в новій гілці три файли, а потім додаємо коміти:
```
$ git status
On branch lab2_1_branch
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        clubman.c
        countryman.c
        hatch.c

nothing added to commit but untracked files present (use "git add" to track)

$ git add clubman.c

$ git commit -m 'clubman.c file was added'
[lab2_1_branch 398c4a94] clubman.c file was added
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 clubman.c

$ git add .

$ git commit -m 'countryman.c and hatch.c were added'
[lab2_1_branch 636f1b6c] countryman.c and hatch.c were added
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 countryman.c
 create mode 100644 hatch.c

$ git status
On branch lab2_1_branch
nothing to commit, working tree clean
```
# 2.4 Пушнути створену гілку `lab2_1_branch` на ремоут з 1lab без зв'язувань локальної гілки з віддаленою.
```
$ git push
fatal: The current branch lab2_1_branch has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin lab2_1_branch

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```
При спробі використання команди `git push` ми отримуємо помилку, оскільки ми не вказуємо на яку саме віддалену копію репозиторію хочемо покласти нову гілку.
Тому використовуємо `git push` вказуючи назву віддаленої копії:
```
$ git push origin lab2_1_branch
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 24 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 505 bytes | 63.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
To file:///f/KPI/tirpz/1lab/branch_1/
 * [new branch]        lab2_1_branch -> lab2_1_branch
```
Пуш відбувся успішно. 
Можемо також перевірити чи не відбулося зв'язування гілок:
```
$ git push
fatal: The current branch lab2_1_branch has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin lab2_1_branch

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```
Бачимо, що нам знову виводить помилку, отже гілки не зв'язані.
# 2.5 Додати до гілки ще коміт.
Для нового коміту можемо видалити якийсь файл, нехай це буде hatch.c:
```
$ git rm hatch.c
rm 'hatch.c''

$ git commit -m 'hatch.c was deleted'
[lab2_1_branch bbbe8ef6] hatch.c was deleted
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 hatch.c
```
# 2.6 Пушнути зміни гілки на ремоут, створений з ЛР1, цього разу зв'язавши гілки.
Для зв'язки гілок потрібно до команди `git push` додати ключ -u, який і проводить зв'язку. Після цього кожен наступний пуш
можна робити просто як git push -- але саме в гілці lab2_1_branch -- git буде автоматично заливати
у вказану віддалену копію та гілку.
```
$ git push -u origin lab2_1_branch
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 24 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 232 bytes | 29.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
To file:///f/KPI/tirpz/1lab/branch_1/
   636f1b6c..bbbe8ef6  lab2_1_branch -> lab2_1_branch
branch 'lab2_1_branch' set up to track 'origin/lab2_1_branch'.

$ git push
Everything up-to-date
```
Тепер після команди `git push` не виникає помилок, отже зв'язування відбулось успішно як і пуш.
# 2.7 Додати до гілки ще коміт.
```
$ git mv clubman.c new_clubman.c

$ git commit -m 'clubman.c was renamed to new_clubman.c'
[lab2_1_branch 2072e792] clubman.c was renamed to new_clubman.c
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename clubman.c => new_clubman.c (100%)
```
# 2.8 Переконатися в тому, що після зв'язування гілок тепер можна пушити просто через `git push`.
```
$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 24 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 258 bytes | 36.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
To file:///f/KPI/tirpz/1lab/branch_1/
   bbbe8ef6..2072e792  lab2_1_branch -> lab2_1_branch
```
Пуш успішно відбувся
# 2.9 Перевірити в репозиторії ЛР1, що після пушу тут з'явилася нова локальна гілка.
Віддалені гілки не є транзитивними, 2lab бачить "віддалені гілки" з 1lab лише ті, що в 1lab - локальні.
Тобто пуш який був виконаний при зв'язувані гілок створив в 1lab нову локальну гілку `lab2_1_branch`.
```
$ git branch
* branch_1
  branch_2
  branch_3
  lab2_1_branch
  tonai-addons
```
# 3 Змерджити гілку, що була створена при виконанні ЛР1, в поточну гілку lab2_1_branch.
Потрібно затягнути в нашу нову гілку lab2_1_branch ті зміни, що були в гілці для ЛР1.
```
$ git merge origin/branch_1
Already up to date.

$ git log --pretty=oneline --graph
* 398c4a94733f6a707720bb7f3abc8f084345de53 (HEAD -> lab2_1_branch) clubman.c file was added
* 0c870824b25a1d883a0c3dcf4b8a265624405c5a (origin/tonai-addons, origin/branch_3, origin/branch_2, origin/branch_1, origin/HEAD, branch_1) rename 4.txt to 4new.txt
* 1f66892f0cb19ccf235cb422ac6b66926056db5d all save
* a0bd1364561cc4857fcfb555117ab093f282a15f all save
* e44c5c06e3fd377134260935b8cffe50518771cc all save
* 616eaecd0c6ab1471d65efdd327933e840f29290 commit 1.txt
* 2b942f22bc78fe78aecdc68d3824009f165df37e delete lab1.txt
* c46504e3d91de4cfaa4255f3bc58cd18d9af45ff lab1.txt
* ba1ff998bd0f3edcb05a6f14d657e3864dfbaf9d (grafted) Merge branch 'main' into tonai-addons
```
### 4. Перенесення комітів.
# 4.1 Створити ще одну гілку і додати до неї три коміти.
```
$ git checkout -b new_lab2_1_branch
```
Створюємо та комітимо файли red.txt, green.txt, blue.txt.
```
$ echo "Change for commit 1" > red.txt
$ git add red.txt
$ git commit -m "First commit"
```
Повторюємо ці ж дії для інших файлів.
# 4.2 Перенести з гілки lab2_new_4.1_branch середній з трьох нових комітів в гілку lab2_new_2.3_branch.
Необхідно середній з трьох зроблених комітів, отже виконаємо `git log` та знайдемо хеш бажаного коміту.
```
$ git log
commit dc7f723c203dd5e36f9061921afbba0838577eea (HEAD -> new_lab2_1_branch)
Author: montrealkiss <darkrollii1@gmail.com>
Date:   Fri Dec 13 20:58:34 2024 +0200

    Third commit

commit 19182c68e50c100e355f889436b5753327c3c2d5
Author: montrealkiss <darkrollii1@gmail.com>
Date:   Fri Dec 13 20:57:59 2024 +0200

    Second commit

commit dc33a4dd60bd5a5611099526aeb432ffcfc5139b
Author: montrealkiss <darkrollii1@gmail.com>
Date:   Fri Dec 13 20:56:55 2024 +0200

    First commit
```
Шуканий хеш `19182c68e50c100e355f889436b5753327c3c2d5`.
Переключаємось на гілку, на яку переноситимемо коміт.
```
$ git checkout lab2_1_branch
Switched to branch 'lab2_1_branch'
Your branch is ahead of 'origin/branch_1' by 1 commit.
  (use "git push" to publish your local commits)

$ git branch
  branch_1
* lab2_1_branch
  new_lab2_1_branch
```
Після переключення виконуємо перенесення коміту за допомогою `git cherry-pick`.
```
$ git cherry-pick 19182c68e50c100e355f889436b5753327c3c2d5
[lab2_1_branch fabebd42] Second commit
 Date: Fri Dec 13 20:57:59 2024 +0200
 1 file changed, 1 insertion(+)
 create mode 100644 blue.txt
```
Перенесення коміту відбулось успішно.
Демонструємо факт перенесення коміту за допомогою `git log --pretty=oneline --graph -n 10 --branches`.
```
$ git log --pretty=oneline --graph -n 10 --branches
* fabebd42793cbc84d9357026324d330b0db72893 (HEAD -> lab2_1_branch) Second commit
| * dc7f723c203dd5e36f9061921afbba0838577eea (origin/new_lab2_1_branch, new_lab2_1_branch) Third commit
| * 19182c68e50c100e355f889436b5753327c3c2d5 Second commit
| * dc33a4dd60bd5a5611099526aeb432ffcfc5139b First commit
|/
* 398c4a94733f6a707720bb7f3abc8f084345de53 clubman.c file was added
* 0c870824b25a1d883a0c3dcf4b8a265624405c5a (origin/tonai-addons, origin/branch_3, origin/branch_2, origin/branch_1, origin/HEAD, branch_1) rename 4.txt to 4new.txt
* 1f66892f0cb19ccf235cb422ac6b66926056db5d all save
* a0bd1364561cc4857fcfb555117ab093f282a15f all save
* e44c5c06e3fd377134260935b8cffe50518771cc all save
* 616eaecd0c6ab1471d65efdd327933e840f29290 commit 1.txt
```
### 5. Визначити останнього спільного предка між двома будь-якими гілками.
Визначимо момент, коли гілки `lab2_1_branch` і `branch_1` "розійшлися".
```
$ git merge-base origin/lab2_1_branch origin/branch_1
0c870824b25a1d883a0c3dcf4b8a265624405c5a

$ git log --pretty=oneline --graph
* fabebd42793cbc84d9357026324d330b0db72893 (HEAD -> lab2_1_branch) Second commit
* 398c4a94733f6a707720bb7f3abc8f084345de53 clubman.c file was added
* 0c870824b25a1d883a0c3dcf4b8a265624405c5a (origin/tonai-addons, origin/branch_3, origin/branch_2, origin/branch_1, origin/HEAD, branch_1) rename 4.txt to 4new.txt
* 1f66892f0cb19ccf235cb422ac6b66926056db5d all save
* a0bd1364561cc4857fcfb555117ab093f282a15f all save
* e44c5c06e3fd377134260935b8cffe50518771cc all save
* 616eaecd0c6ab1471d65efdd327933e840f29290 commit 1.txt
* 2b942f22bc78fe78aecdc68d3824009f165df37e delete lab1.txt
* c46504e3d91de4cfaa4255f3bc58cd18d9af45ff lab1.txt
* ba1ff998bd0f3edcb05a6f14d657e3864dfbaf9d (grafted) Merge branch 'main' into tonai-addons
```
Як бачимо, результат виконання є лише один хеш коміту, але це і є потрібний момент, коли гілки розійшлися.
Цей же коміт ще називають "базовим", оскільки саме відносно нього відбувається вирішення конфліктів. 
Взагалі конфлікт виникає саме в той момент, коли дві паралельні гілки зробили зміни до одного і того ж місця, 
після чого дані зміни намагаються об'єднатися.
### 6. Робота з ничкою.
# 6.1 Зробити трохи unstaged змін.
```
$ git status
On branch lab2_1_branch
Your branch is ahead of 'origin/branch_1' by 5 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   blue.txt
        modified:   clubman.c

no changes added to commit (use "git add" and/or "git commit -a")
```
Було модифіковано 2 файли, тепер необхідно зберегти ці зміни в ничку.
# 6.2 Зберегти до нички.
```
$ git stash
Saved working directory and index state WIP on lab2_1_branch: efe6fcf5 add 13.txt

$ git status
On branch lab2_1_branch
Your branch is ahead of 'origin/branch_1' by 5 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
Було отримане чисте робоче дерево, тепер можемо оглянути вміст нички.
```
$ git stash list
stash@{0}: WIP on lab2_1_branch: efe6fcf5 add 13.txt
```
# 6.3 Зробити ще трохи unstaged змін.
```
$ git status
On branch lab2_1_branch
Your branch is ahead of 'origin/branch_1' by 5 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   11.txt
        modified:   12.txt
        modified:   4new.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
Було модифіковано 3 файли, збережемо зміни в ничку.
# 6.4 Зберегти до нички.
```
$ git stash
Saved working directory and index state WIP on lab2_1_branch: efe6fcf5 add 13.txt

$ git status
On branch lab2_1_branch
Your branch is ahead of 'origin/branch_1' by 5 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
Отримали чисте робоче дерево, оглянемо вміст нички.
```
$ git stash list
stash@{0}: WIP on lab2_1_branch: efe6fcf5 add 13.txt
stash@{1}: WIP on lab2_1_branch: efe6fcf5 add 13.txt
```
# 6.5 Дістати з нички перші збережені зміни з пункту 6.2.
Використаємо `git stash pop`:
```
$ git stash pop stash@{1}
On branch lab2_1_branch
Your branch is ahead of 'origin/branch_1' by 5 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   blue.txt
        modified:   clubman.c

no changes added to commit (use "git add" and/or "git commit -a")
Dropped stash@{1} (ac211654733c85641d3e0199bdd5f02f5b953045)
```
З нички дістались наші перші два модифіковані файли. Виконаємо перевірку чи видалилась ничка.
```
$ git stash list
stash@{0}: WIP on lab2_1_branch: efe6fcf5 add 13.txt
```
Бачимо, що `git stash list` показує лише одну ничку, отже ничка пункту 6.2 була успішно видалена.
### 7. Робота з файлом .gitignore.
# 7.1 Створити кілька файлів з якимось унікальним розширенням.
Було створено наступні три файли: `obi.plus`, `oni.plus` та `ori.txt`.
```
$ git status
On branch lab2_1_branch
Your branch is ahead of 'origin/branch_1' by 6 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        obi.plus
        oni.plus
        ori.txt

nothing added to commit but untracked files present (use "git add" to track)
```
# 7.2 Додати шаблон для цих файлів в ігнор.
Створюємо за допомогою `touch` в корені репозиторію `.gitignore`, додаємо в цей файл розширення `.plus`.
Після цього в статусі більше не будуть показуватися ці файли. Перевіримо це:
# 7.3 Перевірити статус -- файли повинні зникнути.
```
$ git status
On branch lab2_1_branch
Your branch is ahead of 'origin/branch_1' by 6 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitignore

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        ori.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
Все зроблено вірно, файли з розширенням `.plus` не відображаються.
# 7.4 Перевірити статус включно з ігнором.
Для перевірки репозиторію на наявність ігнорованих файлів використовується ключ `--ignored`.
```
$ git status --ignored
On branch lab2_1_branch
Your branch is ahead of 'origin/branch_1' by 6 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitignore

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        ori.txt

Ignored files:
  (use "git add -f <file>..." to include in what will be committed)
        obi.plus
        oni.plus

no changes added to commit (use "git add" and/or "git commit -a")
```
# 7.5 Почистити всі untracked файли з репозиторію, включно з ігнорованими.
Для повної очистки всіх untracked файлів, в тому числі тих, що ігноруються, використаємо команду `git clean`.
```
$ git clean -fdx
Removing obi.plus
Removing oni.plus
Removing ori.txt
```
Всі untracked файли видалені, разом з тими, що ігноруються.
### 8. Робота з reflog.
# 8.1 Переглянути лог станів гілок.
```
$ git log --pretty=oneline --graph -n 15
* f746eca952d46e5e0612db4b855bd32be7a8e564 (HEAD -> lab2_1_branch) clubman.c and blue.txt was modified
* efe6fcf542cab0091fff41abc46592f25f30dade add 13.txt
* c0b443b0468f45360478208d4fcc8932d574af45 add 12.txt
* 5040093492ad2d0ef6680ef9985191353c9e519e add 11.txt
* fabebd42793cbc84d9357026324d330b0db72893 Second commit
* 398c4a94733f6a707720bb7f3abc8f084345de53 clubman.c file was added
* 0c870824b25a1d883a0c3dcf4b8a265624405c5a (origin/tonai-addons, origin/branch_3, origin/branch_2, origin/branch_1, origin/HEAD, branch_1) rename 4.txt to 4new.txt
* 1f66892f0cb19ccf235cb422ac6b66926056db5d all save
* a0bd1364561cc4857fcfb555117ab093f282a15f all save
* e44c5c06e3fd377134260935b8cffe50518771cc all save
* 616eaecd0c6ab1471d65efdd327933e840f29290 commit 1.txt
* 2b942f22bc78fe78aecdc68d3824009f165df37e delete lab1.txt
* c46504e3d91de4cfaa4255f3bc58cd18d9af45ff lab1.txt
* ba1ff998bd0f3edcb05a6f14d657e3864dfbaf9d (grafted) Merge branch 'main' into tonai-addons
```
В цей момент наша локальна гілка `lab2_1_branch` повинна мати чимало нових комітів порівняно із її
станом на сервері origin/lab2_1_branch. 

Переключаємось на гілку `tonai-addons` та видаляємо `lab2_1_branch`, зазначимо, що переключатись обов'язково
бо не можна видаляти поточні активні гілки, а також видалимо цю гілку з серверу.
```
$ git checkout tonai-addons
M       .gitignore
branch 'tonai-addons' set up to track 'origin/tonai-addons'.
Switched to a new branch 'tonai-addons'

$ git branch -D lab2_1_branch
Deleted branch lab2_1_branch (was f746eca9).

$ git push -d origin lab2_1_branch
To file:///f/KPI/tirpz/1lab/branch_1/
 - [deleted]           lab2_1_branch
```
Стан гілки втрачено через видалення, але переглянемо `reflog`
```
$ git reflog
0c870824 (HEAD -> tonai-addons, origin/tonai-addons, origin/branch_3, origin/branch_2, origin/branch_1, origin/HEAD, branch_1) HEAD@{0}: checkout: moving from lab2_1_branch to tonai-addons
f746eca9 HEAD@{1}: commit: clubman.c and blue.txt was modified
efe6fcf5 HEAD@{2}: reset: moving to HEAD
efe6fcf5 HEAD@{3}: reset: moving to HEAD
efe6fcf5 HEAD@{4}: commit: add 13.txt
c0b443b0 HEAD@{5}: commit: add 12.txt
50400934 HEAD@{6}: commit: add 11.txt
fabebd42 HEAD@{7}: cherry-pick: Second commit
398c4a94 HEAD@{8}: checkout: moving from new_lab2_1_branch to lab2_1_branch
dc7f723c (origin/new_lab2_1_branch, new_lab2_1_branch) HEAD@{9}: checkout: moving from lab2_1_branch to new_lab2_1_branch
398c4a94 HEAD@{10}: checkout: moving from new_lab2_1_branch to lab2_1_branch
dc7f723c (origin/new_lab2_1_branch, new_lab2_1_branch) HEAD@{11}: checkout: moving from lab2_1_branch to new_lab2_1_branch
398c4a94 HEAD@{12}: checkout: moving from new_lab2_1_branch to lab2_1_branch
dc7f723c (origin/new_lab2_1_branch, new_lab2_1_branch) HEAD@{13}: checkout: moving from lab2_1_branch to new_lab2_1_branch
398c4a94 HEAD@{14}: checkout: moving from new_lab2_1_branch to lab2_1_branch
dc7f723c (origin/new_lab2_1_branch, new_lab2_1_branch) HEAD@{15}: commit: Third commit
19182c68 HEAD@{16}: commit: Second commit
dc33a4dd HEAD@{17}: commit: First commit
```
# 8.2 Створити нову гілку на будь-який стан зі списку та переключитися на цю гілку.
Бачимо, що ми можемо дуже легко відновити нашу гілку до стану, який був після чері-піка:
```
$ git branch lab2-resurrected f746eca9

$ git checkout lab2-resurrected
M       .gitignore
Switched to branch 'lab2-resurrected'

$ git log --pretty=oneline --graph -n 15
* f746eca952d46e5e0612db4b855bd32be7a8e564 (HEAD -> lab2-resurrected) clubman.c and blue.txt was modified
* efe6fcf542cab0091fff41abc46592f25f30dade add 13.txt
* c0b443b0468f45360478208d4fcc8932d574af45 add 12.txt
* 5040093492ad2d0ef6680ef9985191353c9e519e add 11.txt
* fabebd42793cbc84d9357026324d330b0db72893 Second commit
* 398c4a94733f6a707720bb7f3abc8f084345de53 clubman.c file was added
* 0c870824b25a1d883a0c3dcf4b8a265624405c5a (origin/tonai-addons, origin/branch_3, origin/branch_2, origin/branch_1, origin/HEAD,
 tonai-addons, branch_1) rename 4.txt to 4new.txt
* 1f66892f0cb19ccf235cb422ac6b66926056db5d all save
* a0bd1364561cc4857fcfb555117ab093f282a15f all save
* e44c5c06e3fd377134260935b8cffe50518771cc all save
* 616eaecd0c6ab1471d65efdd327933e840f29290 commit 1.txt
* 2b942f22bc78fe78aecdc68d3824009f165df37e delete lab1.txt
* c46504e3d91de4cfaa4255f3bc58cd18d9af45ff lab1.txt
* ba1ff998bd0f3edcb05a6f14d657e3864dfbaf9d (grafted) Merge branch 'main' into tonai-addons
```
Можемо побачити, що гілка була відновлена.
