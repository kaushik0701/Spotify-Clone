package com.sc.faas.resource;

import com.sc.faas.model.CopsApplicationStatusSG;
import com.sc.faas.repository.CopsApplicationStatusSGRepository;
import org.apache.commons.csv.CSVFormat;
import org.apache.commons.csv.CSVParser;
import org.apache.commons.csv.CSVRecord;

import javax.inject.Inject;
import javax.transaction.Transactional;
import javax.ws.rs.*;
import javax.ws.rs.core.MediaType;
import javax.ws.rs.core.Response;
import java.io.InputStreamReader;
import java.io.Reader;
import java.util.Date;

@Path("/cops-application-status-sg")
@Consumes(MediaType.MULTIPART_FORM_DATA)
@Produces(MediaType.APPLICATION_JSON)
public class CopsApplicationStatusSGResource {

    @Inject
    CopsApplicationStatusSGRepository repository;

    @POST
    @Path("/upload")
    @Transactional
    public Response uploadFile(@FormParam("file") java.io.InputStream fileInputStream) {
        try (Reader reader = new InputStreamReader(fileInputStream);
             CSVParser csvParser = new CSVParser(reader, CSVFormat.DEFAULT.withFirstRecordAsHeader())) {

            for (CSVRecord record : csvParser) {
                CopsApplicationStatusSG entity = new CopsApplicationStatusSG();
                entity.setApplicationRefNo(Long.valueOf(record.get("N_APPLN_REF_NO")));
                entity.setApplicationCreateDate(new Date(record.get("D_APPLN_CREAT")));
                entity.setStatusDesc(record.get("X_STATUS_DESC"));
                entity.setApplicationStatus(record.get("X_APPLN_STATUS"));
                entity.setProductCategory(record.get("X_PRD_CTGRY"));
                entity.setCreateDate(new Date(record.get("D_CREAT")));
                entity.setUpdateDate(new Date(record.get("D_UPD")));
                entity.setCreateBy(record.get("X_CREAT"));
                entity.setUpdateBy(record.get("X_UPD"));

                repository.persist(entity);
            }
            return Response.status(Response.Status.CREATED).build();
        } catch (Exception e) {
            e.printStackTrace();
            return Response.status(Response.Status.INTERNAL_SERVER_ERROR).entity("Error processing file").build();
        }
    }
}
