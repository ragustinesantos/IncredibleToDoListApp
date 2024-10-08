# **System Requirements**

- Intel Core i5 or higher
- A minimum of 8GB of RAM; 16GB is recommended
- At least 10GB of free disk space

# **Software Requirements**

- For Windows, React Native supports all Windows 11 devices.
- Windows 10 devices can be supported with version 10.0.16299.0 or higher.

# **Installation Instructions**

   ## **Chocolatey**
   
   Chocolatey is a package manager for Windows which can help you with the installation of the other applications required to run React Native.
   
   You can install Chocolatey using PowerShell but to ensure that your installation is successful, you will need to run the following:
   
   ```bash
   Set-ExecutionPolicy Bypass -Scope Process -Force; \[System.Net.ServicePointManager\]::SecurityProtocol = \[System.Net.ServicePointManager\]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('<https://community.chocolatey.org/install.ps1>'))
   ```
   
   ## **Node and Java SE Development Kit (JDK)**
   
   After you have installed Chocolatey on your device, right click on your command prompt and select “Run as Administrator”. Afterwards, run the following command:

   ```bash
   choco install -y nodejs-lts microsoft-openjdk17
   ```
   <br>
   
   Afterwards, you may check your installation by going to the command prompt and running the following command:
   
   ```bash
   node -v
   ```
   
   ## **Android Development Environment**
   
   You may download Android Studio at <https://developer.android.com/studio> and simply follow the Setup Wizard.
   
   Ensure that the following items are selected for the installation:
   
   1. Android SDK
   2. Android SDK Platform
   3. Android Virtual Device
   4. Performance (Intel ® HAXM) – Only if you are not already using HyperV
   
   After selecting this options from the wizard, you may proceed with the installation by clicking on “Next”.
   
   ## **Installing Android SDK**
   
   Building a React Native App requires Android 14 (UpsideDownCake) SDK. While Android Studio installs the latest Android SDK by default, you can install additional SDKs through the SDK Manager in Android Studio:
   
   1. Once you open Android Studio, you may click on _More Actions_ button and select _SDK Manager_.
   2. Select the _SDK Platforms_ tab and check the box next to _Show Package Details_ in the bottom right corner.
   3. Expand the Android 14 (UpsideDownCake) selection and check the following items:
      1. Android SDK Platform 34
      2. Intel x86 Atom_64 System Image or Google APIs Intel x86 Atom System Image
   5. Select the _SDK Tools_ tab and check the box next to _Show Package Details_ and expand the Android SDK Build-Tools selection and select the following:
      1. 34.0.0
   7. Click _Apply_ to download and install the Android SDK and build tools

# **Configuration Steps**

   ## **Android Path**
   
   To proceed with building applications with native code, we will need to set up environment variables:
   
   1. Open _Windows Control Panel_
   2. Click on _User Accounts_, then click _User Accounts_ again.
   3. Click on _Change my environment variables_
   4. Click on _New_ and on the _Edit User Variable_ window place “ANDROID_HOME” on the _Variable Name_ field and place your Android SDK path in the _Variable Value_ (path ex. C:\\Users\\{username}\\AppData\\Local\\Android\\Sdk)
   
   To verify if the configuration was successfully implemented, you may copy and paste **_Get-ChildItem -Path Env:\\_** into _PowerShell_. In the result, you should be able to see that “ANDROID_HOME” has been added.
   
   ## **Platform-tools**
   
   To configure platform-tools, the process is similar to the Android Path but with a few differences in the location:
   
   1. Open _Windows Control Panel_ and select _User Accounts_
   2. Select _User Accounts_ again and click on _Change my environment variables_
   3. The _Environment Variables_ window will then pop up and, to avoid path errors, in the _System Variables_ window, select the _Path_ variable and click _Edit._
   4. Click _New_ and add the platform-tools path to the list (default path: %LOCALAPPDATA%\\Android\\Sdk\\platform-tools)
   
   ## **Configuring the virtual device**
   
   In Android Studio, if you’re using it for the first time, you will need to create a new AVD (Android Virtual Device).
   
   1. Select _Create Virtual Device_
   2. You may choose any phone from the list and click _Next_
   3. Select _UpsideDownCakeAPI Level 34 image_
   4. Click _Next_ and then _Finish_ to create the AVD.
   
   After these steps, click on the green triangle button next to the AVD to launch it.
   
   # **Project Creation**
   
   To create a new project, in your terminal, go to the location where you want your project folder to be installed and run this command (you may replace “AwesomeProject” with any project name you desire):

   ```bash
   npx @react-native-community/cli@latest init AwesomeProject
   ```
   
   # **Running the Project**
   
   After your project has been created, move to the directory of your project (ex. cd _ProjectName)_ and run the following command:

   ```bash
   npm start
   ```
   <br>
   
   This will start the Metro Development Server.
   
   Once the necessary files have been installed by Metro, instructions from the CLI will ask you to type in a letter to select a development server to run. Type in “a” to run the Android selection.
   
   After all the set up has been completed by Metro, open another terminal and run the following command:

   ```bash
   npm run android
   ```
   <br>
   
   To verify if your application is working, you should be able to see your app running in the Android emulator.

