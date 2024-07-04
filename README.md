To achieve the file upload and database insertion functionality in Quarkus, you can follow these steps:

1. **Set up Quarkus Project**: First, make sure you have a Quarkus project set up with the necessary dependencies for JDBC and file handling.

2. **Create Entity Class**: Create an entity class that maps to your database table `COPS_CUST_INDICATOR_SG`.

3. **Create Repository**: Create a repository to handle the database operations.

4. **Create Service**: Create a service to handle the file reading and database insertion logic.

5. **Create REST Endpoint**: Create a REST endpoint to trigger the file upload process.

Here's an example of how you can implement this in Quarkus:

### 1. Add Dependencies

Add the following dependencies to your `pom.xml`:

```xml
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-resteasy</artifactId>
</dependency>
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-resteasy-jackson</artifactId>
</dependency>
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-hibernate-orm-panache</artifactId>
</dependency>
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-jdbc-postgresql</artifactId>
</dependency>
```

### 2. Create Entity Class

```java
package com.example;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Column;

@Entity
public class CopsCustIndicatorSG {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    public Long id;

    @Column(name = "REL_ID", length = 25)
    public String relId;

    @Column(name = "F_FEE_WAIVER", length = 1)
    public String feeWaiver;

    @Column(name = "FILE_ID")
    public Long fileId;
}
```

### 3. Create Repository

```java
package com.example;

import io.quarkus.hibernate.orm.panache.PanacheRepository;
import javax.enterprise.context.ApplicationScoped;

@ApplicationScoped
public class CopsCustIndicatorSGRepository implements PanacheRepository<CopsCustIndicatorSG> {
}
```

### 4. Create Service

```java
package com.example;

import javax.enterprise.context.ApplicationScoped;
import javax.inject.Inject;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;

@ApplicationScoped
public class FileUploadService {

    @Inject
    CopsCustIndicatorSGRepository repository;

    public void uploadFile(InputStream fileInputStream, Long fileId) throws IOException {
        try (BufferedReader reader = new BufferedReader(new InputStreamReader(fileInputStream))) {
            String line;
            while ((line = reader.readLine()) != null) {
                // Assume the file has comma-separated values (CSV)
                String[] parts = line.split(",");
                if (parts.length == 2) {
                    CopsCustIndicatorSG record = new CopsCustIndicatorSG();
                    record.relId = parts[0];
                    record.feeWaiver = parts[1];
                    record.fileId = fileId;
                    repository.persist(record);
                }
            }
        }
    }
}
```

### 5. Create REST Endpoint

```java
package com.example;

import javax.inject.Inject;
import javax.ws.rs.Consumes;
import javax.ws.rs.POST;
import javax.ws.rs.Path;
import javax.ws.rs.core.MediaType;
import javax.ws.rs.core.Response;
import org.jboss.resteasy.annotations.providers.multipart.MultipartForm;

@Path("/file-upload")
public class FileUploadResource {

    @Inject
    FileUploadService fileUploadService;

    @POST
    @Consumes(MediaType.MULTIPART_FORM_DATA)
    public Response uploadFile(@MultipartForm FileUploadForm form) {
        try {
            fileUploadService.uploadFile(form.fileInputStream, form.fileId);
            return Response.ok().build();
        } catch (IOException e) {
            return Response.status(Response.Status.INTERNAL_SERVER_ERROR).entity("File upload failed").build();
        }
    }
}
```

### 6. Create Multipart Form Class

```java
package com.example;

import org.jboss.resteasy.annotations.providers.multipart.PartType;

import javax.ws.rs.FormParam;
import java.io.InputStream;

public class FileUploadForm {

    @FormParam("file")
    @PartType(MediaType.APPLICATION_OCTET_STREAM)
    public InputStream fileInputStream;

    @FormParam("fileId")
    @PartType(MediaType.TEXT_PLAIN)
    public Long fileId;
}
```

### 7. Application Configuration

Make sure you have the necessary configurations in `application.properties` for your database connection:

```properties
quarkus.datasource.db-kind=postgresql
quarkus.datasource.username=your-username
quarkus.datasource.password=your-password
quarkus.datasource.jdbc.url=jdbc:postgresql://localhost:5432/LMS_CVD
quarkus.hibernate-orm.database.generation=update
```

With this setup, your Quarkus application will be able to read a file, parse its contents, and insert the data into the `COPS_CUST_INDICATOR_SG` table in the `LMS_CVD` database.
