---
title: "API Reference"
linkTitle: "API Reference"
weight: 20
type: docs
description: >
  Technical API documentation for BRC Risk Management integration developers and advanced users.
---

## API Reference Overview

BRC Risk Management provides comprehensive API integration capabilities for accessing risk data from third-party providers and extending the system with custom functionality. This reference covers both the external provider APIs and Business Central's internal APIs for accessing risk data.

## External Risk Provider API Integration

### TIC API Integration

BRC Risk Management's primary integration is with TIC credit risk services. The system abstracts TIC's REST API into Business Central-friendly operations.

#### Authentication

**API Key Authentication:**
```http
GET /api/v1/companies/{ticCompanyId}
Authorization: Bearer {api-key}
Content-Type: application/json
```

**Configuration in Business Central:**
- API keys stored securely in IsoStorage
- Automatic header injection for all requests
- Support for API key rotation without downtime

#### Company Search API

**Search by Company Name:**
```http
POST /api/v1/companies/search
Authorization: Bearer {api-key}
Content-Type: application/json

{
  "searchCriteria": {
    "companyName": "Example Company Ltd",
    "country": "GB",
    "exactMatch": false
  },
  "includeRiskData": true,
  "maxResults": 50
}
```

**Search Response:**
```json
{
  "searchResults": [
    {
      "ticCompanyId": "123456789",
      "companyName": "Example Company Ltd",
      "registrationNumber": "12345678",
      "vatNumber": "GB123456789",
      "country": "GB",
      "address": {
        "street": "123 Business Street",
        "city": "London",
        "postalCode": "SW1A 1AA"
      },
      "matchConfidence": 95,
      "riskData": {
        "creditScore": 75,
        "riskLevel": "MEDIUM",
        "debtBalance": 25000.00,
        "paymentMarks": 2,
        "dataVersion": 42
      }
    }
  ],
  "totalResults": 1,
  "searchId": "search-789xyz"
}
```

#### Risk Data Retrieval

**Get Risk Data:**
```http
GET /api/v1/companies/{ticCompanyId}/risk-data
Authorization: Bearer {api-key}
```

**Response:**
```json
{
  "ticCompanyId": "123456789",
  "companyName": "Example Company Ltd",
  "lastUpdated": "2025-12-01T10:30:00Z",
  "dataVersion": 42,
  "riskData": {
    "creditScore": 75,
    "creditRating": "BBB",
    "riskLevel": "MEDIUM",
    "debtBalance": {
      "amount": 25000.00,
      "currency": "GBP",
      "asOfDate": "2025-11-30"
    },
    "paymentMarks": {
      "count": 2,
      "severity": "MINOR",
      "lastMarkDate": "2025-10-15"
    },
    "financialData": {
      "turnover": 1500000.00,
      "employees": 45,
      "establishedYear": 2010
    },
    "riskFactors": [
      {
        "factor": "payment_history",
        "score": 80,
        "weight": 0.4
      },
      {
        "factor": "financial_stability",
        "score": 70,
        "weight": 0.3
      }
    ]
  },
  "metadata": {
    "dataFreshness": "CURRENT",
    "confidence": 0.95,
    "sources": ["credit_bureau", "company_registry"]
  }
}
```

#### Bulk Operations

**Bulk Risk Data Fetch:**
```http
POST /api/v1/companies/bulk-fetch
Authorization: Bearer {api-key}
Content-Type: application/json

{
  "companyIds": ["123456789", "987654321", "456789123"],
  "dataTypes": ["risk_data", "financial_data"],
  "includeHistory": false
}
```

#### Watchlist API

**Register Watchlist:**
```http
POST /api/v1/watchlists
Authorization: Bearer {api-key}
Content-Type: application/json

{
  "name": "High Risk Monitor",
  "description": "Monitor entities with credit score < 60",
  "criteria": {
    "creditScore": {
      "operator": "less_than",
      "value": 60
    },
    "riskLevelChange": {
      "operator": "changed_to",
      "values": ["HIGH", "CRITICAL"]
    }
  },
  "notifications": {
    "webhookUrl": "https://yourbc.bc.dynamics.com/webhook/risk/alert",
    "immediateAlert": true
  },
  "entityFilter": {
    "countries": ["GB", "US", "DE"],
    "minTurnover": 100000
  }
}
```

**Response:**
```json
{
  "watchlistId": 12345,
  "triggerId": 67890,
  "status": "ACTIVE",
  "createdDate": "2025-12-01T10:30:00Z",
  "estimatedMatches": 25
}
```