# **Troubleshooting**

   - **Terminating a process on port 8081** – run the following commands to identify the id listening on port 8081 and terminate the process:

   ```bash
   sudo lsof -i :8081
   ```
   
   ```bash
   kill -9 &lt;PID&gt;
   ```

   <br>
   
   - **To run a port other than 8081** – run this command from the root of your project which makes use of the _port_ parameter (you my select another port other than the one in the example):

   ```bash
   npm start -- --port=8088
   ```

   <br>
   
   - **NPM locking** – to address instances where your npm locks, run the following commands while using the React Native CLI:

   ```bash
   sudo chown -R $USER ~/.npm
   ```

   ```bash      
   sudo chown -R $USER /usr/local/lib/node_modules
   ```

   <br>
   
   - **react-native init hangs –** In cases where running the initialization script hangs (init) try to run these commands to allow you to view possible causes for the errors in the logs:

   ```bash
   npx react-native init –verbose
   ```

   ```bash
   npm run android -- --verbose
   ```

   <br>
   
   - **Missing Dependencies** – to address missing dependencies, you may need to reinstall them by running this command:

   ```bash
   npm i
   ```

   <br>
   
   - **Clearing Android Cache** – In instances where the application encounters build failures and fails to send it over to the Android emulator, you may clear the cache to allow for rebuilding of the tool by running the command:

   ```bash
   npm run android -- --clear-cache
   ```

   <br>
   
   - **Rebuilding the Android Gradle File** – Another option for when the application encounters build errors is to go to the directory where your gradle file is found (ex. cd android) and run the following command:

   ```bash
   ./gradlew
   ```

# **Resources**

   The information on this document were referenced from these sources. For additional information you may refer to these resources as well:
   
- <https://chocolatey.org/install> - In this link, you will be able to learn about setting up the Chocolatey package manager.

- <https://reactnative.dev/docs/set-up-your-environment> - This link will provide you with the necessary information about setting up the whole react native environment on your computer which includes the package managers, setting up the environment variables and installing the necessary mobile device emulators.

- <https://intellipaat.com/blog/react-native-environment-setup/> - This link will be helpful in understanding the hardware and software requirements of React Native even before you begin setting it up in your device.

- <https://openjdk.org/projects/jdk/17/> - This link will provide you with more information about the Java Development Kit and will especially be helpful in instances where you're encountering installation issues with it.

- <https://developer.android.com/studio/install> - This link will provide you with the necessary instructions for installing Android Studio along with its SDKs and development environment.

- <https://reactnative.dev/docs/getting-started-without-a-framework> - In this link, you will be able learn how to initialize your first application after your environment has been set up. This includes instructions to start the development server and bridge the application to the AVD emulator.

- <https://docs.npmjs.com/downloading-and-installing-node-js-and-npm> - This link is helpful if you have not downloaded the node package manager before hand as it will provide instructions on the installation and set up of Node.js
