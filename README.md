# learning-pentaho-with-senthil

This repository is dedicated to exploring and learning Pentaho, a versatile data integration and analytics platform. Here, you'll find various examples, tutorials, and resources focused on ETL processes, data lake management, reporting, and visualization using Pentaho. The goal is to provide insights and practical knowledge for anyone looking to harness the power of Pentaho in their data engineering projects. Join me on this journey to master data management and analytics with Pentaho!

## Deploying Pentaho Carte Server in Firecracker VM at Fly.io

**Firecracker** is a lightweight virtualization technology designed to run microVMs (micro virtual machines) efficiently. **Fly.io** is a platform that allows you to deploy applications globally with minimal latency, utilizing Firecracker for fast, scalable deployment. It’s important to note that Firecracker is not Docker; it offers a different approach to virtualization, emphasizing speed and resource efficiency.

**Carte** is a lightweight web container that allows you to set up a dedicated, remote ETL server, making it easier to manage and execute Pentaho jobs.

## Pre-requisites

- [ ] Fly.io account
- [ ] [flyctl CLI](https://fly.io/docs/getting-started/launch/) to be installed.
- [ ] `fly.toml` deployment configuration file
- [ ] Pentaho Developer Edition 10.2.0.0-222. This requires registration before you download.

### Preparing the Code

- Clone the repository: 

```bash
git clone https://github.com/senthilsweb/learning-pentaho-with-me.git
```

- Navigate to the Fly.io deployment folder:

```bash
cd learning-pentaho-with-me/deployment/fly.io
```

- Ensure that you have a `fly.toml` file located in the root of your repository.

- Download the Pentaho Developer Edition `pdi-ce-10.2.0.0-222.zip` and extract it.

- After everything is done, the folder structure should look like this:

```
.
├── fly.toml
├── pdi-ce-10.2.0.0-222 (<you have to download the zip file and extract the contents>)
├── Dockerfile
├── setups
│   ├── config-files
│   │   ├── carte.xml
│   │   ├── repositories.xml
│   │   └── metastore
│   └── jdbc-drivers
│       └── (JDBC driver files. I kept it as empty)
└── jobs
    └── (PDI job files and example datasets)
```

## Deployment at Fly.io

- **Install flyctl**
```

curl -L https://fly.io/install.sh | sh
```
- **Sign in to your Fly.io account**
```
fly auth login
```
- **Launch the Carte server named `learn-pentaho-with-senthil`**
```
fly launch
```
- **Follow the command prompt**

- **Check your app’s status**
```
fly status
```

## Visit the Application 

Visit the `carte` server at [https://[your-app-name].fly.dev/kettle/status](https://learn-pentaho-with-me.fly.dev/kettle/status/). Basic authentication is enabled; in the prompt, enter the login credentials as `cluster` for both the username and password (or whatever you set).

### API Endpoints Example

You can use the following API endpoint to execute a transformation:

```
GET https://learn-pentaho-with-me.fly.dev/kettle/executeTrans?trans=/path-to/your-transformation-file.ktr
```

### Curl Command Example

To execute the transformation via `curl`, use the following command:

```bash
curl --location 'https://learn-pentaho-with-me.fly.dev/kettle/executeTrans?trans=/path-to/your-transformation-file.ktr' \
--header 'Authorization: Basic username:password'
```

## Miscellaneous flyctl Commands

```
# Deploy changes
fly deploy
# Delete the app
fly apps destroy [your-app-name]
# List mounted volumes
fly volumes list      
```

