# Connecting to ARCHER2

On the ARCHER2 system, interactive access can be achieved via SSH, either directly from a command line terminal or using an SSH client. In addition data can be transferred to and from the ARCHER2 system using
`scp` from the command line or by using a file transfer client.

This section covers the basic connection methods.

Before following the process below, we assume you have setup an account on ARCHER2 through the EPCC SAFE. Documentation on how to do this can be
found at:

   - [SAFE Guide for Users](https://epcced.github.io/safe-docs/safe-for-users/)


## Command line terminal

### Linux 

Linux distributions and MacOS each come installed with a terminal application that can be used for SSH access to the login nodes. Linux users will have different terminals depending on their distribution and window manager (e.g. GNOME Terminal in GNOME, Konsole in KDE). Consult your Linux distribution's documentation for details on how to load a terminal.

### MacOS

MacOS users can use the Terminal application, located in the Utilities folder within the Applications folder.

### Windows

A typical Windows installation will not include a terminal client, though there are various clients available. We recommend all our Windows users to download and install MobaXterm to access ARCHER2. It is very easy to use and includes an integrated X server with SSH client to run any graphical applications on ARCHER2.

You can download MobaXterm Home Edition (Installer Edition) from the following link:

  - [Install MobaXterm](http://mobaxterm.mobatek.net/download-home-edition.html)

Double-click the downloaded Microsoft Installer file (.msi), and the Windows wizard will automatically guides you through the installation process. Note, you might need to have administrator rights to install on
some Windows OS. Also make sure to check whether Windows Firewall hasn't blocked any features of this program after installation.

Start MobaXterm and then click "Start local terminal"

!!! Tips
    - If you download the .zip file rather than the .msi, make sure you unzip before attempting to run the installer.

    - If you are using a "managed desktop" machine, so do not have admin rights, you can use the [Portable edition of MobaXterm](https://mobaxterm.mobatek.net/download-home-edition.html) which doesn't need install privilages.

    - If this is your first time using MobaXterm, check that a permanent /home directory has been set up (or all saved info will be lost from session to session). Go to "Settings" -> "Configuration"-> check path to "Persistent home directory" is set and make sure path is "private" if prompted.
    - Any ssh key generated in MobaXterm will, by default, be stored in the permanent /home directory (see above) i.e. if your /home directory is `_MyDocuments_\MobaXterm\home` then within that folder you will find `_MyDocuments_\MobaXterm\home\.ssh` with your keys.  This folder will be 'hidden' by default so you may need to tick 'Hidden items' under 'View' in Windows Explorer to see it.

    - MobaXterm also allows you to set up ssh sessions with the username, login host and key details saved.  You are welcome to use this, rather than using the "Local terminal" but we are not able to assist with debugging connection issues if you choose this method.  We recommend sticking to command line terminal access.


## Access credentials

To access ARCHER2, you need to use two credentials: your password **and** an SSH key pair protected by a passphrase. You can find more detailed instructions on how to set up your credentials to access ARCHER2 from Windows, macOS and Linux below.

### SSH Key Pairs

You will need to generate an SSH key pair protected by a passphrase to access ARCHER2.

Using a [terminal](#command-line-terminal) (the command line), set up a key pair that contains
your e-mail address and enter a passphrase you will use to unlock the
key:

    $ ssh-keygen -t rsa -C "your@email.com"
    ...
    -bash-4.1$ ssh-keygen -t rsa -C "your@email.com"
    Generating public/private rsa key pair.
    Enter file in which to save the key (/Home/user/.ssh/id_rsa): [Enter]
    Enter passphrase (empty for no passphrase): [Passphrase]
    Enter same passphrase again: [Passphrase]
    Your identification has been saved in /Home/user/.ssh/id_rsa.
    Your public key has been saved in /Home/user/.ssh/id_rsa.pub.
    The key fingerprint is:
    03:d4:c4:6d:58:0a:e2:4a:f8:73:9a:e8:e3:07:16:c8 your@email.com
    The key's randomart image is:
    +--[ RSA 2048]----+
    |    . ...+o++++. |
    | . . . =o..      |
    |+ . . .......o o |
    |oE .   .         |
    |o =     .   S    |
    |.    +.+     .   |
    |.  oo            |
    |.  .             |
    | ..              |
    +-----------------+

(remember to replace "your@email.com" with your e-mail address).

### Upload public part of key pair to SAFE

You should now upload the public part of your SSH key pair to the SAFE
by following the instructions at:

[Login to SAFE](https://safe.epcc.ed.ac.uk). Then:

 1.  Go to the Menu *Login accounts* and select the ARCHER2 account you
     want to add the SSH key to
 2.  On the subsequent Login account details page click the *Add
     Credential* button
 3.  Select *SSH public key* as the Credential Type and click *Next*
 4.  Either copy and paste the public part of your SSH key into the
     *SSH Public key* box or use the button to select the public key
     file on your computer.
 5.  Click *Add* to associate the public SSH key part with your account

Once you have done this, your SSH key will be added to your ARCHER2 account.

Remember, you will need to use both an SSH key and password to log into ARCHER2 so you will also need to collect your initial password before you can log into ARCHER2. We cover this next.

!!! note
    If you want to connect to ARCHER2 from more than one machine, e.g. from your home laptop as well as your work laptop, you should generate an ssh key on each machine, and add each of the public keys into SAFE.  

### Initial passwords

The SAFE web interface is used to provide your initial password for logging onto ARCHER2 (see the [SAFE
Documentation](https://epcced.github.io/safe-docs) for more details on requesting accounts and picking up passwords).

!!! note
    You may now change your password on the ARCHER2 machine itself
    using the *passwd* command or when you are prompted the first time you
    login. This change will not be reflected in the SAFE. If you forget your
    password, you should use the SAFE to request a new one-shot password.

## SSH Clients

Interaction with ARCHER2 is done remotely, over an encrypted
communication channel, Secure Shell version 2 (SSH-2). This allows
command-line access to one of the login nodes of a ARCHER2, from which
you can run commands or use a command-line text editor to edit files.
SSH can also be used to run graphical programs such as GUI text editors
and debuggers when used in conjunction with an X client.

### Logging in 

You can use the following command from the [terminal](#command-line-terminal) window to login into
ARCHER2:

    ssh username@login-4c.archer2.ac.uk

You will first be prompted for the passphrase associated with your SSH key pair. Once you have entered this passphrase successfully, you will then be prompted for your machine account password. You need to enter both credentials correctly to be able to access ARCHER2.

!!! warning
    If your SSH key pair is not stored in the default location (usually
    `~/.ssh/id_rsa`) on your local system, you may need to specify the path
    to the private part of the key wih the `-i` option to `ssh`. For
    example, if your key is in a file called `keys/id_rsa_ARCHER2` you would
    use the command `ssh -i keys/id_rsa_ARCHER2
    username@login-4c.archer2.ac.uk` to log in.

!!! tip
    When you first log into ARCHER2, you will be prompted to change your
    initial password. This is a three step process:

    1.  When promoted to enter your *ldap password*: Re-enter the password
        you retrieved from SAFE
    2.  When prompted to enter your new password: type in a new password
    3.  When prompted to re-enter the new password: re-enter the new
        password

    Your password has now been changed

To allow remote programs, especially graphical applications to control your local display, such as being able to open up a new GUI window (such as for a debugger), use:

    ssh -X username@login-4c.archer2.ac.uk

Some sites recommend using the `-Y` flag. While this can fix some
compatibility issues, the `-X` flag is more secure.

Current MacOS systems do not have an X window system. Users should install the XQuartz package to allow for SSH with X11 forwarding on MacOS systems:

  - [XQuartz website](http://www.xquartz.org/)


## Host Keys

A host key adds an extra security layer for users over SSH. Using one enables users to log in to ARCHER2 if the login node has the same corresponding host key. The host key can be found in the entries in `~/.ssh/known_hosts`, as given in the example below: 

    AAAAB3NzaC1yc2EAAAADAQABAAABAQC/zGWlNKRmbGcH3j/+wQ/3vytRJnautfshhKNx6naoymVxmXSg9CvtsJQUCNsNMnYu7NvZwOu1SqouXUNbpXZbOxikPLooRmM6JmCiJ72Zz5ylsXaFaIPmU7nl40J8YP5xcmlW6+HP6/gcnrZeCGLOcCSGHIIAAPotL1hwF9ab0RFbHV1+IyNPc5LYwslwmtn1zU5BY6xKISL8cMy+tAxBExY07xKZ6k+7bNPc4Ia4GfoU+8U9/2ZpN6wpNZVCNOsQ92nyELKveO9PIzLPJvxkxnRYaEfYshnRPCauBEnhZbixqrlnyWQsShbjfxBac3XEgQlg0XIAvHfFLUQNL1bv

Host key verification can fail if this key is out of date, a problem which can be fixed by removing the offending entry in `~/.ssh/known_hosts`.

## Making access more convenient using the SSH configuration file

Typing in the full command to login or transfer data to ARCHER2 can
become tedious as it often has to be repeated many times. You can use
the SSH configuration file, usually located on your local machine at
`.ssh/config` to make things a bit more convenient.

Each remote site (or group of sites) can have an entry in this file
which may look something like:

    Host archer2
      HostName login-4c.archer2.ac.uk
      User username

(remember to replace `username` with your actual username\!).

The `Host archer2` line defines a short name for the entry. In this
case, instead of typing `ssh username@login-4c.archer2.ac.uk` to access the
ARCHER2 login nodes, you could use `ssh archer2` instead. The remaining
lines define the options for the `archer2` host.

   - `Hostname login-4c.archer2.ac.uk` - defines the full address of the
     host
   - `User username` - defines the username to use by default for this
     host (replace `username` with your own username on the remote
     host)

Now you can use SSH to access ARCHER2 without needing to enter your
username or the full hostname every time:

    $ ssh archer2

You can set up as many of these entries as you need in your local
configuration file. Other options are available. See the ssh\_config man
page (or `man ssh_config` on any machine with SSH installed) for a
description of the SSH configuration file. You may find the
`IdentityFile` option useful if you have to manage multiple SSH key
pairs for different systems as this allows you to specify which SSH key
to use for each system.

!!! bug
    There is a known bug with Windows ssh-agent. If you get the error
    message: `Warning: agent returned different signature type ssh-rsa
    (expected rsa-sha2-512)`, you will need to either specify the path to
    your ssh key in the command line (using the `-i` option as described
    above) or add the path to your SSH config file by using the
    `IdentityFile` option.

## SSH debugging tips

If you find you are unable to connect via SSH there are a number of ways
you can try and diagnose the issue. Some of these are collected below -
if you are having difficulties connecting we suggest trying these before
contacting the ARCHER2 service desk.

### Use the `user@login-4c.archer2.ac.uk` syntax rather than `-l user login-4c.archer2.ac.uk`

We have seen a number of instances where people using the syntax

```
ssh -l user login-4c.archer2.ac.uk
```

have not been able to connect properly and get prompted for a password many
times. We have found that using the alternative syntax:

```
ssh user@login-4c.archer2.ac.uk
```

works more reliably. If you are using the `-l user` option to connect and 
are seeing issues, then try using `user@login-4c.archer2.ac.uk` instead.

### Can you connect to the login node?

Try the command `ping -c 3 login-4c.archer2.ac.uk`. If you successfully
connect to the login node, the output should include:

    --- login-4c.archer2.ac.uk ping statistics ---
    3 packets transmitted, 3 received, 0% packet loss, time 38ms

(the ping time '38ms' is not important). If not all packets are received
there could be a problem with your internet connection, or the login
node could be unavailable.

### Password

If you are having trouble entering your password consider using a
password manager, from which you can copy and paste it. This will also
help you generate a secure password. If you need to reset your password,
instructions for doing so can be found in [the SAFE documentation](https://epcced.github.io/safe-docs/safe-for-users/\#reset\_machine)

Windows users please note that `Ctrl+V` does not work to paste in to
PuTTY, MobaXterm, or PowerShell. Instead use `Shift+Ins` to paste.
Alternatively, right-click and select 'Paste' in PuTTY and MobaXterm, or
simply right-click to paste in PowerShell.

### SSH key

If you get the error message `Permission denied (publickey)` this can
indicate a problem with your SSH key. Some things to check:

   - Have you uploaded the key to SAFE? Please note that if the same
     key is reuploaded SAFE will not map the "new" key to ARCHER2. If
     for some reason this is required, please delete the key first,
     then reupload.
 
   - Is ssh using the correct key? You can check which keys are being
     found and offered by ssh using `ssh -vvv`. If your private key has
     a non-default name you can use the `-i` flag to provide it to ssh,
     i.e. `ssh -i path/to/key username@login-4c.archer2.ac.uk`.
 
   - Are you entering the passphrase correctly? You will be asked for
     your private key's passphrase first. If you enter it incorrectly
     you will usually be asked to enter it again, and usually up to
     three times in total, after which ssh will fail with `Permission
     denied (publickey)`. If you would like to confirm your passphrase
     without attempting to connect, you can use `ssh-keygen -y -f
     /path/to/private/key`. If successful, this command will print the
     corresponding public key. You can also use this to check it is the
     one uploaded to SAFE.
 
   - Are permissions correct on the ssh key? One common issue is that
     the permissions are incorrect on either the key file, or the
     directory it's contained in. On Linux/MacOS for example, if your
     private keys are held in `~/.ssh/` you can check this with `ls -al
     ~/.ssh`. This should give something similar to the following
     output:
     
         $ ls -al ~/.ssh/
         drwx------.  2 user group    48 Jul 15 20:24 .
         drwx------. 12 user group  4096 Oct 13 12:11 ..
         -rw-------.  1 user group   113 Jul 15 20:23 authorized_keys
         -rw-------.  1 user group 12686 Jul 15 20:23 id_rsa
         -rw-r--r--.  1 user group  2785 Jul 15 20:23 id_rsa.pub
         -rw-r--r--.  1 user group  1967 Oct 13 14:11 known_hosts
     
     The important section here is the string of letters and dashes at
     the start, for the lines ending in `.`, `id_rsa`, and
     `id_rsa.pub`, which indicate permissions on the containing
     directory, private key, and public key respectively. If your
     permissions are not correct, they can be set with `chmod`. Consult
     the table below for the relevant `chmod` command. On Windows,
     permissions are handled differently but can be set by
     right-clicking on the file and selecting Properties \> Security \>
     Advanced. The user, SYSTEM, and Administrators should have `Full
     control`, and no other permissions should exist for both public
     and private key files, and the containing folder.


| Target      | Permissions  | `chmod` Code |
| ----------- | ------------ | ------------ |
| Directory   | `drwx------` | 700          |
| Private Key | `-rw-------` | 600          |
| Public Key  | `-rw-r--r--` | 644          |

`chmod` can be used to set permissions on the target in the following
way: `chmod <code> <target>`. So for example to set correct permissions
on the private key file `id_rsa_ARCHER2` one would use the command
`chmod 600 id_rsa_ARCHER2`.

### SSH verbose output

Verbose debugging output from `ssh` can be very useful for diagnosing
the issue. In particular, it can be used to distinguish between problems
with the SSH key and password - further details are given below. To
enable verbose output add the `-vvv` flag to your SSH command. For
example:

    ssh -vvv username@login-4c.archer2.ac.uk

The output is lengthy, but somewhere in there you should see lines
similar to the following:

    debug1: Next authentication method: publickey
    debug1: Offering public key: RSA SHA256:<key_hash> <path_to_private_key>
    debug3: send_pubkey_test
    debug3: send packet: type 50
    debug2: we sent a publickey packet, wait for reply
    debug3: receive packet: type 60
    debug1: Server accepts key: pkalg rsa-sha2-512 blen 2071
    debug2: input_userauth_pk_ok: fp SHA256:<key_hash>
    debug3: sign_and_send_pubkey: RSA SHA256:<key_hash>
    Enter passphrase for key '<path_to_private_key>':
    debug3: send packet: type 50
    debug3: receive packet: type 51
    Authenticated with partial success.
    debug1: Authentications that can continue: password, keyboard-interactive

In the text above, you can see which files ssh has checked for private
keys, and you can see if any key is accepted. The line `Authenticated
succeeded` indicates that the SSH key has been accepted. By default ssh
will go through a list of standard private key files, as well as any you
have specified with `-i` or a config file. This is fine, as long as one
of the files mentioned is the one that matches the public key uploaded
to SAFE.

If your SSH key passphrase is incorrect, you will be asked to try again
up to three times in total, before being disconnected with `Permission
denied (publickey)`. If you enter your passphrase correctly, but still
see this error message, please consider the advice under *SSH key*
above.

You should next see something similiar to:

    debug1: Next authentication method: keyboard-interactive
    debug2: userauth_kbdint
    debug3: send packet: type 50
    debug2: we sent a keyboard-interactive packet, wait for reply
    debug3: receive packet: type 60
    debug2: input_userauth_info_req
    debug2: input_userauth_info_req: num_prompts 1
    Password:
    debug3: send packet: type 61
    debug3: receive packet: type 60
    debug2: input_userauth_info_req
    debug2: input_userauth_info_req: num_prompts 0
    debug3: send packet: type 61
    debug3: receive packet: type 52
    debug1: Authentication succeeded (keyboard-interactive).

If you do not see the `Password:` prompt you may have connection issues,
or there could be a problem with the ARCHER2 login nodes. If you do not
see `Authenticated with partial success` it means your password was not
accepted. You will be asked to re-enter your password, usually two more
times before the connection will be rejected. Consider the suggestions
under *Password* above. If you *do* see `Authenticated with partial
success`, it means your password was accepted, and your SSH key will now
be checked.

The equivalent information can be obtained in PuTTY by
enabling all logging in settings.

## Related Software 

### tmux

[tmux](https://github.com/tmux/tmux/wiki) is a multiplexer application 
available on the ARCHER2 login nodes. It allows for multiple sessions to 
be open concurrently and these sessions can be detached and run in the 
background. Furthermore, sessions will continue to run after a user logs 
off and can be reattached to upon logging in again. It is particularly 
useful if you are connecting to ARCHER2 on an unstable Internet connection 
or if you wish to keep an arrangement of terminal applications running 
while you disconnect your client from the Internet -- for example, when 
moving between your home and workplace. 
