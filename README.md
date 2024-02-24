# Elyra Documentation

This documentation provides a comprehensive guide for working on Elyra. Follow the procedures and steps outlined below for a seamless development experience.

## **Procedure**

1. Activate the virtual environment.

    ```bash
    conda activate <env-name>
    ```

2. Perform a clean installation in development mode.

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

## **Fix Issue and Push to PR**

- After fixing the issue, create a file with instructions to deploy that one extension.

    Example:
    - [React JSONSchema Form v5.x Upgrade Guide](https://rjsf-team.github.io/react-jsonschema-form/docs/migration-guides/v5.x%20upgrade%20guide/)

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






