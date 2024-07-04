package com.sc.faas.repository;

import com.sc.faas.model.CopsCustIndicatorsSG;
import io.quarkus.hibernate.orm.panache.PanacheRepository;
import javax.enterprise.context.ApplicationScoped;

@ApplicationScoped
public class CopsCustIndicatorsSGRepository implements PanacheRepository<CopsCustIndicatorsSG> {
}

@ApplicationScoped
public class CopsPreferredLangSGRepository implements PanacheRepository<CopsPreferredLangSG> {
}

@ApplicationScoped
public class CopsRepeatCallerSGRepository implements PanacheRepository<CopsRepeatCallerSG> {
}

@ApplicationScoped
public class CopsCallbackSGRepository implements PanacheRepository<CopsCallbackSG> {
}

@ApplicationScoped
public class CopsTpinDtlsSGRepository implements PanacheRepository<CopsTpinDtlsSG> {
}

@ApplicationScoped
public class CopsApplicationStatusSGRepository implements PanacheRepository<CopsApplicationStatusSG> {
}To work with entity classes and communicate with a SQL database in a Quarkus framework, you need to include the following dependencies in your `pom.xml`:

1. **Quarkus Hibernate ORM**:
   This dependency is used for Object-Relational Mapping (ORM) with Hibernate.

2. **Quarkus JDBC Driver**:
   Depending on the specific SQL database you are using (e.g., PostgreSQL, MySQL, H2), you will need the corresponding JDBC driver.

Here is an example `pom.xml` configuration for a Quarkus project using PostgreSQL:

```xml
<dependencies>
    <!-- Quarkus core dependency -->
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-resteasy</artifactId>
    </dependency>

    <!-- Quarkus Hibernate ORM dependency -->
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-hibernate-orm-panache</artifactId>
    </dependency>

    <!-- Quarkus JDBC driver for PostgreSQL -->
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-jdbc-postgresql</artifactId>
    </dependency>

    <!-- Additional dependencies as needed -->
</dependencies>
```

For other SQL databases, replace `quarkus-jdbc-postgresql` with the appropriate JDBC driver:

- **MySQL**:
  ```xml
  <dependency>
      <groupId>io.quarkus</groupId>
      <artifactId>quarkus-jdbc-mysql</artifactId>
  </dependency>
  ```

- **H2**:
  ```xml
  <dependency>
      <groupId>io.quarkus</groupId>
      <artifactId>quarkus-jdbc-h2</artifactId>
  </dependency>
  ```

Once you have these dependencies, you can define your entity classes using the `@Entity` annotation provided by JPA (Java Persistence API). Here is an example of an entity class:

```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Person {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String email;

    // Getters and setters
}
```

Additionally, you need to configure your database connection in the `application.properties` file:

```properties
# Database configuration
quarkus.datasource.db-kind=postgresql
quarkus.datasource.username=myuser
quarkus.datasource.password=mypassword
quarkus.datasource.jdbc.url=jdbc:postgresql://localhost:5432/mydatabase

# Hibernate configuration
quarkus.hibernate-orm.database.generation=update
```

By adding these dependencies and configurations, you'll be set up to use entity classes and interact with a SQL database in your Quarkus application.

To create model classes for the six tables in the Quarkus framework, you can follow the below steps:

1. **Set up the Quarkus project**: If you haven't already, set up a new Quarkus project using the Quarkus CLI or your IDE.

2. **Add necessary dependencies**: Ensure you have dependencies for JPA and JDBC in your `pom.xml` file.

```xml
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-hibernate-orm-panache</artifactId>
</dependency>
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-jdbc-postgresql</artifactId>
</dependency>
```

3. **Create Entity Classes**: Create the entity classes for each table. Below are the entity classes for the six tables.

### COPS_CUST_INDICATORS_SG

```java
import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_CUST_INDICATORS_SG")
public class CopsCustIndicatorsSG {

    @Id
    @Column(name = "REL_ID")
    private String relId;

    @Column(name = "F_FEE_WAIVER")
    private String feeWaiver;

    @Column(name = "F_KYC_STATUS")
    private String kycStatus;

    @Column(name = "F_TRANSFER_EXCLUSION")
    private String transferExclusion;

    @Column(name = "F_SENSITIVE_CUST")
    private String sensitiveCust;

    @Column(name = "RBS_CUST")
    private String rbsCust;

    @Column(name = "N_RBS_CUST_FILE_ID")
    private Integer rbsCustFileId;

    @Column(name = "N_FEE_WAIVER_FILE_ID")
    private Integer feeWaiverFileId;

    @Column(name = "N_KYC_STATUS_FILE_ID")
    private Integer kycStatusFileId;

    @Column(name = "N_TRANSFER_EXCLUSION_FILE_ID")
    private Integer transferExclusionFileId;

    @Column(name = "N_SENSITIVE_CUST_FILE_ID")
    private Integer sensitiveCustFileId;

    @Column(name = "D_CREAT")
    private Date creatDate;

    @Column(name = "D_UPD")
    private Date updDate;

    @Column(name = "X_CREAT")
    private String creatUser;

    @Column(name = "X_UPD")
    private String updUser;

    // Getters and Setters
}
```

