<!--
  howto.md
  A step-by-step guide to integrate MySQL with Syncfusion Scheduler Application using PHP.
-->
# How to integrate MySQL with Syncfusion Scheduler Application using PHP.

This repository contains a sample full-stack application demonstrating how to synchronize events between MySQL and the Syncfusion Scheduler component using PHP.

## Prerequisites
- MySQL(>= 8.0.41.0)
- XAMPPSERVER(>= 8.2.12)
- A MySQL Database with Username , Password and DataBase (Download at https://dev.mysql.com/downloads/installer/)
- XAMPPSERVER For PHP using apachae server(Download at https://www.apachefriends.org/download.html)
- Basic familiarity with MySQL and PHP
- Make sure the ports nothing run on 80 , 3306

## Project Structure
```
├── README.md                  # This guide
├── DB
│   ├── scheduledb.sql         # DB Query
├── index.php
└── server.php                 # Database Configuration
```  
## Setup and Cloning the repository

### MySQL Configuration
- Create Username , Password and DataBase in MySQL
- In `server.php` file update the username, password, and dbname as per the database configuration.
- The SQL query required for creating the necessary table is being located in the `scheduledb.sql` file within the DB folder.
- In your Database it automatically create a table with the necessary fields

### Start Xampp Server

- After the successful installation of the XAMPP server, launch the application and start the Apache server.
- Move the `Javascript-Scheduler-CRUD-PHP-and-MySQL` repository files in the XAMPP server's root directory, specifically at `C:\xampp\htdocs`.
- Upon completion, Launch a web browser and navigate to `localhost`, you will be able to see the server running.
- Next, Navigate to `localhost/Javascript-Scheduler-CRUD-PHP-and-MySQL` in your web browser. You will now be able to access the running Syncfusion scheduler application.
- Now, you can perform the CRUD operations it will be reflected on MySQL Database.

## Running the application

1. **Start XAMPP services**
  - Open **XAMPP Control Panel**
  - Start **Apache**

2. **Place project files**
  - Copy the project folder `Javascript-Scheduler-CRUD-PHP-and-MySQL` into:
     ```
     C:\xampp\htdocs\
     ```

3. **Open in browser**
  - Go to: `http://localhost/`
   
  - Then open the app:
     ```
     http://localhost/Javascript-Scheduler-CRUD-PHP-and-MySQL
     ```
4. You can perform CRUD operation on the scheduler that will be reflected in the MySQL database table.

## Output Preview
![Frontend Preview](./SampleOutputs/frontend.png)
*Image illustrating the Syncfusion Scheduler Component*

![Database Preview](./SampleOutputs/database.png)
*Image illustrating the events of Syncfusion Scheduler in MySQL*

## Troubleshooting
- **Page Not Found**:Check the file path correctly in the browser search bar
- **Apache Server port stopped in XAMPPSERVER**: Change the Port no in config file and mentioned the port no in url and crudurl in index.php.
- **Refused to Connect with server**: Check the url and crudurl in index.php.

## How To Integrate and build from scratch
### A step by step guide integrate Syncfusion JavaScript Scheduler with MySQL and PHP.

### XAMPP Server

1. Download XAMPPSERVER from [XAMPP Server](https://www.apachefriends.org/download.html).

2. Setup the application by  Run the Installer and keep default component selection.

3. Select Installation folder and Complete Installation

4. Start XAMPP Control Panel and you see the services , click start next to Apache

### MySQL Configuration

1. Download MySQL from [MySQL](https://dev.mysql.com/downloads/installer/)

2. Setup the application by Run the Installer and keep default configuration.

3. Create a new MySQL Database along with Username , Password.

### Connect MySQL with XAMPPSERVER
1. Create your project folder 
2. Create a gitleaks.yaml inside .github/workflows to tool used to what to scan and what to ignore.
    ```bash
    name: Secret Value found!!
    on:
    push:
        public:
    jobs:
      scan:
        name: gitleaks
        runs-on: ubuntu-latest
        steps:
         - name: Checkout
           uses: actions/checkout@v4.2.2 
         - name: Install the gitleaks
           run: wget https://github.com/zricethezav/gitleaks/releases/download/v8.15.2/gitleaks_8.15.2_linux_x64.tar.gz
           shell: pwsh
         - name: Extract the tar file
           run: tar xzvf gitleaks_8.15.2_linux_x64.tar.gz
         - name: Generate the report
           id: gitleaks
           run: $GITHUB_WORKSPACE/gitleaks detect -s $GITHUB_WORKSPACE -f json -r $GITHUB_WORKSPACE/leaksreport.json
           shell: bash
           continue-on-error: true
         - name: Setup NuGet.exe
           if: steps.gitleaks.outcome != 'success'
           uses: nuget/setup-nuget@v2
           with:
              nuget-version: latest
         - name: Install Mono
           if: steps.gitleaks.outcome != 'success'
           run: |
            sudo apt update
            sudo apt install -y mono-complete
         - name: Install the dotnet SDK to a custom directory
           if: steps.gitleaks.outcome != 'success'
           run: |
            mkdir -p $GITHUB_WORKSPACE/dotnet
            curl -sSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin --install-dir $GITHUB_WORKSPACE/dotnet --channel 6.0
         - name: Install the report tool packages
           if: steps.gitleaks.outcome != 'success'
           run: |
               export PATH=$GITHUB_WORKSPACE/dotnet:$PATH
               nuget install "Syncfusion.Email" -source ${{ secrets.NexusFeedLink }} -ExcludeVersion
               dir $GITHUB_WORKSPACE/Syncfusion.Email/lib/net6.0
               dotnet $GITHUB_WORKSPACE/Syncfusion.Email/lib/net6.0/GitleaksReportMail.dll ${{ secrets.CITEAMCREDENTIALS }} "$GITHUB_REF_NAME" ${{ secrets.NETWORKCREDENTIALS }} ${{ secrets.NETWORKKEY }} "$GITHUB_WORKSPACE" ${{ secrets.ORGANIZATIONNAME }}
               exit 1
      ```
3. Create a scheduledb.sql in DB folder to implement table creation query and sample data
    ```bash
      -- phpMyAdmin SQL Dump
      -- version 5.2.1
      -- https://www.phpmyadmin.net/
      --
      -- Host: 127.0.0.1
      -- Generation Time: Jan 18, 2026 at 10:30 AM
      -- Server version: 10.4.32-MariaDB
      -- PHP Version: 8.2.12

      SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
      START TRANSACTION;
      SET time_zone = "+00:00";


      /*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
      /*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
      /*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
      /*!40101 SET NAMES utf8mb4 */;

      --
      -- Database: `scheduledb`
      --

      -- --------------------------------------------------------

      --
      -- Table structure for table `appointments`
      --

      CREATE TABLE `appointments` (
        `Id` int(11) NOT NULL,
        `Subject` varchar(200) DEFAULT NULL,
        `StartTime` datetime NOT NULL,
        `EndTime` datetime NOT NULL,
        `StartTimezone` varchar(200) DEFAULT NULL,
        `EndTimezone` varchar(200) DEFAULT NULL,
        `Location` varchar(200) DEFAULT NULL,
        `Description` varchar(200) DEFAULT NULL,
        `IsAllDay` bit(1) NOT NULL,
        `RecurrenceID` int(11) DEFAULT NULL,
        `FollowingID` int(11) DEFAULT NULL,
        `RecurrenceRule` varchar(200) DEFAULT NULL,
        `RecurrenceException` varchar(200) DEFAULT NULL,
        `IsReadonly` bit(1) DEFAULT NULL,
        `IsBlock` bit(1) DEFAULT NULL,
        `RoomID` int(11) DEFAULT NULL
      ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

      --
      -- Dumping data for table `appointments`
      --

      INSERT INTO `appointments` (`Id`, `Subject`, `StartTime`, `EndTime`, `StartTimezone`, `EndTimezone`, `Location`, `Description`, `IsAllDay`, `RecurrenceID`, `FollowingID`, `RecurrenceRule`, `RecurrenceException`, `IsReadonly`, `IsBlock`, `RoomID`) VALUES
      (1, 'Meeting', '2026-01-16 00:00:00', '2026-01-17 00:00:00', NULL, NULL, '', '', b'1', NULL, NULL, 'FREQ=DAILY;INTERVAL=1;', '20221213T183000Z', NULL, NULL, 4),
      (2, 'edited', '2026-01-15 00:00:00', '2026-01-16 00:00:00', NULL, NULL, '', '', b'1', NULL, NULL, NULL, NULL, NULL, NULL, 4),
      (3, 'Edited event', '2026-01-17 00:00:00', '2026-01-18 00:00:00', NULL, NULL, '', '', b'1', NULL, NULL, NULL, NULL, NULL, NULL, 4);
      COMMIT;

      /*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
      /*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
      /*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;

    ```
4. Create a index.php for define url and scheduler component.
    ```bash
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <title>Essential Studio for JavaScript : Detail Template</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<link href="https://cdn.syncfusion.com/ej2/20.4.38/ej2-base/styles/material.css" rel="stylesheet" type="text/css"/>
        <link href="https://cdn.syncfusion.com/ej2/20.4.38/ej2-buttons/styles/material.css" rel="stylesheet" type="text/css"/>
        <link href="https://cdn.syncfusion.com/ej2/20.4.38/ej2-calendars/styles/material.css" rel="stylesheet" type="text/css"/>
        <link href="https://cdn.syncfusion.com/ej2/20.4.38/ej2-dropdowns/styles/material.css" rel="stylesheet" type="text/css"/>
        <link href="https://cdn.syncfusion.com/ej2/20.4.38/ej2-inputs/styles/material.css" rel="stylesheet" type="text/css"/>
        <link href="https://cdn.syncfusion.com/ej2/20.4.38/ej2-splitbuttons/styles/material.css" rel="stylesheet" type="text/css"/>
        <link href="https://cdn.syncfusion.com/ej2/20.4.38/ej2-lists/styles/material.css" rel="stylesheet" type="text/css"/>
        <link href="https://cdn.syncfusion.com/ej2/20.4.38/ej2-popups/styles/material.css" rel="stylesheet" type="text/css"/>
        <link href="https://cdn.syncfusion.com/ej2/20.4.38/ej2-navigations/styles/material.css" rel="stylesheet" type="text/css"/>
        <link href="https://cdn.syncfusion.com/ej2/20.4.38/ej2-schedule/styles/material.css" rel="stylesheet" type="text/css"/>
		<script src="https://cdn.syncfusion.com/ej2/20.4.38/dist/ej2.min.js" type="text/javascript"></script>
    </head>
    <body>    
    <?php
      // initialize scheduler
      echo '
      <div id="Schedule"></div>
      <script>
      var dataManager = new ej.data.DataManager({
	    url: "http://localhost/Javascript-Scheduler-CRUD-PHP-MySQL/server.php",
	    crudUrl: "http://localhost/Javascript-Scheduler-CRUD-PHP-MySQL/server.php",
	    adaptor: new ej.data.UrlAdaptor(),
	    crossDomain: true
    });
    var scheduleObj = new ej.schedule.Schedule({
		height: "550px",
        selectedDate: new Date(2026, 0, 16),
        views: ["TimelineDay", "TimelineWeek"],
        eventSettings: { dataSource: dataManager },
        group: {
            resources: ["MeetingRoom"]
        },
        resources: [{
                field: "RoomID", title: "Room Type",
                name: "MeetingRoom", allowMultiple: true,
                dataSource: [
                    { text: "Jammy", id: 1, color: "#ea7a57", capacity: 20, type: "Conference" },
                    { text: "Tweety", id: 2, color: "#7fa900", capacity: 7, type: "Cabin" },
                    { text: "Nestle", id: 3, color: "#5978ee", capacity: 5, type: "Cabin" },
                    { text: "Phoenix", id: 4, color: "#fec200", capacity: 15, type: "Conference" },
                    { text: "Mission", id: 5, color: "#df5286", capacity: 25, type: "Conference" },
                    { text: "Hangout", id: 6, color: "#00bdae", capacity: 10, type: "Cabin" },
                    { text: "Rick Roll", id: 7, color: "#865fcf", capacity: 20, type: "Conference" },
                    { text: "Rainbow", id: 8, color: "#1aaa55", capacity: 8, type: "Cabin" },
                    { text: "Swarm", id: 9, color: "#df5286", capacity: 30, type: "Conference" },
                    { text: "Photogenic", id: 10, color: "#710193", capacity: 25, type: "Conference" }
                ],
                textField: "text", idField: "id", colorField: "color"
            }],
      });
      scheduleObj.appendTo("#Schedule");
    </script>
      ';
      ?>
      </body>
      </html>
      ```
5. Create server.php and define the CRUD operations
    ```bash
    <?php
        $servername = "localhost";
		$username = "root";
		$password = "password";
		$dbname = "username";
	
		$conn = new mysqli($servername, $username, $password, $dbname);
		if($conn->connect_error) {        
			die("Connection failed" . $conn->connect_error);
		}

    header("Content-type:application/json; charset=UTF-8");
    header("Access-Control-Allow-Methods: *");
    header("Access-Control-Allow-Headers: *");
    header('Access-Control-Allow-Origin: *', false);
    if($_SERVER['REQUEST_METHOD'] == 'OPTIONS') {
        header( "HTTP/1.1 200 OK" );
        exit;
    }

    $json_param = file_get_contents('php://input');
    $param = json_decode($json_param,true);

    if(isset($param['action'])) {
        if ($param['action'] == "insert" || ($param['action'] == "batch" && !empty($param['added']))) {
            error_log("This is an error message");
            if ($param['action'] == "insert") {
                $id = isset($param['value']['Id']) ? $param['value']['Id'] : null;
                $subject = isset($param['value']['Subject']) ? $param['value']['Subject'] : null;
                $startTime = isset($param['value']['StartTime']) ? $param['value']['StartTime'] : null;
                $endTime = isset($param['value']['EndTime']) ? $param['value']['EndTime'] : null;
                $location = isset($param['value']['Location']) ? $param['value']['Location'] : null;
                $description = isset($param['value']['Description']) ? $param['value']['Description'] : null;
                $isAllDay = isset($param['value']['IsAllDay']) ? $param['value']['IsAllDay'] : null;
                $recurrenceId = isset($param['value']['RecurrenceID']) && $param['value']['RecurrenceID'] > 0 ? $param['value']['RecurrenceID'] : null;
                $recurrenceRule = isset($param['value']['RecurrenceRule']) ? $param['value']['RecurrenceRule'] : null;
                $recurrenceException = isset($param['value']['RecurrenceException']) && !empty($param['value']['RecurrenceException']) ? $param['value']['RecurrenceException'] : null;
                $roomId = isset($param['value']['RoomID']) && !empty($param['value']['RoomID']) ? $param['value']['RoomID'] : null;
    
                $startTime = clone new DateTime($startTime);
                $timezone = new DateTimeZone('Asia/Calcutta');
                $startTime->setTimezone($timezone);
                $startTime = $startTime->format('Y-m-d H:i:s');
                $endTime = clone new DateTime($endTime);
                $timezone = new DateTimeZone('Asia/Calcutta');
                $endTime->setTimezone($timezone);
                $endTime = $endTime->format('Y-m-d H:i:s');
               
                if($recurrenceRule == null) {
                    $sql = "INSERT INTO `appointments` (`Id`, `Subject`, `StartTime`, `EndTime`, `Location`, `Description`, `IsAllDay`, `RoomID`) VALUES ($id, '$subject', '$startTime', '$endTime', '$location','$description', $isAllDay, $roomId)";
                } else {
                    if($recurrenceId == null) {
                        $sql = "INSERT INTO `appointments` (`Id`, `Subject`, `StartTime`, `EndTime`, `Location`, `Description`, `IsAllDay`, `RecurrenceRule`, `RoomID`) VALUES ($id, '$subject', '$startTime', '$endTime', '$location','$description', $isAllDay, '$recurrenceRule', $roomId)";
                    } else {
                        $sql = "INSERT INTO `appointments` (`Id`, `Subject`, `StartTime`, `EndTime`, `Location`, `Description`, `IsAllDay`, `RecurrenceID`, `RecurrenceRule`, `RecurrenceException`, `RoomID`) VALUES ($id, '$subject', '$startTime', '$endTime', '$location','$description', $isAllDay, '$recurrenceId', '$recurrenceRule', '$recurrenceException', $roomId)";
                    }
                }
                $result = $conn->query($sql);
            }
            else if ($param['action'] == "batch" && !empty($param['added'])) {
                foreach($param['added'] as $add) {
                    $id =isset($add['Id']) ? $add['Id'] : null;
                    $subject = isset($add['Subject']) ? $add['Subject'] : null;
                    $startTime = isset($add['StartTime']) ? $add['StartTime'] : null;
                    $endTime = isset($add['EndTime']) ? $add['EndTime'] : null;
                    $location = isset($add['Location']) ? $add['Location'] : null;
                    $description = isset($add['Description']) ? $add['Description'] : null;
                    $isAllDay = !empty($add['IsAllDay']) ? 1 : 0;
                    $recurrenceId = isset($add['RecurrenceID']) && $add['RecurrenceID'] > 0 ? $add['RecurrenceID'] : null;
                    $recurrenceRule = isset($add['RecurrenceRule']) ? $add['RecurrenceRule'] : null;
                    $recurrenceException = isset($add['RecurrenceException']) && !empty($add['RecurrenceException']) ? $add['RecurrenceException'] : null;
                    $roomId = isset($add['RoomID']) && !empty($add['RoomID']) ? $add['RoomID'] : null;
    
                    $startTime = clone new DateTime($startTime);
                    $timezone = new DateTimeZone('Asia/Calcutta');
                    $startTime->setTimezone($timezone);
                    $startTime = $startTime->format('Y-m-d H:i:s');
                    $endTime = clone new DateTime($endTime);
                    $timezone = new DateTimeZone('Asia/Calcutta');
                    $endTime->setTimezone($timezone);
                    $endTime = $endTime->format('Y-m-d H:i:s');
                    
                    if($recurrenceRule == null) {
                        $sql = "INSERT INTO `appointments` (`Id`, `Subject`, `StartTime`, `EndTime`, `Location`, `Description`, `IsAllDay`, `RoomID`) VALUES ($id, '$subject', '$startTime', '$endTime', '$location','$description', $isAllDay, $roomId)";
                    } else {
                        if($recurrenceId == null) {
                            $sql = "INSERT INTO `appointments` (`Id`, `Subject`, `StartTime`, `EndTime`, `Location`, `Description`, `IsAllDay`, `RecurrenceRule`, `RoomID`) VALUES ($id, '$subject', '$startTime', '$endTime', '$location','$description', $isAllDay, '$recurrenceRule', $roomId)";
                        } else {
                            $sql = "INSERT INTO `appointments` (`Id`, `Subject`, `StartTime`, `EndTime`, `Location`, `Description`, `IsAllDay`, `RecurrenceID`, `RecurrenceRule`, `RecurrenceException`, `RoomID`) VALUES ($id, '$subject', '$startTime', '$endTime', '$location','$description', $isAllDay, '$recurrenceId', '$recurrenceRule', '$recurrenceException', $roomId)";
                        }
                    }
                    $result = $conn->query($sql);
                }
            }
        }

        if ($param['action'] == "update" || ($param['action'] == "batch" && !empty($param['changed']))) {
            if ($param['action'] == "update") {
                $id = isset($param['value']['Id']) ? $param['value']['Id'] : null;
                $subject = isset($param['value']['Subject']) ? $param['value']['Subject'] : null;
                $startTime = isset($param['value']['StartTime']) ? $param['value']['StartTime'] : null;
                $endTime = isset($param['value']['EndTime']) ? $param['value']['EndTime'] : null;
                $location = isset($param['value']['Location']) ? $param['value']['Location'] : null;
                $description = isset($param['value']['Description']) ? $param['value']['Description'] : null;
                $isAllDay = isset($param['value']['IsAllDay']) ? $param['value']['IsAllDay'] : false;
                $recurrenceId = isset($param['value']['RecurrenceID']) && $param['value']['RecurrenceID'] > 0 ? $param['value']['RecurrenceID'] : null;
                $recurrenceRule = isset($param['value']['RecurrenceRule']) ? $param['value']['RecurrenceRule'] : null;
                $recurrenceException = isset($param['value']['RecurrenceException']) && !empty($param['RecurrenceException']) ? $param['value']['RecurrenceException'] : null;
                $roomId = isset($param['value']['RoomID']) && !empty($param['RoomID']) ? $param['value']['RoomID'] : null;
    
                $startTime = clone new DateTime($startTime);
                $timezone = new DateTimeZone('Asia/Calcutta');
                $startTime->setTimezone($timezone);
                $startTime = $startTime->format('Y-m-d H:i:s');
                $endTime = clone new DateTime($endTime);
                $timezone = new DateTimeZone('Asia/Calcutta');
                $endTime->setTimezone($timezone);
                $endTime = $endTime->format('Y-m-d H:i:s');
    
                if($recurrenceRule == null){
                    $sql = "UPDATE `appointments` SET `Subject` = '$subject', `StartTime` = '$startTime', `EndTime` = '$endTime', `Location` = '$location', `Description` = '$description', `IsAllDay` = '$isAllDay', `RoomID` = $roomId WHERE `appointments`.`Id` = $id";
                }
                else {
                    $sql = "UPDATE `appointments` SET `Subject` = '$subject', `StartTime` = '$startTime', `EndTime` = '$endTime', `Location` = '$location', `Description` = '$description', `IsAllDay` = $isAllDay, `RecurrenceID` = '$recurrenceId',`RecurrenceRule` = '$recurrenceRule',`RecurrenceException` = '$recurrenceException', `RoomID` = $roomId  WHERE `appointments`.`Id` = $id";
                }

                $result = $conn->query($sql);
            }
            else if ($param['action'] == "batch" && !empty($param['changed'])) {
                foreach($param['changed'] as $update) {
                    $id = isset($update['Id']) ? $update['Id'] : null;
                    $subject = isset($update['Subject']) ? $update['Subject'] : null; 
                    $startTime = isset($update['StartTime']) ? $update['StartTime'] : null; 
                    $endTime = isset($update['EndTime']) ? $update['EndTime'] : null; 
                    $location = isset($update['Location']) ? $update['Location'] : null;
                    $description = isset($update['Description']) ? $update['Description'] : null;
                    $isAllDay = !empty($update['IsAllDay']) ? 1 : 0;
                    $recurrenceId = isset($update['RecurrenceID']) && $update['RecurrenceID'] > 0 ? $update['RecurrenceID'] : null;
                    $recurrenceRule = isset($update['RecurrenceRule']) ? $update['RecurrenceRule'] : null;
                    $recurrenceException = isset($update['RecurrenceException']) && !empty($update['RecurrenceException']) ? $update['RecurrenceException'] : null;
                    $roomId = isset($update['RoomID']) && !empty($update['RoomID']) ? $update['RoomID'] : null;
    
                    $startTime = clone new DateTime($startTime);
                    $timezone = new DateTimeZone('Asia/Calcutta');
                    $startTime->setTimezone($timezone);
                    $startTime = $startTime->format('Y-m-d H:i:s');
                    $endTime = clone new DateTime($endTime);
                    $timezone = new DateTimeZone('Asia/Calcutta');
                    $endTime->setTimezone($timezone);
                    $endTime = $endTime->format('Y-m-d H:i:s');
    
                    if($recurrenceRule == null){
                        $sql = "UPDATE `appointments` SET `Subject` = '$subject', `StartTime` = '$startTime', `EndTime` = '$endTime', `Location` = '$location', `Description` = '$description', `IsAllDay` = $isAllDay, `RoomID` = $roomId WHERE `appointments`.`Id` = $id";
                    }
                    else {
                        if($recurrenceId == null) {
                            if($recurrenceException == null) {
                                $sql = "UPDATE `appointments` SET `Subject` = '$subject', `StartTime` = '$startTime', `EndTime` = '$endTime', `Location` = '$location', `Description` = '$description', `IsAllDay` = $isAllDay, `RecurrenceRule` = '$recurrenceRule', `RoomID` = $roomId  WHERE `appointments`.`Id` = $id";
                            } else {
                                $sql = "UPDATE `appointments` SET `Subject` = '$subject', `StartTime` = '$startTime', `EndTime` = '$endTime', `Location` = '$location', `Description` = '$description', `IsAllDay` = $isAllDay, `RecurrenceRule` = '$recurrenceRule', `RecurrenceException` = '$recurrenceException', `RoomID` = $roomId  WHERE `appointments`.`Id` = $id";
                            }
                        } else {
                            $sql = "UPDATE `appointments` SET `Subject` = '$subject', `StartTime` = '$startTime', `EndTime` = '$endTime', `Location` = '$location', `Description` = '$description', `IsAllDay` = $isAllDay, `RecurrenceID` = '$recurrenceId', `RecurrenceRule` = '$recurrenceRule', `RecurrenceException` = '$recurrenceException', `RoomID` = $roomId WHERE `appointments`.`Id` = $id";
                        }
                    }

                    $result = $conn->query($sql);
                }
            }
        }

        if ($param['action'] == "remove" || ($param['action'] == "batch" && !empty($param['deleted']))) {
            if ($param['action'] == "remove") {
                $id = $param['key'];
                $sql = "DELETE FROM `appointments` WHERE `Id`=$id";   
                $result = $conn->query($sql);
            }
            else if ($param['action'] == "batch" && !empty($param['deleted'])) {
                foreach($param['deleted'] as $delete) {                
                    if($delete['Id'] != null)
                    {
                        $id = $delete['Id'];
                        $sql = "DELETE FROM `appointments` WHERE `Id`=$id";
                        $result = $conn->query($sql);
                    }             
                }
            }
        }
    }

    $json = array();

    if (isset($param["StartDate"]) && isset($param["EndDate"])) {
        $sql = "SELECT * FROM `appointments`";
        $appointmentList = $conn->query($sql);
        $json = $appointmentList->fetch_all(MYSQLI_ASSOC);
    }
    echo json_encode($json, JSON_NUMERIC_CHECK);
    ?>
    ```
### Running the application


1. **Start XAMPP services**
  - Open **XAMPP Control Panel**
  - Start **Apache**

2. **Place project files**
  - Copy the project folder `Your Project Folder Name` into:

     ```
     C:\xampp\htdocs\
     ```

3. **Open in browser**
  - Go to: `http://localhost/`
   
  - Then open the app:
     ```
     http://Your-Project-Folder-Name
     ```
4. You can perform CRUD operation on the scheduler that will be reflected in the MySQL database table.