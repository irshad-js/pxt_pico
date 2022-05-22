# PXT-PCIO

- Libs are removed from original repo


This repository is a fork/clone from Pxt-maker repository. The pxt-maker repository is stripped off all the targets except the 
Raspberry Pi Pico - RP2040

Some steps and commands to follow:

* Clone pxt-pico and place it along with pxt and pxt-common-packages in a different directory.
* Remove read only persmissions from all repos (There will be builds that will be incompatible with RO permissions)
* Enter pxt-pico and run : npm install
* Run : pxt serve --local
* Extract project files for extension from maker.makecode webpage (have the new project linked to git from where it is now downloadable)
* Enter project folder and Enter custom folder
* Run: pxt build --local --force
* Makecode will compile one static version of the binaries for the RP2040 with the CODAL and one more version of UF2 with the 
  final logic compiled and stitched along with the CODAL binary (the main.ts file in the projects directory will be targetted for the compilation)
  
There will be additional compilation logs attached with this repo.

## Who is this for?

This editor is meant for micro-controllers that are friendly to breadboarding. The editor is based on [Microsoft MakeCode](https://makecode.com).

## Local Dev Server

The local server lets you to run the editor and serve the documentation from your own computer.

### Setup

1. Install [Node.js](https://nodejs.org/) 8.9.4 or higher.
2. Install [Docker](https://www.docker.com/) if you are going to edit any `.cpp` files.
3. Clone the pxt repository.
```
git clone https://github.com/microsoft/pxt
cd pxt
```
4. Install the dependencies of ``Microsoft/pxt`` and build it
```
npm install
npm run build
cd ..
```
5. Clone the ``Microsoft/pxt-common-packages`` repository
```
git clone https://github.com/microsoft/pxt-common-packages
cd pxt-common-packages
npm install
cd ..
```
6. Clone the ``Microsoft/pxt-maker`` repository
```
git clone https://github.com/microsoft/pxt-maker
cd pxt-maker
```
7. Install the PXT command line (add `sudo` for Mac/Linux shells).
```
npm install -g pxt
```
8. Install the pxt-maker dependencies.
```
npm install
```
8. Link pxt-maker back to base pxt repo (add `sudo` for Mac/Linux shells).
```
rm -Rf node_modules/pxt-core
rm -Rf node_modules/pxt-common-packages
pxt link ../pxt
pxt link ../pxt-common-packages
```

If you want to know if your folders are link, run ``ls -l``
and it will indicate them.

```
ls -l node_modules/
```

Note the above command assumes the folder structure of   
```
       maker.makecode.com
          |
  ----------------------------------
  |       |                        |
 pxt      pxt-common-packages  pxt-maker
 ```

### Refresh dal.d.ts files

Whenever you make changes to the ``#defines`` in the .cpp files, you will have to refresh
the ``dal.d.ts`` files. For that, run

```
pxt builddaldts
```

### CODAL changes

If you need to do changes to CODAL itself, follow these steps.

* create a new project in the web editor, then close the web server. Select the hardware you want to work with.
* using a command prompt, open the ``projects`` folder and find the subfolder with your new project
* open the folder in Visual Studio Code
```
code .
```
* open ``pxt.json`` and edit the dependencies to use 
the ``file:...`` path instead of ``*``

```
   dependencies: {
        "adafruit-metro-m0-express": "file:../../libs/adafruit-metro-m0-express"
   }
```
* from the command line, set the ``PXT_NODOCKER`` environment variable to ``1``

```
export PXT_NODOCKER=1
```

* run a local build that will create a CODAL checkout automatically. 
If you are missing tools, you will be notified by the build script.

```
pxt build --local --force
```

* go to the ``built/dockercodal`` folder and open all CODAL in a new Visual Studio Code instance

```
cd built/dockercodal
code libraries/*
```

* go to the Git tab in VS Code, and change the branch of the CODAL repository to work on to ``master``. You can create a new branch to start doing your work and pull requests.

* to build CODAL directly, run ``built/codal``
```
python build.py
```

* to rebuild your project from pxt, run ``pxt build --local --force`` from the project folder

### Running

Run this command from inside pxt-maker to open a local web server
```
pxt serve
```
If the local server opens in the wrong browser, make sure to copy the URL containing the local token. 
Otherwise, the editor will not be able to load the projects.

If you need to modify the `.cpp` files (and have installed yotta), enable yotta compilation using the `--localbuild` flag:
```
pxt serve --localbuild
```

```c


Also:

D:\makecode\pxt_pico>npm install -g glob-exec

added 14 packages, and audited 15 packages in 2s

1 package is looking for funding
  run `npm fund` for details

found 0 vulnerabilities

D:\makecode\pxt_pico>npm run svgo

> pxt-maker@0.15.59 svgo
> glob-exec --foreach "**/boardhd.svg" -- "svgo --config=svgo.yml {{file}} -o {{file.dir}}/board.svg

```

