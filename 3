import streamlit as st
import requests
import base64
import io
import asyncio
from edge_tts import Communicate
import logging
from PIL import Image

# 로깅 설정
logging.basicConfig(level=logging.INFO)

# Ollama 서버 주소
OLLAMA_HOST = 'http://localhost:11434'
# 음성 설정
VOICE = "ko-KR-HyunsuNeural"

# 프롬프트 템플릿 (한국어, 이미지 텍스트 추출 및 요약, 자동 분석)
PROMPT_TEMPLATE = """
[INST]
당신은 이미지를 보고 텍스트를 정확하게 파악하고 요약하는 능력이 뛰어난 어시스턴트입니다.  제공된 이미지를 바탕으로 다음을 수행합니다:

1. 이미지 내의 텍스트를 최대한 정확하게 추출하여 별도로 표시합니다.
2. 이미지 내 텍스트와 이미지 내용을 종합하여 이미지를 설명합니다.
3. 이미지 내 텍스트를 요약합니다.
[/INST]

이미지:
"""  # 사용자 입력 부분 제거


async def tts(text, voice=VOICE):
    """Edge TTS를 사용하여 텍스트를 음성으로 변환"""
    try:
        communicate = Communicate(text, voice)
        audio_data = io.BytesIO()
        async for chunk in communicate.stream():
            if chunk["type"] == "audio":
                audio_data.write(chunk["data"])
        audio_data.seek(0)
        return audio_data

    except Exception as e:
        logging.error(f"TTS Error: {e}")
        st.error(f"TTS 오류: {e}")
        return None


def query_ollama(prompt, image_data=None):
    """Ollama API 호출 (이미지)"""
    data = {
        "model": "gemma3:4b",
        "prompt": prompt,
        "stream": False,
        "options": {"temperature": 0.2, "top_p": 0.8},
    }
    if image_data:
        data["images"] = [image_data]

    try:
        response = requests.post(f"{OLLAMA_HOST}/api/generate", json=data, stream=False)
        response.raise_for_status()
        return response.json()
    except requests.exceptions.RequestException as e:
        logging.error(f"Ollama Request Error: {e}")
        return {"error": f"Ollama API 요청 오류: {e}"}


async def main():
    st.title("AI 이미지 분석 (텍스트 추출 + 요약 + 음성)")

    # 세션 상태 초기화
    if "messages" not in st.session_state:
        st.session_state.messages = []
    if "context" not in st.session_state:
        st.session_state.context = []


    # 대화 기록 표시
    for message in st.session_state.messages:
        with st.chat_message(message["role"]):
            st.markdown(message["content"])
            if "audio" in message:
                st.audio(message["audio"])

    # 이미지 업로드
    uploaded_file = st.file_uploader("이미지를 업로드하세요", type=["jpg", "jpeg", "png"], key="image_uploader")  # key 추가
    if uploaded_file is not None:
        image = Image.open(uploaded_file)
        st.image(image, caption="업로드된 이미지", use_column_width=True)
        buffered = io.BytesIO()
        image.save(buffered, format="JPEG")
        img_base64 = base64.b64encode(buffered.getvalue()).decode()

        # 이미지 텍스트 추출, 설명, 요약 요청 (자동)
        with st.spinner("이미지 분석 중..."):
            # prompt = PROMPT_TEMPLATE.format(user_input="이 이미지에서 텍스트를 추출하고, 이미지 설명과 함께 텍스트를 요약해주세요.")
            ollama_response = query_ollama(PROMPT_TEMPLATE, image_data=img_base64) # 바로 prompt 전달

            if "error" in ollama_response:
                st.error(f"이미지 분석 오류: {ollama_response['error']}")
            else:
                response_text = ollama_response["response"].strip()

                # 응답에서 텍스트 추출, 이미지 설명, 요약 분리 (간단한 패턴 사용)
                extracted_text = ""
                description = ""
                summary = ""

                parts = response_text.split("**요약:**")
                if len(parts) > 1:
                    summary = parts[1].strip()

                pre_summary = parts[0].split("**이미지 설명:**")
                if len(pre_summary) > 1:
                    description = pre_summary[1].strip()

                extracted_text_parts = pre_summary[0].split("**추출된 텍스트:**")
                if len(extracted_text_parts) > 1:
                    extracted_text = extracted_text_parts[1].strip()

                # 분리된 내용 표시
                if extracted_text:
                    st.write("### 추출된 텍스트:")
                    st.text_area("", extracted_text, height=100)
                if description:
                    st.write("### 이미지 설명:")
                    st.markdown(description)
                if summary:
                    st.write("### 텍스트 요약:")
                    st.markdown(summary)


                # 전체 응답 저장 및 음성 출력
                st.session_state.messages.append({"role": "assistant", "content": response_text})
                with st.chat_message("assistant"):
                    st.markdown(response_text) # 전체 내용 표시
                    with st.spinner("음성 생성 중..."):
                        audio_data = await tts(response_text)
                        if audio_data:
                            st.audio(audio_data)
                            st.session_state.messages[-1]["audio"] = audio_data


if __name__ == "__main__":
    asyncio.run(main())
