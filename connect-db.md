---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Specify your database
{: #cdb-connect}

Specify a database for your {{site.data.keyword.aios_short}} instance to use.
{: shortdesc}

## Connecting to your database
{: #cdb-config}

{{site.data.keyword.aios_short}} uses a database to store payload, feedback, and measurement data. Besides selecting a database, you may also select a schema for your database - a schema is a named collection of tables in the database.

1.  Choose a database. You have two options: the free Lite plan database, or an existing or new database.

    ![Select database](images/gs-config-database.png)

### Free Lite plan database

The free Lite plan database has some important limitations:

- The free Lite plan database is hosted, and is not directly accessible to you.
- {{site.data.keyword.aios_full}} will have full access to your database, and thus will have full access to your data.
- The free Lite plan database is not GDPR-compliant. If your model processes personally-identifiable information (PII), you cannot use the free Lite plan database. You must purchase a new database, or use an existing database that conforms to GDPR rules. See [Information security](/docs/services/ai-openscale-icp/information-security.html) to learn more.

To proceed with using the free Lite plan database, simply select that option, then review the summary data and click **Save**.

  ![Select database](images/gs-config-database2.png)

### Existing or new database

1.  Once you have selected the "Use existing or purchase new database" option, {{site.data.keyword.aios_short}} checks your {{site.data.keyword.Bluemix_notm}} account to locate any existing databases.

1.  Select your existing database type (Compose for Postgres, Database for Postgres, or Db2), then a database from the **Database** drop-down menu, and then a **Schema**:

    ![Select database](images/gs-config-database3.png)

1.  You can also click **Select a different location** to specify a database location outside of your {{site.data.keyword.Bluemix_notm}} account.

    - Select the **Database Type** (`Compose for PostgreSQL`, `Database for PostgreSQL`, or `Db2`), then provide connection information:

        - For a `Compose for PostgreSQL` database, complete the following:

            - Hostname or IP address
            - Port
            - Database (name)
            - Username
            - Password

            ![Specify Compose for Postgres db location](images/db-config-cpostgres.png)

        - For a `Database for PostgreSQL` database, complete the following:

            - Host name or IP address
            - SSL Port
            - Base-64 encoded certificate
            - Database (name)
            - Username
            - Password

            ![Specify Database for Postgres db location](images/db-config-dpostgres.png)

        - For a `Db2` database, complete the following:

            - Hostname or IP address
            - SSL Port
            - Database (name)
            - Username
            - Password

            ![Specify Db2 location](images/db-config-db2.png)

    - Once you have successfully connected, you can select a schema.

      ![Select schema](images/gs-config-database5.png)

Click **Next** to review the summary data, then click **Save**.

## Sending a scoring request
{: #cdb-scoring}

To configure monitors, {{site.data.keyword.aios_short}} requires you to send a scoring request, in order to begin to log the data that will be monitored.

Models deployed in Watson Machine Learning are automatically scored by {{site.data.keyword.aios_short}}. If you only have models deployed in Watson Machine Learning, you will not see this screen.
{: note:}

Select a deployment, in this case "Fraud Detector", and then use the provided `cURL` or `Python` code snippets to log model deployment request and response data.

The fields and values in the code snippets need to be substituted with your real values, as the ones provided are only examples.
{: important}

![Send scoring request](images/config-send-scoring.png)

Once you have run your payload logging, you will see a checkmark in the "Ready to Monitor" column for the selected deployment. Click **Configure Monitors** to continue.

## Next steps
{: #cdb-next}

{{site.data.keyword.aios_short}} is now ready for you to [configure monitors for your deployments](/docs/services/ai-openscale-icp/monitor-overview.html).
