# **Building Banking Chatbot using Amazon Lex**  

Welcome to the **Banking Chatbot** project! This chatbot is designed to enhance the customer experience by providing real-time assistance for banking-related queries. Built with **Amazon Lex**, this intelligent conversational interface aims to automate a variety of financial tasks, ensuring customers get prompt, secure, and accurate responses to their inquiries.  

Amazon Lex is a fully managed service from AWS that enables developers to build conversational interfaces (chatbots and voice assistants) powered by **natural language understanding (NLU)** and **automatic speech recognition (ASR)**.  

---

## **Project Overview**  
*(Coming Soon: ...)* 

--- 

## **Steps to Complete the Project**  

### **Step 1: Creating Your Bot**  
1. **Select**: Create bot.  
2. **Choose**: Traditional.  
3. **Select**: Create a blank bot.  
4. **Enter Bot Name**:  
   - **BankerBot**  
5. **Description**:  
   - Banker Bot to help customers check their balance and make transfers.  
6. **IAM Permissions**:  
   - Select **Create a role with basic Amazon Lex permissions** (used later for **Lambda** integration).  
7. **COPPA Compliance**:  
   - Select **No** (as the bot is not targeted toward children).  
8. **Idle Session Timeout**:  
   - Keep the default of **5 minutes**.  
9. **Select**: Next to open the **Voice and Language Setup** page.  
10. **Language**:  
   - Keep **English** to explore the full range of Lex features.  
11. **Voice Interaction**:  
   - Explore voice options in the **Voice dropdown** (default: Danielle).  
     - Two popular voices: **Gregory** and **Ruth**. 😊  
12. **Intent Classification Confidence Threshold**:  
   - Keep the default value of **0.40**.  
13. **Select**: Done.  

Your **basic bot structure** is now complete and ready to come to life!  

---

### **Step 2: Creating Your First Intent**  
1. After the bot is created, you’ll be on the **Intent: NewIntent** page.  
2. **Change the Intent Name**:  
   - Under **Intent details**, enter **WelcomeIntent** as the new name.  
3. **Description**:  
   - Add: **Welcoming a user when they say hello**.  
4. **Sample Utterances**:  
   - Scroll down to the **Sample utterances** panel.  
   - Click the **Plain Text** button.  
   - Add these utterances:  
     - Hi  
     - Hello  
     - I need help  
     - Can you help me?  
5. **Preview Utterances**:  
   - Switch back to the **Preview button** to see how these utterances appear in chat.  
6. **Closing Response**:  
   - Scroll down to **Closing response** and expand the speech bubble under **Response sent to the user after the intent is fulfilled**.  
   - In the **Message field**, enter:  
     ```  
     Hi! I'm BB, the Banking Bot. How can I help you today?  
     ```  
7. **Save the Intent**:  
   - Click **Save intent**.  
8. **Build the Bot**:  
   - Click **Build** at the top of the page.  
   - (This process takes about 30 seconds – time for a quick stretch! 😊)  
9. **Test Your Bot**:  
   - After building, click **Test** to interact with the bot using your sample utterances.  
   - Try different phrases:  
     - Hi  
     - Hello  
     - I need help  
     - Can you help me?  

10. **Explore Other Inputs**:  
    - Since we’ve set the confidence threshold to **0.40**, Lex might understand related phrases too! Try these:  
      - Help me  
      - Hiya  
      - How are you?  
      - Good morning  

💡 **Note:**  
- **First three** inputs work fine, as Lex’s **ML engine** can match similar intents.  
- **Last two** may not work and trigger a **FallbackIntent**, meaning Lex doesn’t recognize them yet (we’ll explore this in the next step).

11. **Test Voice Interaction**:  
    - Click the **microphone icon** on the left of the chatbox.  
    - Speak: "Hello" and click the tick icon to submit.  
    - Now, try another greeting or way of saying hello!  

