Registering Clients
===================

## Instructions for registering client systems you wish to manage with Spacewalk 2.6.

> **Note: for previous versions of Spacewalk use following links**
> - Spacewalk 2.5 instructions are available at [[RegisteringClients25]].
> - Spacewalk 2.4 instructions are available at [[RegisteringClients24]].
> - Spacewalk 2.3 instructions are available at [[RegisteringClients23]].
> - Spacewalk 2.2 instructions are available at [[RegisteringClients22]].
> - Spacewalk 2.1 instructions are available at [[RegisteringClients21]].
> - Spacewalk 2.0 instructions are available at [[RegisteringClients20]].
> - Spacewalk 1.9 instructions are available at [[RegisteringClients19]].
> - Spacewalk 1.8 instructions are available at [[RegisteringClients18]].

### Before Starting
1. Create a base channel within Spacewalk (Channels > Manage Software Channels > Create New Channel)
2. Create an activation key (Systems > Activation Keys > Create Key) with the new base channel. When creating a registration key do not use the generate function, create a human-readable version. eg: fedora-server-channel. This makes your installation more understandable and provides greater logical consistency to the whole system. On the other hand, if you want to prevent people from getting access to your channels, letting Spacewalk to generate random activation key name is the best way to go.

> **Note:**
> `rhnreg_ks` is used for registration of clients to Spacewalk. If you need to re-register a client to your Spacewalk server or change registration from one environment or server to another Spacewalk server then use the "--force" flag with `rhnreg_ks`, otherwise there is no need to use "--force".

### Fedora

1. Install the Spacewalk client yum repository
    * For Fedora 23 (x86_64 and i386):
      ```
      # rpm -Uvh http://yum.spacewalkproject.org/2.6-client/Fedora/23/x86_64/spacewalk-client-repo-2.6-0.fc23.noarch.rpm
      ```

    * For Fedora 24 (x86_64 and i386):
      ```
      # rpm -Uvh http://yum.spacewalkproject.org/2.6-client/Fedora/24/x86_64/spacewalk-client-repo-2.6-0.fc24.noarch.rpm
      ```
       
2. Install client packages
      ```
      # dnf -y install rhn-client-tools rhn-check rhn-setup rhnsd dnf-plugin-spacewalk
      ```

3. Install Spacewalk's CA certificate on the server to enable SSL communication (change rpm version in this command if needed)     
      ```
      # rpm -Uvh http://YourSpacewalk.example.com/pub/rhn-org-trusted-ssl-cert-1.0-1.noarch.rpm
      ```

4. Register your Fedora system to Spacewalk using the activation key you created earlier  
      ```
      # rhnreg_ks --serverUrl=https://YourSpacewalk.example.org/XMLRPC --sslCACert=/usr/share/rhn/RHN-ORG-TRUSTED-SSL-CERT --activationkey=<key-with-fedora-custom-channel>
      ```

### Red Hat Enterprise Linux 5, 6 and 7, Scientific Linux 6 and 7, CentOS 5, 6 and 7

> **Warning:**
> If you are installing these packages on a Red Hat Enterprise Linux installation it will override some of the original base packages and you may well be invalidating your support agreement with Red Hat!
    
1. The latest client tools bring the upstream development to your client boxes. That means that the packages may have dependencies that are not found in core Red Hat Enterprise Linux. These dependencies can be found in EPEL. Install the Spacewalk yum repository and matching EPEL repository.
     * RHEL 5 / CentOS 5
       ```
       # rpm -Uvh http://yum.spacewalkproject.org/2.6-client/RHEL/5/x86_64/spacewalk-client-repo-2.6-0.el5.noarch.rpm
       # rpm -Uvh http://dl.fedoraproject.org/pub/epel/epel-release-latest-5.noarch.rpm
       ```
    
     * RHEL 6 / SL 6 / CentOS 6
       ```
       # rpm -Uvh http://yum.spacewalkproject.org/2.6-client/RHEL/6/x86_64/spacewalk-client-repo-2.6-0.el6.noarch.rpm
       # rpm -Uvh http://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
       ```

     * RHEL 7 / SL 7 / CentOS 7
       ```
       # rpm -Uvh http://yum.spacewalkproject.org/2.6-client/RHEL/7/x86_64/spacewalk-client-repo-2.6-0.el7.noarch.rpm
       # rpm -Uvh http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
       ```
    
2. Install client packages

   ```
   # yum -y install rhn-client-tools rhn-check rhn-setup rhnsd m2crypto yum-rhn-plugin
   ```

3. Install Spacewalk's CA certificate on the server to enable SSL communication (change rpm version in this command if needed)
   ```
   # rpm -Uvh http://YourSpacewalk.example.com/pub/rhn-org-trusted-ssl-cert-1.0-1.noarch.rpm
   ```

4. Register your system to Spacewalk using the activation key you created earlier
   ```
   # rhnreg_ks --serverUrl=https://YourSpacewalk.example.org/XMLRPC --sslCACert=/usr/share/rhn/RHN-ORG-TRUSTED-SSL-CERT --activationkey=<key-with-rhel-custom-channel> 
   ```

## CentOS 4

Registering a CentOS 4 server to Spacewalk is exactly the same as it would be for CentOS 5, but rhnreg_ks, rhn_check and other related scripts are located in the package "up2date", and not in "rhn-setup".
    
