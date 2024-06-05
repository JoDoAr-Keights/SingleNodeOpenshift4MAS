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

...and uncheck "Start this VirtualMachine after creation"...

<img width="1237" alt="Screenshot_2024-06-03_12 26 34" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/d516c683-0b8b-4f87-ae00-e14f077f1043">

**time to click Create**
Machine should now be created and be in state "Stopped"

---

Select OpenShift in the Red Hat Hybrid Cloud Console
<img width="827" alt="Screenshot_2024-06-03_14 20 36" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/4740ef10-5e2d-4aba-8d48-b5c34e93ea1c">

---

Click Create Cluster
<img width="647" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/9818dd07-080f-47e9-bcca-876c7a273c99">

<img width="1589" alt="Screenshot_2024-06-03_14 25 57" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/91f885ec-eaca-45cf-bb5f-8822c6fa2227">

---

Select Interactive<br>
<img width="663" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/23c102e0-bbd2-4303-8395-294186c3a9c3">

---

<img width="995" alt="Screenshot_2024-06-03_14 38 06" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/2aad57ac-b2f8-4b81-b0fa-32641182d2f4">

---

When installing in a Fusion HCI (and probably any other Hyper-Converged Infrastructure) add the VLAN ID. Enter a DNS, recommend to use Quad 9 (9.9.9.9) which is a safer DNS service.
<img width="1385" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/ebc20ce8-d901-4b13-82e8-8ad2c5092739">
and click Next

---

Enter the MAC address you received before and an IP address.
![Screenshot_2024-06-05_10 14 46](https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/8546ffe6-2848-4991-9293-738442b24390)

---

Select to install the Logocal Volume Manager Operator
![image](https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/aa32aeca-50c6-431c-a6cb-142e1fa0d462)
click Next

---

Click Add host
![image](https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/b492e6c9-3c28-4bb3-8d82-738574667cb6)

---

and build a boot CD-ROM (Full image file) to be mounted as boot media when starting the machine, click Generate and you will get a Discovery ISO URL, copy it
![image](https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/92d8efa1-0ee0-433b-baca-c3fe5f726b35)

---

Move to the machine you have prepared on the Fusion HCI and add a disk
<img width="1355" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/dcb0f7bb-30ad-4522-88cb-12271af89a45">

---

create a new CD-ROM and set it first in boot order
<img width="561" alt="Screenshot_2024-06-05_10 26 20" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/13c539bb-f65e-498d-a424-4f30de340497">

---

<img width="262" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/dba0eb3a-0f7a-4ed4-b503-8daf87f72a20"><br>
wait for provisioning to be finished, ie that OSV has downloaded the ISO and stored in onto a virtual CD-ROM
<img width="396" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/6c79e1d6-fc3f-467e-9807-629062c60b59"><br>
after a couple of minutes...
<img width="380" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/5f21a83f-e1ae-47fc-8db8-965c15390e3e">

---

Time to start the new single node openshift server
<img width="1344" alt="image" src="https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/9c1a4a7f-dfa2-48e6-aa83-2cca96abdf3e">

---

This is the result of a succesful installation, screenshot is from older installation in order to finalize this documentation
![image](https://github.com/DougAtIBM/SingleNodeOpenshift4MAS/assets/18483022/b0f69ead-167e-4ba1-881a-c68d5de0522a)

