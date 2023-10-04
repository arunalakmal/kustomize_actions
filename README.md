# Kustomize GitHub Actions

The main purpose of this action is updating the [GitOps](https://www.gitops.tech/) repository and rollout the new image changes to the respective environments. As the underline technology `[Kustomize](https://kustomize.io/)` which is the Kubernetes native configuration management tool is used. Idea was to have a pipeline in the GitOps manifest repository, triggers based on an event such as completion of `CI` workflow.

This action will set the new image and perform a commit to the repository. Each usage of this action will have it's own commit in the git history.

# Usage

This pipeline can be used as below, main requirement is all the inputs should be specified and otherwise it will be failed during the parameter check, also `Kustomize` will validate the environment before it updates the images. 

```
- name: Application Image Deployment
  uses: arunalakmal/kustomize_actions@v1
  with:
    bot_name: "ImageUpdater"
    path: "envs/development"
    image: 'arunalakmal/application-image'
    tag: '0.0.1'
    version: "v4.5.7"
```

__Parameters (inputs) Explanation__

+ `bot_name` - Account Name which commits to the repository.
+ `path` - Relative path to the `Kustomize` environment.
+ `ìmage` - The application image repository.
+ `tag` - Image tag which should be deployed. 
+ `version` - The `Kustomize` version. (Tested with version 4.5.7)

# Limitations

This action will perform an automatic commit and it shouldn't be blocked by a rule. Alternatively, may be a special account such as a `Service Account` should be used to perform the Operation and that account should be having a special rule to ignore the GitHub rules. 

What else we can do, may be we can update to push as a `force` push in the action and GitHub rules shoul allow it. 

Otherwise, manual `PR` should be used for your image updates. 
