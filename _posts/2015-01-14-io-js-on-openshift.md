---
layout: post
title: Running io.js on OpenShift
---

## **io.js is still beta stability - so please proceed with caution.**


I threw together a quick [io.js](https://iojs.org/) cartridge that can be used on [OpenShift](https://www.openshift.com/).

Two options for testing:

1. Bare bones cartridge: `rhc create-app <name> http://tinyurl.com/OpenShiftIOJS`
2. Cartridge with an express.js hello world example: `rhc create-app <name> http://tinyurl.com/OpenShiftIOJS --from-code https://github.com/connyay/express-openshift-iojs.git`

You can find the source for the cartridge [here](https://github.com/connyay/openshift-iojs).


I hope you find this useful! If you have any questions feel free to reach out at [@_connyay](https://twitter.com/_connyay)
