# AKSW Maven-Based Data Deployment



* **Step 1** Install Maven
  `sudo apt install maven`
  * Ensure you have at Java 11+
    `sudo apt install openjdk-XX-jdk`
    * Check with `sudo update-java-alternatives -l` 
    * Set with `sudo update-java-alternatives -s java-X.XX.X-openjdk-amd64`

* **Step 2** Set up your master password

  * `mvn --encrypt-master-password`

  * Create or update `$HOME/.m2/settings-security.xml` with the content

    ```xml
    <settingsSecurity>
      <master>{SECRET}</master>
    </settingsSecurity>
    ```

  * Details: https://maven.apache.org/guides/mini/guide-encryption.html

* **Step 3** Run the following command to encrypt your passwords (LDAP, TIB DataManager)

  * `mvn --encrypt-password`

* **Step 4** Add repository declarations to `$HOME/.m2/settings.xml`

  * ```xml
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
    	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    	xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          http://maven.apache.org/xsd/settings-1.0.0.xsd">
      <servers>
        <server>
          <id>dm.coypu.org</id>
          <username>aklakan_github</username>
          <password>{SECRET}</password>
        </server>
    
        <server>
          <id>et.aksw.internal</id>
          <username>ClausStadler</username>
          <password>{SECRET}</password>
        </server>
    
        <server>
          <id>et.aksw.snapshots</id>
          <username>ClausStadler</username>
          <password>{SECRET}</password>
        </server>
      </servers>
    </settings>
    ```

  * **Step 5** Try to deploy `https://github.com/Scaseco/maven4data/tree/develop/examples/geodata/simple`

  * **Step 6** Tell the Admin to grant you write priviledges

