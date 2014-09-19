---
layout: post
title: A workaround for --from-code on openshift
---

I have been unable to get the `--from-code` flag to work on openshift... I may be doing something incorrectly, but I am not sure. Every attempt I make results in 504 errors and an overall bad time.

Here is what I am talking about:  
`rhc create-app <app-name> "http://cartreflect-claytondev.rhcloud.com/reflect?github=connyay/openshift-node-diy" --from-code https://github.com/connyay/rh-labs-angular.git`

After getting frustrated with this, I wrote a script. I integrated this script into my cartridge and have found it very useful.

{% gist connyay/8c0f4eeb9ec6e617da48 init.sh %}

### Usage

Make the app  
`rhc create-app <app name> "http://cartreflect-claytondev.rhcloud.com/reflect?github=connyay/openshift-node-diy"`

Go into the directory  
`cd <app name>`

Lay down your code  
`./init.sh -r <your repo> -t <your tag> -n <app name>`

How I use the script (as an example)

`./init.sh -r connyay/rh-labs-angular -t 1.0.1 -n <app name>`


### What the script does

1. Removes everything from the directory except for the init script, and the .git directory.
2. Downloads the tarball for the repository at the optional tag.
3. Replaces references to the 'boilerplate app name' to the optional name
4. Does the first git push to the repository. (can be disabled with `-no-push`)


I hope you find this useful! If you have any questions feel free to reach out at [@_connyay](https://twitter.com/_connyay)
