    v To run a workflow manually, the workflow must be configured to run on the workflow_dispatch event.
    v events can be:
        • Events that occur in your workflow's repository
        • Events that occur outside of GitHub and trigger a repository_dispatch event on GitHub
        • Scheduled times
        • Manual
    v to trigger a workflow run following steps are occur:
        1. An event occurs on your repository. The event has an associated commit SHA and Git ref.
        2. GitHub searches the .github/workflows directory in the root of your repository for workflow files that are present in the associated commit SHA or Git ref of the event.
        3. A workflow run is triggered for any workflows that have on: values that match the triggering event. Some events also require the workflow file to be present on the default branch of the repository in order to run.
    
    v Using events to trigger workflows
        on: push
        ○ triggers when push is made to any branch in workflow's repository
        ○ we can use multiple events also:
            § on: [push, fork]
        ○ If multiple triggering events for your workflow occur at the same time, multiple workflow runs will be triggered.
    v Using activity types and filters with multiple events
        labels only works when issue is created inside workflow code not from github ai 
        For example, a workflow with the following on value will run when:
            • A label is created
            • A push is made to the main branch in the repository
            • A push is made to a GitHub Pages-enabled branch
        on:
  label:
    types:
      - created
  push:
    branches:
      - main
  page_build:
    v Using filters
        ○ the push event has a branches filter that causes your workflow to run only when a push to a branch that matches the branches filter occurs, instead of when any push occurs.
        ○ on:
  push:
    branches:
      - main
      - 'releases/**'
        ○ on:
  pull_request:
    branches:
      - 'releases/**'
      - '!releases/**-alpha'
    v Example: Including paths
          If at least one path matches a pattern in the paths filter, the workflow runs. For example, the following workflow                 would run anytime you push a JavaScript file (.js).
    ○ on:
  push:
    paths:
      - '**.js'
    ○ Example: Excluding paths
    When all the path names match patterns in paths-ignore, the workflow will not run. If any path names do not match patterns in paths-ignore, even if some path names match the patterns, the workflow will run.
    A workflow with the following path filter will only run on push events that include at least one file outside the docs directory at the root of the repository.
    
    ○ on:
  push:
    paths-ignore:
      - 'docs/**'
    ○ a workflow with the following trigger will only run when the workflow named Build runs on a branch whose name starts with releases/:
        ○ on:
  workflow_run:
    workflows: ["Build"]
    types: [requested]
    branches:
      - 'releases/**'
    v Using conditionals
        on:
  issues:
    types:
      - labeled
        jobs:
  run_if_label_matches:
    if: github.event.label.name == 'bug'
    runs-on: ubuntu-latest
    steps:
      - run: echo 'The label was bug'
        
    
        
        
        
        
    
        
        
            
        
    
    
        
    
        
    
    
