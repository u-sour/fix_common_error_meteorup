# fix_common_error_meteorup
a simple repository about fix common error with meteor up
## Common Errors (15/12/2023)
- All configured authentication methods failed
- Esbuild on macOs M1 (apple chip)
- Error deploy with Meteor 2.13

    #10 3.512 NODE_VERSION=14.21.4    
    #10 ERROR: process "/bin/sh -c bash ./scripts/onbuild-node.sh" did not complete successfully: exit code: 3
- Error with dynamic import (vue-router)

    Errors prevented bundling:                 
    While minifying app code:                  
    packages/minifyStdJS/plugin/minify-js.js:49:25: terser minification error (SyntaxError:"Import" statement may only appear at the top level)
    Source file: node_modules/mongo-object/dist/esm/main.js  (2:0)
    Line content: import MongoObject from './mongo-object.js';

    at maybeThrowMinifyErrorBySourceFile (packages/minifyStdJS/plugin/minify-js.js:49:25)
    at packages/minifyStdJS/plugin/minify-js.js:77:11
    at Array.forEach (<anonymous>)
    at MeteorMinifier.processFilesForBundle (packages/minifyStdJS/plugin/minify-js.js:66:11)


    While minifying app code:
    packages/minifyStdJS/plugin/minify-js.js:49:25: terser minification error (SyntaxError:"Import" statement may only appear at the top level)
    Source file: client/main.js  (2:0)
    Line content: import "./vite/meteor-entry.js"

    at maybeThrowMinifyErrorBySourceFile (packages/minifyStdJS/plugin/minify-js.js:49:25)
    at packages/minifyStdJS/plugin/minify-js.js:77:11
    at Array.forEach (<anonymous>)
    at MeteorMinifier.processFilesForBundle (packages/minifyStdJS/plugin/minify-js.js:66:11)
                                           
    => Build Error. Check the logs printed above.

## How to fix ?
### All configured authentication methods failed

    step 1: connect with your deployment server (EC2 etc ...)
    
    step 2: open file /etc/ssh/sshd_config by cmd `sudo nano /etc/ssh/sshd_config`

    step 3: add this line `PubkeyAcceptedKeyTypes=+ssh-rsa` to the end > exit > save

    step 4: restart the service sshd and ssh (optional : if it existed) with
    `sudo systemctl restart sshd.service`

    step 5: copy your ssh public key (ip_rsa.pub) from your local computer
    
    step 6: go to home root (~) open file /ssh/authorized_keys by cmd `sudo nano ./ssh/authorized_keys` paste your ssh public key at the end > exit > save

### Esbuild on macOs M1 (apple chip)
    
    type cmd  `npm uninstall esbuild` and then `npm install esbuild`

### Error deploy with Meteor 2.13

    change your docker image from `zodern/meteor:latest` to `duodeka/meteor:latest`

### Error with dynamic import (vue-router)
    step 1: type cmd `meteor remove vite:bundler`
    step 2: meteor add jorgenvatle:vite-bundler@1.9.1 && meteor npm i -D vite meteor-vite
