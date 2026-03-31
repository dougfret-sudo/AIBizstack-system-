```mermaid
graph TD
  subgraph Customer_Side [Customer Experience]
        A[Visit aibizstack.com] --> B{Checkout via Stripe}
        B -- Success --> C[Success Inbox]
        B -- Retry --> D[Retry / Support]
    end

 subgraph Logic_Layer [PHP Webhook Handler]
        B --> E[Webhook: Validate Payment]
        E -- Valid --> F[Access Product Files]
        E -- Declined/Error --> G[Log Error & Alert]
        
        F --> H{Check .htaccess}
        H -- Secure --> I[PHPMailer Engine]
        
        I --> N[Business Email Support]
    end

    subgraph Monitoring_Layer [Support & Alerts]
        N -- Send Success --> C[Customer Inbox]
        N -- Silent Forward --> L[Personal Phone]
        G -- Alert --> N
    end
```
