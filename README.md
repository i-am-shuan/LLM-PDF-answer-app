<p align="center">
	<img alt="image" src="https://github.com/i-am-shuan/LLM-PDF-answer-app/assets/161431602/8c758c8e-9689-4255-aa55-5ce502586d1f" width="60%" height="60%">
</p>

---

<p align="center">
	<img alt="image" src="https://github.com/i-am-shuan/LLM-PDF-answer-app/assets/161431602/b89f470c-0fb3-4779-b7af-d609e8affe26" width="50%" height="50%">
</p>

---

- PDF 질의응답 프로그램
  - spec: streamlit cloud, gpt-3.5-turbo, langchain, RAG - FAISS
    - FAISS: 다양한 벡터 간의 유사도를 계산할 수 있는알고리즘을 모은 패키지.
  - 설명:
  	- 사용자가 PDF 파일 업로드
  	- 텍스트 추출 
  	- 추출한 텍스트 chunk 단위로 분할 (chunk; 한 묶음, 한 덩어리 단위)
  		- chunk 조건: 사용하는 언어 모델의 max token 보다는 작은 크기여야 한다.
  	- (추출한 텍스트 파일) 임베딩 to 벡터DB
  		- 인간의 언어(자연어)를 컴퓨터가 이해할 수 있는 벡터로 번역해주는 작업
  	- (사용자로부터 입력받은 질문)  to 벡터DB
  	- 벡터DB에서 사용자의 질문과 유사한 내용이 포함된 chunk를 검색 및 추출
  		- Semantic Search
  		- 사용자의 질문과 유사한 내용이 포함되어 있는 몇개의 chunk를 추출
  	- ChatGPT에게 질문과 Chunk를 전달
  		- GPT야, 질문과 Chunk를 읽고 질문에 답해줘
  		- 그러면 ChatGPT가 마치 PDF를 모두 읽고 질문에 답변하는 것처럼 답변을 생성하여 반환한다.
   - 설명상세:
    - PyPDF2 pakage를 활용해서 PDF 안의 텍스트 추출
    - 추출한 텍스트 chunk size로 자른다. (chunk에 overlap 적용)
    - chunk들을 임베딩
    - 텍스트 임베딩 모델을 설정
      - 임베딩 모델: (openai) text-embedding-ada-002
      - Cosine Similarity 기반 Semantic Search
      - 입력받은 질문과 가장 유사한 chunk를 추출
      - 추출한 chunk들과 질문을 합쳐서 같이 chatGPT에게 질문
      - 최종 답변


