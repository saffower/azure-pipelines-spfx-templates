# Azure Pipeline Templates for SharePoint Framework Projects

This repo contains job templates for SharePoint Framework (SPFx) projects using Azure Pipelines.

Three different job templates are provided in this project:

- **job-build**: Used for building, bundling & creating the SharePoint `*.sppkg` file for your project.
- **job-test**: Used to execute your tests & publish the resulting JUnit & code coverage report.
- **job-deploy**: Used to upload & deploy the SharePoint package `*.sppkg` file to the specified App Catalog site (*both tenant & site collection scoped are support*).

## Usage

Follow these steps to use the templates in your SPFx project Azure pipeline.

### Step 1: Import job templates into your Azure pipeline

Add a [repository resource](https://docs.microsoft.com/azure/devops/pipelines/yaml-schema?view=azure-devops&tabs=schema#resources)

```yml
# azure-pipelines.yml
resources:
  repositories:
  - repository: azure-pipelines-spfx-templates
    type: github
    name: voitanos/azure-pipelines-spfx-templates
    endpoint: github
```

> Note: If you do not have a `github` service connection in the project hosting your pipeline (or you do not have access to it), you can create one via **Project Settings**. Just make sure the name of this service connection is specified in the `endpoint` field. See [service connections](https://docs.microsoft.com/azure/devops/pipelines/library/service-endpoints?view=azure-devops&tabs=yaml) for more details.

### Step 2: Add the job template to your Azure pipeline

Create a stage for building the project that contains the template:

```yml
# azure-pipelines.yml
- stage: Build
  jobs:
    - template: jobs/build.yml@azure-pipelines-spfx-templates
```

## Templates

This project includes the following templates:

### job-build

This job template does the following:

1. Install all dependencies using Yarn
1. Build the project using `gulp build`
1. Bundle the project using `gulp bundle --ship`
1. Package the solution using `gulp package-solution --ship`
1. Publish the resulting `*.sppkg` as a build artifact named **spfx-package**

#### Parameters

None.

### Requirements

> todo

### Limitations

1. The templates use the Microsoft hosted Linux agent Ubuntu 16.04.
