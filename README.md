# elyra-documentation

**Procedure**
conda activate <env-name>
make clean install-dev


**Resolve Peer Dependency Warnings**
- Address the peer dependency warnings listed during the yarn install process. Ensure that the versions specified in the warnings are compatible with your project's dependencies.
**Link and Unlink Packages**
Fix the linking issues for pipeline-services and pipeline-editor

**Update Packages If Necessary**
- @elyra/pipeline-services
- @elyra/pipeline-editor 

**Check Dependencies and Fix Warnings**
- Inspects the dependencies errors from untitled.pdf. 
- Run yarn install again and carefully review and fix any dependency warnings or errors.

**Migrate elyra extensions to support JupyterLab 4.x**
How to work from existing pr.
- make install
- cd packages/theme
- more packages.json -> find the commond to build
- jlpm run build && jlpm run build::lab extension:dev -> find and debug the warnings and errors

https://github.com/elyra-ai/elyra/pull/3201
https://github.com/lresende/elyra/tree/lresende-lab4

Fixed yarn linking by deleting the .yarnc.yml and reinstalling yarn
Or can be resolved by installing yarn within .yarn

Checking errors:
npm i --legacy-peer-deps 


**Resolving   ERROR: Failed building wheel for pyzmq**
ERROR: Could not build wheels for pyzmq, which is required to install pyproject.toml-based projects

conda update --all
conda install -c conda-forge pyzmq

Trying to upgrade python
Which seems to work correctly.

jlpm install


Errors:
(elyra) xinchaochen@nuthatch-402 theme % jlpm run build:lib && jlpm run build:labextension:dev

src/index.ts:69:18 - error TS2339: Property 'id' does not exist on type 'IteratorResult<Widget, any>'.
  Property 'id' does not exist on type 'IteratorReturnResult<any>'.

69       if (widget.id === 'jp-MainLogo') {
                    ~~

src/index.ts:71:29 - error TS2339: Property 'node' does not exist on type 'IteratorResult<Widget, any>'.
  Property 'node' does not exist on type 'IteratorReturnResult<any>'.

71           container: widget.node,
                               ~~~~

src/index.ts:72:11 - error TS2345: Argument of type '{ container: any; justify: string; margin: string; height: string; width: string; }' is not assignable to parameter of type 'IProps'.
  Object literal may only specify known properties, and 'justify' does not exist in type 'IProps'.

72           justify: 'center',
             ~~~~~~~

src/launcher.tsx:27:10 - error TS2305: Module '"@lumino/algorithm"' has no exported member 'ArrayIterator'.

27 import { ArrayIterator, each, IIterator } from '@lumino/algorithm';
            ~~~~~~~~~~~~~

src/launcher.tsx:27:31 - error TS2305: Module '"@lumino/algorithm"' has no exported member 'IIterator'.

27 import { ArrayIterator, each, IIterator } from '@lumino/algorithm';
                                 ~~~~~~~~~


Found 5 errors in 2 files.

Errors  Files
     3  src/index.ts:69
     2  src/launcher.tsx:27
(elyra) xinchaochen@nuthatch-402 theme % 
jlpm add @lumino/algorithm@2.0.1 

npm list @lumino/algorithm
https://lumino.readthedocs.io/en/latest/migration.html
	upgrade api to latest


Building extension in .
An error occurred.
ValueError: Extensions require a devDependency on @jupyterlab/builder@^3.6.7, you have a dependency on 4.1.1
See the log file for details:  /var/folders/g0/58s2gb0j08350ftl0tvbd_zc0000gn/T/jupyterlab-debug-hjlhm2bx.log
(elyra) xinchaochen@nuthatch-402 theme % jupyterlab --version
zsh: command not found: jupyterlab

Fixed by upgrading jupyter lab
Do: pip install --upgrade jupyterlab
Check: jupyter lab --version

After the extension complied, check working:
// jupyterlab in dev mode
jupyter lab --watch

Check the theme. Once JupyterLab is open, you can check if your theme is applied correctly. You can change the theme in JupyterLab by going to Settings > JupyterLab Theme and selecting your theme.


