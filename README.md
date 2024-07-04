To implement CSV file upload functionality in Quarkus and persist the data into a database (Oracle in your case, assuming from the DDL script), you'll need to follow these steps:

### 1. Model Classes

Create model classes that represent your database tables. Based on your provided DDL script, here are simplified versions for each table:

#### COPS_CUST_INDICATORS_SG Entity

```java
package com.example.model;

import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_CUST_INDICATORS_SG")
public class CopsCustIndicatorsSg {

    @Id
    @Column(name = "REL_ID", length = 25)
    private String relId;

    @Column(name = "F_FEE_WAIVER", length = 1)
    private String feeWaiver;

    @Column(name = "F_KYC_STATUS", length = 1)
    private String kycStatus;

    @Column(name = "F_TRANSFER_EXCLUSION", length = 1)
    private String transferExclusion;

    @Column(name = "F_SENSITIVE_CUST", length = 1)
    private String sensitiveCust;

    @Column(name = "RBS_CUST", length = 1)
    private String rbsCust;

    @Column(name = "N_RBS_CUST_FILE_ID")
    private Long rbsCustFileId;

    // Add other columns and their mappings

    @Column(name = "D_CREAT")
    private Date createDate;

    @Column(name = "D_UPD")
    private Date updateDate;

    @Column(name = "X_CREAT", length = 25)
    private String createBy;

    @Column(name = "X_UPD", length = 25)
    private String updateBy;

    // Getters and setters
}
```

#### COPS_PREFERRED_LANG_SG Entity

```java
package com.example.model;

import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_PREFERRED_LANG_SG")
@IdClass(CopsPreferredLangSgPK.class)
public class CopsPreferredLangSg {

    @Id
    @Column(name = "ID")
    private Long id;

    @Id
    @Column(name = "X_REL_ID", length = 25)
    private String relId;

    @Column(name = "X_LANG_CD", length = 3)
    private String langCode;

    @Column(name = "D_CREAT")
    private Date createDate;

    @Column(name = "D_UPD")
    private Date updateDate;

    @Column(name = "X_CREAT", length = 25)
    private String createBy;

    @Column(name = "X_UPD", length = 25)
    private String updateBy;

    // Getters and setters
}
```

#### COPS_REPEAT_CALLER_SG Entity

```java
package com.example.model;

import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_REPEAT_CALLER_SG")
public class CopsRepeatCallerSg {

    @Id
    @Column(name = "X_REL_ID", length = 25)
    private String relId;

    @Column(name = "F_REPEAT", length = 3)
    private String repeat;

    @Column(name = "D_CREAT")
    private Date createDate;

    @Column(name = "D_UPD")
    private Date updateDate;

    @Column(name = "X_CREAT", length = 25)
    private String createBy;

    @Column(name = "X_UPD", length = 25)
    private String updateBy;

    // Getters and setters
}
```

#### COPS_CALLBACK_SG Entity

```java
package com.example.model;

import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_CALLBACK_SG")
public class CopsCallbackSg {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "ID")
    private Long id;

    @Column(name = "X_REL_ID", length = 25)
    private String relId;

    @Column(name = "X_CUST_TYPE", length = 3)
    private String custType;

    @Column(name = "X_CUST_NAME", length = 25)
    private String custName;

    @Column(name = "X_MOB_NO", length = 25)
    private String mobNo;

    @Column(name = "X_STATUS", length = 5)
    private String status;

    @Column(name = "D_CREAT")
    private Date createDate;

    @Column(name = "D_UPD")
    private Date updateDate;

    @Column(name = "X_CREAT", length = 25)
    private String createBy;

    @Column(name = "X_UPD", length = 25)
    private String updateBy;

    // Getters and setters
}
```

#### COPS_TPIN_DTLS_SG Entity

