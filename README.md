# ZZZ 디스크 판정 데이터

Android 앱이 실행될 때 이 저장소의 data/manifest.json을 확인하고, SHA-256이 바뀐 캐릭터 파일만 다운로드합니다. APK 업데이트와 독립적으로 배포됩니다.

- data/manifest.json: 데이터 버전, 캐릭터 경로와 SHA-256, 미완성 캐릭터 목록
- data/characters/*.json: 캐릭터별 4세트·2세트·주옵션·유효/필수 부옵션과 출시 순서
- schemaVersion: 1

모든 파일을 준비한 뒤 manifest와 함께 한 커밋으로 게시합니다. 캐릭터를 수정하면 해당 SHA-256과 manifest의 전체 version도 다시 계산해야 합니다. version은 version 필드를 제외한 manifest를 키 정렬·공백 없는 UTF-8 JSON과 마지막 줄바꿈으로 직렬화한 SHA-256입니다.

클라이언트는 HTTPS와 파일 해시·데이터 형식을 검사하고 전체 검증 후 한 번에 적용합니다. 실패하면 마지막 정상 데이터를 유지합니다.

[앱 개인정보처리방침 / Privacy Policy (13 languages)](https://seoki0903-forest.github.io/ZZZ-disk/privacy.html)


## OCR 모델 다운로드

v0.4.19부터 기본 제목 인식까지 실패하면 선택한 게임 언어의 PP-OCRv5 보조 모델로 한 번 더 확인합니다. 처음 실행하거나 인식 언어를 바꾸면 필요한 모델 하나만 자동 준비합니다. 이미 검증한 파일은 재사용합니다. 화면 이미지나 판독 결과를 서버로 보내지 않습니다.

- [보조 OCR 모델 고정 배포](https://github.com/Seoki0903-forest/ZZZ-disk/releases/tag/ocr-models-v1): 5개 모델과 라이선스. 로그인 없이 다운로드합니다.
- [모델 크기·SHA-256·원출처·언어 연결](ocr/models-v1.json)
- [다운로드 구조와 유지관리](docs/downloads.md)

모델 바이너리는 Git 이력 대신 Release 첨부 파일에 보관합니다. 기존 앱에서 사용하는 태그와 첨부 파일은 삭제하거나 다른 내용으로 교체하지 마세요. 새 모델은 새 태그와 해시를 가진 앱 버전으로 배포합니다. 모델 선택은13언어를 지원하지만 모든 실제 게임 화면의 정확도를 보장한다는 뜻은 아닙니다.
