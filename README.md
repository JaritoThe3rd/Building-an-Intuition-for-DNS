# Azure DNS Lab: A-Record, DNS Cache, and CNAME

## Lab Preparation

- **Ensure Both VMs Are Running**
  - Start `DC-1` and `Client-1` in the Azure Portal if they are off.

---

## A-Record Exercise

1. **Log into DC-1**
    - Sign in as your domain admin account:  
      ```
      mydomain.com\jane_admin
      ```
2. **Log into Client-1**
    - Sign in as:  
      ```
      mydomain\jane_admin
      ```
3. **Test Name Resolution from Client-1**
    - Attempt to ping `mainframe`:
      ```
      ping mainframe
      ```
      > Expected: Fails (host not found).
    - Use nslookup on `mainframe`:
      ```
      nslookup mainframe
      ```
      > Expected: No DNS record found.
4. **Create an A-Record for "mainframe" on DC-1**
    - On DC-1, open DNS Manager.
    - Create a new A-record:
      - **Name:** `mainframe`
      - **IP Address:** (Use DC-1’s private IP address)
5. **Verify from Client-1**
    - Ping `mainframe` again:
      ```
      ping mainframe
      ```
      > Expected: Now resolves and succeeds.


https://github.com/user-attachments/assets/66cd8414-7651-477f-9d00-8b4772e550a0


---

## Local DNS Cache Exercise

1. **Modify the A-Record for "mainframe" on DC-1**
    - Change the IP address of `mainframe` to `8.8.8.8` in DNS Manager.
2. **Test Name Resolution from Client-1**
    - Ping `mainframe`:
      ```
      ping mainframe
      ```
      > Expected: Still responds with the old address due to DNS cache.
3. **View and Flush Local DNS Cache on Client-1**
    - Display the DNS cache:
      ```
      ipconfig /displaydns
      ```
    - Flush the DNS cache:
      ```
      ipconfig /flushdns
      ```
    - Confirm cache is cleared:
      ```
      ipconfig /displaydns
      ```
4. **Test Again from Client-1**
    - Ping `mainframe`:
      ```
      ping mainframe
      ```
      > Expected: Now resolves to `8.8.8.8`.

---

## CNAME Record Exercise

1. **Create a CNAME Record on DC-1**
    - In DNS Manager, create a CNAME record:
      - **Name:** `search`
      - **FQDN Target:** `www.google.com`
2. **Test CNAME Record from Client-1**
    - Ping `search`:
      ```
      ping search
      ```
    - Use nslookup on `search`:
      ```
      nslookup search
      ```
      > Expected: CNAME record points to `www.google.com`.

---

## Lab Completion

- **Do not delete the VMs.** These will be used in future labs.
- If you are done for the day, you may "Stop" (deallocate) the VMs in the Azure Portal to save on costs.

---

**End of Lab**
