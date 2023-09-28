---
{"dg-publish":true,"permalink":"/almraje-fleeting-notes/how-to-run-program-without-admin-privileges-and-to-bypass-uac-prompt-windows-os-hub/"}
---

 [Windows OS Hub](http://woshub.com/) / [Windows 10](http://woshub.com/windows-10/) / How to Run Program without Admin Privileges and to Bypass UAC Prompt?

When started, many programs require permission elevation (shield on the app icon), but actually they don’t need the administrator privileges for their normal operation. For example, you can manually grant permissions for your users on the app folder in the *ProgramFiles* and/or registry keys used by the program. So when starting such a program under non-admin user account, a UAC prompt will appear and the user will be required to enter an administrator password (if User Account Control is enabled on the computer). To bypass this mechanism, many users simple disable UAC or grant admin privileges to a user by [adding a user account to the local group “Administrators”](http://woshub.com/add-domain-users-local-admin-group-gpo/). Of course, both methods are not safe.

Contents:

-   [Why some Windows apps not run under standard users and require administrator permissions?](http://woshub.com/run-program-without-admin-password-and-bypass-uac-prompt/#h2_1)
-   [How to run a program that requires admin privileges under standard user?](http://woshub.com/run-program-without-admin-password-and-bypass-uac-prompt/#h2_2)
-   [How to Bypass UAC with RunAsInvoker in \_\_COMPAT\_LAYER?](http://woshub.com/run-program-without-admin-password-and-bypass-uac-prompt/#h2_3)
-   [Enable RunAsInvoker Mode in the EXE File Manifest](http://woshub.com/run-program-without-admin-password-and-bypass-uac-prompt/#h2_4)

## Why some Windows apps not run under standard users and require administrator permissions?

An app may need the administrator privileges to modify some files (logs, configs, etc.) in its own folder in the C:\\Program Files (x86)\\SomeApp. By default, users don’t have edit (write and modify) permissions on this directory. In order this program to work normally, the administrator permissions are required. To solve this problem, you have to manually grant the *modify* and/or *write* permission for a user (or the built-in Users group) on the app folder at the NTFS file system level.

**![assigning edit permissions on folder for regular users](http://woshub.com/wp-content/uploads/2019/04/assigning-edit-permissions-on-folder-for-regular-u.png)**

**Note**. Actually, it is not recommended to store the changing application data in its own folder under C:\\Program Files. It’s better to store the app data in the user profile. But it is a question of laziness and incompetence of the app developers.

## How to run a program that requires admin privileges under standard user?

Earlier we described how to [disable a UAC prompt for the certain app](http://woshub.com/how-to-disable-uac-for-specific-applications/) using **RunAsInvoker** parameter. However, this method is not flexible enough.

You can also use [RunAs](http://woshub.com/run-program-as-different-user-windows/) with the saved administrator password (in the Windows Credentials Manager) using the `/SAVECRED` option. It is also insecure because the user can use the saved administrator credentials password to run any program on this computer.

Let’s consider an easier way to force any program to run without administrator privileges (without entering the admin password) and with UAC enabled (Level 4, 3 or 2 of the [UAC slider](http://woshub.com/user-account-control-slider-and-group-policy-settings/)).

Let’s take the Registry Editor as an example — **regedit.exe** (it is located in the C:\\Windows\\ folder). Notice the UAC shield next to the app icon. This icon means that elevation of privileges via UAC will be requested to run this program.

[![uac shield next to the app icon on windows10](http://woshub.com/wp-content/uploads/2019/04/uac-shield-next-to-app-icon-windows10.jpg)](http://woshub.com/wp-content/uploads/2019/04/uac-shield-next-to-app-icon-windows10.jpg)

If you run `regedit.exe`, you will see a User Account Control window asking for the administrator credentials (`Do you want to allow this app to make changes to your device?`). If you do not provide a password and do not confirm elevation, the app won’t start.

[![uac prompts for admin password to run program](http://woshub.com/wp-content/uploads/2019/04/uac-prompts-admin-password-to-run-app.jpg)](http://woshub.com/wp-content/uploads/2019/04/uac-prompts-admin-password-to-run-app.jpg)

Let’s try to bypass the UAC request for this program. Create the text file **run-as-non-admin.bat** containing the following code on your Desktop:

`cmd /min /C "set __COMPAT_LAYER=RUNASINVOKER && start "" %1"`

To force the regedit.exe to run without the administrator privileges and to suppress the UAC prompt, simple drag the EXE file you want to start to this BAT file on the desktop.

![run a program under user with UAC prompt bypass ](http://woshub.com/wp-content/uploads/2019/04/run-a-program-under-user-with-uac-prompt-bypass.png)

Then the Registry Editor should start without a UAC prompt and without entering an administrator password. If you open the Task Manager and add the **Elevated** column, you will see that there is the regedit.exe process without the elevated status (run with non-admin user permissions).

[![task manager not elevated app](http://woshub.com/wp-content/uploads/2019/04/task-manager-not-elevated-app.jpg)](http://woshub.com/wp-content/uploads/2019/04/task-manager-not-elevated-app.jpg)

Try to edit any parameter in the HKEY\_LOCAL\_MACHINE registry hive. As you can see, a user cannot edit the item in this registry key (the user doesn’t have write permissions to the system registry keys). But you can add or edit registry keys and parameters in your user hive — HKEY\_CURRENT\_USER.

![regedit run as standard user without admin rights ](http://woshub.com/wp-content/uploads/2019/04/regedit-run-as-standard-user-without-admin-rights.png)

In the same way you can run any app using the BAT file. Just specify the path to the executable file.

**run-app-as-non-admin.bat**  
`Set ApplicationPath="C:\Program Files\SomeApp\testapp.exe"   cmd /min /C "set __COMPAT_LAYER=RUNASINVOKER && start "" %ApplicationPath%"`

You can also add a context menu that allows to run all apps without elevation. To do it, create the RunAsUser.REG file, copy the following code into it, save and import it into the Windows registry by double clicking on the reg file (you will need administrator permissions to apply this change).

Windows Registry Editor Version 5.00
\[HKEY\_CLASSES\_ROOT\\\*\\shell\\forcerunasinvoker\]
@="Run as user without UAC privilege elevation"
\[HKEY\_CLASSES\_ROOT\\\*\\shell\\forcerunasinvoker\\command\]
@="cmd /min /C \\"set \_\_COMPAT\_LAYER=RUNASINVOKER && start \\"\\" \\"%1\\"\\""

[![add run without uac elevation to file explorer on win10](http://woshub.com/wp-content/uploads/2019/04/add-run-without-uac-elevation-to-file-explorer.jpg)](http://woshub.com/wp-content/uploads/2019/04/add-run-without-uac-elevation-to-file-explorer.jpg)

After that, to run any application without the administrator privileges, just select “**Run as user without UAC privilege elevation**” in the context menu of File Explorer.

![Run program as user without UAC privilege elevation](http://woshub.com/wp-content/uploads/2019/04/run-program-as-user-without-uac-privilege-elevatio.png)

Let me remind you once again that using the program in the RUNASINVOKER mode won’t allow you to elevate the program. The RunAsInvoker suppresses UAC prompt and tells the program that it should run with the permissions of the current user, and not ask for elevation of privileges. If a program really needs elevated privileges to edit system settings or files, it won’t work or will ask for admin permissions again.

## How to Bypass UAC with RunAsInvoker in \_\_COMPAT\_LAYER?

The environment variable \_\_COMPAT\_LAYER allows you to set different compatibility levels for the applications (the **Compatibility** tab in the properties of an EXE file). Using this variable, you can specify the compatibility settings to be used when starting a program. For example, to start an app in Windows 8 compatibility mode and 640×480 resolution, set the following:

`set __COMPAT_LAYER=Win8RTM 640x480`

![run an ap in windows compatibility mode](http://woshub.com/wp-content/uploads/2019/04/run-an-ap-in-windows-compatibility-mode.png)

The \_\_COMPAT\_LAYER variable has some options we are interested in. There are the following parameters:

-   **RunAsInvoker** – run an app with the privileges of a parent process without the UAC prompt;
-   **RunAsHighest** – run a program with the highest-level permission available to the user (the UAC prompt will appear if a user has the administrator privileges);
-   **RunAsAdmin** – run an app as administrator (the UAC prompt appears each time).

It means that the RunAsInvoker parameter doesn’t provide the administrator permissions, but only suppresses the UAC prompt.

The following CMD code enables the RunAsInvoker mode for the current process and runs the specified program without elevation:

`set __COMPAT_LAYER=RUNASINVOKER   start "" "C:\Program Files\MyApp\testapp.exe"`

## Enable RunAsInvoker Mode in the EXE File Manifest

As we said above, Windows 10 displays a UAC shield icon for programs that require elevation to run. Developers set this requirement when compiling the application in the program **manifest** .

You can edit the manifest of any exe file and disable the requirement to run the program in elevated mode.

To edit the program manifest, you can use the free **Resource Hacker** tool. Open the executable file of the app in Resource Hacker.

In the tree on the left, go to the Manifest section and open the program manifest. Pay attention to the following xml section:

<requestedPrivileges>
<requestedExecutionLevel level="requireAdministrator" uiAccess="false"/>
</requestedPrivileges>

It is thanks to the **requireAdministrator** option that Windows always tries to run this program as an administrator.

Change requireAdministrator to **asInvoker** and the save changes in exe file.

[![edit manifest of the exe file add asInvoker option](http://woshub.com/wp-content/uploads/2019/04/edit-exe-file-manifest-add-asInvoker.jpg)](http://woshub.com/wp-content/uploads/2019/04/edit-exe-file-manifest-add-asInvoker.jpg)

Note that now the UAC shield has disappeared from the program icon, and you can run it without asking for administrator password with the current user permissions.

[![remove uac shield from app icon via manifest](http://woshub.com/wp-content/uploads/2019/04/remove-uac-shield-from-app-icon-via-manifest.jpg)](http://woshub.com/wp-content/uploads/2019/04/remove-uac-shield-from-app-icon-via-manifest.jpg)

If the executable app file is signed with MS Authenticode ([Code Signing certificate](http://woshub.com/how-to-sign-powershell-script-with-a-code-signing-certificate/)), then after modifying the exe file, it may stop working or issue a warning.

In this case, you can force the program to use an external manifest file. Create a plain text file **appname.exe.manifest** (for example, `Autologon.exe.manifest`) in the directory with the exe file and copy the manifest code from Resource Hacker into it. Change requireAdministrator to **asInvoker**. Save the manifest file.

To have Windows always try to use the external manifest file when launching exe files, enable a special registry parameter:

`REG ADD "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\SideBySide" /v PreferExternalManifest /t REG_DWORD /d 1 /f`

Restart Windows and make sure the program is using an external manifest file that says to run without administrator privileges.