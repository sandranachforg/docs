<Steps>
  <Step title= "Create A Dataset">

<Tip>

**Pro Tip**: Hamming accepts CSV & JSON files up to 10MB.

</Tip>
    
    1. Visit [app.hamming.ai/datasets](https://app.hamming.ai/datasets?page=1) to create a dataset.
    2. Click on **+Add New Dataset**. You can either upload an existing dataset or create an empty dataset and then use the JSON editor to build your dataset.
       The dataset should contain **all phone calls scenarios** you'd like Hamming's test agent to simulate. 
    3. Enter a dataset name and description.
    4. Select the input columns. The input columns are the data points you'd like the Hamming test agent to reference. 



<iframe src="https://www.youtube.com/embed/Sw1GgRYKUG4" width="500" height="280" frameborder="0" allowfullscreen></iframe>

  </Step>

 <Step title="Create A Scoring Prompt" >

<Tip>

**Pro Tip**: We recommend using gpt-4o with temperature 0 to get the best results.

</Tip>

    1. Visit [app.hamming.ai/prompts](http://app.hamming.ai/prompts) to create a scoring prompt.
       The prompt should contain concise instructions for the scorer.
    2. Click on **+Add Prompt**.
    3. Enter a prompt name and description.
    4. Select the model that you want to use to evaluate your virtual voice agent.
    5. Add a system prompt.

<Accordion icon="message-bot" title="System Prompt">
```
You are an expert data analyst, with 30 years of experience analyzing phone call transcripts. You have a great attention to details.
```
</Accordion>

    6. Add a user prompt.


<Warning>

**Important**: The output of the prompt must be an XML structure like described below.

</Warning>

<Accordion icon="message-bot" title="User Prompt">
  ```
[TASK]
You are given the <transcript> of a phone call between a receptionist (HUMAN) and a customer (BOT).
Your task is to classify the transcript of the phone call, given the [CRITERIA]. 

[CRITERIA]
Was the receptionist (HUMAN) able to schedule an appointment for the customer? 1 - Yes; 0 - No;
If there is not enough information in the transcript to determine the correct classification, label as 2 - N/A;

Assign one of the labels above and provide reasoning for why the call should be assigned that label.

[INPUT]
<transcript>
{{transcript}}
</transcript>

[OUTPUT]
<score>
<reason>
Find evidence in the transcript to prove whether the interviewer succeeded or failed to meet the criteria.
Provide a detailed, step-by-step explanation for assigning a label, based on the available evidence or the absence of it.
</reason>
<value>
0 | 1 | 2
</value>

```

</Accordion>

    7. Save the prompt and deploy to production


    
<iframe src="https://www.youtube.com/embed/0eSTDSic8aQ" width="500" height="280" frameborder="0" allowfullscreen></iframe>
 

  </Step>

<Step title="Create A Scorer">

<Warning>

**Important**: Ensure that the values in the scorer align with the labels from your scoring prompt. For example, if the value "0" represents "No" in your prompt, make sure the scorer also labels "0" as "No."

</Warning>

    1. Visit [app.hamming.ai/evals](http://app.hamming.ai/evals) to create a scorer, which simply acts as a wrapper for the scoring prompt.
    2. Click on **+Add Scorer**.
    3. Enter a scorer name and description.
    4. Add values and labels which will be used to display the results of the test.
    5. Select the scoring prompt you created in Step 2 and set the prompt label to **production**.
    6. Change the Variable Mappings field to **Output** and enter **transcript** in the field on the right. 


<iframe src="https://www.youtube.com/embed/fsbpJAc3evI" width="500" height="280" frameborder="0" allowfullscreen></iframe>

  </Step>

<Step title="Create A Hamming Test Agent">

<Tip>

**Pro Tip**: If you want to speak to Hamming's test agent, you can enter your own phone number and Hamming's test agent will call you.

</Tip>

    1. Visit [app.hamming.ai/voice-agents](http://app.hamming.ai/voice-agents) to set up a Hamming test agent (customer).
    2. Click on **+Add Voice Agent**.
    3. Enter a name.
    4. Select **Function** from the Scoring dropdown and select the scorer you created in the previous step.
    5. Configure a prompt for the Hamming test agent with input variables from your dataset, allowing it to simulate a 
       variety of customer situations. We recommend following the format below.

<Accordion icon="message-bot" title="Test Agent (Customer) Prompt">
  ```
You are calling a car dealership and talking to the front-desk assistant. Follow the scenario below:

Your name: {name}
Department you want to talk to: {department_name}
Buying / Leasing interest: {buy_or_lease}
Your Customer Status: {existing_customer}
Your budget for buying car: {budget}
Your phone number: {phone_number}
When to schedule appointment: {appointment_schedule}
Service Requested: {type_of_service}


[RULES]
Only answer questions when you are asked. Don't disclose any information without being asked first.
Say goodbye at the end.

```

</Accordion>

   

<iframe src="https://www.youtube.com/embed/Y2hkuLD5kmY" width="500" height="280" frameborder="0" allowfullscreen></iframe>


  </Step>

<Step title="Run Hamming Test Agent">

1. Under dataset, select the dataset you created in Step 1.
2. Click on Run.
3. Enter the phone number of your virtual voice agent.
4. Click on Run Calls.
5. Once your calls have finished, you will be able to see the results in the evaluation column.


<iframe src="https://youtube.com/embed/HCPrkT6I_kA" width="500" height="280" frameborder="0" allowfullscreen></iframe>

</Step>

</Steps>
