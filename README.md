@Entity
@Table(name = "SalesPitch")
public class SalesPitch {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @Column(name = "IVRCPWOV_ED")
    private Date ivrcpwovEd;

    @Column(name = "IVRCPWV_SD")
    private Date ivrcpwvSd;

    @Column(name = "IVRCPWV_ED")
    private Date ivrcpwvEd;

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
    private Date pitchDate;
