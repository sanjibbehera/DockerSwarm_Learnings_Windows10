# dockerswarmlearnings_windows10
My experience with Docker Swarm.

> <b>powershell should be configured in PATH.</b>  
Make sure the below PATH is configured in PATH Environment Variable.  
C:\Windows\System32\WindowsPowerShell\v1.0

> <b>executing docker-machine should be done in powershell admin mode or else the below error will come.  
 Below 2 options can be choosed to create Docker Hosts as per your environment<b>  
> docker-machine create --driver hyperv manager1  
> docker-machine create --driver virtualbox manager1

##### Make sure you trigger the above cmd from Powershell or CMD as Administrator or else the below error will come.  
Running pre-create checks...  
<b>Error with pre-create check: "Hyper-v commands have to be run as an Administrator"</b>

### Make sure external vswitch is enabled, or else you may face the below issue.  
no External vswitch found. A valid vswitch must be available for this command to run.

#### Create a virtual switch by using Windows PowerShell, if it is not available in your Windows.

> <b>Find existing network adapters by running the Get-NetAdapter cmdlet.</b>  
--> Get-NetAdapter

> <b>Create a virtual switch by using the New-VMSwitch cmdlet.</b>  
--> New-VMSwitch -name ExternalSwitch  -NetAdapterName Ethernet -AllowManagementOS $true

> <b>To create an internal switch, run the following command.</b>  
--> New-VMSwitch -name InternalSwitch -SwitchType Internal

> <b>To create an private switch, run the following command.</b>  
--> New-VMSwitch -name PrivateSwitch -SwitchType Private

#### Once the manager node is created, creae rest nodes as per your requirement.
> docker-machine --debug create -d hyperv dockernode1  
docker-machine --debug create -d hyperv dockernode2  
docker-machine --debug create -d hyperv dockernode3

#### Initialize Master node into Docker Swarm.
> docker-machine ssh manager1  
docker swarm init --advertise-addr <Manager1 IP>  
<b>[You can find out the IP by the command: docker-machine ip manager1]</b>
 
#### Join the worker nodes into Docker Swarm.
> docker-machine ssh dockernode1  
<b>docker swarm join --token <SWARM TOKEN ID GENERATED AFTER DOCKER SWARM MANAGER INITIALIZED> <MANAGER NODE IP>:2377</b>  
[SAME SHOULD BE DONE FOR THE REST WORKER NODEs].
 
### IF WE NEED ADDITONAL DOCKER SWARM MANAGER.
> docker-machine --debug create -d hyper manager2  ## create an additional docker manager host.  
docker-machine ssh manager2  ## ssh into the newly created manager  
docker swarm join-token manager   ## execute this command to generate a token from the actual manager.  
docker swarm join --token <SWARM TOKEN ID GENERATED> <MANAGER IP>:2377
 
 
