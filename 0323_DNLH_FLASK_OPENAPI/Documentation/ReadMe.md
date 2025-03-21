# Global AI Hyderabad - Monthly Online Event - Mar 2025

## Date Time: 23-Mar-2025 at 09:00 AM IST



## Event URL: [https://www.meetup.com/global-ai-hyderabad/events/306606120](hhttps://www.meetup.com/global-ai-hyderabad/events/306606120)

## YouTube URL: [https://www.youtube.com/live/RUeaM9Rix60](https://www.youtube.com/live/RUeaM9Rix60)





![Information | 100x100](../Documentation/Images/Information.PNG)

![Seat Belt | 100x100](../Documentation/Images/SeatBelt.PNG)


Session Title: Building Intelligent APIs: Flask API with Azure OpenAI

---

### [Introduction – 2 Minutes]

1. Greeting & Session Overview:  
   - “Good morning, everyone! I’m Madapthi Archana, and today I’ll show you how to build an intelligent Flask API that interacts with Azure OpenAI.”  
   - “In the next 20 minutes, we’ll explore our project’s architecture, dive into the core code, and see a live demo where we send a sample prompt to our API.”

2. Session Objectives:  
   - Explain the overall system architecture.
   - Walk through how the Flask API integrates with Azure OpenAI.
   - Demonstrate how to test the API using a PowerShell command.

---

### [Section 1: System Architecture Overview – 4 Minutes]

1. The Architectural Diagram:

![System Architecture | 100x100](../Documentation/Images/SystemArchitecture.jpg)

    
     - Frontend (React UI) – The user interface (even if it’s not the focus today).  
     - Flask API (Backend) – The core engine handling requests.  
     - Azure OpenAI Service – The service generating AI responses.  
     - Auth0 & Logging (Optional) – For authentication and debugging.
  
2. Describing the Interaction Flow:  
   - “The React UI sends a request to our Flask API. The API processes the request and calls Azure OpenAI to get a response. Once received, the API sends the result back to the UI.”
   - Emphasize the importance of using environment variables to secure keys and configuration.

---

### [Section 2: Code Walkthrough – 8 Minutes]

1. Project Structure Overview:  
   - Show the directory layout:
     
     flask-react-aoai-completions/
     │── docs/
     │── src/
     │   ├── backend/
     │   │   ├── api/
     │   │   │   ├── home_routes.py
     │   │   │   ├── completions_routes.py
     │   │   ├── services/
     │   │   │   ├── azure_openai_service.py
     │   │   ├── utils/
     │   │   │   ├── env_config.py
     │   │   │   ├── error_handling.py
     │   │   │   ├── logging_config.py
     │   │   ├── app.py
     │── .env
     │── README.md
     

2. Flask API Initialization (app.py):  
   - “In app.py, we initialize our Flask application, configure logging, and register our blueprints. This is the entry point of our API.”
   - Highlight the error handler and blueprint registration.

3. Azure OpenAI Service (azure_openai_service.py):  
   - Walk through how environment variables are loaded (API key, endpoint, deployment name, API version).  
   - Show the core function (for example, a simplified version) that calls the Azure OpenAI API:
     python
     def fetch_openai_response(prompt):
         chat_prompt = [
             {"role": "system", "content": "You are an AI assistant that helps people find information."},
             {"role": "user", "content": prompt}
         ]
         try:
             response = client.chat.completions.create(
                 model=deployment_name,
                 messages=chat_prompt,
                 max_tokens=800,
                 temperature=0.7,
                 top_p=0.95,
                 frequency_penalty=0,
                 presence_penalty=0,
                 stop=None,
                 stream=False
             )
             return response.choices[0].message.content
         except Exception as e:
             return f"Error: {str(e)}"
     
   - Explain that this function encapsulates the logic of communicating with Azure OpenAI and returning the complete response.
  
4. API Route for Completions (completions_routes.py):  
   - Show how the route is set up to handle POST requests:
     python
     @completions_api_bp.route("/completions", methods=["POST"])
     def generate_completion():
         data = request.get_json()
         prompt = data.get("prompt", "")
         return Response(fetch_openai_response(prompt), content_type="text/plain")
     
   - Emphasize that the endpoint accepts a JSON payload and returns the AI-generated response.

---

### [Section 3: Live Demo – 5 Minutes]

1. Start the Flask Server:  
   - “I’ll now start our Flask server by running python app.py.”
   - Show terminal output indicating the server is running on a specified port.

2. Test the API with PowerShell:  
   - “Let’s test the API using the following PowerShell command:”
     powershell
     Invoke-RestMethod -Uri "http://127.0.0.1:5009/api/completions" `
                       -Method POST `
                       -Headers @{"Content-Type"="application/json"} `
                       -Body '{"prompt": "What is an Orange"}'
     
   - Execute the command and display the resulting output.
   - “Here, you can see that the prompt is sent to our Flask API, which in turn calls Azure OpenAI and returns the complete response.”

3. Highlight Key Points:  
   - Discuss how the API is secure by using environment variables.
   - Mention that while this version is synchronous, it lays the foundation for future enhancements (like streaming or integrating with a frontend).

---

### [Section 4: Q&A and Wrap-Up – 3 Minutes]

1. Recap Key Takeaways:  
   - “Today we saw how Flask and Azure OpenAI can be integrated to build a powerful intelligent API.”
   - “We walked through the architecture, code, and even saw a live demo using a PowerShell command.”
   - “This foundation is scalable and can be extended to include real-time streaming, a dynamic React UI, and robust authentication with Auth0.”

2. Future Enhancements:  
   - “In future sessions, we’ll explore adding streaming support, a React frontend, and securing the API with Auth0.”
   - “This is just the beginning of building secure and intelligent AI applications.”

3. Open the Floor for Questions:  
   - “I’d now like to take any questions you might have about the architecture, code, or potential next steps.”

4. Closing:  
   - “Thank you for your attention and participation today. I’m excited to see how we can evolve this project further.”