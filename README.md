# Temperature 實驗：區塊鏈說明
final_prompt = "請說明什麼是區塊鏈，用給高中生看的方式講解。"
temperatures = [0.0, 0.5, 1.0]

print("Temperature 實驗開始...\n")

for temp in temperatures:
    print(f"Temperature = {temp}")
    answer = generate_answer(final_prompt, temperature=temp, max_tokens=300)

    if answer:
        print("回答（前300字）：\n", answer[:300])
        try:
            filename = f"temp_{str(temp).replace('.', '_')}_response.txt"
            with open(filename, "w", encoding="utf-8") as f:
                f.write(f"Temperature: {temp}\n\n")
                f.write(answer)
            print(f"已儲存：{filename}")
        except Exception as e:
            print(f"儲存錯誤：{e}")
    else:
        print("沒有產生回答")

    print("-" * 60 + "\n")
