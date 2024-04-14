```markdown
# Elyra Documentation

This documentation provides a comprehensive guide for working on Elyra. Follow the procedures and steps outlined below for a seamless development experience.

## **Procedure**

1. **Activate the virtual environment:**
    ```bash
    conda activate <env-name>
    ```

2. **Perform a clean installation in development mode:**
    ```bash
    make clean install-dev
    ```

## **Resolve Peer Dependency Warnings**

- Address the peer dependency warnings listed during the yarn install process. Ensure that the versions specified in the warnings are compatible with your project's dependencies.

## **Link and Unlink Packages**

- Fix the linking issues for `pipeline-services` and `pipeline-editor`.

## **Update Packages If Necessary**

- Update `@elyra/pipeline-services`.
- Update `@elyra/pipeline-editor`.

## **Check Dependencies and Fix Warnings**

- Inspect the dependency errors from `untitled.pdf`.
- Run `yarn install` again and carefully review and fix any dependency warnings or errors.

## **Migrate Elyra Extensions to Support JupyterLab 4.x**

- Work from an existing pull request.
- Run the following commands:
    ```bash
    make install
    cd packages/theme
    more packages.json  # Find the command to build
    jlpm run build && jlpm run build::lab extension:dev  # Find and debug the warnings and errors
    ```

    Example PRs:
    - [Elyra PR #3201](https://github.com/elyra-ai/elyra/pull/3201)
    - [lresende-lab4 Branch](https://github.com/lresende/elyra/tree/lresende-lab4)

- Fix yarn linking by deleting `.yarnc.yml` and reinstalling yarn. Alternatively, resolve by installing yarn within `.yarn`.
- Check errors using:
  ```bash
  npm i --legacy-peer-deps
  ```

## **Resolving ERROR: Failed Building Wheel for pyzmq**

- Resolve by updating all conda packages and reinstalling pyzmq.
  ```bash
  conda update --all
  conda install -c conda-forge pyzmq
  ```

- Try upgrading Python, which should work correctly.
  ```bash
  jlpm install
  ```

## **Handling Compilation Errors**

- If errors occur during compilation, address them accordingly.
    ```bash
    jlpm run build:lib && jlpm run build:labextension:dev
    ```

    Example Errors:
    - `TS2339: Property 'id' does not exist on type 'IteratorResult<Widget, any>'.`
    - `TS2614: Module '"@rjsf/core"' has no exported member 'Field'.`

    Fix:
    - Install missing dependencies, e.g., `@lumino/algorithm@2.0.1`.
    - Upgrade `jupyterlab` to a version that supports the extension.

- After the extension compiles, check its functionality:
  ```bash
  jupyter lab --watch
  ```

- Check the theme. Once JupyterLab is open, verify if your theme is applied correctly. Change the theme in JupyterLab by going to `Settings > JupyterLab Theme` and selecting your theme.

## **Troubleshooting Yarn and JupyterLab Versions**

- To change the yarn version:
  ```bash
  yarn set version berry  # Switch to 4.0
  yarn set version 3.5    # or to a specific version
  ```

- Upgrade Jupyter Lab:
  ```bash
  pip install --upgrade jupyterlab
  jupyter lab --version
  ```

- Remove yarn log, clean cache, and switch between yarn versions.

- Note:
  - Jupyter Lab 4.x is using yarn 3.5
  - Every time running make clean install, have to manually update Jupyter Lab from 3.6x to 4.x


## Need to pass test

### OK

**metadata-common**


### Working On
- **services**

### Need to Work On
- **script-editor**
- **pipeline-editor**


### To Be Discovered
- **code-viewer**
- **theme**
- **python-editor**
- **ui-components**
- **r-editor**
- **scala-editor**
- **script-debugger**
- **metadata**
- **code-snippet**

# Elyra Project Documentation

## Overview

This documentation provides guidance on troubleshooting common errors encountered while running tests in the Elyra project.

## Error 1: Corepack/Yarn Version Mismatch on workflow

### Original Issue:
When attempting to prepare and activate Yarn version 3.5.0 using Corepack, the following error is encountered:

```
Preparing yarn@3.5.0 for immediate activation...
node:internal/modules/cjs/loader:1146
  throw err;
  ^