### Error Handling

**Standard Error Response:**
```json
{
  "error": {
    "code": "INVALID_API_KEY",
    "message": "The provided API key is invalid or expired",
    "details": {
      "requestId": "req-123456",
      "timestamp": "2025-12-01T10:30:00Z"
    }
  }
}
```

**Common Error Codes:**
- `INVALID_API_KEY`: Authentication failed
- `RATE_LIMIT_EXCEEDED`: API call limit reached  
- `COMPANY_NOT_FOUND`: Search returned no results
- `INVALID_REQUEST`: Malformed request data
- `SERVICE_UNAVAILABLE`: Temporary service outage

## Business Central API Integration

### Risk Data Access via Business Central APIs

**OData Endpoints:**

```http
# Business Entities
GET /api/brightcom/risk/v1.0/companies({companyId})/businessEntities
GET /api/brightcom/risk/v1.0/companies({companyId})/businessEntities({entityId})

# Risk Levels
GET /api/brightcom/risk/v1.0/companies({companyId})/riskLevels

# Watchlists
GET /api/brightcom/risk/v1.0/companies({companyId})/watchlists
GET /api/brightcom/risk/v1.0/companies({companyId})/watchlists({watchlistId})/matches

# API Call History
GET /api/brightcom/risk/v1.0/companies({companyId})/apiCallLedger
```

### Custom API Pages

**Business Entity API Page:**
```al
page 70080 "Business Entity API"
{
    APIVersion = 'v1.0';
    APIPublisher = 'BrightCom';
    APIGroup = 'risk';
    Caption = 'Business Entity API';
    DelayedInsert = true;
    EntityName = 'businessEntity';
    EntitySetName = 'businessEntities';
    PageType = API;
    SourceTable = "Business Entity";

    layout
    {
        area(Content)
        {
            repeater(GroupName)
            {
                field(entryNo; Rec."Entry No.")
                {
                    Caption = 'Entry No.';
                }
                field(ticCompanyId; Rec."TIC Company ID")
                {
                    Caption = 'TIC Company ID';
                }
                field(companyName; Rec.CompanyName)
                {
                    Caption = 'Company Name';
                }
                field(creditScore; Rec.CreditScore)
                {
                    Caption = 'Credit Score';
                }
                field(riskLevel; Rec.RiskLevel)
                {
                    Caption = 'Risk Level';
                }
                field(debtBalance; Rec.DebtBalance)
                {
                    Caption = 'Debt Balance';
                }
                field(paymentMarks; Rec.PaymentMarks)
                {
                    Caption = 'Payment Marks';
                }
                field(lastFetchDateTime; Rec.LastFetchDateTime)
                {
                    Caption = 'Last Fetch Date/Time';
                }
            }
        }
    }
}
```

### Integration Events API

**Available Events for Custom Integration:**

```al
namespace BrightCom.Risk.Events;

/// <summary>
/// Integration events for custom risk assessment logic
/// </summary>
codeunit 70100 "Risk Integration Events"
{
    /// <summary>
    /// Event fired before fetching risk data from external API
    /// </summary>
    [IntegrationEvent(false, false)]
    procedure OnBeforeRiskDataFetch(var BusinessEntity: Record "Business Entity"; var ApiRequest: JsonObject; var IsHandled: Boolean)
    begin
    end;

    /// <summary>
    /// Event fired after successful risk data update
    /// </summary>
    [IntegrationEvent(false, false)]
    procedure OnAfterRiskDataUpdated(var BusinessEntity: Record "Business Entity"; OldRiskLevel: Code[10]; ApiResponse: JsonObject)
    begin
    end;

    /// <summary>
    /// Event fired when risk level changes
    /// </summary>
    [IntegrationEvent(false, false)]
    procedure OnRiskLevelChanged(var BusinessEntity: Record "Business Entity"; OldRiskLevel: Code[10]; NewRiskLevel: Code[10])
    begin
    end;

    /// <summary>
    /// Event fired when watchlist criteria are matched
    /// </summary>
    [IntegrationEvent(false, false)]
    procedure OnWatchlistCriteriaMatched(var RiskWatchList: Record "Risk Watch List"; var BusinessEntity: Record "Business Entity"; MatchDetails: JsonObject)
    begin
    end;

    /// <summary>
    /// Event fired after API call completion (success or failure)
    /// </summary>
    [IntegrationEvent(false, false)]
    procedure OnApiCallCompleted(var APICallLedger: Record "API Call Ledger"; Success: Boolean; ResponseTime: Duration)
    begin
    end;
}
```

