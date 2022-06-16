# DockerDotNetCore 
This application can be deploy and test on local machine and Docker Environment

## Local Deployment and Testing

### Create an Application

` dotnet new console -o App -n DotNet.Docker `

### Structure of an Application
`
📁 docker-working
    └──📂 App
        ├──DotNet.Docker.csproj
        ├──Program.cs
        └──📂 obj
            ├── DotNet.Docker.csproj.nuget.dgspec.json
            ├── DotNet.Docker.csproj.nuget.g.props
            ├── DotNet.Docker.csproj.nuget.g.targets
            ├── project.assets.json
            └── project.nuget.cache

Edit me to generate
  a
    nice
      tree
        diagram!
        :)
  Use indentation
    to indicate
      file
      and
      folder
      nesting.
    - You can even
      - use
        - markdown
        - bullets!

https://tree.nathanfriend.io/

Edit me to generate
├── a
│   └── nice
│       └── tree
│           ├── diagram!
│           └── :)
└── Use indentation
    ├── to indicate
    │   ├── file
    │   ├── and
    │   ├── folder
    │   └── nesting.
    └── You can even
        └── use
            ├── markdown
            └── bullets!

https://ascii-tree-generator.com/

`

### Run an Application

` dotnet run `

### Publish .Net App
` dotnet publish -c Release `

### Create the Dockerfile

```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env `
WORKDIR /app

# Copy everything
COPY . ./
# Restore as distinct layers
RUN dotnet restore
# Build and publish a release
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "DotNet.Docker.dll"]
```


### Directory Structure is:
📁 docker-working
    └──📂 App
        ├── Dockerfile
        ├── DotNet.Docker.csproj
        ├── Program.cs
        ├──📂 bin
        │   └──📂 Release
        │       └──📂 net6.0
        │           └──📂 publish
        │               ├── DotNet.Docker.deps.json
        │               ├── DotNet.Docker.exe
        │               ├── DotNet.Docker.dll
        │               ├── DotNet.Docker.pdb
        │               └── DotNet.Docker.runtimeconfig.json
        └──obj 📁


### Build Docker Image
``` docker build -t counter-image -f Dockerfile . ```

### Check Docker Image Build or not
``` docker images ```

### Create Container

``` docker create --name core-counter counter-image ```

### Check in Stop Container List

``` docker ps -a  ```

### Manage the Container
``` docker start core-counter ```

### Check Running Container
``` docker ps ```

### Connect to Container
``` docker attach --sig-proxy=false core-counter ```

In this the --sig-proxy=false parameter ensures that Ctrl+C will not stop the process in the container.


### Stop Container
``` docker stop core-counter ```

### Check if exists or not
``` docker ps ```

### Delete Container
``` docker rm core-counter ```


### Single Run Command
``` docker run -it --rm counter-image ```
    OR
``` docker run -it --rm counter-image 3 ```

### Change Entry Point if you want
``` docker run -it --rm --entrypoint "cmd.exe" counter-image ```