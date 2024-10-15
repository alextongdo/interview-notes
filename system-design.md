# System Design

## Docker
- Containerization packages a piece of software's source code, dependencies, etc...

## Kubernetes
- Kubernetes allows for the automatic scaling up and down of Docker images to match the dynamic needs of an application.

<img src="./assets/components-of-kubernetes.svg" height="300">

- Pods (not shown), which do the actual work, are a Kubernetes abstraction for Docker containers.
- Each worker node can contain multiple pods, each of which are (usually) a single application.
- K8s Components:
    - **Service**: Assigns a static IP address to each pod so that they are accessible to each other (even on restart after failure) within a node.
    - **Ingress**: Translates the external (public) service into a readable url where you can access the application pod.
    - **ConfigMap**: Instead of hard coding the API endpoints of other pods into your images, you can use ConfigMap to configure your applications externally from the pod.
    - **Secret**: Same thing as ConfigMap, except better suited to storing private config data like usernames and passwords. These are meant to be encrypted with a 3rd party service.
    - **Volume**: Persistent data storage, even if your pods fail.
    - **Deployment**: Blueprint for pods so that you can replicate many nodes with the same pods for load balancing.
    - **StatefulSet**: Some pods (like a database) can't be replicated via deployments because they rely on some external state. Use a StatefulSet instead.

## Azure DevOps
- Provides a suite of tools used for developing some software from ideation all the way to production.
- Azure Boards: Basically just a **scrum board** dividing development tasks into "New", "Active", "Staging", and "Deployed".
- Azure Repos: Pretty much an integrated Github clone.
- Azure Pipelines: CI/CD tool that tests, run pipelines, etc for any code changes we are making.
    - Define an `azure-pipelines.yml` in the Git repo.
        - `trigger`: Defines which branches when changed will trigger the pipeline.
        - `vmImage`: Defines what type of machine will run the pipeline.
        - `stage > jobs > job > step > task`: Defines the steps the pipelines will take. 