Error: Cannot find module '/home/runner/work/elyra/elyra/.yarn/releases/yarn-3.5.0.cjs'
    at Module._resolveFilename (node:internal/modules/cjs/loader:1143:15)
    at Module._load (node:internal/modules/cjs/loader:984:27)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:135:12)
    at node:internal/main/run_main_module:28:49 {
  code: 'MODULE_NOT_FOUND',
  requireStack: []
}

Node.js v20.12.1
Error: Process completed with exit code 1..
```

### Attempts :
To address the Yarn version mismatch issue, attempted to update the workflow, but unsuccessful as other errors appears:

1. **Enable Corepack**: Corepack is installed globally and enabled using the following commands:
   ```yaml
   - name: Enable Corepack
     run: |
       npm install -g corepack
       corepack enable
   ```

2. **Install and Activate Yarn**: The workflow includes a step to prepare and activate Yarn version 3.5.0 using Corepack:
   ```yaml
   - name: Install and Activate Yarn
     run: |
       corepack prepare yarn@3.5.0 --activate
       yarn --version
   ```

## Error 2: Jest Test Failure in @elyra/services

### Description:
During the execution of Jest tests for the `@elyra/services` project, the following error is encountered:

```
@elyra/services:  FAIL  src/test/services.spec.ts
@elyra/services:  - Test suite failed to run
@elyra/services:     TypeError: Cannot read properties of undefined (reading 'testEnvironmentOptions')
@elyra/services:       at new JSDOMEnvironment (../../node_modules/jest-environment-jsdom/build/index.js:66:28)
@elyra/services: Test Suites: 1 failed, 1 total
@elyra/services: Tests:       0 total
@elyra/services: Snapshots:   0 total
@elyra/services: Time:        1.054s
@elyra/services: Ran all test suites.
```

### Progress:
To address this error, follow these steps:

1. **Review Test Environment Configuration**: Check the test environment setup, particularly the `testEnvironmentOptions`, in the Jest configuration for the `@elyra/services` project.

2. **Debug Test Suite**: Have to inspect the test suite in the `services.spec.ts` file to identify any potential issues with the test setup or environment and make necessary changes.

## Error 3: getIcon is Undefined in Jupyter Lab

### Description:
When testing Elyra in Jupyter Lab, encountered an error indicating that `getIcon` is undefined when attempting to create an r file and other files under elyra. This error typically occurs when attempting to utilize an icon that is not properly defined or imported.

### Progress:

1. **Checked Icon Usage**: Reviewed the code where `getIcon` is used and ensure that it is being called correctly with a valid icon identifier. But still need further investigation base on the documentations for jupyter lab.

## Conclusion
By following the provided steps, you should be able to address the encountered errors and ensure smooth execution of tests and functionality in the Elyra project. If you continue to experience issues, consider reaching out to the project maintainers for further assistance.

## **Additional Resources**
- [JupyterLab Extension Migration Guide](https://jupyterlab.readthedocs.io/en/latest/extension/extension_migration.html)
- [React JSONSchema Form Documentation](https://rjsf-team.github.io/react-jsonschema-form/docs/advanced-customization/custom-widgets-fields/)
- [JupyterLab Documentation](https://jupyterlab.readthedocs.io/en/latest/)
- [JupyterLab API: CodeEditor.IModel](https://jupyterlab.readthedocs.io/en/stable/api/interfaces/codeeditor.CodeEditor.IModel.html)
- [JupyterLab API: UI Components](https://jupyterlab.readthedocs.io/en/stable/api/modules/ui_components.html)
- [TypeScript React FC Props Confusion](https://stackoverflow.com/questions/59988667/typescript-react-fcprops-conf

usion)
- [JupyterLab API: IFormRendererRegistry](https://jupyterlab.readthedocs.io/en/stable/api/interfaces/ui_components.IFormRendererRegistry.html)
- [JupyterLab 4.0 Documentation](https://jupyterlab.readthedocs.io/en/4.0.x/extension/virtualdom.html)
