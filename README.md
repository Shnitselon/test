

# Shell L1 Driver Standard
<a name="CreateNewDriver"></a>

### Creating a new driver and installing the driver's environment

1. Start a new project with [shellfoundry](https://github.com/QualiSystems/shellfoundry). We recommend to do that in CloudShell's *Drivers* folder (usually at *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers* on the Quali Server machine):

    `shellfoundry new DriverName --template layer-1-switch`

2. To install the driver's environment and dependencies defined in the driver's *requirements.txt* file, in command-line, navigate to the *~\QualiSystems\CloudShell\Server* folder and run the appropriate command:
 
    * If you're using Quali's default python interpreter (at *~\QualiSystems\CloudShell\Server\python*), run the following:

        `install_driver.bat`

    * If you want to use a different python interpreter, you will need to  and then running the command:
        1. Install the *virtualenv* package by running:
        
        `<interpreter-path>\python.exe -m pip install virtualenv` using your python interpreter
        2. And then run:
        
            `install_driver.bat "<interpreter-path>\python.exe"`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The driver is installed.

3. To verify, return to the *\Drivers* folder at *~\QualiSystems\CloudShell\Server\Drivers*, and run the new driver exe file.


### Implementing the driver in CloudShell

Now that you have a new driver, it is time to implement the driver's commands. Note that at this point, the L1 driver includes the command structure but no working commands.

1. Implement methods of the *DriverCommands* class in *<project_slug>/driver_commands.py*. 

    * Follow the [DEVGUIDE](https://github.com/QualiSystems/shell-L1-standard/blob/dev/DEVGUIDE.md) and docstrings with description, as an example of an L1 driver with CLI usage you can refer to the [cloudshel-L1-mrv](https://github.com/QualiSystems/cloudshell-L1-mrv) project.
    * To debug the driver, use the [DEBUGGING GUIDE](https://github.com/QualiSystems/shell-L1-template/blob/dev/DEBUGGING.md).

2. Update the driver's version in the *version.txt* file.
<a name="CreateNewDriver"></a>

### Testing in CloudShell

Do the following in Resource Manager Client.

1. Import the new data model. 
    1. In the **Resource Families** explorer, right-click **Resource Families** and selct **Import**.
    2. In the driver package's *datamodel* folder, select the *<driver0name>_ResourceConfiguration.xml* file and click **Open**.
2. Create an L1 resource. 
    1. In **Resource Explorer**, right click **Root** and create a new resource.
    2. Give it a **Name**, and the device's **Address**. 
    3. Select the L1 Switch **Family** and make sure the correct **Model** and **Driver** are selected.
    4. Click **OK**.
    
3. [Follow this guide](http://help.quali.com/Online%20Help/9.0/Portal/Content/Admn/Cnct-Ctrl-L1-Swch.htm) to set the timeout period (for L1 drivers in CloudShell), autoload and configure your L1 resource's physical connections

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Autoload and any other commands executed on the L1 resource are logged at *~\QualiSystems\CloudShell\Server\Logs*.

4. After validating Autoload, you can validate the mapping functions either in Resource Manager Client (in the L1 resource's **Settings>Mappings** page, or in CloudShell Portal, by [building a blueprint](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Rsc-Cnct/Phys-Ntwrk-Crt.htm) with 2 resources and a route, then reserving this blueprint and connecting the route.


### Building and installing the driver's package on CloudShell:**

Once you’ve finished implementing and testing the driver, it’s time to create the shell package and install it in your CloudShell production environment. Note that you can skip this section altogether if you developed your driver in the production environment.

1. From the *\Drivers* folder, run the following command:
    
        `Scripts\build_driver.exe`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The L1 shell package is created in the shell project's *dist* folder, bearing the shell's name and version.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;For example: *dist\cloudshell-L1-DriverName-1.0.1.zip*

2. Extract the driver's package to the *\Drivers* folder *C:\\Program Files (x86)\\QualiSystems\\CloudShell\\Server\\Drivers*
3. Navigate to the extracted folder and install the driver, as explained in [Create a new driver and install the driver's environment](#CreateNewDriver)
4. Follow the steps in [Testing in CloudShell](#CreateNewDriver) to install the driver on CloudShell.


