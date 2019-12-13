# dockerswarmlearnings_windows10
My experience with Docker Swarm.

> <b>powershell should be configured in PATH.</b>  
Make sure the below PATH is configured in PATH Environment Variable.  
C:\Windows\System32\WindowsPowerShell\v1.0

> <b>executing docker-machine should be done in powershell admin mode or else the below error will come.  
 Below 2 options can be choosed to create Docker Hosts as per your environment<b>  
> docker-machine create --driver hyperv manager1  
> docker-machine create --driver virtualbox manager1

##### Once you execute the above command, make sure you trigger from Powershell or CMD as Administrator.  
Running pre-create checks...  
<b>Error with pre-create check: "Hyper-v commands have to be run as an Administrator"</b>

> <b>Make sure external vswitch is enabled, or else you may face the below issue.</b>  
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