### COPS_PREFERRED_LANG_SG

```java
import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_PREFERRED_LANG_SG")
public class CopsPreferredLangSG {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "ID")
    private Long id;

    @Column(name = "X_REL_ID")
    private String relId;

    @Column(name = "X_LANG_CD")
    private String langCd;

    @Column(name = "D_CREAT")
    private Date creatDate;

    @Column(name = "D_UPD")
    private Date updDate;

    @Column(name = "X_CREAT")
    private String creatUser;

    @Column(name = "X_UPD")
    private String updUser;

    @Column(name = "F_LATEST")
    private String latest;

    // Getters and Setters
}
```

### COPS_REPEAT_CALLER_SG

```java
import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_REPEAT_CALLER_SG")
public class CopsRepeatCallerSG {

    @Id
    @Column(name = "X_REL_ID")
    private String relId;

    @Column(name = "F_REPEAT")
    private String repeat;

    @Column(name = "D_CREAT")
    private Date creatDate;

    @Column(name = "D_UPD")
    private Date updDate;

    @Column(name = "X_CREAT")
    private String creatUser;

    @Column(name = "X_UPD")
    private String updUser;

    // Getters and Setters
}
```

### COPS_CALLBACK_SG

```java
import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_CALLBACK_SG")
public class CopsCallbackSG {

    @Id
    @Column(name = "ID")
    private Long id;

    @Column(name = "X_REL_ID")
    private String relId;

    @Column(name = "X_CUST_TYPE")
    private String custType;

    @Column(name = "X_CUST_NAME")
    private String custName;

    @Column(name = "X_MOB_NO")
    private String mobNo;

    @Column(name = "X_STATUS")
    private String status;

    @Column(name = "D_CREAT")
    private Date creatDate;

    @Column(name = "D_UPD")
    private Date updDate;

    @Column(name = "X_CREAT")
    private String creatUser;

    @Column(name = "X_UPD")
    private String updUser;

    // Getters and Setters
}
```

### COPS_TPIN_DTLS_SG

```java
import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_TPIN_DTLS_SG")
public class CopsTpinDtlsSG {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "ID")
    private Long id;

    @Column(name = "X_REL_ID")
    private String relId;

    @Column(name = "X_TPIN")
    private String tpin;

    @Column(name = "X_TPIN_IDX")
    private String tpinIdx;

    @Column(name = "D_CREAT")
    private Date creatDate;

    @Column(name = "D_UPD")
    private Date updDate;

    @Column(name = "X_CREAT")
    private String creatUser;

    @Column(name = "X_UPD")
    private String updUser;

    @Column(name = "F_LATEST")
    private String latest;

    // Getters and Setters
}
```

### COPS_APPLICATION_STATUS_SG

```java
import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_APPLICATION_STATUS_SG")
public class CopsApplicationStatusSG {

    @Id
    @Column(name = "N_APPLN_REF_NO")
    private Long applnRefNo;

    @Column(name = "D_APPLN_CREAT")
    private Date applnCreatDate;

    @Column(name = "X_STATUS_DESC")
    private String statusDesc;

    @Column(name = "X_APPLN_STATUS")
    private String applnStatus;

    @Column(name = "X_PRD_CTGRY")
    private String prdCtgry;

    @Column(name = "D_CREAT")
    private Date creatDate;

    @Column(name = "D_UPD")
    private Date updDate;

    @Column(name = "X_CREAT")
    private String creatUser;

    @Column(name = "X_UPD")
    private String updUser;

    // Getters and Setters
}
```

4. **Create a Repository Interface**: Create a repository interface for each entity to handle database operations using Panache.

### Example for `CopsCustIndicatorsSG`

```java
import io.quarkus.hibernate.orm.panache.PanacheRepository;
import javax.enterprise.context.ApplicationScoped;

@ApplicationScoped
public class CopsCustIndicatorsSGRepository implements PanacheRepository<CopsCustIndicatorsSG> {
    // Custom query methods can be defined here
}
```

Repeat this step for the other entities as needed.

5. **Database Configuration**: Make sure your `application.properties` file is correctly configured to connect to your database.

```properties
quarkus.datasource.db-kind=postgresql
quarkus.datasource.username=<username>
quarkus.datasource.password=<password>
quarkus.datasource.jdbc.url=jdbc:postgresql://<host>:<port>/<database>
quarkus.hibernate-orm.database.generation=update
```

With these steps, you will have created the model classes and repositories for the six tables in the Quarkus framework.
