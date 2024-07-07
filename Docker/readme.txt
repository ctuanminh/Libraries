Pull 2 images 
docker pull mcr.microsoft.com/mssql/server:2019-CU15-ubuntu-20.04
docker pull mcr.microsoft.com/mssql/server:2017-CU28-ubuntu-16.04
docker pull mcr.microsoft.com/mssql/server:2017-latest
tag = version
Create containers from images
1 image => multiple containers
-d : Detach(background) mode
-e: environment variables
--name : container's name
-p: map port

MacOS/Linux:
docker run \
-e "ACCEPT_EULA=Y" \
-e "SA_PASSWORD=Abc@123456789" \
--name sql-server-2019-container \
-p 1435:1433 \
-v /Users/hoangnd/Desktop/temp:/var/opt/mssql \
-d mcr.microsoft.com/mssql/server:2019-CU15-ubuntu-20.04

Windows: 
docker run ^
-e "ACCEPT_EULA=Y" ^
-e "SA_PASSWORD=@dmin1234" ^
--network springboot-app-network ^
--name sql-server-2017-container ^
-p 1435:1433 ^
-v sql-server-2017:/var/opt/mssql ^
-d mcr.microsoft.com/mssql/server:2017-latest

Docker container with default volume
MacOS/Linux:
docker run \
-e "ACCEPT_EULA=Y" \
-e "SA_PASSWORD=Abc@123456789" \
--name sql-server-2019-container \
-p 1435:1433 \
-v my-volume-1:/var/opt/mssql \
-d mcr.microsoft.com/mssql/server:2019-CU15-ubuntu-20.04

Windows:
docker run ^
-e "ACCEPT_EULA=Y" ^
-e "SA_PASSWORD=Abc@123456789" ^
--name sql-server-2019-container ^
-p 1435:1433 ^
-v my-volume-1:/var/opt/mssql ^
-d mcr.microsoft.com/mssql/server:2019-CU15-ubuntu-20.04

Volume's path in Host(your PC, laptop):
ls -la ~/Library/Containers/com.docker.docker/Data/vms

In Windows:
\\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes

remove container => data lost => how to solve ?
Let's map container's volume to your host(PC)'s volume
docker rm 
-f: force
-v "host' volume":"container's volume" 

Create a container for mysql:
Windows:
docker run ^
-e MYSQL_ROOT_PASSWORD=@dmin1234 ^
--name mysql-server-container ^
--network springboot-app-network ^
-p 3309:3306 ^
-v mysql-shopapp:/var/lib/mysql ^
-d f2ad9f23df82a3e5efabd1574b862a94c0657c73a6179efec07d5cf9ae5a307f

MacOS(Linux):
docker run \
-e MYSQL_ROOT_PASSWORD=Abc@123456789 \
--name mysql8-container \
-p 3308:3306 \
-v mysql8-volume:/var/lib/mysql \
-d mysql

Go inside the container:
-it = interactive mode
docker exec -it mysql8-container bash
Then:
mysql -u root -p
