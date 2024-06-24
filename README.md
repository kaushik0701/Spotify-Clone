CREATE TABLE Application_Status (
    Application_reference_number NUMBER(20, 0) PRIMARY KEY,
    Date DATE,
    Status_Description VARCHAR2(50 BYTE),
    Application_Status VARCHAR2(20 BYTE),
    Product_Category VARCHAR2(5 BYTE)
);
