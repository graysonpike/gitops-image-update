# GitOps: Update Image

This GitHub Action updates the Image in a GitOps repository. It's designed to streamline the process of modifying image tags in your infrastructure-as-code (IaC) setups.

Example Usage:

```yaml
jobs:
    push_to_registries:
        name: Build, push, and update GitOps repo
        runs-on: self-hosted
        steps:
            - name: Update image tag in resy-bot-gitops repository
                uses: 'graysonpike/gitops-image-update'
                with:
                REPOSITORY_NAME: 'TripleZip/triplezip-gitops'
                ACCESS_TOKEN: ${{ secrets.GITOPS_REPO_PAT }}
                BRANCH: "main"
                VALUES_FILE_PATH: 'api/deployment.yaml'
                VALUE_PATH: 'spec.template.spec.containers[0].image'
                IMAGE: 593793025909.dkr.ecr.us-east-1.amazonaws.com/triplezip-api:${{ steps.extract_tag.outputs.TAG }}
                DEPLOYMENT_NAME: 'triplezip-api'
```
