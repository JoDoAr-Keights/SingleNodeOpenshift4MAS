# SingleNodeOpenshift4MAS
Single Node Openshift for Maximo or something else using Red Hat Cloud Console
This is an example of how to build a single-node openshift cluster on a IBM Fusion Storage box using Red Hat Cloud Console and deploy it on OpenShift Virtualization (OSV) in an OpenShift cluster

## Prerequisites:
- Have access to the Bare Metal Openshift cluster on a Fusion HCI
- Have an account on https://console.redhat.com/

### Provision a server of suitable size on your platform
minimum vCPU's for a single node openshift server is 10 vCPU
<img width="1337" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/fd78821f-5c3b-4650-8c74-63125f26defb">

pick a suitable operating system for the server, RHEL9 is a good choice, it will be replaced by CoreOS during the installation process
<img width="623" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/e6135c9b-df11-4cd1-bf5a-c3b9c2132c7e">

Be sure to uncheck "start this virtual machine after creation" and click Customize
<img width="909" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/bc745616-9afe-4836-9384-18e7677000af">

Select a suitable server name and leave the other parameters on this page, click next
<img width="561" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/fadc53b4-d93a-41dc-94a6-00f8e73a57b5">

On this page, UNCHECK "Start this VirtualMachine after creation", the GUI is unfortunately very persistent in not wanting you to succeed
<img width="1109" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/9b3cdd71-4e11-43dc-8a3d-4dcc8924a50f">

<img width="569" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/b1f92d4c-e6c2-41dc-860e-4578b00088c4">

Select the disks tab ind edit the rootdisk
<img width="1344" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/2e8eb38f-bceb-46f9-925b-e54372b0e1d6">

Increase the PVC size for the root disk, 600 GiB is a good number for a MAS system
<img width="558" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/c3224a6c-1ddf-4f9e-890b-fe18b474b731">

...and uncheck "Start this VirtualMachine after creation"...

Next, go to Network Interfaces, and add a Network Interface.
Give it a nice name and ensure that you select "nad" as Network, and "Bridge" as type

<img width="560" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/27027e02-cae3-4d72-b781-c1ff01c65483">

Note down the MAC address you receive for the new NIC, in this example it is 02:8e:f3:00:00:32
<img width="1327" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/1c83e9a7-e5f3-4215-96d9-ca25dc64563d">








Skapar en maskin med 32 cpu, 128 GiB mem, 600 gib disk, STARTAR INTE maskinen. Lägger till nätverkskort med rätt IP???, får en Mac-adress

### Create the single-node boot cd-rom image needed when starting the installation
