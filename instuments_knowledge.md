## TASKS:

 <details><summary>  Docker </summary>

  1.Создать аккаунт на DockerHub с публичным репозиторием.
  
  
  2.Создать Dockerfiles для сборки образов headnode и worker. 
    Для хранения файлов  Namenode и  DatanodeсервисаHDFS, а такжеNodemanagerсервиса YARN следует использовать Dockervolumes.
    Также   поменяется   способ   запуска   процессов,   они   должны стартовать при запуске контейнеров.
  
  
  3.Собрать образ и запушить в репозиторий.
  
  
  4.Предоставить два  Dockerfiles  и имена образов в формате <youraccount>/<imagename>:<tag>,которые можно запустить ипроверить,что сервисы доступны и работают.   
    При этом предполагается, что проверяющий не знает, что и куда монтировать volumes и какие порты необходимо пробрасывать для корректной работы сервисов.
  
  
  5.* Создать docker-compose.yml файл, запускающий оба образа.
 </details>
 <details><summary> GIT </summary>
1.

  1. Create local repository named lection_git_hw
  2. Create file "homework" in this repo and commit it in master branch
  3. Create branch "hw_git" and insert anything in the file and commit these changes to this branch
  4. Switch back to master branch and add anything else to the empty file "homework" there too
  5. Merge branch "hw_git" to "master", keep only changes from "hw_git" branch
  6. Switch to "hw_git" branch again and create new file "temp_file" and commit it
  7. Revert to the first commit in "hw_git" branch

2.
  1. Register in Github (if you are not registered yet) and create empty repository "lection_git_hw"
  2. Set remote from your local repo from task 1 to this new repo (https://help.github.com/articles/changing-a-remote-s-url/)
  3. Push all branches to the remote repo
  4. Change everything in file "homework" in branch "hw_git" to one line "Hello Github", commit it and push
  5. Create Pull Request from branch "hw_git" to the master branch and assign me as reviewer to this merge request 

3.
  1. Set up Gitlab CE in docker container (image "gitlab/gitlab-ce:latest", ports to publish – 80 and 22, you can choose any ports to be published on your machine)
  2. Log in as root (it will offer you to change password in gitlab webui on your first visit)
  Make screenshots on each step below, pack them as tgz archive and attach it to your homework
  3. Create group "hw_git"
  4. Create two users: maintainer and developer
  5. Add these users to the group and set them proper permissions in the group (maintainer – maintainer, developer – developer)
  6. Create new project with any name
  7. Create all branches for GitFlow in this project (you can create one feature and one release branch and don't create hotfix branch)
  8. Protect master branch to allow only maintainers to merge into it, and restrict all to push there
  9. Protect release branches by wildcard (release-* for example) and allow only maintainers to merge into it
  10. Protect develop branch to allow everyone to create Merge Request into it
  11. Allow anyone do anything in branches like "feature-*"

EXTRA (*)
  1. Add TravisCI to your Github repo from the first task
  2. Create .travis.yml, it should do only echo "Hello World"
  3. Trigger your CI on each commit to any branch
  4. Test it, make screenshot from TravisCI webui with success run
 </details>
