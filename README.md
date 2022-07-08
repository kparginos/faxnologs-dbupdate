# FaxNoLogs Containers Preparation and Database Update Setup

<details><summary>Installation Pre-requisities</summary>
<p>

- Please make sure you have apply the [Initial Setup](https://github.com/kparginos/faxnologs-dbsetup).
	
>### If you already have done it, **DO NOT RUN IT AGAIN !!!**

</p>
</details>

<details><summary>How to update the containers(db and app) on a host machine</summary>
<p>

In order to update the latest containers you need to do the following:

* For the Windows Host run this command:

```
docker-compose -f FaxNoLogs-Containers-WinSetup.yml pull
```

* For the Linux Host run this command:

```
docker-compose -f FaxNoLogs-Containers-LinuxSetup.yml pull
```

Once finished run the following to update the web app container:

```
docker-compose up -d --no-deps faxnologs_webapp
```


</p>
</details>

<details><summary>How to apply the DB Update</summary>
<p>
At the host machine run the following:

```
docker exec faxnologs_webapp bash -c "apt-get update && apt-get -y install wget && wget --no-check-certificate https://github.com/kparginos/faxnologs-dbsetup/raw/main/DBUpdate.tar && tar xf DBUpdate.tar -C dbsetup && cd dbsetup && dotnet FaxNoLogs.Migrations.dll -u"
```

The above command, should it run correctly, must apply the following:

  1. Update the container's OS
  2. Install **wget** utility
  3. Use wget to download the **DBUpdate.tar**
  4. Extract to above folder the contents of DBUpdate.tar
  5. Switch to dbsetup folder
  6. Run the DB update script
	
If the last command that updates the database completes successfully, there should be the following output to console:

```
Start Database Update...
Create Views...
Create Views - OK
Database Update Completed
```
</p>
</details>
