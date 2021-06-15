##If the local is very old
 -npm uninstall -g @angular/cli
 -npm cache verify
 -npm install -g @angular/cli@latest
#Then in your Local project package:
 -rm -rf node_modules dist 
 -npm install --save-dev @angular/cli@latest
 -npm i 
 -ng update @angular/cli 
 -ng update @angular/core
 -npm install --save-dev @angular-devkit/build-angular
