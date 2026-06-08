# Paris-Travel-Chatbot
AI-powered Paris travel guide chatbot built with OpenAI API: multi-turn conversation, guardrails, and deterministic responses.

# Project Objective
To build a context-aware AI travel chatbot using the OpenAI API that answers Parisian tourist questions through multi-turn conversation, system-level guardrails, and deterministic response control.

# Tools & Technologies Used
Language: Python       
Libraries: OpenAI        
Environment: DataCamp DataLab

# Key Insights
Temperature (0.0) controls how "creative" vs "deterministic" the model is. At 0.0, the model always picks the most likely next token, the responses are consistent and factual, ideal for a travel guide where accuracy matters more than creative variations for each run.                          
Shot prompting - this code uses zero-shot prompting (no examples given), relying purely on the system prompt to guide the model's behavior. The questions are passed directly as user messages.                                        
Guardrails via sys_msg. The system message acts as a behavioral contract. It sets the model's persona ("a local Parisian") and explicitly restricts it to Paris-only topics, making it refuse off-topic questions.                             
Conversation memory (the conversation list). The OpenAI API is stateless meaning it has no memory between calls. The code reconstructs memory manually: every user message and every assistant reply is appended to conversation, which is then sent in full on every API call. By question 3, the model "sees" questions 1 and 2 and their answers, giving it context (ex. It knows Questions 1 & 2 asked). This is the standard pattern for building multi-turn chatbots on top of a stateless API.
