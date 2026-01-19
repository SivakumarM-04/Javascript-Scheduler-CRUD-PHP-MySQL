<!--
  howto.md
  A step-by-step guide to integrate PHP and MySQL with Syncfusion Scheduler CRUD Application
-->
# How to integrate PHP and MySQL with Syncfusion Scheduler CRUD Application.

This repository contains a sample full-stack application demonstrating how to synchronize events between Apple iCloud Calendar and the Syncfusion Angular Scheduler component. The Node.js backend proxies CalDAV calls, while the Angular frontend provides a responsive UI for viewing and managing calendar events.

## Prerequisites
- MySQL(>= 8.0.41.0)
- XAMPPSERVER(>= 8.2.12)
- A MySQL Database with Username and Password (Download at https://dev.mysql.com/downloads/installer/)
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
## Setup the application

### MySQL Configuration

- In `server.php` file update the USER Name, PASSWORD, and DataBase as per the database configuration.
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
4. You can perform CRUD operation on the scheduler that will be reflected in the postgreSQL database table.

## Output Preview
![Frontend Preview](./SampleOutputs/frontend.png)
*Image illustrating the Syncfusion Scheduler Component*

![Database Preview](./SampleOutputs/database.png)
*Image illustrating the events of Syncfusion Scheduler in MySQL*

## Troubleshooting
- **Page Not Found**:Check the file path correctly in the browser search bar
- **Apache Server port stopped in XAMPPSERVER**: Change the Port no in config file and mentioned the port no in url and crudurl in index.php.
- **Refused to Connect with server**: Check the url and crudurl in index.php.
