# GanetiCon 2018

The GanetiCon 2018 was held on September 25th and 26th in Duesseldorf, Germany.

## Talks & Sessions

Following you will find a list / short summaries of the sessions held during the first day of the conference

### Ganeti setup at sipgate / Best Practices

TBD

### Ganeti Control Center / Do we need another web interface?

TBD

### Ressource management in Ganeti

TBD

### Thoughts on the past and current state of the Ganeti community

[sildes](ganeti_status.pdf) from talk "Status of Ganeti"

### Live Demo of different ganeti hacks/improvements

- Demo #1: yet another console solution (using websockify/novnc)
  - [idea described at ganeticon 2017](https://github.com/ge-fa/ganeti-presentations/blob/master/2017/GanetiCon/ganeti_at_gisa-sascha_lucas.pdf)
  - goals:
    - small enough to run on ganeti cluster (master node)
    - single point of contact (master IP/name, only one port)
    - secure (HTTPS encryption, HTTP basic auth, ACLs to consoles via groups i.e. LDAP groups, no need to expose VNC to public network -> 127.0.0.1 is enough)

- Demo #2: grow a disk online (without instance reboot)
  - this solves [Issue #28](https://github.com/ganeti/ganeti/issues/28) via a hook script
  - hook script catn be found [here](https://github.com/saschalucas/ganeti-hook-grow-disk)
  
- Demo #3: DRBD out of sync from userspace
  - this is the same as this [thread](https://groups.google.com/forum/#!msg/ganeti/GRVFKv0sVjY/L4JmCdeHAwAJ;context-place=forum/ganeti) on the ML
  - and this k.o. [bug](https://bugzilla.kernel.org/show_bug.cgi?id=99171)
  
- Hint #4: be aware of kvm:cpu_type to use a IBRS (spectre/meltdown) protected CPU type

### Current state of the debian packages

TBD

### (Possible) future of the Ganeti project / community

TBD

## Scripts and resources shared during the conference
- [Ganeti Tools by FHD](https://colorfreedom.org/fhd/ganeti-tools)

## Workshops, sprints etc.

Workshops, sprints etc. held during the second day of the conference.

### ganeti.org content fixes

Following some findings and comments on the state of various resources for information:

www aka https://github.com/ganeti/website

* Sanitize next-level links to Documentation, Source, Downloads
* Clear out what is /rendered/ where and how
* Identify the actual up-to-date-state of the information, this leads to investigation of "ganeti/docs" and features
* Move "Development" information to i.e. to "ganeticon/ganeti" (the ganeti source repo, where the development are taking place), and remove CLA
* Fix/Remove linkage to "wiki" or keep it and bring it up-to-date, too. See "wiki"
* Issue tracker links is down. Just point the the corresponding github issue page?


wiki aka https://code.google.com/p/ganeti.wiki/
* git remote url is down, but Georg has a local copy and can push it to "ganeticon" (maybe mark it as old and/or legacy)
* Summarize the state and compare to the other sources

docs aka https://github.com/ganeti/docs

* Needs massive house keeping
* Volunteers needed to check the truth of the information and keep in sync with Apollon when and how which defaults will be changed.
* Some kind of best practices or at least various simple setups need to be handled differently
* Group content into install-, admin-, and maybe even user-guides
* The website repo includes a dump/backup of rendered content from "docs". Why? How should the old information be keeped to do not brake current documentation state?


Till we have a proper workflow, who has time to have an eye on these topics, too? Any ideas on how to coordinate work? Pair-sessions via voice/video-call?
How wants to go through i.e. the install docs and test it on Debian _AND_ Ubuntu to identify missing pieces and errors?

### vCluster Howto

We set up an example vCluster to ease testing/development within or around ganeti:
```
apt-get install ganeti

ip link add gnt type dummy
ip link up gnt

mkdir -p /opt/ganeti-vcluster
cd /usr/lib/ganeti/tools/
./vcluster-setup -c 3 /opt/ganeti-vcluster
cd /opt/ganeti-vcluster
```
Now follow the commands printed by the ```vcluster-setup``` script to initialise the cluster and add the virtual nodes to it. This will leave you with a fake cluster running three nodes on your local single server. In ```/opt/ganeti-vcluster``` are some mainteance scripts to start/stop the vCluster. If you are running ```systemd```, please export the following variable before issuing any of the commands:
```
export _SYSTEMCTL_SKIP_REDIRECT=1
```

### Ganeti Github repository bug closing sprint

TBD

## Code diet - how to improve the codebase

We discussed possible ways to cleanup the ganeti codebase:
* Migrate the qemu management interface from "human monitor" to "QMP"
* Remove the "human monitor" abstraction library once finished
* Remove lots of obsolete conditionals which are used to detect/interface older/obsolete kvm versions
* Ask the mailing list to determine  obsolete features (e.g. unused hypervisor integrations)

We also talked about things to improve:
* What's going on with half-implemented features targeted for 2.17 - remove them? finish them?
* Python 2.7 is going EOL in 2020 - the Python 3 migration needs to be finished and tested before Python-3-only-distribution-releases freeze package versions
 * Apollon has a git branch available which contains partly automatic, partly manual conversions to Python 3 with ~96% of tests passing so far (Does anyone have the URL?)

## Next year's GanetiCon

We discussed options for next year's GanetiCon - if you have other suggestions, feel free to add below:

### May 2019, Copenhagen
Petter suggested to integrate the GanetiCon with the NeIC (Nordic e-Infrastructure Collaboration) conference happening in May 2019 (14th - 16th of May). The conference is governmentally funded so there might be a (small) conference fee for attendants to cover the location and catering. We will update this document as soon as we know more.
The GanetiCon would run as a workshop during the conference and can extend up to two days.

## Other upcoming meetups/workshops

We might be able to meet/setup workshops during the following future events:
* Fosdem
* FrosCon
* 35C3

