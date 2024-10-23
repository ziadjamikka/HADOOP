the steps for installing Hadoop:

 Step One: Install Java and Hadoop

  1. Install JDK (Java Development Kit)
   a. Download JDK version 8 from [this link](https://www.oracle.com/eg/java/technologies/downloads/#java8-windows).
   
   b. Create a folder named `java` in the root of Local Disk C (`C:\java`).
   
   c. Install the downloaded JDK into this newly created folder (`C:\java`).

   d. After the installation, delete any existing Java folders from the `Program Files` directory on Local Disk C (if applicable).

  2. Install Apache Hadoop
   a. Download Hadoop 3.3.6 from [this link](https://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-3.3.6/hadoop-3.3.6.tar.gz).
   
   b. Extract the downloaded Hadoop folder and move it to the root of Local Disk C. Rename the folder to `hadoop` (`C:\hadoop`).
   
   c. Delete the existing `bin` folder inside the Hadoop directory.
   
   d. Replace the deleted `bin` folder with the one available for download [here](https://drive.google.com/file/d/1nCN_jK7EJF2DmPUUxgOggnvJ6k6tksYz/view) and copy it into the Hadoop directory (`C:\hadoop`).


Step Two: Create Environment Variables for Hadoop and Java

 1. Open the Environment Variables settings:
   a. Search for "Environment Variables" in the Start menu and open it.
   
   b. Click on "Environment Variables."

 2. Set the `HADOOP_HOME` and `JAVA_HOME` variables:
   a. Under "User Variables," click "New."
   
   b. Set the `HADOOP_HOME` variable:
   - Variable name: `HADOOP_HOME`
   - Variable value: The path to the Hadoop folder (`C:\hadoop`).
   
   c. Set the `JAVA_HOME` variable:
   - Variable name: `JAVA_HOME`
   - Variable value: The path to the Java JDK (`C:\java\jdk-1.8`).

 3. Edit the system `Path` variable:
   a. In the "System Variables" section, select "Path" and click "Edit."
   
   b. Add the following paths:
   - `C:\hadoop\bin`
   - `C:\hadoop\sbin`
   - `C:\java\jdk-1.8\bin`
   
   c. Click "OK" after adding each path.

 4. Edit `hadoop-env.cmd`:
   a. Navigate to `C:\hadoop\etc\hadoop`.
   
   b. Open the file `hadoop-env.cmd` for editing.
   
   c. Locate the line containing `set JAVA_HOME=` and modify it to:
   bash
   set JAVA_HOME=C:\java\jdk-1.8
   



Step Three: Verify Hadoop and Java Installation

 1. Open the Command Prompt (CMD):
   a. Type `hadoop -version` and press Enter.
   
   b. If installed correctly, you should see output similar to:
   ```
   java version "1.8.0_431"
   Java(TM) SE Runtime Environment (build 1.8.0_431-b10)
   Java HotSpot(TM) 64-Bit Server VM (build 25.431-b10, mixed mode)
   ```
   
   c. Type `java -version` and press Enter to verify the Java installation.



Step Four: Edit Hadoop Configuration Files

 1. Navigate to the Hadoop configuration directory:
   a. Open the directory `C:\hadoop\etc\hadoop`.

  2. Edit the following files:

   **For `core-site.xml`:
   ```xml
   <property>
     <name>fs.defaultFS</name>
     <value>hdfs://localhost:9000</value>
   </property>
   ```

   For `hdfs-site.xml`:
   ```xml
   <property>
     <name>dfs.replication</name>
     <value>1</value>
   </property>
   <property>
     <name>dfs.namenode.name.dir</name>
     <value>C:\hadoop\data\namenode</value>
   </property>
   <property>
     <name>dfs.datanode.data.dir</name>
     <value>C:\hadoop\data\datanode</value>
   </property>
   ```

   For `mapred-site.xml`:
   ```xml
   <property>
     <name>mapreduce.framework.name</name>
     <value>yarn</value>
   </property>
   ```

   or `yarn-site.xml`:
   ```xml
   <property>
     <name>yarn.nodemanager.aux-services</name>
     <value>mapreduce_shuffle</value>
   </property>
   <property>
     <name>yarn.nodemanager.auxservices.mapreduce.shuffle.class</name>
     <value>org.apache.hadoop.mapred.ShuffleHandler</value>
   </property>
   ```

---

 Step Five: Install Additional Tools

 1. Install `MSVCR120.DLL`:
   a. Download the `MSVCR120.DLL` file from [this link](https://www.dll-files.com/msvcr120.dll.html).
   
   b. Extract the file and place it in the `System32` folder (`C:\Windows\System32`).

2. Install Microsoft Visual C++ Redistributable:
   a. Download the latest version from [this link](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170).
   
   b. Install the redistributable package.

---

 Step Six: Start Hadoop

1. Format the NameNode:
   a. Open CMD and type:
   ```bash
   hdfs namenode -format
   ```

2. Start Hadoop:
   a. Navigate to the Hadoop `sbin` directory:
   ```bash
   cd C:\hadoop\sbin
   ```
   
   b. Start the Distributed File System (DFS):
   ```bash
   start-dfs.cmd
   ```
   - Two terminals should open. Allow Java through public networks when prompted.

 3. Verify Hadoop Services:
   a. In CMD, type:
   ```bash
   jps
   ```
   - This should display the running services, including `NameNode` and `DataNode`.

 4. Start YARN:
   a. In CMD, type:
   ```bash
   start-yarn.cmd
   ```
   - Two additional terminals should open.

 5. Verify YARN Services:
   a. In CMD, type:
   ```bash
   jps
   ```
   - This should display `ResourceManager` along with `NameNode` and `DataNode`.

 6. Access Hadoop through the browser:
   a. Open your web browser and visit:
   ```bash
   http://localhost:9870/
   ```
   b. If everything is set up correctly, you will see the Hadoop interface.

---
