# ai-recommender
import google.generativeai as genai
from google.generativeai.types import GenerationConfig

# 設定 API 金鑰
genai.configure(api_key="你的API金鑰")  # ⚠️ 建議用變數讀取，避免直接暴露金鑰

# 初始化模型
model = genai.GenerativeModel(model_name="models/gemini-1.5-pro")

# 回答函式
def generate_answer(prompt, temperature=0.7, max_tokens=512):
    config = GenerationConfig(
        temperature=temperature,
        max_output_tokens=max_tokens
    )
    try:
        response = model.generate_content(prompt, generation_config=config)
        return response.text
    except Exception as e:
        print(f"❌ 發生錯誤：{e}")
        return None

# 測試 1：單純提問
prompt = "請解釋量子糾纏是什麼？用簡單的語言"
answer = generate_answer(prompt, temperature=0.3, max_tokens=300)
print("🌟 AI 回答：\n", answer)

# 測試 2：模擬根據檢索結果回答問題
retrieved_context = "量子糾纏是量子力學中的一種現象，當兩個粒子以某種方式交互作用後，它們的量子狀態會變得緊密相關..."
user_question = "量子糾纏是什麼？"

full_prompt = f"根據以下文章內容回答問題：\n\n文章內容：\n{retrieved_context}\n\n問題：{user_question}"

answer = generate_answer(full_prompt, temperature=0.5, max_tokens=400)
print("🔍 根據內容回答：\n", answer)
