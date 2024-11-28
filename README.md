## Національний технічний університет України<br>“Київський політехнічний інститут ім. Ігоря Сікорського”

## Факультет прикладної математики<br>Кафедра системного програмування і спеціалізованих комп’ютерних систем


# Лабораторна робота №2<br>"Розширена робота з git"

## КВ-21 Юдін Дмитро

## Хід виконання роботи

### 1. Зклонувати репозиторій для цієї роботи використавши локальний репозиторій від lab1 в якості "віддаленого".
Локальний репозиторій знаходиться за шляхом F:\KPI\tirpz\lab1\branch_1
```
$ git clone file:///F:/KPI/tirpz/lab1/branch_1
Cloning into 'branch_1'...
remote: Enumerating objects: 682, done.
remote: Counting objects: 100% (682/682), done.
remote: Compressing objects: 100% (622/622), done.
remote: Total 682 (delta 32), reused 679 (delta 31), pack-reused 0 (from 0)
Receiving objects: 100% (682/682), 8.56 MiB | 3.40 MiB/s, done.
Resolving deltas: 100% (32/32), done.
```
Репозиторій було успішно зклоновано.
Виконаємо перевірку, спершу подивимось зміст гілки branch_1 в теці lab1:
```
$ git branch -a
* tonai-addons
  remotes/origin/tonai-addons
```
Тепер оглянемо зміст з теки lab2:
```
$ git branch -a
* tonai-addons
  remotes/origin/HEAD -> origin/tonai-addons
  remotes/origin/tonai-addons
```
Клонування пройшло вірно.
### 2. Робота з ремоутами
# 2.1 Додати новий ремоут використавши URI на інтернет-джерело вашого репозиторію.
Інтернет-джерело репозиторію використаного в першій Лабораторній роботі має наступне посилання:
https://github.com/slidevjs/slidev.
Додаємо новий ремоут використавши це посилання:
```
$ git remote add upstream https://github.com/slidevjs/slidev
```
Виконаємо перевірку додавання нового ремоута:
```
git remote -v
$ git remote -v
origin  file:///F:/KPI/tirpz/lab1/branch_1 (fetch)
origin  file:///F:/KPI/tirpz/lab1/branch_1 (push)
upstream        https://github.com/slidevjs/slidev (fetch)
upstream        https://github.com/slidevjs/slidev (push)
```
# 2.2 Показати список віддалених гілок, так щоби було видно гілки з різних ремоутів.
Спочатку завантажимо нові гілки використовуючи `git fetch upstream`.
Далі виконуємо команду `git branch -a` аби показати що було додано новим ремоутом, і тим самим будемо транслювати нові гілки з нового ремоуту
та старі з першого:
```
$ git fetch upstream
$ git branch -a
* tonai-addons
  remotes/origin/HEAD -> origin/tonai-addons
  remotes/origin/tonai-addons
  remotes/upstream/docs-legacy
  remotes/upstream/feat/hookable
  remotes/upstream/feat/light-or-dark-component
  remotes/upstream/feat/try-prettier
  remotes/upstream/fix/shortcuts-not-removable
  remotes/upstream/main
  remotes/upstream/tonai-addons
```
# 2.3 Створити нову гілку і додати до неї декілька комітів.
Створюємо нову гілку:
```
$ git checkout -b lab2-branch
Switched to a new branch 'lab2-branch'
```
Створюємо в новій гілці три файли, а потім додаємо коміти:
```
$ git status
On branch lab2-branch
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        energy.c
        stalker.c
        stream.c

nothing added to commit but untracked files present (use "git add" to track)

$ git add energy.c

$ git commit -m 'energy.c file was added'
[lab2-branch 41bef1e1] energy.c file was added
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 energy.c

$ git add .

$ git commit -m 'stalker.c and stream.c were added'
[lab2-branch 65f54c12] stalker.c and stream.c were added
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 stalker.c
 create mode 100644 stream.c

$ git status
On branch lab2-branch
nothing to commit, working tree clean
```
# 2.4 Пушнути створену гілку `lab2-branch` на ремоут з lab1 без зв'язувань локальної гілки з віддаленою.
```
$ git push
fatal: The current branch lab2-branch has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin lab2-branch

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```
При спробі використання команди `git push` ми отримуємо помилку, оскільки ми не вказуємо на яку саме віддалену копію репозиторію хочемо покласти нову гілку.
Тому використовуємо `git push` вказуючи назву віддаленої копії:
```
$ git push origin lab2-branch
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 24 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 488 bytes | 61.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
To file:///F:/KPI/tirpz/lab1/branch_1
 * [new branch]        lab2-branch -> lab2-branch
```
Пуш відбувся успішно. 
Можемо також перевірити чи не відбулося зв'язування гілок:
```
$ git push
fatal: The current branch lab2-branch has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin lab2-branch

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```
Бачимо, що нам знову виводить помилку, отже гілки не зв'язані.
# 2.5 Додати до гілки ще коміт.
Для нового коміту можемо видалити якийсь файл, нехай це буде stream.c:
```
$ git rm stream.c
rm 'stream.c'

$ git commit -m "stream.c file was deleted"
[lab2-branch 7cf28e14] stream.c file was deleted
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 stream.c
```
# 2.6 Пушнути зміни гілки на ремоут, створений з ЛР1, цього разу зв'язавши гілки.
Для зв'язки гілок потрібно до команди `git push` додати ключ -u, який і проводить зв'язку. Після цього кожен наступний пуш
можна робити просто як git push -- але саме в гілці lab2-branch -- git буде автоматично заливати
у вказану віддалену копію та гілку.
```
$ git push -u origin lab2-branch
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 24 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 235 bytes | 29.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
To file:///F:/KPI/tirpz/lab1/branch_1
   65f54c12..7cf28e14  lab2-branch -> lab2-branch
branch 'lab2-branch' set up to track 'origin/lab2-branch'.

$ git push
Everything up-to-date
```
Тепер після команди `git push` не виникає помилок, отже зв'язування відбулось успішно як і пуш.
# 2.7 Додати до гілки ще коміт.
```
$ git mv energy.c fullenergy.c

$ git commit -m 'energy.c was renamed to fullenergy.c'
[lab2-branch 2ddc4201] energy.c was renamed to fullenergy.c
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename energy.c => fullenergy.c (100%)
```
# 2.8 Переконатися в тому, що після зв'язування гілок тепер можна пушити просто через `git push`.
```
$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 24 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 263 bytes | 32.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
To file:///F:/KPI/tirpz/lab1/branch_1
   7cf28e14..2ddc4201  lab2-branch -> lab2-branch
```
Пуш успішно відбувся
# 2.9 Перевірити в репозиторії ЛР1, що після пушу тут з'явилася нова локальна гілка.
Віддалені гілки не є транзитивними, lab2 бачить "віддалені гілки" з lab1 лише ті, що в lab1 - локальні.
Тобто пуш який був виконаний при зв'язувані гілок створив в lab1 нову локальну гілку `lab2_branch`.
```
$ git branch
* lab2-branch
  tonai-addons
```
# 3 Змерджити гілку, що була створена при виконанні ЛР1, в поточну гілку lab2-branch.
