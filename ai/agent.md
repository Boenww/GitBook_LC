# Agent

## A2A

复杂任务拆分（工具、上下文、注意力有限），并行处理

agent-card.json

agent==微服务



## SSE

LLM输出token，用户看

still HTTP, but client - Accept: text/event-stream; server - Content-Type: text/event-stream

纯文本格式，不是json，lines of “data: ... \n\n”

TCP is necessary for reliability (order and retransmission)



