%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#FCEEF5', 'edgeLabelBackground':'#ffffff', 'tertiaryColor': '#fff', 'lineColor': '#333'}}}%%

graph TD
    %% 1. 데이터 수집 단계 (비정형 데이터)
    subgraph Input_Layer [INPUT: 비정형 기술 데이터 수집]
        direction TB
        Demand[("대기업/중견기업 (수요)<br/>기술 소개서 & 니즈 정의서<br/>(Unstructured Text)")]
        Supply[("스타트업 (공급)<br/>보유 기술 명세서 & 특허<br/>(Unstructured Text)")]
    end

    %% 2. 데이터 정제 단계 (LLM 활용)
    subgraph Preprocessing [PROCESS 1: LLM 기반 데이터 정제]
        direction TB
        Ollama["🤖 Ollama (Local LLM)<br/>핵심 키워드 추출 & 노이즈 제거"]
        Refined_Data["📄 정제된 기술 요약 데이터<br/>(Structured Summary)"]
    end

    %% 3. 임베딩 및 매칭 단계 (핵심 로직)
    subgraph Matching_Engine [PROCESS 2: 벡터 임베딩 & 매칭 엔진]
        direction TB
        KoSBERT["🔠 Ko-SBERT 모델<br/>(Korean Sentence-BERT)"]
        Vector["📊 고차원 벡터 변환<br/>(Text to Vector Embedding)"]
        Algo["📐 코사인 유사도 계산<br/>(Cosine Similarity Matching)"]
    end

    %% 4. 결과 출력 단계
    subgraph Output_Layer [OUTPUT: 오픈 이노베이션 매칭]
        direction TB
        Result["🤝 최적 파트너 추천 리스트<br/>(Top-N Ranking)"]
        Insight["💡 매칭 적합도(Score) 및<br/>협업 제안 포인트 제공"]
    end

    %% 흐름 연결
    Demand & Supply ==> Ollama
    Ollama ==> Refined_Data
    Refined_Data ==> KoSBERT
    KoSBERT --> Vector
    Vector ==> Algo
    Algo ==> Result
    Result -.-> Insight

    %% 스타일 정의 (iStaging 브랜드 컬러)
    classDef input fill:#f9f9f9,stroke:#666,stroke-width:2px,color:#333;
    classDef llm fill:#FCEEF5,stroke:#9E1E7F,stroke-width:2px,color:#333;
    classDef engine fill:#FCEEF5,stroke:#EA0772,stroke-width:3px,color:#000,font-weight:bold;
    classDef output fill:#4a4a4a,stroke:#333,stroke-width:2px,color:#fff;

    class Demand,Supply input;
    class Ollama,Refined_Data llm;
    class KoSBERT,Vector,Algo engine;
    class Result,Insight output;