```java
package com.example.model;

import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_TPIN_DTLS_SG")
public class CopsTpinDtlsSg {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "ID")
    private Long id;

    @Column(name = "X_REL_ID", length = 25)
    private String relId;

    @Column(name = "X_TPIN", length = 258)
    private String tpin;

    @Column(name = "X_TPIN_IDX", length = 25)
    private String tpinIndex;

    @Column(name = "D_CREAT")
    private Date createDate;

    @Column(name = "D_UPD")
    private Date updateDate;

    @Column(name = "X_CREAT", length = 25)
    private String createBy;

    @Column(name = "X_UPD", length = 25)
    private String updateBy;

    @Column(name = "F_LATEST", length = 1)
    private String latest;

    // Getters and setters
}
```

#### COPS_APPLICATION_STATUS_SG Entity

```java
package com.example.model;

import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "COPS_APPLICATION_STATUS_SG")
public class CopsApplicationStatusSg {

    @Id
    @Column(name = "N_APPLN_REF_NO")
    private Long applnRefNo;

    @Column(name = "D_APPLN_CREAT")
    private Date applnCreateDate;

    @Column(name = "X_STATUS_DESC", length = 50)
    private String statusDesc;

    @Column(name = "X_APPLN_STATUS", length = 20)
    private String applnStatus;

    @Column(name = "X_PRD_CTGRY", length = 5)
    private String prdCategory;

    @Column(name = "D_CREAT")
    private Date createDate;

    @Column(name = "D_UPD")
    private Date updateDate;

    @Column(name = "X_CREAT", length = 25)
    private String createBy;

    @Column(name = "X_UPD", length = 25)
    private String updateBy;

    // Getters and setters
}
```

### 2. Repository Interfaces

Create repository interfaces using PanacheRepository for each entity. Panache simplifies the implementation of the repository with common CRUD operations.

```java
package com.example.repository;

import com.example.model.CopsCustIndicatorsSg;
import io.quarkus.hibernate.orm.panache.PanacheRepository;
import javax.enterprise.context.ApplicationScoped;

@ApplicationScoped
public class CopsCustIndicatorsSgRepository implements PanacheRepository<CopsCustIndicatorsSg> {
}
```

Repeat the above for each entity (e.g., `CopsPreferredLangSgRepository`, `CopsRepeatCallerSgRepository`, etc.).

### 3. Service Classes (Optional)

Create service classes to encapsulate business logic if needed. For simple CRUD operations, services might not be necessary, and you can directly use repositories in resources.

### 4. Resource Classes

Create RESTful resource classes to handle HTTP requests. Here's an example for uploading CSV files:

```java
package com.example.resource;

import com.example.model.*;
import com.example.repository.*;
import org.apache.commons.csv.*;
import javax.inject.*;
import javax.transaction.*;
import javax.ws.rs.*;
import javax.ws.rs.core.*;
import java.io.*;
import java.util.*;

@Path("/api/upload")
@Produces(MediaType.APPLICATION_JSON)
@Consumes(MediaType.MULTIPART_FORM_DATA)
public class UploadResource {

    @Inject
    CopsCustIndicatorsSgRepository custIndicatorsSgRepository;

    @Inject
    CopsPreferredLangSgRepository preferredLangSgRepository;

    @Inject
    CopsRepeatCallerSgRepository repeatCallerSgRepository;

    @Inject
    CopsCallbackSgRepository callbackSgRepository;

    @Inject
    CopsTpinDtlsSgRepository tpinDtlsSgRepository;

    @Inject
    CopsApplicationStatusSgRepository applicationStatusSgRepository;

    @POST
    @Transactional
    public Response uploadCsvFile(@FormParam("file") InputStream fileInputStream) {
        try (Reader reader = new InputStreamReader(fileInputStream);
             CSVParser csvParser = new CSVParser(reader, CSVFormat.DEFAULT.withFirstRecordAsHeader())) {

            List<CopsCustIndicatorsSg> custIndicatorsList = new ArrayList<>();
            List<CopsPreferredLangSg> preferredLangList = new ArrayList<>();
            List<CopsRepeatCallerSg> repeatCallerList = new ArrayList<>();
            List<CopsCallbackSg> callbackList = new ArrayList<>();
            List<CopsTpinDtlsSg> tpinDtlsList = new ArrayList<>();
            List<CopsApplication
