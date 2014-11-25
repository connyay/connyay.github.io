---
layout: post
title: Hosting PencilBlue on OpenShift by Red Hat
---

## Prerequisites:

1. Have created an account with [OpenShift](https://www.openshift.com/app/account/new)
2. Have installed the [rhc command line tools](https://developers.openshift.com/en/getting-started-client-tools.html)
3. Have setup the rhc command line tools by running `rhc setup`
4. Have added an ssh key via the [online console](https://openshift.redhat.com/app/console/settings) or the `rhc sshkey-add <name> <path to SSH key file>` command
5. Have Mac / Linux :grimacing: (Not really, but Windows users will need to adjust some commands.)


## Let's get started!

1. Navigate to the directory you'd like to create your new blog in
2. Create a new app on OpenShift with the following command: (replacing `<name>` with your desired application name)  
    **Note:** If desired, adding `-s` to the below command will automatically scale the application with traffic. This setting has to be set during application creation, and can not be changed.

    ```bash
    rhc create-app <name> "http://cartreflect-claytondev.rhcloud.com/reflect?github=connyay/openshift-node-diy" "http://cartreflect-claytondev.rhcloud.com/reflect?github=smarterclayton/openshift-redis-cart" mongodb-2.4
    ```
    - What is this command doing?
        - Creating a new rhc app with the provided name.
        - Using node.js via the [connyay/openshift-node-diy](https://github.com/connyay/openshift-node-diy) cartridge
        - Using redis via the [smarterclayton/openshift-redis-cart](https://github.com/smarterclayton/openshift-redis-cart) cartridge
        - Using the default OpenShift mongo cartridge
  
3. After the `create-app` is finished (it will probably take a bit) navigate into the cloned directory (`cd <name>`)
4. Add a reference to PencilBlue upstream  
    `git remote add upstream https://github.com/pencilblue/pencilblue.git`
5. Fetch upstream remote  
    `git fetch upstream`
6. Pull in master from PencilBlue  
    `git reset --hard upstream/master`
7. Create (or download) a config.js file  
    `vi config.js` **or** `curl -O https://gist.githubusercontent.com/connyay/76102b76413588f68d12/raw/config.js`
    Your `config.js` should look like this: 
    {% gist connyay/76102b76413588f68d12 config.js %}
8. Add an `.openshift/action_hooks` directory  
    `mkdir -p .openshift/action_hooks`
9. Create (or download) an .openshift build actionhook  
    `vi .openshift/action_hooks/build` **or** `curl -o .openshift/action_hooks/build https://gist.githubusercontent.com/connyay/76102b76413588f68d12/raw/build`
    Your `build` should look like this: 
    {% gist connyay/76102b76413588f68d12 build %}
10. Make the build action hook executable  
    `chmod +x .openshift/action_hooks/build`
11. git add -> git commit -> git push  
    `git add -A && git commit -m 'Hello PencilBlue!' && git push origin master -f`
12. Visit your new PencilBlue website at: ht<span>tp://</span>&lt;your app name&gt;-&lt;your namespace&gt;.rhcloud.com


## Prefer a shell script? Steps 4-11 can be completed by using this script
(Only tested on Mac)  
`curl https://gist.githubusercontent.com/connyay/76102b76413588f68d12/raw/setup.sh | bash`  
{% gist connyay/76102b76413588f68d12 setup.sh %}


## Demo
A demo of PencilBlue running on Openshift can be found [here](https://pencilblue-connyay.rhcloud.com/article/hello-openshift)
