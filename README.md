# Unraid Scripts

A personal collection of scripts for Unraid Server. These scripts can be executed via SSH, console, or through the User Scripts plugin.

(Currently in use on Unraid v7.0.0-rc.2)

## [vm_cycle.sh](vm_cycle.sh)

Designed for resource-sharing VMs (such as gaming/mining VMs sharing the same GPU), this script cycles through a list shutting down one VM and starting the next, with some error handling (restarting the original VM if startup fails).

* The user must set `VM_NAMES` upon import.

If executed from within a VM on the list, run it in the background to prevent script termination upon VM shutdown.

Inspired by [a tutorial video by SpaceInvader One](https://www.youtube.com/watch?v=QoVJ0460cro).

## [vm_start_shared_gpu.sh](vm_start_shared_gpu.sh)

Intended for use when passing the same GPU to both a VM and a Docker container.

This script automatically starts the VM in a detached screen session and then stops the container, allowing the VM to utilize the GPU. Once the VM is stopped, the container is automatically started again. This allows for seamless sharing of a single GPU between VMs and Docker containers alternating resource reservation.

* The user must set `VM_NAME` and `CONTAINER_NAME` variables upon import.
* If both `COMPOSE_FILE_PATH` and `ENV_FILE_PATH` are set, the script stops the container and starts a new one, using the new env file. Gpu access should be disabled by this env file provided by the user.

## [vm_bind_usb_devices.sh](vm_bind_usb_devices.sh) (⚠️WIP)

Binds USB devices to a VM until successful (or timeout occurs). Currently a Work In Progress (WIP) and is missing important functionality.

* The user must set `VM_NAME` and `DEVICES_LIST` upon import.

This script is intended to address the issue of permanently binding USB devices to a VM, which requires these devices to be connected at startup.  To work around this, the script binds devices on each VM startup, ensuring proper VM startup even when using KVM switches or other devices. This offers a not so convenient solution of binding through this script, but works around the issue.
