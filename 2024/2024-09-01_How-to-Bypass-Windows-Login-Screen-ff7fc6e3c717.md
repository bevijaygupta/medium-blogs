::: {}
# How to Bypass Windows Login Screen {#how-to-bypass-windows-login-screen .p-name}
:::

::: {.section .p-summary field="subtitle"}
1\. Introduction
:::

::::::::::::::::::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#8646 .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### How to Bypass Windows Login Screen {#6da9 .graf .graf--h3 .graf--leading .graf--title name="6da9"}

<figure id="11b0" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*dtEFClYfnNZqSDykpBTZLw.png"
class="graf-image" data-image-id="1*dtEFClYfnNZqSDykpBTZLw.png"
data-width="680" data-height="250" />
</figure>

### 1. Introduction {#05cc .graf .graf--h3 .graf-after--figure name="05cc"}

Bypassing the Windows login screen can be necessary in cases where users
forget their passwords or need to access a locked-out system.
Understanding these methods also highlights potential vulnerabilities in
the Windows operating system, allowing students and IT professionals to
reinforce system security.
:::
::::
::::::

:::::: {#24a4 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 2. Why Understanding Windows Login Mechanisms is Important {#d41a .graf .graf--h3 .graf--leading name="d41a"}

Windows login screens are the first line of defense for a system. By
understanding how these mechanisms work and how they can be bypassed,
students can better appreciate the importance of strong password
policies, the risks of unauthorized access, and the necessity of regular
system audits.
:::
::::
::::::

:::::: {#ddaa .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 3. Method 1: Using Safe Mode {#213e .graf .graf--h3 .graf--leading name="213e"}

**Safe Mode** is a diagnostic mode of Windows that starts the system
with a minimal set of drivers and services. This mode can sometimes
bypass the login screen, especially if the issue is related to a system
malfunction.

#### Step-by-Step Guide: {#47fd .graf .graf--h4 .graf-after--p name="47fd"}

**Restart the Computer:**

- [Press the power button and immediately start pressing
  `F8`{.markup--code .markup--li-code} repeatedly until the Advanced
  Boot Options menu appears.]{#0dac}

**Select Safe Mode:**

- [Use the arrow keys to highlight **Safe Mode** and press
  `Enter`{.markup--code .markup--li-code}.]{#2a52}

**Login Screen:**

- [If a login screen appears, try entering the default Administrator
  account. If this account is not password-protected, you'll gain
  access.]{#64bc}

**Remove the Password:**

- [Once logged in, go to `Control Panel`{.markup--code .markup--li-code}
  \> `User Accounts`{.markup--code .markup--li-code} and remove or reset
  the password for the locked account.]{#b931}
:::
::::
::::::

:::::: {#a0bd .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 4. Method 2: Bypassing with Command Prompt {#e0ba .graf .graf--h3 .graf--leading name="e0ba"}

Using the **Command Prompt** to bypass the Windows login screen is one
of the most well-known methods. This method requires booting from a
Windows installation disk or a bootable USB drive.

#### Step-by-Step Guide: {#39c7 .graf .graf--h4 .graf-after--p name="39c7"}

**Create a Bootable USB or Use a Windows Installation Disk:**

- [Download the Windows ISO file and create a bootable USB using
  software like Rufus.]{#fc14}

**Boot from USB/Disk:**

- [Insert the bootable USB or installation disk, restart the computer,
  and boot from the USB/disk.]{#5fc9}

**Access Command Prompt:**

- [In the Windows setup screen, press `Shift + F10`{.markup--code
  .markup--li-code} to open the Command Prompt.]{#04fa}

**Replace Utility Manager with Command Prompt:**

- [Enter the following commands one by one:]{#8ae9}
- [`move c:\windows\system32\utilman.exe c:\ copy c:\windows\system32\cmd.exe c:\windows\system32\utilman.exe`{.markup--code
  .markup--li-code}]{#f3e3}
- [These commands will rename `utilman.exe`{.markup--code
  .markup--li-code} and replace it with `cmd.exe`{.markup--code
  .markup--li-code}.]{#423c}

**Reboot and Access the Login Screen:**

- [Restart your computer. At the login screen, click the **Ease of
  Access** button to open the Command Prompt.]{#11f0}

**Create a New User or Reset Password:**

- [To create a new user:]{#846f}
- [`net user [username] [password] /add`{.markup--code
  .markup--li-code}]{#debb}
- [To add the user to the administrators group:]{#a236}
- [`net localgroup administrators [username] /add`{.markup--code
  .markup--li-code}]{#a215}
- [To reset the password:]{#495b}
- [`net user [username] [newpassword]`{.markup--code
  .markup--li-code}]{#b2ce}
- [Now you can log in with the new account or the reset
  password.]{#05ba}

**Restore the Original Settings:**

- [After logging in, revert the changes:]{#c8a3}
- [`move c:\utilman.exe c:\windows\system32\utilman.exe`{.markup--code
  .markup--li-code}]{#f63d}
:::
::::
::::::

:::::: {#3679 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 5. Method 3: Resetting Password Using a Password Reset Disk {#1173 .graf .graf--h3 .graf--leading name="1173"}

A **Password Reset Disk** is a tool that allows users to reset their
Windows password if they forget it. However, this method is only
applicable if the reset disk was created before the password was
forgotten.

#### Step-by-Step Guide: {#32e8 .graf .graf--h4 .graf-after--p name="32e8"}

**Insert the Password Reset Disk:**

- [At the login screen, insert the disk or USB flash drive.]{#ced1}

**Click on "Reset Password":**

- [If you've inserted the disk correctly, an option will appear below
  the password field.]{#31c7}

**Follow the Password Reset Wizard:**

- [Follow the on-screen instructions to reset your password.]{#70e8}

1.  [**Login with the New Password:**]{#3699}

- [After the reset process]{#57c6}

### 3. Method 1: Using Safe Mode {#419f .graf .graf--h3 .graf-after--li name="419f"}

**Safe Mode** is a diagnostic mode of Windows that starts the system
with a minimal set of drivers and services. This method can be useful if
you need to bypass the login screen due to forgotten passwords or
corrupted profiles.

#### Step-by-Step Guide {#2d91 .graf .graf--h4 .graf-after--p name="2d91"}

**Restart Your Computer**:

- [Begin by restarting your computer.]{#7d7e}

**Enter Safe Mode**:

- [As the system starts, press `F8`{.markup--code .markup--li-code}
  repeatedly before the Windows logo appears. This will bring up the
  Advanced Boot Options menu.]{#453b}
- [From the options, select **Safe Mode with Command Prompt** using the
  arrow keys and press `Enter`{.markup--code .markup--li-code}.]{#6bbc}

**Accessing Command Prompt**:

- [Once the system boots into Safe Mode, the Command Prompt window will
  appear instead of the usual desktop.]{#0654}

**Create a New User Account**:

- [In the Command Prompt window, type the following command to create a
  new user account with administrative privileges:]{#2c96}
- [`net user username password /add`{.markup--code
  .markup--li-code}]{#45a7}
- [Replace `username`{.markup--code .markup--li-code} with the desired
  username and `password`{.markup--code .markup--li-code} with a
  password of your choice.]{#484a}

**Add the User to the Administrators Group**:

- [Next, type the following command to add the newly created user to the
  Administrators group:]{#3c83}
- [`net localgroup administrators username /add`{.markup--code
  .markup--li-code}]{#357f}
- [Replace `username`{.markup--code .markup--li-code} with the username
  you created in the previous step.]{#761b}

**Restart Your Computer**:

- [Type `exit`{.markup--code .markup--li-code} to close the Command
  Prompt and restart your computer normally.]{#ff7f}
- [Log in using the new account you created.]{#fe1c}

By following these steps, you can bypass the login screen and access the
system with a new administrative account.
:::
::::
::::::

:::::: {#df2d .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 4. Method 2: Bypassing with Command Prompt {#6f27 .graf .graf--h3 .graf--leading name="6f27"}

The Command Prompt method is one of the most common techniques used to
bypass the Windows login screen. It involves replacing the Ease of
Access button with Command Prompt, allowing you to reset passwords or
create new accounts from the login screen.

#### Step-by-Step Guide {#9be1 .graf .graf--h4 .graf-after--p name="9be1"}

**Boot from Windows Installation Media**:

- [Insert a Windows installation DVD or USB drive and boot from
  it.]{#a1a6}
- [When the Windows Setup screen appears, click on **Repair your
  computer**.]{#5f73}

**Access Command Prompt**:

- [Select **Troubleshoot** \> **Advanced options** \> **Command
  Prompt**.]{#b90f}

**Backup and Replace Utilman.exe**:

- [In the Command Prompt window, type the following commands to backup
  the `Utilman.exe`{.markup--code .markup--li-code} file (the Ease of
  Access button executable) and replace it with `cmd.exe`{.markup--code
  .markup--li-code}:]{#a878}
- [`move C:\Windows\System32\Utilman.exe C:\Windows\System32\Utilman.exe.bak copy C:\Windows\System32\cmd.exe C:\Windows\System32\Utilman.exe`{.markup--code
  .markup--li-code}]{#21c9}

**Reboot the System**:

- [Close the Command Prompt and restart your computer.]{#232d}

**Open Command Prompt from Login Screen**:

- [At the login screen, click on the Ease of Access button (bottom-right
  corner). This will now open Command Prompt instead of the Ease of
  Access menu.]{#d1b6}

**Reset the Password**:

- [In the Command Prompt, type the following command to reset the
  password for any user:]{#f908}
- [`net user username newpassword`{.markup--code
  .markup--li-code}]{#6a08}
- [Replace `username`{.markup--code .markup--li-code} with the target
  account\'s username and `newpassword`{.markup--code .markup--li-code}
  with the new password.]{#bf93}

**Restore the Original Utilman.exe**:

- [After logging in, restore the original `Utilman.exe`{.markup--code
  .markup--li-code} file by running the following command:]{#b619}
- [`copy C:\Windows\System32\Utilman.exe.bak C:\Windows\System32\Utilman.exe`{.markup--code
  .markup--li-code}]{#1d0b}

By following these steps, you can successfully bypass the login screen
and reset the password of any local user account.
:::
::::
::::::

:::::: {#17ee .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 5. Method 3: Resetting Password Using a Password Reset Disk {#47ad .graf .graf--h3 .graf--leading name="47ad"}

A Password Reset Disk is a built-in Windows feature that allows you to
reset your password if you forget it. This method only works if you've
previously created a Password Reset Disk for your account.

#### Step-by-Step Guide {#e395 .graf .graf--h4 .graf-after--p name="e395"}

**Insert the Password Reset Disk**:

- [At the login screen, insert the Password Reset Disk (usually a USB
  drive).]{#6af8}

**Click on the 'Reset Password' Link**:

- [Click on the **Reset password** link that appears under the password
  field.]{#1498}

**Password Reset Wizard**:

- [The Password Reset Wizard will launch. Follow the on-screen
  instructions to create a new password.]{#972b}

**Complete the Process**:

- [Once the process is complete, log in with the new password.]{#6f06}

This method is the most straightforward, but it requires prior
preparation by creating a Password Reset Disk.
:::
::::
::::::

:::::: {#8023 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 6. Method 4: Using Third-Party Software {#05d4 .graf .graf--h3 .graf--leading name="05d4"}

There are various third-party tools available that can help bypass the
Windows login screen. These tools are often used by IT professionals and
are generally easy to use. Here, we will discuss two popular tools:
**Ophcrack** and **PCUnlocker**.

#### Recommended Tools {#6e6a .graf .graf--h4 .graf-after--p name="6e6a"}

**Ophcrack**:

- [Ophcrack is an open-source tool that uses rainbow tables to crack
  passwords. It's useful for recovering passwords rather than bypassing
  the login screen directly.]{#6df7}

**PCUnlocker**:

- [PCUnlocker is a paid tool designed to bypass or reset Windows
  passwords, making it a more direct solution.]{#e5e7}

#### Step-by-Step Guide (Using PCUnlocker) {#18d1 .graf .graf--h4 .graf-after--li name="18d1"}

**Download and Create Bootable Media**:

- [Download PCUnlocker from the official website.]{#00c0}
- [Create a bootable USB or CD/DVD using the downloaded ISO
  file.]{#7369}

**Boot from PCUnlocker Media**:

- [Insert the bootable media into the locked computer and restart
  it.]{#71eb}
- [Boot from the USB or CD/DVD by accessing the boot menu (usually by
  pressing `F12`{.markup--code .markup--li-code}, `F2`{.markup--code
  .markup--li-code}, or `Del`{.markup--code .markup--li-code}).]{#6468}

**Select the User Account**:

- [Once PCUnlocker loads, you'll see a list of user accounts. Select the
  account you want to unlock or reset the password for.]{#c274}

**Reset Password or Unlock Account**:

- [Click on **Reset Password** to create a new password or choose
  **Unlock Account** if the account is locked.]{#9634}

**Reboot and Log In**:

- [After resetting the password or unlocking the account, reboot the
  computer and log in using the new credentials.]{#56ce}

This method is efficient but involves using third-party software, which
may require a purchase.
:::
::::
::::::

:::::: {#d679 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 7. Method 5: Editing the Registry {#7e75 .graf .graf--h3 .graf--leading name="7e75"}

Editing the Windows Registry is a more advanced method for bypassing the
login screen. This method should be used with caution, as incorrect
changes to the registry can cause system instability.

#### Step-by-Step Guide {#4693 .graf .graf--h4 .graf-after--p name="4693"}

**Boot from Windows Installation Media**:

- [Insert a Windows installation DVD or USB drive and boot from
  it.]{#f12f}
- [Access the **Command Prompt** via **Repair your computer** \>
  **Troubleshoot** \> **Advanced options** \> **Command
  Prompt**.]{#a812}

**Open the Registry Editor**:

- [In the Command Prompt, type `regedit`{.markup--code .markup--li-code}
  to open the Registry Editor.]{#791f}

**Navigate to the Winlogon Registry Key**:

- [Navigate to the following path:]{#925a}
- [`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon`{.markup--code
  .markup--li-code}]{#2658}

**Edit the AutoAdminLogon Key**:

- [Find the `AutoAdminLogon`{.markup--code .markup--li-code} key, and
  double-click it to change its value from `0`{.markup--code
  .markup--li-code} to `1`{.markup--code .markup--li-code}.]{#2b63}

**Edit the DefaultUserName and DefaultPassword Keys**:

- [Locate the `DefaultUserName`{.markup--code .markup--li-code} and
  `DefaultPassword`{.markup--code .markup--li-code} keys and set them to
  the username and password of the account you wish to log in
  automatically.]{#306d}

**Close the Registry Editor and Reboot**:

- [Close the Registry Editor, type `exit`{.markup--code
  .markup--li-code} in the Command Prompt, and reboot the
  system.]{#aa50}

After completing these steps, the system should automatically log in to
the specified account without prompting for a password.
:::
::::
::::::

:::::: {#8dc6 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 8. Method 6: Using a Local Administrator Account {#eca0 .graf .graf--h3 .graf--leading name="eca0"}

Windows often has a hidden local Administrator account that can be
accessed if enabled. This method allows you to bypass the login screen
using this account.

#### Step-by-Step Guide {#6483 .graf .graf--h4 .graf-after--p name="6483"}

**Boot into Safe Mode**:

- [Restart your computer and press `F8`{.markup--code .markup--li-code}
  to enter the Advanced Boot Options menu.]{#8e5f}
- [Select **Safe Mode** and press `Enter`{.markup--code
  .markup--li-code}.]{#d8c5}

**Log in as Administrator**:

- [If the hidden Administrator account is enabled, it will appear on the
  login screen. Click on the **Administrator** account to log
  in.]{#9420}

**Reset the Password of Other Accounts**:

- [Once logged in, go to **Control Panel** \> **User Accounts** \>
  **Manage another account**.]{#503c}
- [Select the user account you want to reset and click on **Change the
  password**.]{#808f}

**Reboot and Log In**:

- [Restart the computer and log in with the newly reset
  password.]{#8b5e}

This method is simple but relies on the availability of the hidden
Administrator account.
:::
::::
::::::

:::::: {#bc40 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 9. Legal and Ethical Considerations {#e8d5 .graf .graf--h3 .graf--leading name="e8d5"}

While bypassing the Windows login screen can be technically fascinating
and useful in certain scenarios, it's essential to consider the legal
and ethical implications. Unauthorized access to computer systems is
illegal and can lead to severe consequences, including criminal charges.

**Always ensure** that you have explicit permission to access and modify
the system. In a professional environment, this could mean working with
IT administrators or security teams to ensure all activities comply with
company policies and legal standards.

Educational institutions should emphasize the ethical use of these
techniques, teaching students about the importance of cybersecurity and
the responsibility that comes with technical knowledge.
:::
::::
::::::

:::::: {#8610 .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 10. Conclusion {#98ef .graf .graf--h3 .graf--leading name="98ef"}

Bypassing the Windows login screen is a powerful skill that underscores
the importance of robust security practices. Whether through Safe Mode,
Command Prompt, third-party tools, or registry edits, each method
provides insight into the vulnerabilities of the Windows operating
system.

However, this knowledge must be handled responsibly. Use these
techniques only for legitimate purposes, such as recovering access to
your own systems or for educational study under proper guidance.
Understanding these methods can help you become a more knowledgeable and
ethical IT professional, better prepared to protect systems from
unauthorized access.

By mastering these techniques, students can gain a deeper understanding
of both the strengths and weaknesses of Windows security, laying the
groundwork for further studies in cybersecurity and system
administration.

### Promote and Collaborate on Cybersecurity Insights {#c86e .graf .graf--h3 .graf-after--p name="c86e"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#c7b5 .graf .graf--h3 .graf-after--p name="c7b5"}

[Vijay
Gupta](https://medium.com/@bevijaygupta/who-is-vijay-gupta-2ecad87f92a2){.markup--anchor
.markup--p-anchor
data-href="https://medium.com/@bevijaygupta/who-is-vijay-gupta-2ecad87f92a2"
rel="noopener" target="_blank"} is a cybersecurity enthusiast with
several years of experience in cyber security, [cyber crime forensics
investigation](https://play.google.com/store/books/details?id=VRz7EAAAQBAJ){.markup--anchor
.markup--p-anchor
data-href="https://play.google.com/store/books/details?id=VRz7EAAAQBAJ"
rel="noopener ugc nofollow noopener" target="_blank"}, and security
awareness training in schools and colleges. With a passion for
safeguarding digital environments and educating others about
cybersecurity best practices, Vijay has dedicated his career to
promoting cyber safety and resilience. Stay connected with Vijay Gupta
on various social media platforms and professional networks to access
valuable insights and stay updated on the latest cybersecurity trends.
:::
::::
::::::
:::::::::::::::::::::::::::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [September 1, 2024](https://medium.com/p/ff7fc6e3c717).

[Canonical
link](https://medium.com/@bevijaygupta/how-to-bypass-windows-login-screen-ff7fc6e3c717){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
