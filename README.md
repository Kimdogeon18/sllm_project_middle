# SLLM: 스마트 채팅 서비스 📝
<hr>

# 🎂 프로젝트 소개

본 프로젝트는 **Microsoft/Phi-3.5-mini-instruct** 모델을 활용하여 사용자의 자연어 입력을 받아 AI가 텍스트를 생성하는 시스템을 구축하는 것을 목표로 합니다.  
간단한 웹 인터페이스를 통해 질문을 입력하고, AI 모델이 자연어로 답변을 생성하는 시스템을 제공합니다. 이 시스템은 대화형 인공지능 응답을 제공하며, 일상 대화부터 전문적인 질문 응답까지 다양한 분야에 활용 가능합니다.

# 🖌️ 사용 모델

**모델**: `microsoft/Phi-3.5-mini-instruct`

이 모델은 **지시형**(Instruction-based) AI로, 주어진 텍스트에 대해 명확하고 자연스러운 응답을 생성합니다.  
다양한 질문과 명령을 이해하고, 높은 품질의 텍스트 응답을 생성하는 데 최적화되어 있습니다.

### 대화 품질 향상
- **적합한 분야**: 일상적인 대화에서부터 깊이 있는 전문적인 질문까지 모두 커버 
- **특징**:  AI는 사용자의 질문 의도를 정확히 파악하고, 자연스럽고 흐름 있는 응답을 생성합니다. 다양한 시나리오에서 유용하게 활용할 수 있습니다.

### 오픈소스 기반 및 손쉬운 적용
- **빠르게 시작하기**  Hugging Face에서 제공하는 모델을 바로 사용하여 손쉽게 시작할 수 있습니다.
- **유연한 커스터마이징** PyTorch 기반으로 설계되어, 필요에 따라 모델을 세밀하게 조정하거나 기능을 추가할 수 있어 매우 유연합니다.

# 🔩 기술 스택

| 항목          | 내용                                    |
|---------------|-----------------------------------------|
| **언어 모델** | `microsoft/Phi-3.5-mini-instruct`       |
| **백엔드**    | FastAPI, Uvicorn                       |
| **프론트엔드**| HTML + JavaScript (jQuery)              |
| **실행 환경** | PyTorch + Hugging Face + GPU (CUDA) 🖥️  |



# 🌈 특징

| 항목           | 설명                                        |
|----------------|---------------------------------------------|
| **다국어 지원** | 한국어 중심, 다국어 대화 가능                |
| **고효율 추론**| 4-bit 양자화로 메모리 사용량 최소화          |
| **직관적 UI**  | 간결한 웹 인터페이스로 쉬운 사용자 경험       |
| **빠른 응답**  | FastAPI와 최적화된 모델로 짧은 대기 시간     |
| **확장 가능**  | CORS 지원으로 다양한 클라이언트와 통합 가능  |

# 📜 주요 코드 정리

### 1. 백엔드 (`main.py`)
- **모델 로드**: 4-bit 양자화로 효율적 실행  
  ```python
  model = AutoModelForCausalLM.from_pretrained(
      model_id,
      quantization_config=BitsAndBytesConfig(load_in_4bit=True)
  )
  ```
- **API 엔드포인트**: 사용자 입력 처리 및 응답 생성  
  ```python
  @app.post("/v1/chat/completions")
  async def chat_completion(request: ChatRequest):
      output_text = tokenizer.decode(model.generate(**inputs)[0])
  ```

### 2. 프론트엔드 (`index.html`)
- **구성**: 채팅창, 입력창, 전송 버튼으로 간결한 UI  
  ```html
  <div id="chatBox" style="height: 400px; overflow-y: auto;"></div>
  <input type="text" id="userInput" placeholder="궁금한 점을 입력하세요!" />
  ```

### 3. JavaScript (`test.js`)
- **UI 스타일링**: 동적 CSS로 깔끔한 디자인  
  ```javascript
  document.getElementById("chatContainer").style.backgroundColor = "#ffffff";
  ```
- **메시지 전송**: AJAX로 백엔드와 통신  
  ```javascript
  $.ajax({
      url: 'http://localhost:8000/v1/chat/completions',
      data: JSON.stringify({ model: 'phi', messages: [{ role: 'user', content: inputText }] })
  });
  ```

# 🎀 실행 화면

### 1. 한국어 질문
- **질문**: "네이버는 무슨 회사야?"  
![Image](https://github.com/user-attachments/assets/5c9d1c65-4ca5-4b97-b47c-4f0513cc97b4)
- **설명**: 사용자가 "네이버는 무슨 회사야?"라는 한국어 질문으로 AI가 네이버에 대한 간단한 소개와 주요 서비스(웹사이트, 앱, 웹 매칭 서비스 등)를 설명합니다. 응답 시간은 6.4초로 표시됩니다.  
### 2. 영어 질문
- **질문**: "What company is Naver?"  
![Image](https://github.com/user-attachments/assets/88d9cd52-6472-4ccd-befa-5f83e05871d5)
- **설명**: 사용자가 "What company is Naver?"라는 영어 질문으로 네이버에 대해 물었고, AI가 네이버의 설립 배경, 주요 서비스(검색 엔진, 커뮤니케이션, 전자상거래, 콘텐츠 플랫폼)를 자세히 설명했습니다. 응답 시간은 16.9초로 표시됩니다.  
## 📌 참고

| 항목          | 링크                                    |
|---------------|-----------------------------------------|
| **모델**      | [Phi-3.5-mini-instruct](https://huggingface.co/microsoft/Phi-3.5-mini-instruct) |
| **FastAPI**   | [FastAPI 문서](https://fastapi.tiangolo.com/) |
| **jQuery**    | [jQuery 문서](https://jquery.com/) |

