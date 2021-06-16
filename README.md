# If the local is very old
 - npm uninstall -g @angular/cli
 - npm cache verify
 - npm install -g @angular/cli@latest
## Then in your Local project package:
 - rm -rf node_modules dist 
 - npm install --save-dev @angular/cli@latest
 - npm i 
 - ng update @angular/cli 
 - ng update @angular/core
 - npm install --save-dev @angular-devkit/build-angular
 - You have to create a .gitignore file and add node_modules/ 
inside it to tell git not to track them as they are third party code.

### Updating gh-pages with master
 - $ git add .
 - $ git status // to see what changes are going to be commited
 - $ git commit -m 'Some descriptive commit message'
 - $ git push origin master

 - $ git checkout gh-pages // go to the gh-pages branch
 - $ git rebase master // bring gh-pages up to date with master
 - $ git push origin gh-pages // commit the changes
 - $ git checkout master // return to the master branch
