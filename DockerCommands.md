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

`

### Run an Application

` dotnet run `
