// src/main/java/com/sc/faas/util/CSVParser.java
package com.sc.faas.util;

import com.sc.faas.model.CopsApplicationStatusSG;
import com.sc.faas.model.CopsCustIndicatorsSG;
import org.apache.commons.csv.CSVFormat;
import org.apache.commons.csv.CSVParser;
import org.apache.commons.csv.CSVRecord;

import java.io.Reader;
import java.util.ArrayList;
import java.util.List;

public class CSVParserUtil {

    public static List<CopsApplicationStatusSG> parseCopsApplicationStatusSG(Reader reader) throws Exception {
        List<CopsApplicationStatusSG> records = new ArrayList<>();
        CSVParser csvParser = new CSVParser(reader, CSVFormat.DEFAULT.withFirstRecordAsHeader());
        for (CSVRecord csvRecord : csvParser) {
            CopsApplicationStatusSG record = new CopsApplicationStatusSG();
            record.setApplicationRefNo(Long.parseLong(csvRecord.get("N_APPLN_REF_NO")));
            record.setApplicationCreateDate(java.sql.Date.valueOf(csvRecord.get("D_APPLN_CREAT")));
            record.setStatusDesc(csvRecord.get("X_STATUS_DESC"));
            record.setApplicationStatus(csvRecord.get("X_APPLN_STATUS"));
            record.setProductCategory(csvRecord.get("X_PRD_CTGRY"));
            record.setCreateDate(java.sql.Date.valueOf(csvRecord.get("D_CREAT")));
            record.setUpdateDate(java.sql.Date.valueOf(csvRecord.get("D_UPD")));
            record.setCreatedBy(csvRecord.get("X_CREAT"));
            record.setUpdatedBy(csvRecord.get("X_UPD"));
            records.add(record);
        }
        return records;
    }

    public static List<CopsCustIndicatorsSG> parseCopsCustIndicatorsSG(Reader reader) throws Exception {
        List<CopsCustIndicatorsSG> records = new ArrayList<>();
        CSVParser csvParser = new CSVParser(reader, CSVFormat.DEFAULT.withFirstRecordAsHeader());
        for (CSVRecord csvRecord : csvParser) {
            CopsCustIndicatorsSG record = new CopsCustIndicatorsSG();
            record.setRelId(csvRecord.get("REL_ID"));
            record.setFeeWaiver(csvRecord.get("F_FEE_WAIVER"));
            record.setKycStatus(csvRecord.get("F_KYC_STATUS"));
            record.setTransferExclusion(csvRecord.get("F_TRANSFER_EXCLUSION"));
            record.setSensitiveCust(csvRecord.get("F_SENSITIVE_CUST"));
            record.setRbsCust(csvRecord.get("RBS_CUST"));
            record.setFeeWaiverFileId(Long.parseLong(csvRecord.get("N_FEE_WAIVER_FILE_ID")));
            record.setKycStatusFileId(Long.parseLong(csvRecord.get("N_KYC_STATUS_FILE_ID")));
            record.setTransferExclusionFileId(Long.parseLong(csvRecord.get("N_TRANSFER_EXCLUSION_FILE_ID")));
            record.setSensitiveCustFileId(Long.parseLong(csvRecord.get("N_SENSITIVE_CUST_FILE_ID")));
            record.setRbsCustFileId(Long.parseLong(csvRecord.get("N_RBS_CUST_FILE_ID")));
            record.setCreateDate(java.sql.Date.valueOf(csvRecord.get("D_CREAT")));
            record.setUpdateDate(java.sql.Date.valueOf(csvRecord.get("D_UPD")));
            record.setCreatedBy(csvRecord.get("X_CREAT"));
            record.setUpdatedBy(csvRecord.get("X_UPD"));
            records.add(record);
        }
        return records;
    }
}
