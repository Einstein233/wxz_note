**通过vllm运行模型的命令**
3号显卡，qwen3-8b的模型，占本卡85%的内存，最大上下文长度，端口80，运行模式
CUDA_VISIBLE_DEVICES=3 python -m vllm.entrypoints.openai.api_server \
    --model Qwen/Qwen3-8B \
    --gpu-memory-utilization 0.85 \
    --max-model-len 8192 \
    --port 8000 \
    --enforce-eager

**模型调用测试命令**
curl http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "Qwen/Qwen3-8B",
    "messages": [
      {"role": "system", "content": "你是一个极其专业的AI基础设施架构师。"},
      {"role": "user", "content": "请用一句话告诉我，vLLM框架最核心的两个技术是什么？"}
    ],
    "max_tokens": 100
  }'