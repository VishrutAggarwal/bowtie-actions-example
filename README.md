# bowtie-actions-example
A test repository for documenting bowtie in GitHub Actions.



## Documentation outline

- Setup bowtie
- Validate using bowtie


### Setup bowtie

#### Initial Steps

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

#### Verification Steps

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