
MSR Tools project provides utilities to access the processor MSRs and CPU ID directly.

This project is composed of three different user space console applications.

* rdmsr – read MSR from any CPU or all CPUs
* wrmsr – write values to MSR on any CPU or all CPUs
* cpuid – show identification and feature information of any CPU

For more information, visit [project website](https://01.org/zh/msr-tools/overview?langredirect=1).

## Disclaimer

Direct access to MSRs could harm a system. Because `wrmsr` requires root privilege, a root user could corrupt the system in any other ways. But a user is still recommended to be careful when writing values to MSRs. cpuid does not require any privilege to run and CPUID values are immutable.

## Pre-requisite

To use '/dev/cpu/<cpu#>/msr' devices, 'msr' kernel module needs to be loaded. Do it by

```sh
$ modprobe msr
```

Similarly, to use '/dev/cpu/<cpu#>/cpuid' devices, 'cpuid' kernel module needs to be loaded. Do it by

```sh
$ modprobe cpuid
```

## Build msr-tool
```sh
$ ./autogen.sh
$ make
```

Do the following if `/dev/cpu` DOES NOT EXIST on your system:

```sh
# create profile for each CPU core
$ ./MAKEDEV-cpuid-msr
```

## Use msr-tool

Refer to tutorial [here](https://01.org/zh/msr-tools/overview?langredirect=1).

### rdmsr / wrmsr

rdmsr / wrmsr give access to MSRs. Since it operates with '/dev/cpu/<cpu#>/msr' deivce, it requires a root privilege. And it can specify any CPU in a multi-processor system.

```
$ sudo rdmsr -p2 0x10

    => read the register value from Time Stamp Counter MSR 0x10 of CPU 2
```

### cpuid

cpuid reads CPUID values from '/dev/cpu/<cpu#>/cpuid' device and shows a complete CPUID table for the specified processor. It should not require root access.

```
$ cpuid 3

	=> show all CPUID values of CPU 3
```