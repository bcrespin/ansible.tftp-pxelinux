Role Name
=========
install & configure a pxe server, menu customizable based on syslinux 
for now, only OpenBSD supported, but other Os support should be easy

Requirements
------------
none

Role Variables
--------------
TODO

Dependencies
------------
none

Example Playbook
----------------
```yaml

    - hosts: pxe_servers
      vars:
      tftp_pxe_mainmenu:
        - name: "Hardware diagnostics & tools"
          file: hardware
          images:
          - name: "Western Digital Data Lifeguard Diagnostic 5.22"
            url: "https://dl.dropboxusercontent.com/u/83439503/iso"
            filename: "wddiag522.img"
            kernel: memdisk
            append: iso raw
            initrd: "pxe_images/wddiag522.img"
          - name: "Memtest86+ v7.2" 
            url: "https://dl.dropboxusercontent.com/u/83439503/iso"
            filename: "Memtest86-7.2.iso"
            kernel: memdisk
            append: iso raw
            initrd: "pxe_images/Memtest86-7.2.iso"
        - name: "(Live/Install) OS"
          file: os
          images:
            - name: "mfsBSD 11.0-RELEASE amd64 (user:root pwd:mfsroot)"
              url: "http://mfsbsd.vx.sk/files/iso/11/amd64"
              filename: "mfsbsd-11.0-RELEASE-amd64.iso"
              kernel: "memdisk"
              append: "raw initrd=pxe_images/mfsbsd-11.0-RELEASE-amd64.iso iso"         
      roles:
         - { role: ansible.tftp-pxelinux }
```

License
-------
BSD

