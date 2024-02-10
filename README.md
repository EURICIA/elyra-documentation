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
