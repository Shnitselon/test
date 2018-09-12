
<link rel="stylesheet" Type="text/css" href="../README/styles.css">

# Shell L1 Driver Standard
<a name="CreateNewDriver"></a>

### Creating a new driver and installing the driver's environment

1. Start a new project with [shellfoundry](https://github.com/QualiSystems/shellfoundry), better to do that in the *Drivers* folder on the Quali Server machine, usually this is *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers*:

{% highlight bash %}
shellfoundry new DriverName --template layer-1-switch
{% endhighlight %}

2. To install the driver's environment and dependencies defined in the driver's *requirements.txt* file, in command-line, navigate to the *~\QualiSystems\CloudShell\Server* folder and run the appropriate command:
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If you're using Quali's default python interpreter (at *~\QualiSystems\CloudShell\Server\python*), run the following:

{% highlight bash %}
install_driver.bat
{% endhighlight %}

However, if you want to use a different python interpreter, you will need to install the *virtualenv* package by running *<interpreter-path>\python.exe -m pip install virtualenv* using your python interpreter and then running the command:

{% highlight bash %}

install_driver.bat "<interpreter-path>\python.exe".
{% endhighlight %}
You can specify the driver's python interpreter by adding it as a first argument to the script.


The driver is installed.

3. To verify, return to the CloudShell Drivers folder at *~\QualiSystems\CloudShell\Server\Drivers*, and run the new driver exe file.


### Implementing the driver in CloudShell

Now that you have a new driver, it is time to implement the driver's commands. Note that at this point, the L1 driver includes the command structure but no working commands.

1. Implement methods of the *DriverCommands* class in *<project_slug>/driver_commands.py*. Follow the [DEVGUIDE](https://github.com/QualiSystems/shell-L1-standard/blob/dev/DEVGUIDE.md) and docstrings with description, as an example of an L1 driver with CLI usage you can reffer to the [cloudshel-L1-mrv](https://github.com/QualiSystems/cloudshell-L1-mrv) project.
To debug the driver, use the [DEBUGGING GUIDE](https://github.com/QualiSystems/shell-L1-template/blob/dev/DEBUGGING.md).

2. Update the driver version in the *version.txt* file.
<a name="CreateNewDriver"></a>

### Testing in CloudShell

Do the following in Resource Manager Client.

1. Import the new data model. 
a. In the **Resource Families** explorer, right-click **Resource Families** and selct **Import**.
b. In the driver package's *datamodel* folder, select the *<driver0name>_ResourceConfiguration.xml* file and click **Open**.
2. Create an L1 resource. 
a. In **Resource Explorer**, right click **Root** and create a new resource.
b. Give it a **Name**, and the device's **Address**. 
c. Select the L1 Switch **Family** and make sure the correct **Model** and **Driver** are selected.
d. Click **OK**.
3. [Follow this guide](http://help.quali.com/Online%20Help/8.3/Portal/Content/Admn/Cnct-Ctrl-L1-Swch.htm) to set the timeout period, auto load it and configure its physical connections

When you run Autoload (or any other command later), the log files are created under the *~\QualiSystems\CloudShell\Server\Logs* folder.

4. After validating Autoload, you can validate the mapping functions either in Resource Manager Client (in the L1 resource's **Settings>Mappings** page, or in CloudShell Portal, by [building a blueprint](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Rsc-Cnct/Phys-Ntwrk-Crt.htm) with 2 resources and a route, then reserving this blueprint and connecting the route.


**Build the driver's package:**

Once you’ve finished implementing and testing the driver, it’s time to create a package to be used in your CloudShell production environment. Note that you can skip this step altogether if you developed your driver in the production environment.

* In the driver's folder run command *Scripts\build_driver.exe*. It will create a zip package *dist\cloudshell-L1-DriverName-1.0.1.zip*
    
{% highlight bash %}
Scripts\build_driver.exe
{% endhighlight %}
 
    
### Install the driver's package

1. Extract the driver's package to the Drivers folder *C:\\Program Files (x86)\\QualiSystems\\CloudShell\\Server\\Drivers*
2. Navigate to the extracted folder and install the driver, as explained in [Create a new driver and install the driver's environment](#CreateNewDriver)
3. Follow the steps in [Testing in CloudShell](#CreateNewDriver) to install the driver on CloudShell.


