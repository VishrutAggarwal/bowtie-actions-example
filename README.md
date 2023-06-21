# bowtie-actions-example
A test repository for documenting bowtie in GitHub Actions.



## Documentation outline

- Setup bowtie
- Validate using bowtie


### Setup bowtie

#### **Initial Steps**

- Create `.github/workflows' directory in your repository.
- Create a file with `.yml` extension.
- Enter the following code in the YAML file:

```yaml
name: Setup Bowtie
run-name: ${{ github.actor }} is learning to use Bowtie

on: [push]

jobs:
sets-up-bowtie:
    runs-on: ubuntu-latest

    steps:
    - name: Install Bowtie
        uses: bowtie-json-schema/bowtie@v2023.05.12
```

_This will install bowtie every time you push onto the repository._

#### **Verification Steps**

- Append the following code in the already created YAML file:
```yaml
      - name: Run Bowtie
        run: bowtie --version
```

- The YAML file will look something like this: 
```yaml
name: Setup Bowtie
run-name: ${{ github.actor }} is learning to use Bowtie

on: [push]

jobs:
  sets-up-bowtie:
    runs-on: ubuntu-latest

    steps:
      - name: Install Bowtie
        uses: bowtie-json-schema/bowtie@v2023.05.12

      - name: Run Bowtie
        run: bowtie --version
```

- Push the changes to your repository.
- Go to the `Actions` tab of your repository and wait for the action to complete.
- If the run was successful, you will see a green circle with a tick.
- Click on the Workflow and then click on the ` sets-up-bowtie` Job.
- Open the drop down of the `Run Bowtie` step.
- If it shows something like this, bowtie is running successfully: 
```bash
bowtie, version 2023.6.4
```

> IF THE RUN WAS NOT SUCCESSFUL, YOU WILL SEE A RED CIRCLE WITH A CROSS. RECHECK THE CODE YOU HAVE WRITTEN, AND CORRECT IN CASE OF ANY DISCREPANCY.

_This will help us to test if bowtie is working in the GitHub action._

### Validate using bowtie

Now that you have successfully added bowtie to your workflow, let's work on using it to validate your JSON Specifications.

#### **Add the validate command**

- Add the following code snippet to your YAML file:
```yaml
      - name: Validate Schema
        run: bowtie validate -i lua-jsonschema schema.json instance.json
```
Let's break down this command:

- `bowtie validate`: It tells which command to run.
- `-i`: It is a required flag for `validate` command and specifies which implementation to be used, which in this case is `lua-jsonschema`.
- `schema.json`: It is the name of the file containing the defined schema against which instances will be validated.
- `instance.json`: It is the name of the file containing the instances to be validated.
<!-- [Please note that this can also be a directory.]-->

_You will see that the implementation is skipped and thus does not validate the instances. This is because the lua implementation does not support the default 2020-12 draft._

#### **Change the dialect**

- To change the dialect used by the implementation, change the validate command to this:
```yaml
      - name: Validate Schema
        run: bowtie validate -i lua-jsonschema --dialect 7 schema.json instance.json
```
_This will change the dialect used to draft 7 instead of the default 2020-12._

#### **Use two implementations**

- You might require using two or more different implementations for the same schema and instances. This is how you can get it done:
```yaml
      - name: Validate Schema
        run: bowtie validate -i lua-jsonschema -i python-jsonschema schema.json instance.json
```
_Here we have used just two implementations, namely: python and lua. You may make changes according to your requirements._