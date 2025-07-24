# Sphinx Deployment Test

This repository is used to test the build and deployment of 
NIU's Sphinx websites.

We deploy most of our website by combining two of [our re-usable GitHub Actions](https://github.com/neuroinformatics-unit/actions) in a workflow:
- [build_sphinx_docs](https://github.com/neuroinformatics-unit/actions/tree/main/build_sphinx_docs)
- [deploy_sphinx_docs](https://github.com/neuroinformatics-unit/actions/tree/main/deploy_sphinx_docs)

Whenever we make a change to these actions, we ran the risk of breaking the deployment of our Sphinx websites.
This repository allows us to test the changes before applying them to our main repositories.

## Usage

First create a Draft Pull Request (PR) to [our actions repository](https://github.com/neuroinformatics-unit/actions)
with you desired changes. Let's assume the branch of your PR is `my-changes`.

Then, edit the [workflow file](.github/workflows/docs_build_and_deploy.yml) in this repository.
Replace the respective action links with:
```yaml
- uses: neuroinformatics-unit/actions/build_sphinx_docs@my-changes
# and/or
- uses: neuroinformatics-unit/actions/deploy_sphinx_docs@my-changes
```

Make sure the rest of the workflow closely reflects the one used in the target repository,
i.e. the one you intend to actually deploy with the updated actions.

Finally, push the changes to this repository and wait for the build step to successfully complete in CI.
If you also want to test the deployment step, you may need to trigger it via manual workflow dispatch
or via pushing a tag to the `main` branch (depending on the workflow configuration).

You probably also want to examine the deployed test website at <http://neuroinformatics.dev/sphinx-deployment-test/>
