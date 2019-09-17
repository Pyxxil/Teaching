---
title: "Virtual Machines"
categories:
  - Teaching
tags:
  - Virtual Machines
  - Hypervisors
  - Operating Systems
toc: true
toc_label: "Contents"
toc_icon: "cog"
---

A Virtual Machine refers to the _emulation_ of a computer system, which we typically refer to as a _guest_. The Virtual Machine runs the same architecture as the machine running the virtualisation software (which is actually the difference between _emulation_ and _virtualisation_), which we refer to as the _host_.

When we talk about Virtual Machines, we often refer to them in manners such as:

 > I have a Linux guest running in VirtualBox.

In this case, we are referring to the _Hypervisor_, VirtualBox, which runs our Linux Virtual Machine.

A Hypervisor is a piece of software, firmware, or hardware which creates and runs the Virtual Machine. In the above scenario, Virtual Box is the hypervisor and Linux is the Virtual Machine we are running. Such Hypervisors come in two different types.

## Types of Hypervisors

While the different types of hypervisors effectively serve the same purpose, they differ in how they carry about their business.

### Type-1 Hypervisors
These types of Hypervisors run directly on the hosts hardware in order to control the guests.

### Type-2 Hypervisors
These types of Hypervisors run on top of a host Operating System as with any other program does. The guests run as a process in the host OS.


The distinction between these two types of Hypervisors has blurred somewhat, as such efforts as Linux's Kernel-Based Virtual Machine (KVM) effectively transform the host OS into a Type-1 Hypervisor.
