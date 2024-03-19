# RHEL 8 CIS

## Configure a RHEL/Rocky/AlmaLinux 8 machine to be [CIS](https://www.cisecurity.org/cis-benchmarks/) compliant

### Based on [ CIS RedHat Enterprise Linux 8 Benchmark v3.0.0 - 11-10-2023 ](https://www.cisecurity.org/cis-benchmarks/)

---

## Looking for support?

[Lockdown Enterprise](https://www.lockdownenterprise.com#GH_AL_RH8_cis)

[Ansible support](https://www.mindpointgroup.com/cybersecurity-products/ansible-counselor#GH_AL_RH8_cis)

### Community

Join us on our [Discord Server](https://www.lockdownenterprise.com/discord) to ask questions, discuss features, or just chat with other Ansible-Lockdown users.

---

## Caution(s)

This role **will make changes to the system** which may have unintended consequences. This is not an auditing tool but rather a remediation tool to be used after an audit has been conducted.

Check Mode is not supported! The role will complete in check mode without errors, but it is not supported and should be used with caution. The RHEL8-CIS-Audit role or a compliance scanner should be used for compliance checking over check mode.

This role was developed against a clean install of the Operating System. If you are implementing to an existing system please review this role for any site specific changes that are needed.

To use release version please point to main branch and relevant release for the cis benchmark you wish to work with.

If moving across major releases e.g. v2.0.0 - v3.0.0 there are significant changes to the benchmarks and controls it is suggested to start as a new standard not to upgrade.

**Este rol esta modificado solo para algunas reglas especificas las cuales son las siguientes : 
rule_1.1.1.3, rule_1.1.2.1.1, rule_1.1.2.3.3, rule_1.1.2.4.2, rule_1.1.2.4.3, rule_1.1.2.6.2, rule_1.1.2.6.3, rule_1.1.2.6.4, rule_1.1.2.7.2, rule_1.1.2.7.3, rule_1.1.2.7.4, rule_1.3.2, rule_1.4.2, rule_1.4.3, rule_1.4.4, rule_1.5.1.2, rule_1.5.1.6, rule_1.6.1, rule_1.6.2, rule_1.7.1, rule_1.7.4, rule_1.8.6, rule_2.1.2, rule_3.4.2.2, rule_3.4.2.5, rule_4.2.10, rule_4.2.11, rule_4.2.13, rule_4.2.14, rule_4.2.19, rule_4.2.20, rule_4.2.4, rule_4.2.7, rule_4.2.9, rule_4.3.6, rule_4.3.7, rule_4.4.2.1, rule_4.4.3.2.1, rule_4.4.3.2.4, rule_4.4.3.2.5, rule_4.4.3.2.7, rule_4.4.3.3.1, rule_4.4.3.3.2, rule_4.4.3.3.3, rule_4.5.1.2, rule_4.5.1.3, rule_4.5.1.4, rule_4.5.2.3, rule_4.5.3.2, rule_5.1.1.4, rule_5.1.2.1.4, rule_5.1.2.3, rule_5.1.2.4, rule_5.2.4.1, rule_5.2.4.2, rule_5.2.4.3, rule_5.2.4.4, rule_5.2.4.5, rule_5.2.4.6, rule_5.2.4.7, rule_5.3.1, rule_5.3.2, rule_5.3.3**

---

## Matching a security Level for CIS

It is possible to to only run level 1 or level 2 controls for CIS.
This is managed using tags:

- level1_server
- level1_workstation
- level2_server
- level2_workstation

The control found in defaults main also need to reflect this as this control the testing thet takes place if you are using the audit component.

## Coming from a previous release

CIS release always contains changes, it is highly recommended to review the new references and available variables. This have changed significantly since ansible-lockdown initial release.
This is now compatible with python3 if it is found to be the default interpreter. This does come with pre-requisites which it configures the system accordingly.

Further details can be seen in the [Changelog](./ChangeLog.md)

## Auditing (new)

This can be turned on or off within the defaults/main.yml file with the variable rhel8cis_run_audit. The value is false by default, please refer to the wiki for more details. The defaults file also populates the goss checks to check only the controls that have been enabled in the ansible role.

This is a much quicker, very lightweight, checking (where possible) config compliance and live/running settings.

A new form of auditing has been developed, by using a small (12MB) go binary called [goss](https://github.com/goss-org/goss) along with the relevant configurations to check. Without the need for infrastructure or other tooling.
This audit will not only check the config has the correct setting but aims to capture if it is running with that configuration also trying to remove [false positives](https://www.mindpointgroup.com/blog/is-compliance-scanning-still-relevant/) in the process.

Refer to [RHEL8-CIS-Audit](https://github.com/ansible-lockdown/RHEL8-CIS-Audit).

## Example Audit Summary

This is based on a vagrant image with selections enabled. e.g. No Gui or firewall.
Note: More tests are run during audit as we check config and running state.

```txt

ok: [default] => {
    "msg": [
        "The pre remediation results are: ['Total Duration: 5.454s', 'Count: 338, Failed: 47, Skipped: 5'].",
        "The post remediation results are: ['Total Duration: 5.007s', 'Count: 338, Failed: 46, Skipped: 5'].",
        "Full breakdown can be found in /var/tmp",
        ""
    ]
}

PLAY RECAP *******************************************************************************************************************************************
default                    : ok=270  changed=23   unreachable=0    failed=0    skipped=140  rescued=0    ignored=0
```

## Documentation

- [Read The Docs](https://ansible-lockdown.readthedocs.io/en/latest/)
- [Getting Started](https://www.lockdownenterprise.com/docs/getting-started-with-lockdown#GH_AL_RH8_cis)
- [Customizing Roles](https://www.lockdownenterprise.com/docs/customizing-lockdown-enterprise#GH_AL_RH8_cis)
- [Per-Host Configuration](https://www.lockdownenterprise.com/docs/per-host-lockdown-enterprise-configuration#GH_AL_RH8_cis)
- [Getting the Most Out of the Role](https://www.lockdownenterprise.com/docs/get-the-most-out-of-lockdown-enterprise#GH_AL_RH8_cis)

## Requirements

**General:**

- Basic knowledge of Ansible, below are some links to the Ansible documentation to help get started if you are unfamiliar with Ansible

  - [Main Ansible documentation page](https://docs.ansible.com)
  - [Ansible Getting Started](https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html)
  - [Tower User Guide](https://docs.ansible.com/ansible-tower/latest/html/userguide/index.html)
  - [Ansible Community Info](https://docs.ansible.com/ansible/latest/community/index.html)
- Functioning Ansible and/or Tower Installed, configured, and running. This includes all of the base Ansible/Tower configurations, needed packages installed, and infrastructure setup.
- Please read through the tasks in this role to gain an understanding of what each control is doing. Some of the tasks are disruptive and can have unintended consequences in a live production system. Also familiarize yourself with the variables in the defaults/main.yml file.

**Technical Dependencies:**

RHEL/AlmaLinux/Rocky/Oracle 8 - Other versions are not supported.

- AlmaLinux/Rocky Has been tested on 8.8(enabling crypto (sections 1.10 & 1.11) breaks updating or installs : July 01 2021
- Access to download or add the goss binary and content to the system if using auditing
(other options are available on how to get the content to the system.)
- Python3.8
- Ansible 2.11+
- python-def (should be included in RHEL 8)
- libselinux-python

## Role Variables

This role is designed that the end user should not have to edit the tasks themselves. All customizing should be done via the defaults/main.yml file or with extra vars within the project, job, workflow, etc.

## Tags

There are many tags available for added control precision. Each control has it's own set of tags noting what level, if it's scored/notscored, what OS element it relates to, if it's a patch or audit, and the rule number.

Below is an example of the tag section from a control within this role. Using this example if you set your run to skip all controls with the tag services, this task will be skipped. The opposite can also happen where you run only controls tagged with services.

```sh
      tags:
      - level1-server
      - level1-workstation
      - scored
      - avahi
      - services
      - patch
      - rule_2.2.4
```

## Community Contribution

We encourage you (the community) to contribute to this role. Please read the rules below.

- Your work is done in your own individual branch. Make sure to Signed-off and GPG sign all commits you intend to merge.
- All community Pull Requests are pulled into the devel branch
- Pull Requests into devel will confirm your commits have a GPG signature, Signed-off, and a functional test before being approved
- Once your changes are merged and a more detailed review is complete, an authorized member will merge your changes into the main branch for a new release

## Known Issues

cloud0init - due to a bug this will stop working if noexec is added to /var.
rhel8cis_rule_1_1_3_3

[bug 1839899](https://bugs.launchpad.net/cloud-init/+bug/1839899)

Almalinux BaseOS, EPEL and many cloud providers repositories, do not allow repo_gpgcheck on rule_1.2.3 this will cause issues during the playbook unless or a workaround is found.

-------------------
TASK [RHEL8-CIS : 1.2.5 | PATCH | Ensure updates, patches, and additional security software are installed | Patch] ***
fatal: [localhost]: FAILED! => {"changed": false, "msg": "Failed to download metadata for repo 'epel': GPG verification is enabled, but GPG signature is not available. This may be an error or the repository does not support GPG verification: Status code: 404 for http://mirrors.upr.edu/epel/8/Everything/x86_64/repodata/repomd.xml.asc (IP: 136.145.244.40)", "rc": 1, "results": []}

solucion: fuente : https://access.redhat.com/solutions/7019126

*Modificacion del archivo /root/.ansible/roles/RHEL8-CIS/tasks/section_1/cis_1.2.x.yml

Linea 52 
#line: line: gpgcheck=1 --> line: gpgcheck=0 Modificacion

Linea 85
#line: line: gpgcheck=1 --> line: gpgcheck=0 Modificacion

archivo del server 
vi /etc/dnf/dnf.conf

[main]

gpgcheck=0

installonly_limit=3

clean_requirements_on_remove=True

best=True

skip_if_unavailable=False

**repo_gpgcheck=0**


------------------


## Pipeline Testing

uses:

- ansible-core 2.12
- ansible collections - pulls in the latest version based on requirements file
- runs the audit using the devel branch
- This is an automated test that occurs on pull requests into devel

## Local Testing

Molecule can be used to work on this role and test in distinct _scenarios_.

### examples

```bash
molecule test -s default
molecule converge -s wsl -- --check
molecule verify -s localhost
```

local testing uses:
- ansible 2.15.3 **usado el 19/03/2024
- ansible 2.13.3
- molecule 4.0.1
- molecule-docker 2.0.0
- molecule-podman 2.0.2
- molecule-vagrant 1.0.0
- molecule-azure 0.5.0

## Added Extras

- [pre-commit](https://pre-commit.com) can be tested and can be run from within the directory

```sh
pre-commit run
```

## Credits and Thanks
Massive thanks to the fantastic community and all its members.
This includes a huge thanks and credit to the original authors and maintainers.
Josh Springer, Daniel Shepherd, Bas Meijeri, James Cassell, Mike Renfro, DFed, George Nalen, Mark Bolwell

## pasos para servidor nuevo:
los siguientes pasos se sugieren para un servidor nuevo sin configuraciones para evitar futuros errores :

    1  subscription-manager register 
    2  subscription-manager refresh 
    3  subscription-manager attach --auto 
    4  dnf install python3
    5  yum install ansible-core
    6  ansible --version
**Instalar las colecciones necesarias especificas:**

ansible-galaxy collection install dsglaser.cis_security

ansible-galaxy collection install ansible.posix

**instalar goss:**
curl -L https://github.com/goss-org/goss/releases/latest/download/goss-linux-amd64 -o /usr/local/bin/goss

chmod +rx /usr/local/bin/goss

curl -L https://github.com/goss-org/goss/releases/latest/download/dgoss -o /usr/local/bin/dgoss
 
chmod +rx /usr/local/bin/dgoss

**EPEL para rhel 8**
subscription-manager repos --enable codeready-builder-for-rhel-8-$(arch)-rpms
dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
yum install python3-jmespath 
yum install python3.11-jmespath
 
**Instalar el rol desde github**

ansible-galaxy install git+https://github.com/JohanaER/RHEL8-CIS-OK.git

**NOTA** : Puede eliminar el rol completo con el siguiente comando (si así lo desea)
rm -rf /root/.ansible/roles/RHEL8-CIS-OK


**crear audit.yml y site.yml, estos se crearon en /root/site.yml y /root/audit.yml** 
---
**crear audit.yml** 

- name: RHEL8 CIS Audit
  hosts: all
  become: true
  roles:
    - name: "RHEL8-CIS-OK"
      vars:
        setup_audit: true
        run_audit: true

**crear site.yml**
- name: Run RHEL8 CIS hardening
  hosts: all
  become: true

  roles:

      - role: "RHEL8-CIS-OK"
  
**Ejecutar auditoria** 
cd /root/.ansible/roles/RHEL8-CIS-OK
ansible-playbook -i "localhost," -c local audit.yml

**Ver las reglas y tareas que se pueden ejecutarán**
[root@cis ~]# ansible-playbook -i "localhost," -c local site.yml --list-tags

**ejecutar una regla en especifico** 
[root@cis ~]# ansible-playbook -i "localhost," -c local site.yml --tags rule_1.1.1.3

**Ejecutar el rol completo**
[root@cis ~]# ansible-playbook -i "localhost," -c local site.yml

