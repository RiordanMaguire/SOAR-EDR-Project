# 🛡️ SOAR + EDR Project

## 🎯 Objective

The goal of this project is to reduce repetitive tasks through automation by implementing a structured process using playbooks.

In this project, the objective is to build a detection rule in **LimaCharlie** to identify the execution of `LaZagne.exe`, an open-source post-exploitation tool used to recover stored passwords on a system.

Once detected, the event is forwarded to **Tines**, where a custom playbook (Story) triggers the following sequence:

1. Notify the user via **email** and **Slack**  
2. Prompt the user with a **YES/NO** question asking whether to isolate the affected machine  
3. If the user selects **YES**, LimaCharlie automatically isolates the machine and sends a Slack message:  
   > `"The computer <computer> has been isolated."`
4. If the user selects **NO**, a Slack message is sent:  
   > `"The computer <computer> was not isolated. Please investigate."`
   >##  Workflow Diagram
   > The following diagram outlines the automated workflow from detection to response, highlighting the integration between LimaCharlie, Tines, Slack, and email.
   > ![RIO EDR SOAR Workflow](https://github.com/user-attachments/assets/3e607b04-69f3-4772-878b-13f1b19ce64b)
   > ## 🧠 Skills Learned

### 🔍 EDR Integration & Threat Detection

- Developed custom detection rules using LimaCharlie, demonstrating proficiency in endpoint detection and response (EDR) platforms.
- Analysed host telemetry to identify suspicious behavior and trigger actionable alerts.

### ⚙️ SOAR Automation

- Automated incident response using Tines, showcasing skills in Security Orchestration, Automation, and Response (SOAR).
- Designed and implemented a no-code workflow that responded to detections by executing an automated computer isolation action.

### 🧩 Incident Response Workflow Engineering

- Built real-time alerting and response flow between LimaCharlie, Slack, and Tines.
- Ensured alerts from LimaCharlie detection rules triggered Slack notifications and isolation commands without manual intervention.

### 🔗 Cross-Platform Tool Integration

- Integrated APIs between multiple security tools and communication platforms.
- Demonstrated technical understanding of webhooks, JSON handling, and API authentication.

### 🛡️ Risk Reduction via Automation

- Minimised Incident Response time and improved containment efficiency, aligning with best practices for MITRE ATT&CK response strategies.

---

## 🛠️ Tools Used

- LimaCharlie  
- Tines  
- Slack  
- Virtual Machine  
- Email

- ## 📋 Steps

1. Onboarded LimaCharlie to the VM using the sensor key.

   ![unnamed](https://github.com/user-attachments/assets/760f688b-aa49-486e-9e64-14df45ad1da3)









2. Verified that the agent was installed and that the VM was onboarded by checking the sensor list page on LimaCharlie, confirming the process was successful (Hostname: RIO-SOAR-EDR).

    ![step 2 refix](https://github.com/user-attachments/assets/7dc68e16-6b11-4c48-ab36-c1031d28c647)



   






3. Installed and ran `LaZagne.exe` on the VM — an open-source post-exploitation tool used to recover stored passwords on a system.![step 3](https://github.com/user-attachments/assets/af129eab-0480-4c69-b968-c2358bf59bb1) ![step3 2](https://github.com/user-attachments/assets/83f33b0e-568e-48fa-8a64-6f80dcac203c)





4. Checked the timeline on LimaCharlie to verify that the EDR detected `LaZagne.exe` being executed.![step 4 refix](https://github.com/user-attachments/assets/dadf1f10-6e5c-458f-8517-f669e115ce6a)



5. Navigated to **Automation > D&R Rules** and created a detection rule to identify events related to `LaZagne.exe`.![step 5 1 refix](https://github.com/user-attachments/assets/a26d25b3-3a2b-4e22-b72c-4d32ee194148)![step 5 2 refix](https://github.com/user-attachments/assets/c70d87e6-e319-45dc-9f7e-b59605980466)





6. Tested the rule by selecting the **Target Event** tab, pasting the event into the input box, and confirming the rule successfully detected the desired events.![step 6 refix](https://github.com/user-attachments/assets/6401565f-f262-491b-a21e-59221e3d62eb)![step 6 1 refix](https://github.com/user-attachments/assets/8090104e-6f5f-4bb1-a361-5348d29be60a)





7. Re-ran `LaZagne.exe` and verified detection under the **Detections** tab on LimaCharlie.![step 7](https://github.com/user-attachments/assets/d97803ce-cbff-42fa-8de7-c37ff8c0c078)![step 7 refix](https://github.com/user-attachments/assets/9b78c818-1b9d-4cbc-b821-f9911b51205a)




8. Created a channel in Slack named `alerts`.![step 8](https://github.com/user-attachments/assets/fa078419-8073-4baf-a2f5-278ec93713fc)


9. Created a Tines account and established the connection between LimaCharlie and Tines using a **WebHook Action (Retrieve Detections)**
   - Navigated to **Output Streams** in LimaCharlie  
   - Selected **Detections**, chose **Tines** as destination  
   - Configured the name and destination host, then saved the configuration  
   - Confirmed that Tines Webhooks was receiving the detections.![step 9](https://github.com/user-attachments/assets/9141b2ef-6ded-4cdf-b74a-20f55d9ea6e9)![step 9 1](https://github.com/user-attachments/assets/1d20ddf3-6ba0-4d82-b917-de8818a98ef4)![step 9 2](https://github.com/user-attachments/assets/a21745a2-a88c-467c-a0fb-1f60a8e06ace)![step9 3](https://github.com/user-attachments/assets/b927cfb2-a205-42ff-9f7a-eca73927bcda)![step 9 4](https://github.com/user-attachments/assets/e2eea357-15e4-4bd4-8114-03390c7e8e78)![step 9 5](https://github.com/user-attachments/assets/878cab1d-3c4d-42ed-bca5-80dc4b2c3bd6)


10. Integrated Slack with Tines by adding Slack credentials to Tines.  
    - Added the Slack template to the Story (playbook)  
    - Used the **Send a Message** function with the Slack channel ID  
    - Configured it to send detection alerts to the `alerts` channel![10](https://github.com/user-attachments/assets/6958258b-dfa0-44bb-841d-ca802c69c00d)![10 1](https://github.com/user-attachments/assets/40de344a-a436-4e92-ab62-da01ee8bc925)![10 2](https://github.com/user-attachments/assets/219d22ed-3ee0-4cf6-bc5c-85271db500a5)




11. Added the **Send an Email** function and configured it to email detection details.![11](https://github.com/user-attachments/assets/03c3bbef-5d2f-4892-8d0f-34fceb4b0982)![11 1](https://github.com/user-attachments/assets/4f731c70-c5c4-45c8-8aeb-b05f01372f56)



12. Added a **User Prompt** with detection details and the question:  
    > “Does the user want to isolate the machine? (YES/NO)”![12](https://github.com/user-attachments/assets/fc2d10db-8444-44b2-82b0-cdf17719c233)![step 11 refix](https://github.com/user-attachments/assets/3e577b03-f41c-4f23-a2fb-ba047514cdfa)



13. Configured the **NO** trigger to send a Slack message:
 > “The computer `<computer>` was not isolated. Please investigate.”![13](https://github.com/user-attachments/assets/d30af0a2-f731-4dfe-8b3d-e7029f64b008)![13 1](https://github.com/user-attachments/assets/4a04a180-20a8-4057-bf62-7ad52cc3dbfa)![13 2](https://github.com/user-attachments/assets/a2b22342-aad3-4a7e-be8f-f764cdf00b34)




14. Configured the **YES** trigger and added the **LimaCharlie Isolate Server** template.![14](https://github.com/user-attachments/assets/545e5e41-1cbb-4e61-9b8e-9413952fce6f)


15. Copied the **ORG JWT key** from LimaCharlie and used it to register LimaCharlie credentials in Tines.![15](https://github.com/user-attachments/assets/782f304e-603e-46c4-8879-ab3769b6f94c)![15 1](https://github.com/user-attachments/assets/11b84f5e-c894-49d6-b0ca-d10f806f8794)



16. Added the **LimaCharlie Get Isolation Status** template and linked it to Slack to send a message after isolation with content:  
    ```
    Isolation Status: True  
    The Computer: <Computer Name>!
    ```

    ![16](https://github.com/user-attachments/assets/815a1174-a5b8-4089-a11c-5e0fe43a385e)






17. Ran `LaZagne.exe`, received Slack and email alerts, selected **YES** for device isolation in the prompt, received a Slack confirmation message, and verified that the VM was automatically isolated in LimaCharlie — confirming full functionality and successful project completion.![step 17](https://github.com/user-attachments/assets/39831cf6-9760-4142-85a3-ddc011632355)![step 17 1](https://github.com/user-attachments/assets/2ef1c2b4-77f6-4c4e-adc1-5971df6cb63e)







