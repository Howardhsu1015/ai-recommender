# 假設 generate_answer() 已定義好

prompt = "請用簡單語言解釋區塊鏈是什麼。"
temperature = 0.5
token_limits = [20, 50, 200]

print("🧪 Token 限制實驗開始...\n")

for limit in token_limits:
    print(f"🔢 max_output_tokens = {limit}")
    answer = generate_answer(prompt, temperature=temperature, max_tokens=limit)

    if answer:
        print("✏️ 回答（前300字）：\n", answer[:300])
        try:
            filename = f"tokens_{limit}_response.txt"
            with open(filename, "w", encoding="utf-8") as f:  # ✅ 指定編碼
                f.write(f"🔢 max_output_tokens = {limit}\n\n")
                f.write(answer)
            print(f"📄 已儲存：{filename}")
        except Exception as e:
            print(f"⚠️ 儲存失敗：{e}")
    else:
        print("❌ 沒有產生回答")

    print("-" * 60 + "\n")
