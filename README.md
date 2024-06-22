package com.example.demo.entity;

import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "Application_Status")
public class ApplicationStatus {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "application_reference_number")
    private Long applicationReferenceNumber;

    @Column(name = "date")
    private Date date;

    @Column(name = "status_description", length = 50)
    private String statusDescription;

    @Column(name = "application_status", length = 20)
    private String applicationStatus;

    @Column(name = "product_category", length = 5)
    private String productCategory;

    // Getters and Setters
    public Long getApplicationReferenceNumber() {
        return applicationReferenceNumber;
    }

    public void setApplicationReferenceNumber(Long applicationReferenceNumber) {
        this.applicationReferenceNumber = applicationReferenceNumber;
    }

    public Date getDate() {
        return date;
    }

    public void setDate(Date date) {
        this.date = date;
    }

    public String getStatusDescription() {
        return statusDescription;
    }

    public void setStatusDescription(String statusDescription) {
        this.statusDescription = statusDescription;
    }

    public String getApplicationStatus() {
        return applicationStatus;
    }

    public void setApplicationStatus(String applicationStatus) {
        this.applicationStatus = applicationStatus;
    }

    public String getProductCategory() {
        return productCategory;
    }

    public void setProductCategory(String productCategory) {
        this.productCategory = productCategory;
    }
}
