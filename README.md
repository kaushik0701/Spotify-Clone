import javax.persistence.*;
import java.util.Date;

@Entity
@Table(name = "SalesPitch")
public class SalesPitch {

    @Id
    @Column(name = "RELID", length = 20)
    private String relId;

    @Column(name = "SEGMENT", length = 3)
    private String segment;

    @Column(name = "DND_FLAG", length = 1)
    private String dndFlag;

    @Column(name = "FILE_RELEASE_DATE")
    @Temporal(TemporalType.DATE)
    private Date fileReleaseDate;

    @Column(name = "HP1_FLAG", length = 1)
    private String hp1Flag;

    @Column(name = "HP2_FLAG", length = 1)
    private String hp2Flag;

    @Column(name = "HP3_FLAG", length = 1)
    private String hp3Flag;

    @Column(name = "HP1_SD_DATE")
    @Temporal(TemporalType.DATE)
    private Date hp1SdDate;

    @Column(name = "HP1_ED_DATE")
    @Temporal(TemporalType.DATE)
    private Date hp1EdDate;

    @Column(name = "HP2_SD_DATE")
    @Temporal(TemporalType.DATE)
    private Date hp2SdDate;

    @Column(name = "HP2_ED_DATE")
    @Temporal(TemporalType.DATE)
    private Date hp2EdDate;

    @Column(name = "HP3_SD_DATE")
    @Temporal(TemporalType.DATE)
    private Date hp3SdDate;

    @Column(name = "HP3_ED_DATE")
    @Temporal(TemporalType.DATE)
    private Date hp3EdDate;

    @Column(name = "HP_MSG", length = 40)
    private String hpMsg;

    @Column(name = "PP1_FLAG", length = 1)
    private String pp1Flag;

    @Column(name = "PP2_FLAG", length = 1)
    private String pp2Flag;

    @Column(name = "PP3_FLAG", length = 1)
    private String pp3Flag;

    @Column(name = "PP4_FLAG", length = 1)
    private String pp4Flag;

    @Column(name = "PP1_SD_DATE")
    @Temporal(TemporalType.DATE)
    private Date pp1SdDate;

    @Column(name = "PP1_ED_DATE")
    @Temporal(TemporalType.DATE)
    private Date pp1EdDate;

    @Column(name = "PP2_SD_DATE")
    @Temporal(TemporalType.DATE)
    private Date pp2SdDate;

    @Column(name = "PP2_ED_DATE")
    @Temporal(TemporalType.DATE)
    private Date pp2EdDate;

    @Column(name = "PP3_SD_DATE")
    @Temporal(TemporalType.DATE)
    private Date pp3SdDate;

    @Column(name = "PP3_ED_DATE")
    @Temporal(TemporalType.DATE)
    private Date pp3EdDate;

    @Column(name = "PP4_SD_DATE")
    @Temporal(TemporalType.DATE)
    private Date pp4SdDate;

    @Column(name = "PP4_ED_DATE")
    @Temporal(TemporalType.DATE)
    private Date pp4EdDate;

    @Column(name = "PP1_MSG", length = 40)
    private String pp1Msg;

    @Column(name = "PP2_MSG", length = 40)
    private String pp2Msg;

    @Column(name = "PP3_MSG", length = 40)
    private String pp3Msg;

    @Column(name = "PP4_MSG", length = 40)
    private String pp4Msg;

    @Column(name = "IVRCPWOV_FLAG", length = 1)
    private String ivrcpwovFlag;

    @Column(name = "IVRCPWV_FLAG", length = 1)
    private String ivrcpwvFlag;

    @Column(name = "IVRCPVALUE")
    private Integer ivrcpValue;

    @Column(name = "IVRCPWOV_SD_DATE")
    @Temporal(TemporalType.DATE)
    private Date ivrcpwovSdDate;

    @Column(name = "IVRCPWOV_ED_DATE")
    @Temporal(TemporalType.DATE)
    private Date ivrcpwovEdDate;

    @Column(name = "IVRCPWV_SD_DATE")
    @Temporal(TemporalType.DATE)
    private Date ivrcpwvSdDate;

    @Column(name = "IVRCPWV_ED_DATE")
    @Temporal(TemporalType.DATE)
    private Date ivrcpwvEdDate;

    @Column(name = "HP1_PRODUCTNAME", length = 25)
    private String hp1ProductName;

    @Column(name = "HP2_PRODUCTNAME", length = 25)
    private String hp2ProductName;

    @Column(name = "HP3_PRODUCTNAME", length = 25)
    private String hp3ProductName;

    @Column(name = "PP1_PRODUCTNAME", length = 25)
    private String pp1ProductName;

    @Column(name = "PP2_PRODUCTNAME", length = 25)
    private String pp2ProductName;

    @Column(name = "PP3_PRODUCTNAME", length = 25)
    private String pp3ProductName;

    @Column(name = "PP4_PRODUCTNAME", length = 25)
    private String pp4ProductName;

    @Column(name = "IVRCPWOV_PRODUCTNAME", length = 25)
    private String ivrcpwovProductName;

    @Column(name = "IVRCPWV_PRODUCTNAME", length = 25)
    private String ivrcpwvProductName;

    @Column(name = "PRODUCT_PITCH", length = 3)
    private String productPitch;

    @Column(name = "PITCH_DATE")
    @Temporal(TemporalType.DATE)
    private Date pitchDate;

    // Getters and Setters
    // (omitted for brevity)
}
