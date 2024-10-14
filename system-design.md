# System Design

## Docker
- Containerization packages a piece of software's source code, dependencies, etc...

## Kubernetes
- Kubernetes allows for the automatic scaling up and down of Docker images to match the dynamic needs of an application.

## Azure DevOps
- Provides a suite of tools used for developing some software from ideation all the way to production.
- Azure Boards: Basically just a **scrum board** dividing development tasks into "New", "Active", "Staging", and "Deployed".
- Azure Repos: Pretty much an integrated Github clone.
- Azure Pipelines: CI/CD tool that tests, run pipelines, etc for any code changes we are making.
    - Define an `azure-pipelines.yml` in the Git repo.
        - `trigger`: Defines which branches when changed will trigger the pipeline.