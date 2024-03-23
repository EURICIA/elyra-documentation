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


## Included Features

### OK
- **code-viewer**
- **services**
- **theme**
- **script-editor**
- **python-editor**
- **ui-components**
- **r-editor**
- **scala-editor**
- **script-debugger**
- **metadata**

**metadata-common**


### Working On
- **code-snippet**
- **pipeline-editor**

### Need to Work On


### To Be Discovered

##code-snippet
Found 7 errors in the same file, starting at: src/CodeSnippetWidget.tsx:178

(elyra) xinchaochen@baker-16 code-snippet % jlpm run build:lib && jlpm run build:labextension:dev
src/CodeSnippetWidget.tsx:178:78 - error TS2345: Argument of type 'CodeCell' is not assignable to parameter of type 'Cell[]'.
  Type 'CodeCell' is missing the following properties from type 'Cell[]': length, pop, push, concat, and 31 more.

178         notebookWidget.model?.sharedModel.insertCells(notebookCellIndex + 1, cell);
                                                                                 ~~~~

src/CodeSnippetWidget.tsx:377:53 - error TS2345: Argument of type '{ placeholder: any; }' is not assignable to parameter of type 'IOptions'.
  Type '{ placeholder: any; }' is missing the following properties from type 'IOptions': rendermime, model, contentFactory

377     const markdownCell = Factory.createMarkdownCell({placeholder});
                                                        ~~~~~~~~~~~~~

src/CodeSnippetWidget.tsx:385:11 - error TS2339: Property 'value' does not exist on type 'CodeCell | MarkdownCell'.
  Property 'value' does not exist on type 'CodeCell'.

385     model.value.text = content;
              ~~~~~

src/CodeSnippetWidget.tsx:395:47 - error TS2339: Property 'toJSON' does not exist on type 'CodeCell | MarkdownCell'.
  Property 'toJSON' does not exist on type 'CodeCell'.

395     const selected: nbformat.ICell[] = [model.toJSON()];
                                                  ~~~~~~

src/CodeSnippetWidget.tsx:515:41 - error TS2339: Property 'refresh' does not exist on type 'IEditor'.

515             this.editors[metadata.name].refresh();
                                            ~~~~~~~

src/CodeSnippetWidget.tsx:535:46 - error TS2339: Property 'value' does not exist on type 'IModel'.

535         this.editors[codeSnippet.name].model.value.text =
                                                 ~~~~~

src/CodeSnippetWidget.tsx:547:13 - error TS2345: Argument of type '{ value: any; mimeType: string; }' is not assignable to parameter of type 'IOptions'.
  Object literal may only specify known properties, and 'value' does not exist in type 'IOptions'.

547             value: codeSnippet.metadata.code.join('\n'),
                ~~~~~


Found 7 errors in the same file, starting at: src/CodeSnippetWidget.tsx:178

Notes:
contentFactory from NotebookPanel is not working as desired.
Unable to resolve the parameter error of type IOptions, don't know what exactly to pass.
Still need to resolve issue wth IEditor and IModel, which is missing from the migration guide.
Might have to search through the source code to resolve it. 

## Latest make clean install error
/Users/xinchaochen/Desktop/RCOS/elyra/packages/python-editor/src/index.ts
  25:10  warning  'CodeEditor' is defined but never used   @typescript-eslint/no-unused-vars
  43:8   warning  'IDisposable' is defined but never used  @typescript-eslint/no-unused-vars

/Users/xinchaochen/Desktop/RCOS/elyra/packages/ui-components/src/FormComponents/DropDown.tsx
  17:8   warning  'Field' is defined but never used                                 @typescript-eslint/no-unused-vars
  23:11  error    Interface name `DropDownProps` must match the RegExp: /^I[A-Z]/u  @typescript-eslint/naming-convention

/Users/xinchaochen/Desktop/RCOS/elyra/packages/ui-components/src/FormComponents/PasswordField.tsx
  16:8  warning  'Field' is defined but never used  @typescript-eslint/no-unused-vars

/Users/xinchaochen/Desktop/RCOS/elyra/packages/ui-components/src/FormEditor.tsx
  22:8  warning  'Field' is defined but never used                     @typescript-eslint/no-unused-vars
  26:3  warning  'RegistryFieldsType' is defined but never used        @typescript-eslint/no-unused-vars
  29:3  warning  'ErrorListProps' is defined but never used            @typescript-eslint/no-unused-vars
  30:3  warning  'ObjectFieldTemplateProps' is defined but never used  @typescript-eslint/no-unused-vars
  31:3  warning  'RJSFSchema' is defined but never used                @typescript-eslint/no-unused-vars

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
