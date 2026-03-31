# AIBizstack-system- 
graph TD
    subgraph Customer_Side [Customer Experience]
        A[Visit aibizstack.com] --> B{Checkout via Stripe}
        B -- Success --> C[Success Inbox]
        B -- Retry --> D[Retry / Support]
    end

    subgraph Logic_Layer [PHP Webhook Handler]
        B --> E[Webhook: Validate Payment]
        E -- Valid --> f[Access Product Files]
        E -- Declined/Error --> G[Log Error & Alert]
        
        f --> H{Check .htaccess}
        H -- Secure --> I[PHPMailer Engine]
        H -- File Error --> G
        
        I -- Send Success --> C
        I -- Bounce/Failure --> J[Catch SMTP Exception]
    end

    subgraph Monitoring_Layer [Silent Alerts & Phone]
        G --> K[Alert via Gmail]
        G --> L[Personal Phone]
        J --> M[Silent Forward]
    end
