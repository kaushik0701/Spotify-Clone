package com.crm.controller;

import com.crm.dto.cc.request.CardListRequest;
import com.crm.dto.cc.response.CardListResponse;
import com.crm.service.CCService;
import com.fasterxml.jackson.databind.ObjectMapper;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;

import javax.servlet.http.HttpServletRequest;

import static org.mockito.ArgumentMatchers.any;
import static org.mockito.Mockito.when;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.post;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

public class CRMControllerTest {

    private MockMvc mockMvc;

    @InjectMocks
    private CRMController crmController;

    @Mock
    private CCService ccService;

    @Mock
    private HttpServletRequest httpServletRequest;

    @BeforeEach
    public void setup() {
        MockitoAnnotations.openMocks(this);
        mockMvc = MockMvcBuilders.standaloneSetup(crmController).build();
    }

    @Test
    public void testGetCardList() throws Exception {
        // Mock request
        CardListRequest request = new CardListRequest();
        request.setMessageId("12345");
        String country = "SG";

        // Mock response
        CardListResponse response = new CardListResponse();
        response.setStatus(new CardListResponse.Status());
        response.getStatus().setStatusCode("0000");
        response.getStatus().setMessageID(request.getMessageId());

        when(ccService.processRequest(any(CardListRequest.class), any(String.class))).thenReturn(response);

        // Perform and verify the request
        mockMvc.perform(post("/api/{service}", "cc")
                .contentType(MediaType.APPLICATION_JSON)
                .header("country", country)
                .content(asJsonString(request)))
                .andExpect(status().isOk())
                .andExpect(content().contentType(MediaType.APPLICATION_JSON))
                .andExpect(jsonPath("$.status.statusCode").value("0000"))
                .andExpect(jsonPath("$.status.messageID").value("12345"));
    }

    // Helper method to convert object to JSON string
    private static String asJsonString(final Object obj) {
        try {
            return new ObjectMapper().writeValueAsString(obj);
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
}
