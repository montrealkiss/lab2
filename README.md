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
```


