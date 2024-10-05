### Log in to the IBM Cloud

```bash
ibmcloud login --apikey <key> 
```

### Create a project

- Creating a resource group:
```bash
ibmcloud resource group-create <development>
```

- Check the resources groups:
```bash
ibmcloud resource groups
```

- Select the resource group: 
```bash
ibmcloud target -g <development>
```

- Creating the project:
```bash
ibmcloud ce project create --name <sn-lab>
```

- Creating a **registry secret**:
```bash
ibmcloud ce secret create --name icr-secret /
--format registry --server us.icr.io /
--username iamapikey --password
```

- Check the secret: 
```bash
ibmcloud ce secret list
```

### Container registry

- Create a namespace: 
```bash
ibmcloud cr namespace-add <sn-lab>
```

- Build the image:
```bash
docker build . -t us.icr.io/${SN_ICR_NAMESPACE}/guess-the-capital
```

- Push the image to IBM Cloud:
```bash
docker push us.icr.io/${SN_ICR_NAMESPACE}/guess-the-capital
```

- Deploy the image on IBM CE:
```bash
ibmcloud ce application create --name guess-the-capital /
--image us.icr.io/${SN_ICR_NAMESPACE}/guess-the-capital /
--registry-secret icr-secret --port 80
```

- Check the status:
```bash
ibmcloud ce application get --name guess-the-capital
```

ibmcloud cr images


### IBM Cloud Engine

#### Create an application

```shell
ibmcloud ce app create
```

--name: Name ot the application
--image: Image reference in a a container
--registry-secret: Regstry access

```Shell
ibmcloudd ce app create --name helloworldapp --image us.irc.io/mynamespace/hello_repo --registry-secret myregistry
```

**Run the app**

```Shell
ibmcloud ce app get
```

--name: Name of the application
--output: Ouput format of the application

Example:
> `ibmcloud ce app get --name helloworldapp --ouput url`

**Create tha application**

```Shell
ibmcloud ce application create --name helloworld2 --image us.icr.io/${SN_ICR_NAMESPACE}/helloworld2 --registry-secret icr-secret --port 5000
```

> the command creates the application and also internally sets up the required infrastructure

To update the application:

```Shell
ibmcloud ce application update --name helloworld2 --image us.icr.io/${SN_ICR_NAMESPACE}/helloworld2 --registry-secret icr-secret --port 5000
```

Show the current project status:

```Shell
ibmcloud ce project current
```

#### Deploying the first application

1. Run the following command to see the list of applications that exist.
	`ibmcloud code-engine application list
2.  alternatively use the short command
	`ibmcloud ce app list
3. Deploy the app
	`ibmcloud ce application create --name helloworld --build-source https://github.com/ibm-developer-skills-network/danum-pythonflaskserver  --image us.icr.io/${SN_ICR_NAMESPACE}/helloworld --registry-secret icr-secret --port 5000`
4. Get the details of the app
	 `ibmcloud ce app get --name helloworld`


```Shell
# perform all app updates-related operations
ibmcloud ce application update 
```

--name: Name of the application
--env: Environment variable

```Shell
ibmcloud ce app update --name pet_db_service --env DB_HOST=localhost

ibmcloud ce app get --name pet_db_service
```
The get command display detailed information of the argument

Update application visibility via CLI:
`ibmcloud ce app update` --> receives to main arguments: --name and --visibility
--name: Name of the application
--visiblity: The application visibility 

```Shell
ibmcloud ce app update --name per_db_service --visibility private
```

Update image reerencia via CLI:

```Shell
ibmcloud ce app update --name per_db_service --image us.icr.io/petshop/no_sql_db_service --registry-secret myregistry
```
--image: New Image reference
--secret: Secret to access non-pubic container registry

Update CPU and Memory via CLI:

```Shell
ibmcloud ce app update --name per_db_service --cpu 2 --memory 16GB
```
--cpu: The amount of CPU set for the instance
--memory: The amount of memory set for the instance