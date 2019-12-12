# dockerswarmlearnings_windows10
My experience with Docker Swarm.

-- powershell should be configured in PATH.

-- executing docker-machine shud b done in powershell admin mode.
PS C:\docker_learnings\swarm> docker-machine create --driver hyperv manager1
Running pre-create checks...
Error with pre-create check: "Hyper-v commands have to be run as an Administrator"

-- no External vswitch found. A valid vswitch must be available for this command to run.

Create a virtual switch by using Windows PowerShell.

Find existing network adapters by running the Get-NetAdapter cmdlet.
--> Get-NetAdapter
Create a virtual switch by using the New-VMSwitch cmdlet.
--> New-VMSwitch -name ExternalSwitch  -NetAdapterName Ethernet -AllowManagementOS $true
To create an internal switch, run the following command.
--> New-VMSwitch -name InternalSwitch -SwitchType Internal
To create an private switch, run the following command.
--> New-VMSwitch -name PrivateSwitch -SwitchType Private