### Custom Integration Examples

**Example: Custom Risk Calculation**
```al
[EventSubscriber(ObjectType::Codeunit, Codeunit::"Risk Integration Events", 'OnAfterRiskDataUpdated', '', false, false)]
local procedure CustomRiskCalculation(var BusinessEntity: Record "Business Entity"; OldRiskLevel: Code[10]; ApiResponse: JsonObject)
var
    CustomRiskScore: Decimal;
    IndustryFactor: Decimal;
begin
    // Add custom industry risk factor
    IndustryFactor := GetIndustryRiskMultiplier(BusinessEntity."Industry Code");
    CustomRiskScore := BusinessEntity.CreditScore * IndustryFactor;
    
    // Update custom risk level based on enhanced calculation
    BusinessEntity."Custom Risk Score" := CustomRiskScore;
    BusinessEntity.Modify();
    
    // Trigger additional business logic
    if CustomRiskScore < 40 then
        CreateHighRiskAlert(BusinessEntity);
end;
```

**Example: CRM Integration**
```al
[EventSubscriber(ObjectType::Codeunit, Codeunit::"Risk Integration Events", 'OnRiskLevelChanged', '', false, false)]
local procedure SyncRiskToCRM(var BusinessEntity: Record "Business Entity"; OldRiskLevel: Code[10]; NewRiskLevel: Code[10])
var
    CRMConnector: Codeunit "CRM Integration Management";
    Customer: Record Customer;
begin
    // Find linked customer
    if Customer.Get(BusinessEntity."Customer No.") then begin
        // Update CRM system with new risk level
        CRMConnector.UpdateAccountRiskLevel(Customer."No.", NewRiskLevel);
        
        // Log the integration
        LogCRMSync(Customer."No.", OldRiskLevel, NewRiskLevel);
    end;
end;
```

## Webhook Integration

### Inbound Webhooks (From Risk Providers)

**Webhook Endpoint Configuration:**
```
URL: https://yourtenant.bc.dynamics.com/api/brightcom/risk/v1.0/webhook/notification
Method: POST
Content-Type: application/json
Authentication: Bearer token or API key
```

**Webhook Payload Structure:**
```json
{
  "eventType": "riskLevelChanged",
  "timestamp": "2025-12-01T10:30:00Z",
  "providerId": "TIC",
  "entity": {
    "ticCompanyId": "123456789",
    "companyName": "Example Company Ltd"
  },
  "riskChange": {
    "field": "creditScore",
    "oldValue": 75,
    "newValue": 45,
    "newRiskLevel": "HIGH"
  },
  "metadata": {
    "confidence": 0.95,
    "dataSource": "credit_bureau",
    "webhookId": "wh-789xyz"
  }
}
```

**Webhook Processing Codeunit:**
```al
codeunit 70110 "Webhook Processor"
{
    procedure ProcessRiskNotification(WebhookPayload: JsonObject): Boolean
    var
        BusinessEntity: Record "Business Entity";
        TICCompanyId: BigInteger;
        NewRiskLevel: Code[10];
    begin
        // Parse webhook payload
        if not ExtractTICCompanyId(WebhookPayload, TICCompanyId) then
            exit(false);
            
        // Find corresponding Business Entity
        BusinessEntity.SetRange("TIC Company ID", TICCompanyId);
        if not BusinessEntity.FindFirst() then
            exit(false);
            
        // Update risk data from webhook
        ExtractRiskData(WebhookPayload, BusinessEntity);
        BusinessEntity.Modify();
        
        // Trigger business logic
        OnRiskDataUpdatedViaWebhook(BusinessEntity, WebhookPayload);
        
        exit(true);
    end;
}
```

### Outbound Webhooks (To External Systems)

