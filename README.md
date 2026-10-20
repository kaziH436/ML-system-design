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

