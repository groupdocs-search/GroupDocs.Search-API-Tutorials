---
date: 2025-12-18
description: GroupDocs.Search를 사용하여 검색 인덱스 Java 애플리케이션을 만드는 방법을 배우세요. 인덱싱, 검색, 하이라이팅,
  OCR 및 Java 성능 최적화를 탐색하세요.
is_root: true
linktitle: GroupDocs.Search for Java Tutorials
title: 검색 인덱스 만들기 Java – GroupDocs.Search 튜토리얼
type: docs
url: /ko/java/
weight: 10
---

# GroupDocs.Search for Java와 함께 Java 검색 인덱스 만들기

GroupDocs.Search for Java를 사용하여 **검색 인덱스 Java 생성** 애플리케이션을 만드는 궁극적인 가이드에 오신 것을 환영합니다. 우리의 포괄적인 API는 Java 개발자가 최소한의 노력으로 고성능 문서 검색 기능을 추가할 수 있게 해줍니다. 작은 내부 도구를 만들든 대규모 엔터프라이즈 솔루션을 구축하든, PDF, Office, HTML 및 기타 다양한 형식에 대해 인덱싱, 검색, 하이라이트 및 결과 미세 조정에 필요한 모든 것을 찾을 수 있습니다.

## 빠른 개요

GroupDocs.Search for Java는 다음을 가능하게 합니다:

- **다양한 문서 유형 인덱싱** – PDFs, DOCX, PPTX, XLSX, HTML 등.  
- **고급 쿼리 실행** – Boolean, fuzzy, wildcard, phrase, regex, faceted 검색.  
- **언어 처리 활용** – 동의어, 맞춤법 검사, 동음이의어 감지, 사용자 정의 사전.  
- **OCR 통합** – 스캔된 이미지에서 텍스트를 추출하고 검색 가능한 인덱스에 포함.  
- **성능 최적화** – 메모리 사용량, 인덱스 크기, 쿼리 응답 시간을 제어.  
- **결과 하이라이트** – 원본 문서 또는 HTML 미리보기에서 직접 매치를 표시.  

아래에서는 이러한 기능을 단계별로 안내하는 전용 튜토리얼 목록을 확인할 수 있습니다.

## GroupDocs.Search for Java 튜토리얼

### [시작하기](./getting-started/)
GroupDocs.Search for Java의 기본을 배우고 설치, 라이선스 및 첫 번째 검색 애플리케이션 만들기를 다루는 입문 튜토리얼을 확인하세요.

### [인덱싱](./indexing/)
인덱스 생성, 다양한 문서 소스 처리, 최적 성능을 위한 옵션 구성 등 문서 인덱싱 기술을 마스터하세요.

### [검색](./searching/)
불리언, 퍼지, 와일드카드, 구문, 정규식 검색 및 포괄적인 결과 처리를 포함한 강력한 검색 기능을 구현하세요.

### [하이라이팅](./highlighting/)
원본 문서에서 검색 매치를 하이라이트하고 사용자 정의 스타일링이 가능한 HTML 미리보기를 생성하여 사용자 경험을 향상시키세요.

### [사전 및 언어 처리](./dictionaries-language-processing/)
동의어 사전, 맞춤법 검사, 사용자 정의 알파벳, 동음이의어 감지 및 기타 언어 처리 기능으로 검색 품질을 향상시키세요.

### [문서 관리](./document-management/)
검색 인덱스에서 문서를 추가, 업데이트 및 제거하면서 최적 성능을 유지하는 효과적인 기술을 배우세요.

### [OCR 및 이미지 검색](./ocr-image-search/)
이미지에서 텍스트 추출 및 역 이미지 검색 기능을 구현하여 애플리케이션의 검색 기능을 확장하세요.

### [고급 기능](./advanced-features/)
Faceted 검색, 검색 보고서, 문서 필터링 및 메타데이터 기반 검색 등 특화된 검색 기능을 탐색하세요.

### [검색 네트워크](./search-network/)
샤딩, 동기화 및 최적화된 네트워크 구성을 통해 확장 가능한 분산 검색 솔루션을 구축하세요.

### [성능 최적화](./performance-optimization/)
Java 환경에서 인덱스 크기, 메모리 사용량 및 검색 응답 시간을 최적화하는 기술로 검색 효율성을 극대화하세요.

### [예외 처리 및 로깅](./exception-handling-logging/)
견고한 오류 관리 및 로깅을 구현하여 신뢰할 수 있는 프로덕션 준비 검색 애플리케이션을 만들세요.

### [라이선스 및 구성](./licensing-configuration/)
프로덕션 환경에서 최적 성능을 위해 라이선스를 올바르게 설정하고 GroupDocs.Search를 구성하세요.

### [텍스트 추출 및 처리](./text-extraction-processing/)
Java에서 사용자 정의 추출기, 세그멘터 및 문자 교체 규칙을 사용해 텍스트 추출 동작을 맞춤화하세요.

## Java 문서 검색 기능 개요

GroupDocs.Search for Java는 강력한 검색 애플리케이션 구축을 위한 포괄적인 기능을 제공합니다:

- **다중 형식 지원** – PDF, DOCX, PPT, XLS, HTML 및 기타 많은 문서 유형을 검색  
- **고급 검색 유형** – Boolean, fuzzy, wildcard, phrase, regex 및 faceted 검색 옵션  
- **지능형 인덱싱** – 구성 가능한 옵션을 통해 빠르고 효율적인 문서 인덱싱  
- **언어 처리** – 동의어 감지, 맞춤법 검사 및 동음이의어 인식  
- **OCR 지원** – 이미지 및 스캔된 문서에서 텍스트를 추출하고 검색  
- **성능 최적화** – 메모리 사용량 및 검색 속도를 위한 구성 옵션  
- **결과 하이라이팅** – 원본 문서에서 검색 매치를 시각적으로 강조  
- **사전 지원** – 특수 용어 및 도메인을 위한 사용자 정의 사전  
- **분산 검색** – 네트워크 기능을 활용한 확장 가능한 분산 검색 솔루션 구축  
- **초고속** – 수천 개의 문서를 초단위로 처리 및 검색  

## 학습 자료

GroupDocs는 GroupDocs.Search for Java를 최대한 활용할 수 있도록 포괄적인 리소스를 제공합니다:

- [Documentation](https://docs.groupdocs.com/search/java/) - 상세한 API 문서 및 사용자 가이드  
- [API Reference](https://reference.groupdocs.com/search/java/) - 전체 메서드 및 클래스 레퍼런스  
- [GitHub Examples](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) - 샘플 프로젝트 및 코드 예제  
- [Free Support Forum](https://forum.groupdocs.com/c/search) - 질문에 대한 커뮤니티 지원  
- [Download Free Trial](https://releases.groupdocs.com/search/java) - 무료 체험 다운로드  

---

**마지막 업데이트:** 2025-12-18  
**작성자:** GroupDocs