1. Enable "spacewalk-tools" repo for Yum and install "up2date" package:
   ```
   # rpm -ivh http://stahnma.fedorapeople.org/spacewalk-tools/spacewalk-client-tools-0.0-1.noarch.rpm
   # yum install up2date 
   ```

2. Install Spacewalk's CA certificate on the server to enable SSL communication (change rpm version in this command if needed)
   ```
   # rpm -Uvh http://YourSpacewalk.example.com/pub/rhn-org-trusted-ssl-cert-1.0-1.noarch.rpm
   ```

3. Register your CentOS system to Spacewalk using the activation key you created earlier:
   ```
   # rhnreg_ks --serverUrl=https://YourSpacewalk.example.org/XMLRPC --sslCACert=/usr/share/rhn/RHN-ORG-TRUSTED-SSL-CERT --activationkey=<key-with-centos-custom-channel>
   ```

## SUSE

1. Add the *spacewalk-tools* repo to get access to the tools and install them:

    * For openSUSE 13.2:

    ```
    #  zypper ar -f http://download.opensuse.org/repositories/systemsmanagement:/spacewalk:/2.6/openSUSE_13.2/ spacewalk-tools
    #  zypper install rhn-client-tools zypp-plugin-spacewalk rhnsd rhn-setup rhn-check
    ```

    * For openSUSE Leap 42.1:
    
    ```
    #  zypper ar -f http://download.opensuse.org/repositories/systemsmanagement:/spacewalk:/2.6/openSUSE_Leap_42.1/ spacewalk-tools
    #  zypper install rhn-client-tools zypp-plugin-spacewalk rhnsd rhn-setup rhn-check
    ```

    * For openSUSE Leap 42.2:

    ```
    #  zypper ar -f http://download.opensuse.org/repositories/systemsmanagement:/spacewalk:/2.6/openSUSE_Leap_42.2/ spacewalk-tools
    #  zypper install rhn-client-tools zypp-plugin-spacewalk rhnsd rhn-setup rhn-check
    ```

    * For Tumbleweed:

    ```
    #  zypper ar -f http://download.opensuse.org/repositories/systemsmanagement:/spacewalk:/2.6/openSUSE_Tumbleweed/ spacewalk-tools
    #  zypper install rhn-client-tools zypp-plugin-spacewalk rhnsd rhn-setup rhn-check
    ```

    * For SLE12_SP1:

    ```
    #  zypper ar -f http://download.opensuse.org/repositories/systemsmanagement:/spacewalk:/2.6/SLE_12_SP1/ spacewalk-tools
    #  zypper install rhn-client-tools zypp-plugin-spacewalk rhnsd rhn-setup rhn-check
    ```

2. Install Spacewalk's CA certificate on the server to enable SSL communication

    ```
    # wget http://YourSpacewalk.example.org/pub/RHN-ORG-TRUSTED-SSL-CERT -O /usr/share/rhn/RHN-ORG-TRUSTED-SSL-CERT
    # ln -s /usr/share/rhn/RHN-ORG-TRUSTED-SSL-CERT /usr/share/pki/trust/anchors/RHN-ORG-TRUSTED-SSL-CERT.pem
    # update-ca-certificates
    ```

3. Register your SUSE system to Spacewalk using the activation key you created earlier

    ```   
    # rhnreg_ks --serverUrl=https://YourSpacewalk.example.org/XMLRPC --sslCACert=/usr/share/rhn/RHN-ORG-TRUSTED-SSL-CERT --activationkey=<key-with-SUSE-custom-channel> 
    ```

## Debian

> **note:**
> DEBIAN PACKAGES ARE NOT YET UPDATED FOR SPACEWALK-2.6! Any volunteers?
    
All core clients packages are already in Debian and Ubuntu. See:
    
    http://packages.debian.org/sid/apt-transport-spacewalk
    http://packages.debian.org/sid/python-rhn
    http://packages.debian.org/sid/python-ethtool
    http://packages.debian.org/sid/rhnsd
    http://packages.debian.org/sid/rhn-client-tools

Install the packages:

  ```
  # apt-get update
  # apt-get install apt-transport-spacewalk rhnsd
  ```

If you want to run rhnsd. You have to manually create one directory:

  ```
  # mkdir /var/lock/subsys
  ```
  
If you need some additional packages (e.g. rhnpush or osad), add following line to file /etc/apt/sources.list:

  ```
  # deb http://miroslav.suchy.cz/spacewalk/debian spacewalk-unstable ./
  ```

But this is not needed for most clients.

> **note:**
> packages on miroslav.suchy.cz are not signed.


And then register with your Spacewalk server using rhnreg_ks and activation key.


    # wget http://YourSpacewalk.example.org/pub/RHN-ORG-TRUSTED-SSL-CERT -O /usr/share/rhn/RHN-ORG-TRUSTED-SSL-CERT
    rhnreg_ks --serverUrl=https://YourSpacewalk.example.org/XMLRPC --sslCACert=/usr/share/rhn/RHN-ORG-TRUSTED-SSL-CERT --activationkey=1-my-debian-key

When updating the Apt cache you can watch the status of communication between Apt and Spacewalk.

    # apt-get update

Finally, you rhnpush your favourite Debian packages to your Spacewalk server in order to be able to apply them using the Spacewalk WebUI. You can push packages from your Spacewalk server. There is no needed to run rhnpush on Debian machine.

> **note:** 
> for Debian clients neither Spacewalk proxy, satellite-sync, repo-sync, source packages nor staging content will work.
