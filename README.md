# ML-system-design

codebasics [AI System Design Tutorial](https://www.youtube.com/watch?v=S6jy0T85DFs)

## High Level System Design 
Connects how all the components work together with boxes

## Low Level System Design 
Connects how all the components work together with boxes and what each class would do with system design principles and patterns 


## Requirements for System Design 
1. Functional: what it must do
- track orders
- process refunds

3. Non-functional: how well it must do
- 10k users
- latency
- llm bill
- uptime
- Pll leaks
- Own Data

### Back of envelop estimation
Traffic: 10k users * 5 messages / day = 50k requests / day
Throughput: 0.6 req/s, in per hour 6 req/s
Tokens: 50k*2k= 3b tokens/month
cost: 
- small model: cost per token * number of tokens required
- frontier model: cost per token * number of tokens required


## Architecture 
### Situation: I need a refund on my last order from Priya and Rahul

#### Authentication Module
1. OpenID Connect that uses a tool like keycloak (also has SSO)
2. AuthO supports Oauth and multiple sign ons like google, microsoft
3. Single sign on
- lets say there is multiple apps under a ecosystem like in google. e.g. docs, slides, etc
- Those require one email account for sign in, which is single sign on

### Situation: What if an AI account startings spamming our chatbot 

#### Rate limit required for Authentication
This is implemented using:
1. An API gateway like nginx or cloudflare (firewalls, ratelimiters, loadbalancers)
2. These gateways also helps prevent like DDOS

#### limit token consumption

### Situation: Hacking Attack like prompt injection 

#### Input Guardrails (fallback idea?)
1. semantic matching
2. Jex models
3. LLM as a judge
4. Regex/keywords

#### no PII leakage
1. using langchain

### Situation Repetitive 
1. semantic cache
##### Implementation 
- when a user asks a question for the first time, cache is empty and it goes to AI model
- once answer is generated, it will be stored in cache
- If the user asks this again, it will be a cache hit

What kind of questions can be cached? 
Intent Model to do and orchestrator:
- knowledge based questions that can be cached
- but not questions that require api calls or tool calls

### Situation: return window for electronics was cut from 20 to 7 days but the bot still says 30 days 

#### Implementation
- Using rag that is connected to vector database and uses knowledge injestion (PDF, docs) 
- Change data capture event will check what changed and reindex into vector database
  - this also makes a part cache invalidate as well
 

### Situation: I was charged 4200 INR for a 399 INR order. Cancel the membership
- identify the event has happened using the router/orchestrator
- escalate the human (human in the loop)

### Situation: monthly llm is very hi

#### Hybrid model
use a rules based + ML classifier + RAG + Small model + LLM (gpt-oss with 120B Params) to reduce the cost
- heavy model: for more reasoning
- light model: for light reasoning
Follows the minimum sufficient intelligence principle. Each time the data hunger increasing, cost increases, and autonomy increases.

### Situation: OpenAI model is down? 

#### Fallback scenario 
fallback can be anthropic 

#### Security
Vercel, liteLLM 
- providing a proxy api key
- rate limiters
