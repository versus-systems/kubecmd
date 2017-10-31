kubecmd
=======

Run commands easily on dedicated deployment's pods.

It creates a pod based on your deployment's container, it runs the command on it, and deletes the pod after it's done.

But why?
You could run your commands directly on a deployment's pod but have in mind that it's the same pod that is running your app, any deployment update can terminate the pod in the middle of your script's execution plus you have to figure out the pod's name.

*kubecmd* makes it easier to run any command creating a dedicated pod based on the specified deployment, it won't go away if a deployment update happens but until it's done with your command and you already know your deployment's name.

## Instalation

* Install [jq](https://stedolan.github.io/jq/).
```bash
brew install jq
```
* Install [kubecmd](https://raw.githubusercontent.com/stevenbarragan/dotfiles/master/kubecmd)
```bash
curl -fsSL https://raw.githubusercontent.com/versus-systems/kubecmd/master/kubecmd > /usr/local/bin/kubecmd
chmod +x /usr/local/bin/kubecmd
```

## Usage

Run any command as: `kubecmd -d <deployment-name> -n <namespace> <command>`

```bash
kubecmd -d my-rails-app rails console          # it opens a rails console on a pod based on my-rails-app deployment on the default namespace
kubecmd -d my-rails-app -n production rails c  # same as above but under the production namespace
```

If you just want to ssh into it, you can run `/bin/sh` or `/bin/bash`.

```bash
kubecmd -d my-app -n namespacename /bin/sh
kubecmd -d my-app -n namespacename /bin/bash
```

Tested on:
- GNU bash, version 3.2.57(1)-release (x86_64-apple-darwin16)
