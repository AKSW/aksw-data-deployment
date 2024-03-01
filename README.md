# AKSW Maven-Based Data Deployment

See [https://scaseco.github.io/maven4data/](https://scaseco.github.io/maven4data/) for guides about why and how to use Maven for data publishing.

This repository contains a pom.xml with several default settings (repository URLs and versions) intended for use as a parent pom for data publishing project within the AKSW organization.
The POM is intended **only** for use with AKSW projects.

## The Parent POM

The following parent declaration adds the AKSW repositories (see the [pom.xml](pom.xml) to the maven projects:

```xml
<parent>
  <groupId>org.aksw.data.config</groupId>
  <artifactId>aksw-data-deployment</artifactId>
  <version>0.0.8</version>
  <relativePath></relativePath>
</parent>
```

## Setup Maven

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
        <server>
          <id>et.aksw.internal</id>
          <username>USERNAME</username>
          <password>{SECRET}</password>
        </server>
    
        <server>
          <id>et.aksw.snapshots</id>
          <username>USERNAME</username>
          <password>{SECRET}</password>
        </server>
      </servers>
    </settings>
    ```

* **Step 5** Try to deploy an example project such as [geodata/simple](https://github.com/Scaseco/maven4data/tree/develop/examples/geodata/simple).

* **Step 6** If necessary, please tell the admin to grant you write priviledges to our archiva instance.

