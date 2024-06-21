import org.springframework.stereotype.Service;

@Service
public class CASAServiceImpl implements CASAService {

    @Override
    public CASAListResponsePayload getCASAList(CASAListRequestPayload request, String country) {
        // Mock response data
        CASAListResponsePayload response = new CASAListResponsePayload();
        response.setStatus(new CASAListResponsePayload.Status());
        response.getStatus().setStatusCode("eeee");
        response.getStatus().setStatusDesc("");
        response.getStatus().setMessageID("2bd4ea21176a4ccf8990929bd11927c3");
        response.getStatus().setInteractionId("00004101051717343657");
        response.getStatus().setTimestamp("2024.06.02.23.54.24");
        response.getStatus().setInputID("");
        response.getStatus().setCurrencyCode("GBP");
        response.getStatus().setAccountStatus("U");
        response.getStatus().setProductCode("206523");
        response.getStatus().setLedgerBalance("0.00");
        response.getStatus().setAvailBalancewithLimit("0.00");
        response.getStatus().setInputIDType("10");

        CASAListResponsePayload.AccountList accountList = new CASAListResponsePayload.AccountList();
        CASAListResponsePayload.Account account = new CASAListResponsePayload.Account();
        account.setAcctNumber("4009815670");
        account.setCurrencyCode("SGD");
        account.setProductCode("206523");
        account.setAccountStatus("0");
        account.setAvailBalancewithoutLimit("6766.53");
        account.setLedgerBalance("6766.53");
        account.setProductCategory("S");
        account.setOperatingInstruction("001");
        account.setSegmentCode("03");
        account.setAccountCategory("N");
        account.setAccOpenDate("2017-01-13");
        account.setCustomerSegmentCode("013");

        accountList.setAccList(Collections.singletonList(account));
        response.setAccountList(accountList);

        return response;
    }
}