💡 **Voice Tips:**  
- The bot uses the **English (US) dialect**, so it may not perfectly transcribe other English accents.  
- Amazon Lex supports multiple **English dialects** for better accuracy.

---

### **Step 3: Managing the FallbackIntent**  

1. **Navigate**: On the left-hand navigation, choose **FallbackIntent**.  

💡 **What is FallbackIntent?**  
- If the confidence score for a user input is **below 0.40**, Lex triggers the **FallbackIntent**. This intent acts as a safety net when the bot doesn't understand the user's request. It helps maintain a smooth interaction by providing a helpful error message.  

2. **Customize the Fallback Message**:  
   - Scroll to **Closing responses** and expand the speech bubble.  
   - Update the **Message field** with the following:  
     ```  
     Sorry, I am having trouble understanding. Can you describe what you'd like to do in a few words?  
     I can help you find your account balance, transfer funds, and make a payment.  
     ```  

💡 **Best Practice:**  
- Provide hints in fallback messages about the type of commands the bot can understand. This improves the user experience by guiding users back on track.  

3. **Add Variations**:  
   - Toggle the **Variations - optional** setting.  
   - Add this variation:  
     ```  
     Hmm, could you try rephrasing that? I can help you find your account balance, transfer funds, and make a payment.  
     ```  
   - Add one more variation to keep the bot’s responses dynamic.  

💡 **What are Variations?**  
- Variations are alternate responses. When the FallbackIntent is triggered, Lex randomly picks a variation to respond, making the chatbot sound more conversational.  

4. **Save and Build**:  
   - Click **Save intent** and then **Build** (another ~30 seconds).  

5. **Test the FallbackIntent**:  
   - Try the messages that previously failed (e.g., "Good morning" or "How are you").  
   - Observe how the bot now provides more helpful fallback messages.  

6. **Test Voice Input**:  
   - Use the **microphone icon** to test voice input with phrases like "Hello" or "Hiya."  
   - Remember, the bot uses the **English (US)** dialect, so accents might affect recognition. If needed, explore Lex’s **multiple English dialects** for better accuracy.

---

### **Step 4: Create a Custom Slot for Account Types**  

1. **Navigate**: On the left-hand panel, go to **Slot Types**.  
2. **Create Slot Type**:  
   - Click **Create slot type**.  
   - **Name the Slot**: `AccountType`.  
   - **Description**: Slot to capture different types of accounts (e.g., savings, checking).  

3. **Add Slot Values**:  
   - In the **Values** section, add the following options:  
     - Savings  
     - Checking  
     - Credit
          - credit card
          - visa
          - mastercard
          - amex
          - american express


4. **Save Slot Type**:  
   - Click **Save** to store your custom slot.  

5. **Add Slot to an Intent**:  
   - Navigate back to **Intents**.  
   - Open the **CheckBalance Intent**.  
   - In the **Slot section**, click **Add a slot**.  
   - **Name**: `accountType`  
   - **Slot Type**: Choose `accountType` from the dropdown.  
   - **Prompt**: For which account would you like your balance?
     ```  
     Which account would you like to use?  
     ```
   - Navigate back to **Intents**
   - Open the **CheckBalance Intent**
   - In the **Slots pane**
   - Click on add slot
   - Add **name** as **dateOfBirth**
   - Select slot type as AMAZON.Date
   - **Prompt**: For verification purposes, what is your date of birth?

6. **Test Your Slot**:  
   - Save and build the bot.  
   - Go to **Test** mode and try interacting with the bot:  
     - "Transfer funds from my savings account."  
     - "I want to move money to my credit account."  

💡 **Note:**  
- If the bot doesn't recognize the account type immediately, try adjusting the slot synonyms for better coverage.  

---

### Step 5: **Create Your AWS Lambda Function**
💡 **What is AWS Lambda?** 
- AWS Lambda is a service that lets you run code without provisioning or managing servers.Lambda runs your code only when needed and scales automatically, from a few requests per day to thousands per second - 
  all you need to do is supply your code in one of the languages that Lambda supports.
