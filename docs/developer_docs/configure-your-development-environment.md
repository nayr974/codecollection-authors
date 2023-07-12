# Configure Your Development Environment

In order for you to do development on codebundles within your CodeCollection you'll need to prepare a few things in your development environment. As we say on the RunWhen team: "dev how you like to" - we'll provide a few different ways to dev in this doc but ultimately they're not prescriptive so if you find a different way to dev that works for you then go for it! In fact, we'd love to hear about how you're doing dev differently on CodeCollections.

Come have a discussion with us in #codecollection-discussion on the public Slack!

### Method 1:  Devtools Devcontainer

We have an image you can pull and run to do CodeCollection development in. The image provides some scripts, binaries and configuration to get you going faster. There's an available devcontainer spec which uses this image that provides an IDE experience in a sandboxed container.

#### Devcontainer Topology Overview

![DevContainer Topology](/docs/.assets/devcontainer_topology.png)

*Devcontainer Topology from https://code.visualstudio.com/docs/devcontainers/containers*

Here's what the image includes:

* An always-on HTTP server to view robot logs so you can quickly get feedback locally
* Configuration for VSCode to start within the container via [Remote Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)
* Installed Robot Framework and Python dependenices **in the devcontainer environment** via a postcreate command in the devcontainer spec
* Preset pythonpaths for robot framework, `libraries/,` and `codebundles/`&#x20;
* The `kubectl` and `gcloud` binaries for manually interacting with cloud resources
* A dev script called `ro` that shorthands the robot CLI with preset flags for the HTTP server

#### Getting Started

```bash
# First set these for use in the following commands
MY_REPO_GIT_URL=git@github.com:OWNER/REPO.git #eg: git@github.com:jon-funk/my-codecollection.git
MY_REPO_NAME=REPO #eg: my-codecollection

mkdir codecollectiondev && cd codecollectiondev
```

Now we fetch the devcontainer spec:

```bash
git clone $MY_REPO_GIT_URL \
&& mv $MY_REPO_NAME codecollection \
&& mkdir auth && touch auth/auth_files_here \
&& touch .env \
&& wget -O .devcontainer.json https://raw.githubusercontent.com/runwhen-contrib/codecollection-devtools/main/.devcontainer.json
# from this point you'll want to proceed to 'Setting up the Devtools Container'
# you can run 'code .' here to open VSCode
```

> Note: notice the `mv $MY_REPO_NAME codecollection` line, this moves your codecollection source code to a recognized pythonpath, this way you don't need to configure any pythonpaths yourself.

> Note: the codecollection/ path is expected by the postcreate command contained in the devcontainer.json spec

#### Setting up the Devtools Container

First, these steps assume you're within the `codecollection-devtools` directory and have performed the steps in the 'Getting Started' section above.

* Install [Remote Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack) in your VSCode IDE
* Ensure nothing is currently bound to port `3000` locally
*   In VSCode hit `F1` (`ctrl+shift+p` on linux) and select the option: `Remote-Containers: Open Folder In Container` then Hit `OK` as `./` will already be selected.\

![VSCode DevContainer Command](/docs/.assets/vscode.png)

* VSCode will now detect the `.devcontainer.json` contained within and restart in the sandboxed container

> VSCode may take up to 5 minutes for the first-time setup.

* There's a postcreate command that installs packages for you into the container, you can hit any key once it's finished

![The postcreate command running and installing pip packages](/docs/.assets/robot_deps.png)
*The postcreate command running and installing pip packages*



![Container Running](/docs/.assets/container_ps.png)
*DevContainer Running*


### Method 2: Terminal Only

If you're comfortable with a terminal-only experience using an editor such as vim, you can run the container and exec into it. Similar to method 1, prep the local directory:

```bash
# First set these for use in the following commands
MY_REPO_GIT_URL=git@github.com:OWNER/REPO.git #eg: git@github.com:jon-funk/my-codecollection.git
MY_REPO_NAME=REPO #eg: my-codecollection

mkdir codecollectiondev && cd codecollectiondev
```

With docker:

```bash
which docker \
&& git clone $MY_REPO_GIT_URL \
&& mv $MY_REPO_NAME codecollection \
&& mkdir auth && touch auth/auth_files_here \
&& touch .env \
&& docker run -d -p 3000:3000 --user 1000:1000 --env-file .env \
-v ${PWD}/codecollection/:/app/codecollection/:z -v ${PWD}/auth/:/app/auth/:z --name devtools \
us-docker.pkg.dev/runwhen-nonprod-shared/public-images/codecollection-devtools:main-2bdce5a3 \
&& docker exec devtools bash -c \
"pip install --user --no-cache-dir -r /app/codecollection/requirements.txt" \
&& docker exec -it -- devtools bash

```

You can now proceed to running a codebundle locally on the next page!

### Method 3: Codespaces

> This section is under construction, please check back later!

### Method 4: Devtools Container from source

You can build from the source dockerfile located at: [https://github.com/runwhen-contrib/codecollection-devtools](https://github.com/runwhen-contrib/codecollection-devtools)

#### Build Steps

```bash
# First set these for use in the following commands
# this should be the codecollection repo you setup earlier
MY_REPO_GIT_URL=git@github.com:OWNER/REPO.git #eg: git@github.com:jon-funk/my-codecollection.git
MY_REPO_NAME=REPO #eg: my-codecollection

git clone git@github.com:runwhen-contrib/codecollection-devtools.git
cd codecollection-devtools
```

```bash
which docker && which docker compose \
&& git clone $MY_REPO_GIT_URL \
&& mv $MY_REPO_NAME codecollection \
&& touch .env \
&& docker compose up -d devtools \
&& docker compose exec devtools bash -c "pip install --user --no-cache-dir -r /app/codecollection/requirements.txt"
```

Otherwise refer to Method 1 for configuration details post-build. Plus the following steps:

* Requires docker compose >= v2 and docker >= v20
* Run `cp .devcontainer.source.json .devcontainer.json`
* Run`docker compose up -d devtools`
* If desired, you can now attach to the devcontainer


## Up Next: [Running Your First CodeBundle Locally](./running-your-first-codebundle-locally.md)