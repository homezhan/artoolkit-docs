# Setting an Environment Variable

Environment variables can be used to specify configuration information to software.

## Set an environment variable for a single command shell

An environment variable can be set temporarily in a single shell, and will only affect applications launched from that shell. Once the shell is closed (e.g. on a logout or reboot) the environment variable is removed.

### Windows

From a "cmd.exe" shell, use the 'set' command:
<pre> set NAME=value </pre>

### Mac OS X / Linux

The syntax varies depending on the shell you're using. First, open a Terminal window, then if using bash (default on Linux and Mac OS X) type:
<pre> NAME=VALUE; export NAME </pre>
or if using csh or tcsh:
<pre> setenv NAME VALUE </pre>

## Set an environment variable persistently

If you wish to retain an environment variable across shells and reboots etc., use this method:

### Windows

First, open the "Environment variables" editor. Its location is a little bit hidden.

Windows XP:

Image:Windows_system_control_panel.png|Open the system control panel
Image:Windows_env_vars_button.png|Click the "Environment variables" button

Windows 7:

Image:Windows_7_system_control_panel_1.png|In Windows 7 Control Panel, choose "System and Security"
Image:Windows_7_system_control_panel_2.png|Next, click on the heading "System"
Image:Windows_7_system_control_panel_3.png|Next, click on "Advanced system settings" in the sidebar
Image:Windows_7_system_control_panel_4.png|Next, click the "Environment variables" button

On the left hand side of the window, you will see the environment variable name, and on the right hand side the variables value. Variables can be set either just for the current user or system-wide for all users.

*Windows stores system-wide environment variables in the registry, as a string under the key HKLM\\System\\CurrentControlSet\\Control\\Session Manager\\Environment*

### Mac OS X

1.  Environment variables can be set from a Terminal window.
2.  From a terminal window, type the following lines, replacing "NAME" with the environment variable name and "VALUE" with its value:

<pre>
echo "NAME=VALUE; export NAME" >> ~/.profile
echo "setenv NAME VALUE" >> ~/.cshrc
defaults write ~/.MacOSX/environment NAME -string "VALUE"; plutil -convert xml1 ~/.MacOSX/environment.plist
</pre>

The first line sets the environment for users with users with sh or bash as their shell, the second for users with csh or tcsh as their shell, and the third for programs launched by the Finder (including Xcode).

### Linux

1.  Environment variables can be set from a Terminal window.
2.  From a terminal window, type the following lines, replacing "NAME" with the environment variable name and "VALUE" with its value:

<pre>
echo "NAME=VALUE; export NAME" >> ~/.profile
echo "setenv NAME VALUE" >> ~/.cshrc
</pre>

The first line sets the environment for users with users with sh or bash as their shell, the second for users with csh or tcsh as their shell.