**Configuration for External System Notifications:**
```al
procedure SendRiskAlert(BusinessEntity: Record "Business Entity"; AlertType: Enum "Risk Alert Type")
var
    HttpClient: HttpClient;
    HttpRequest: HttpRequestMessage;
    HttpResponse: HttpResponseMessage;
    WebhookPayload: JsonObject;
begin
    // Build webhook payload
    WebhookPayload.Add('eventType', Format(AlertType));
    WebhookPayload.Add('timestamp', CurrentDateTime());
    WebhookPayload.Add('entityId', BusinessEntity."Entry No.");
    WebhookPayload.Add('ticCompanyId', BusinessEntity."TIC Company ID");
    WebhookPayload.Add('companyName', BusinessEntity.CompanyName);
    WebhookPayload.Add('riskLevel', BusinessEntity.RiskLevel);
    WebhookPayload.Add('creditScore', BusinessEntity.CreditScore);
    
    // Send to configured webhook endpoint
    HttpRequest.Method := 'POST';
    HttpRequest.SetRequestUri(GetWebhookUrl());
    HttpRequest.Content().WriteFrom(Format(WebhookPayload));
    
    if HttpClient.Send(HttpRequest, HttpResponse) then
        LogWebhookSuccess(BusinessEntity, AlertType)
    else
        LogWebhookError(BusinessEntity, AlertType, HttpResponse);
end;
```

## Rate Limiting and Performance

### API Rate Limit Management

**Rate Limit Headers:**
```http
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 847
X-RateLimit-Reset: 1638360000
```

**Implementation in Business Central:**
```al
procedure CheckRateLimit(): Boolean
var
    RiskSetup: Record "Risk Setup";
    APICallLedger: Record "API Call Ledger";
    CurrentMonthCalls: Integer;
begin
    RiskSetup.Get();
    
    // Count current month's API calls
    APICallLedger.SetRange("Call Date", CalcDate('<-CM>', Today()), Today());
    CurrentMonthCalls := APICallLedger.Count();
    
    // Check against limit with warning threshold
    if CurrentMonthCalls >= RiskSetup."Monthly API Call Limit" then
        exit(false);
        
    if CurrentMonthCalls >= (RiskSetup."Monthly API Call Limit" * RiskSetup."Warning Threshold" / 100) then
        ShowRateLimitWarning(CurrentMonthCalls, RiskSetup."Monthly API Call Limit");
        
    exit(true);
end;
```

### Performance Optimization

**Caching Strategy:**
```al
procedure GetCachedRiskData(TICCompanyId: BigInteger): JsonObject
var
    CacheKey: Text;
    CachedData: JsonObject;
    CacheAge: Duration;
begin
    CacheKey := StrSubstNo('risk_data_%1', TICCompanyId);
    
    // Check if data exists in cache and is fresh
    if GetFromCache(CacheKey, CachedData) then begin
        CacheAge := CurrentDateTime() - GetCacheTimestamp(CacheKey);
        if CacheAge < GetCacheExpiryTime() then
            exit(CachedData);
    end;
    
    // Fetch fresh data and update cache
    CachedData := FetchRiskDataFromAPI(TICCompanyId);
    SetCache(CacheKey, CachedData, CurrentDateTime());
    
    exit(CachedData);
end;
```

## Security Considerations

### API Key Management

**Secure Storage:**
```al
procedure SetAPIKey(NewAPIKey: Text)
var
    RiskSetup: Record "Risk Setup";
    EncryptionMgt: Codeunit "Encryption Management";
begin
    RiskSetup.Get();
    
    // Encrypt and store API key
    if EncryptionMgt.IsEncryptionEnabled() then
        RiskSetup."Encrypted API Key" := EncryptionMgt.EncryptText(NewAPIKey)
    else
        RiskSetup."API Key" := NewAPIKey;  // Fallback for environments without encryption
        
    RiskSetup.Modify();
    
    // Test connection with new key
    TestAPIConnection();
end;
```

### Audit Trail

**API Call Logging:**
```al
procedure LogAPICall(RequestType: Enum "API Request Type"; TICCompanyId: BigInteger; Success: Boolean; ResponseTime: Duration; ErrorMessage: Text)
var
    APICallLedger: Record "API Call Ledger";
begin
    APICallLedger.Init();
    APICallLedger."Entry No." := GetNextEntryNo();
    APICallLedger."Call Date" := Today();
    APICallLedger."Call Time" := Time();
    APICallLedger."Request Type" := RequestType;
    APICallLedger."TIC Company ID" := TICCompanyId;
    APICallLedger.Success := Success;
    APICallLedger."Response Time (ms)" := ResponseTime;
    APICallLedger."User ID" := UserId();
    
    if not Success then
        APICallLedger."Error Message" := CopyStr(ErrorMessage, 1, MaxStrLen(APICallLedger."Error Message"));
        
    APICallLedger.Insert();
end;
```

---

*For implementation assistance with API integrations, contact BrightCom Solutions or your Business Central development partner.*