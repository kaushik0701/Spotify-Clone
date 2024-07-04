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
