# Devcontainer
Setting up a dev container can streamline development by standardizing the environment across different systems. Below is a guide to setting up a basic development container using Visual Studio Code (VS Code) and Docker.

### Prerequisites
1. **Docker**: Ensure Docker is installed and running on your machine.
2. **Visual Studio Code**: Install VS Code if you haven't already.
3. **Remote - Containers Extension**: Install the [Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension in VS Code.

### Steps to Set Up a Dev Container

#### 1. Create a New Project or Open an Existing One
Open the folder in VS Code where you want to set up the dev container.

#### 2. Create a `.devcontainer` Folder
In the root of your project, create a folder named `.devcontainer`. This folder will contain the configuration files for the dev container.

#### 3. Create a `Dockerfile` (Optional)
If you need a custom Docker image, create a `Dockerfile` inside the `.devcontainer` folder. Here’s an example of a basic `Dockerfile`:

```dockerfile
# Use an official Python runtime as a parent image
FROM python:3.10

# Set the working directory in the container
WORKDIR /workspace

# Install any needed packages specified in requirements.txt
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the current directory contents into the container at /workspace
COPY . /workspace

# Make port 8000 available to the world outside this container
EXPOSE 8000

# Run the application
CMD ["python", "app.py"]
```

#### 4. Create a `devcontainer.json` File
Create a `devcontainer.json` file inside the `.devcontainer` folder. This file defines how the dev container should be built and configured. Here’s a simple example:

```json
{
  "name": "My Dev Container",
  "build": {
    "dockerfile": "Dockerfile",
    "context": ".."
  },
  "settings": {
    "terminal.integrated.shell.linux": "/bin/bash"
  },
  "extensions": [
    "ms-python.python",
    "dbaeumer.vscode-eslint"
  ],
  "forwardPorts": [8000],
  "postCreateCommand": "pip install -r requirements.txt",
  "remoteUser": "vscode",
  "mounts": [
    "source=/path/on/host,target=/path/in/container,type=bind"
  ]
}
```

- **`build`**: Defines how the Docker image is built.
- **`settings`**: VS Code settings that apply within the container.
- **`extensions`**: List of VS Code extensions to install in the container.
- **`forwardPorts`**: Ports to forward from the container to your local machine.
- **`postCreateCommand`**: Commands to run after the container is created, like installing dependencies.
- **`remoteUser`**: User to be used inside the container.
- **`mounts`**: Bind mount local directories to the container.

#### 5. Reopen Folder in Container
After configuring the `devcontainer.json`, VS Code should prompt you to reopen the folder in a container. You can also do this manually by clicking on the green remote status bar (bottom-left corner of VS Code) and selecting "Reopen in Container".

#### 6. Develop Inside the Container
Once the container is up and running, you can develop as usual. All VS Code features like debugging, terminal, and extensions work inside the container.

#### 7. Version Control
Add the `.devcontainer` folder to your version control system (e.g., Git) so others can use the same environment.

### Customizing Further
You can extend this setup by adding environment variables, additional Docker Compose services, and more.

Let me know if you need help with any specific part of the setup



























V