RAG Project 

**This below line will import the environment values**
from dotenv import load_dotenv
load_dotenv()


**import OpenAI**

from openai import OpenAI
openai_client = OpenAI()


def llm(prompt):
    response = openai_client.responses.create(
        model='gpt-5.4-mini',
        input=prompt
    )
    return response.output_text
	
	
**Before RAG**


question ='What is the rent amount?'
answer = llm(question)
print(answer)

**After RAG implementation**

context = '''
	Rental Agreement

	Landlord: Rajesh Kumar
	Tenant: Tamilselvi M
	Property Address: 12 MG Road, Chennai, Tamil Nadu
	Monthly Rent: ₹15,000
	Security Deposit: ₹60,000
	Lease Start Date: 01 January 2026
	Lease End Date: 31 December 2026
	Rent Due Date: 5th of every month
	Maintenance Charges: ₹1,500 per month paid by the tenant
	Pets Allowed: No
	Notice Period: 2 months for both landlord and tenant
	'''


  **Prompt**

  
prompt = f'''
you are a helpful assistant for answering questions about the course. Use the following context to answer the question.

if the question is not related to the context, say "I don't know".

Question: 
{question}

context:
{context}
'''


print(prompt)



**JSON data **



def rag(question):
    search_results = search(question)
    user_prompt = build_prompt(question, search_results)
    return llm(user_prompt)


import requests

docs_url = "https://raw.githubusercontent.com/Tamiltam0007/RAG_Repo_dataSet/main/dataset.json"

courses_raw = requests.get(docs_url).json()
response = requests.get(docs_url)
courses_raw = response.json()



